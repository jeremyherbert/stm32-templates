vpath %.c $(LIB_ROOT)/src $(LIB_ROOT)/src/core $(LIB_ROOT)/src/peripherals

CFLAGS+= -I$(LIB_ROOT)/inc -I$(LIB_ROOT)/inc/core -I$(LIB_ROOT)/inc/peripherals

SRCS  = STM32vldiscovery.c
SRCS += misc.c stm32f10x_dac.c stm32f10x_gpio.c stm32f10x_sdio.c \
	stm32f10x_adc.c stm32f10x_dbgmcu.c stm32f10x_i2c.c stm32f10x_spi.c \
	stm32f10x_bkp.c stm32f10x_dma.c stm32f10x_iwdg.c stm32f10x_tim.c \
	stm32f10x_can.c stm32f10x_exti.c stm32f10x_pwr.c stm32f10x_usart.c \
	stm32f10x_cec.c stm32f10x_flash.c stm32f10x_rcc.c stm32f10x_wwdg.c \
	stm32f10x_crc.c stm32f10x_fsmc.c stm32f10x_rtc.c
SRCS += core_cm3.c system_stm32f10x.c

OBJS = $(SRCS:.c=.o)

libstm32f10x.a: $(OBJS)
	$(AR) rcs $@ $(OBJS)

clean:
	rm -f $(OBJS) libstm32f10x.a
