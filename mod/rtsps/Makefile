
HOME := $(shell echo ${GSF_HOME})
CC := $(shell echo ${GSF_CC})
AR := $(shell echo ${GSF_AR})
CFLAGS := $(shell echo ${GSF_CFLAGS})
LDFLAGS := -g $(shell echo ${GSF_LDFLAGS})
TARG := bin/rtsps.exe

#============================================================= 

INCS := -I$(HOME) -Isrc -Iinc -Isrc/libbase -Isrc/librtsps -Isrc/st-rtsp \
        -I$(HOME)/fw/libst/inc \
        -I$(HOME)/fw/libhttp/inc \
        -I$(HOME)/fw/librtp/inc \
        -I$(HOME)/fw/librtsp/inc 
        
#SRCS := $(shell ls src/*.c)
SRCS := $(shell find src -type f -name "*.c" -o -name "*.cpp")
OBJS := $(patsubst %.c, %.o, $(SRCS))

LIBS += -L$(HOME)/lib/$(GSF_CPU_ARCH) -lrtsp -lrtp -lhttp -lst -lcfifo -lrt -lnm -lcjson -lm -lpthread

$(TARG): SJB $(OBJS)
	$(CC) $(LDFLAGS) -o $@ $(OBJS) $(LIBS)
	cp $(TARG) $(HOME)/bin/$(GSF_CPU_ARCH)/ -v

.c.o:
	$(CC) $(CFLAGS) -c $< $(INCS) -o $@

SJB:
	touch src/sjb_rtsps.c;touch src/cfg.c
  
.Phony: clean
clean:
	-rm $(TARG) $(OBJS) src/*.bak -rf
