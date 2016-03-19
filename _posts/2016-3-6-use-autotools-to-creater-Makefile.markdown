--- 
layout: posts
categories: kernel
title: How to use autotools to create Makefile
---
##Study something new every day!

<ol>
<li>
在当前目录下运行autoscan,生成configure.scan文件；
</li>
<li>

修改configure.scan文件，
AC_INIT([main], [1.0], [your email])
AC_CONFIG_SRCDIR([queue.c])
AC_CONFIG_HEADERS([config.h])
AM_INIT_AUTOMAKE([main], [1.0])

AC_PROG_CC
CFLAGS="-g -O2" 

AC_OUTPUT(Makefile)

将configure.scan重命名为configure.ac文件；
</li>
<li>
aclocal
</li>
<li>
autoconf
</li>
<li>
autoheader
</li>
<li>
automake -a
</li>
<li>
创建Makefile.am文件:
bin_PROGRAMS=main
main_SOURCES=producer_consumer.c queue.c
LIBS=-lpthread
</li>
<li>
automake 
</li>
<li>
./configure
</li>
</ol>

diff -Naur linux-2.4.22/.version linux-2.4.22osd/.version
--- linux-2.4.22/.version	2005-04-14 03:02:11.000000000 -0400
+++ linux-2.4.22osd/.version	2005-04-14 02:53:44.000000000 -0400
@@ -1 +1 @@
-2
+3
diff -Naur linux-2.4.22/drivers/scsi/scsi.h linux-2.4.22osd/drivers/scsi/scsi.h
--- linux-2.4.22/drivers/scsi/scsi.h	2005-04-14 03:02:00.000000000 -0400
+++ linux-2.4.22osd/drivers/scsi/scsi.h	2005-04-14 03:00:45.000000000 -0400
@@ -89,7 +89,7 @@
 #define FALSE 0
 #endif
 
-#define MAX_SCSI_DEVICE_CODE 14
+#define MAX_SCSI_DEVICE_CODE 15
 extern const char *const scsi_device_types[MAX_SCSI_DEVICE_CODE];
 
 #ifdef DEBUG
@@ -351,7 +351,7 @@
 #define DRIVER_MASK         0x0f
 #define SUGGEST_MASK        0xf0
 
-#define MAX_COMMAND_SIZE    16
+#define MAX_COMMAND_SIZE        256
 #define SCSI_SENSE_BUFFERSIZE   64
 
 /*
@@ -655,6 +655,7 @@
 	struct request sr_request;	/* A copy of the command we are
 				   working on */
 	unsigned sr_bufflen;	/* Size of data buffer */
+	unsigned sr_bidi_bufflen; /* for OSD */
 	void *sr_buffer;		/* Data buffer */
 	int sr_allowed;
 	unsigned char sr_data_direction;
@@ -737,6 +738,7 @@
 	/* These elements define the operation we are about to perform */
 	unsigned char cmnd[MAX_COMMAND_SIZE];
 	unsigned request_bufflen;	/* Actual request size */
+	unsigned bidi_request_bufflen;  /* for OSD */
 
 	struct timer_list eh_timeout;	/* Used to time out the command. */
 	void *request_buffer;		/* Actual requested buffer */
diff -Naur linux-2.4.22/drivers/scsi/scsi_dma.c linux-2.4.22osd/drivers/scsi/scsi_dma.c
--- linux-2.4.22/drivers/scsi/scsi_dma.c	2005-04-14 03:02:00.000000000 -0400
+++ linux-2.4.22osd/drivers/scsi/scsi_dma.c	2005-04-14 02:59:36.000000000 -0400
@@ -245,7 +245,7 @@
 			 * estimate 4k buffer/command for devices of unknown type (should panic).
 			 */
 			if (SDpnt->type == TYPE_WORM || SDpnt->type == TYPE_ROM ||
-			    SDpnt->type == TYPE_DISK || SDpnt->type == TYPE_MOD) {
+			    SDpnt->type == TYPE_DISK || SDpnt->type == TYPE_MOD || SDpnt->type == TYPE_OSD) {
 				int nents = host->sg_tablesize;
 #ifdef DMA_CHUNK_SIZE
 				/* If the architecture does DMA sg merging, make sure
diff -Naur linux-2.4.22/drivers/scsi/scsi_merge.c linux-2.4.22osd/drivers/scsi/scsi_merge.c
--- linux-2.4.22/drivers/scsi/scsi_merge.c	2005-04-14 03:02:00.000000000 -0400
+++ linux-2.4.22osd/drivers/scsi/scsi_merge.c	2005-04-14 02:58:44.000000000 -0400
@@ -406,6 +406,10 @@
 	Scsi_Device *SDpnt = q->queuedata;
 	struct Scsi_Host *SHpnt = SDpnt->host;
 
+	/* for OSD */
+        if ((SDpnt->type==0x0e)&&(bh->b_hack_ino!=req->bh->b_hack_ino))
+                return 0;
+
 	if (max_segments > scsi_max_sg)
 		max_segments = scsi_max_sg;
 
@@ -465,6 +469,10 @@
 	Scsi_Device *SDpnt = q->queuedata;
 	struct Scsi_Host *SHpnt = SDpnt->host;
 
+	/* for OSD */
+        if ((SDpnt->type==0x0e)&&(bh->b_hack_ino!=req->bh->b_hack_ino))
+                return 0;
+
 	if (max_segments > scsi_max_sg)
 		max_segments = scsi_max_sg;
 
diff -Naur linux-2.4.22/drivers/scsi/scsi_scan.c linux-2.4.22osd/drivers/scsi/scsi_scan.c
--- linux-2.4.22/drivers/scsi/scsi_scan.c	2005-04-14 03:02:00.000000000 -0400
+++ linux-2.4.22osd/drivers/scsi/scsi_scan.c	2005-04-14 02:59:13.000000000 -0400
@@ -686,6 +686,7 @@
 	case TYPE_SCANNER:
 	case TYPE_MEDIUM_CHANGER:
 	case TYPE_ENCLOSURE:
+	case TYPE_OSD:
 	case TYPE_COMM:
 		SDpnt->writeable = 1;
 		break;
diff -Naur linux-2.4.22/fs/buffer.c linux-2.4.22osd/fs/buffer.c
--- linux-2.4.22/fs/buffer.c	2005-04-14 03:02:02.000000000 -0400
+++ linux-2.4.22osd/fs/buffer.c	2005-04-14 02:57:18.000000000 -0400
@@ -1741,6 +1741,7 @@
 	bh = head;
 	nr = 0;
 	i = 0;
+        bh->b_hack_ino = inode->i_ino; /* for OSD */
 
 	do {
 		if (buffer_uptodate(bh))
diff -Naur linux-2.4.22/include/linux/fs.h linux-2.4.22osd/include/linux/fs.h
--- linux-2.4.22/include/linux/fs.h	2005-04-14 03:02:07.000000000 -0400
+++ linux-2.4.22osd/include/linux/fs.h	2005-04-14 02:56:49.000000000 -0400
@@ -268,6 +268,7 @@
 
 	unsigned long b_rsector;	/* Real buffer location on disk */
 	wait_queue_head_t b_wait;
+        ino_t b_hack_ino;               /* for OSD */
 
 	struct list_head     b_inode_buffers;	/* doubly linked list of inode dirty buffers */
 };
diff -Naur linux-2.4.22/include/scsi/scsi.h linux-2.4.22osd/include/scsi/scsi.h
--- linux-2.4.22/include/scsi/scsi.h	2005-04-14 03:02:08.000000000 -0400
+++ linux-2.4.22osd/include/scsi/scsi.h	2005-04-14 03:01:22.000000000 -0400
@@ -142,6 +142,7 @@
 #define TYPE_MEDIUM_CHANGER 0x08
 #define TYPE_COMM           0x09    /* Communications device */
 #define TYPE_ENCLOSURE      0x0d    /* Enclosure Services Device */
+#define TYPE_OSD            0x0e    /* Object-based storage device */
 #define TYPE_NO_LUN         0x7f
 
 /*
