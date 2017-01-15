include ../Makefile.param
####SENSOR_TYPE ?= SONY_IMX122_DC_1080P_30FPS

TARGET      = sample_venc_rtsp
OBJPATH     = .
##SOURCES     = $(wildcard *.c ./cdr_sd/*.c ./common/*.c ./cdr_mpp/*c ./mmap/*c ./osd_region/*c ./cdr_rec/*c) 
SOURCES     = $(wildcard *.c ./librtsp/*c ./librtsp/comm/*.c ./librtsp/net/*c ./librtsp/rtcp/*c \
./librtsp/rtp/*c ./librtsp/rtsp/*c ./librtsp/utils/*c) 

CDRBASE_DIR = $(shell pwd)


OBJS        = $(patsubst %.c,%.o,$(SOURCES))
FULLOBJS    = $(patsubst %.c,$(OBJPATH)/%.o,$(SOURCES))

CDRINCPATH := -I$(CDRBASE_DIR)/librtsp
CDRINCPATH += -I$(CDRBASE_DIR)/librtsp/comm
CDRINCPATH += -I$(CDRBASE_DIR)/librtsp/net
CDRINCPATH += -I$(CDRBASE_DIR)/librtsp/rtcp
CDRINCPATH += -I$(CDRBASE_DIR)/librtsp/rtp
CDRINCPATH += -I$(CDRBASE_DIR)/librtsp/rtsp
CDRINCPATH += -I$(CDRBASE_DIR)/librtsp/utils


OTHER_LIB:= -lstdc++ -lpthread -lm 

##COMPFLAGS   = -c -O2 -fPIC  -lm -D_GNU_SOURCE -DRTSARM

###添加-c 选项把源代码都编译成为中间文件.
COMPFLAGS   = -c -O2 -fPIC

all:$(TARGET)
$(TARGET):$(OBJS)	
	$(CC) $(CFLAGS) $(FULLOBJS) $(COMM_OBJ) \
	-o $(TARGET) $(MPI_LIBS) $(AUDIO_LIBA) $(SENSOR_LIBS) $(OTHER_LIB) $(CDRINCPATH)
	arm-hisiv300-linux-strip $(TARGET)
	ls -lh $(TARGET)
	###@cp $(TARGET) /nfs/sample/hisi3516v200/ -f
	
$(OBJS):$(SOURCES) $(COMM_OBJ)
	$(CC) $*.c -o $(OBJPATH)/$@ $(CDRINCPATH) $(CFLAGS) \
	$(MPI_LIBS) $(AUDIO_LIBA) $(SENSOR_LIBS) $(OTHER_LIB) $(COMPFLAGS)
###	$(CC) $(CFLAGS) $(CDRINCPATH) $*.c -o $(OBJPATH)/$@  $(MPI_LIBS) $(AUDIO_LIBA) $(SENSOR_LIBS) $(OTHER_LIB) 
clean:		
	###@echo $(FULLOBJS)
	@rm -rf $(FULLOBJS)	
	@rm -f $(OBJPATH)/.*.swp
	@rm -f $(TARGET)	
	@rm -f $(COMM_OBJ)



