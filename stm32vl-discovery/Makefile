# put your *.o targets here, make should handle the rest!

OBJS = main.o stm32f10x_it.o

# all the files will be generated with this name (main.elf, main.bin, main.hex, etc)

PROJ_NAME=main

# that's it, no need to change anything below this line!

###################################################

export CC=arm-none-eabi-gcc
export LD=arm-none-eabi-gcc
export AR=arm-none-eabi-ar
export AS=arm-none-eabi-as
export OBJCOPY=arm-none-eabi-objcopy

export ASFLAGS=-g
export LDFLAGS=-Tstm32f100.ld -Llib
export CFLAGS=-g -O1 -c -fno-common -mcpu=cortex-m3 -mthumb -DSTM32F10X_MD_VL=1 -DUSE_STDPERIPH_DRIVER=1

CWD = $(shell pwd)
export ROOT=$(CWD)
export LIB_ROOT=$(ROOT)/lib

###################################################

vpath %.c $(ROOT)/src  

CFLAGS += -I$(ROOT)/inc -I$(LIB_ROOT) -I$(LIB_ROOT)/inc 
CFLAGS += -I$(LIB_ROOT)/inc/core -I$(LIB_ROOT)/inc/peripherals 

OBJS += $(LIB_ROOT)/startup_stm32f10x_md_vl.s # add startup file to build

###################################################

.PHONY: lib proj

all: 	lib proj

lib:
	$(MAKE) -C lib

proj: 	$(PROJ_NAME).elf

$(PROJ_NAME).elf: $(OBJS)
	$(LD) $(LDFLAGS) -o $@ $(OBJS) -lstm32f10x
	$(OBJCOPY) -O ihex $(PROJ_NAME).elf $(PROJ_NAME).hex
	$(OBJCOPY) -O binary $(PROJ_NAME).elf $(PROJ_NAME).bin

clean:
	rm -f *.o
	rm -f lib/*.o
	rm -f lib/libstm32f10x.a
	rm -f $(PROJ_NAME).elf
	rm -f $(PROJ_NAME).hex
	rm -f $(PROJ_NAME).bin
