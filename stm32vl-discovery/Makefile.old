# put your *.o targets here. everything else (should be) magic

OBJS= main.o stm32f10x_it.o

####################################
# DON'T CHANGE BELOW UNLESS YOU KNOW WHAT YOU ARE DOING
####################################

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

export DEVICE=$(ROOT)/lib/an3268/stm32vldiscovery_package/Libraries/CMSIS/CM3/DeviceSupport/ST/STM32F10x
export CORE=$(ROOT)/lib/an3268/stm32vldiscovery_package/Libraries/CMSIS/CM3/CoreSupport
export PERIPH=$(ROOT)/lib/an3268/stm32vldiscovery_package/Libraries/STM32F10x_StdPeriph_Driver
export UTIL=$(ROOT)/lib/an3268/stm32vldiscovery_package/Utilities

###################################

PROJ=main
ELF=$(PROJ).elf

vpath %.c $(ROOT)/src
vpath %.s $(ROOT)/lib # for startup.s

CFLAGS+= -I$(ROOT) -I$(ROOT)/inc
CFLAGS+= -I$(DEVICE) -I$(CORE) -I$(UTIL) -I$(PERIPH)/inc
OBJS+= startup_stm32f10x_md_vl.o

###################################

.PHONY: lib proj

all: lib proj

lib:
	$(MAKE) -C lib

proj: $(ELF)

$(ELF): $(OBJS)
	$(LD) $(LDFLAGS) -o $@ $(OBJS) -lst32
	$(OBJCOPY) -O ihex $(PROJ).elf $(PROJ).hex
	$(OBJCOPY) -O binary $(PROJ).elf $(PROJ).bin

clean:
	rm -f *.o
	rm -f lib/*.o
	rm -f lib/libst32.a
	rm -f $(PROJ).bin
	rm -f $(PROJ).elf
	rm -f $(PROJ).hex
