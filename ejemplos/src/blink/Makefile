include makefile.conf
#NAME=blink
#STARTUP_DEFS=-D__STARTUP_CLEAR_BSS -D__START=main

#LDSCRIPTS=-L. -L$(BASE)/ldscripts -T stm32f.ld
#LFLAGS=$(USE_NANO) $(USE_NOHOST) $(LDSCRIPTS) $(GC) $(MAP)


#$(NAME)-$(CORE).axf: $(NAME).c $(STARTUP)
#	$(CC) $^ $(CFLAGS) $(LFLAGS) -o $@

#clean: 
#	rm -f $(NAME)*.axf *.map *.o

#--------------------------
PROJECT = blink
.PHONY: clean

OBJECTS += main.o
OBJECTS += startup_ARMCM4.o

DEFINES= -D__STARTUP_CLEAR_BSS -D__START=main
TOOLCHAIN=arm-none-eabi-

CFLAGS=$(ARCH_FLAGS) $(DEFINES) -Wall -ffunction-sections -fdata-sections -fno-builtin
LFLAGS= --specs=nosys.specs -Wl,--gc-sections -Wl,-Map=$(PROJECT).map -T stm32f.ld

%.o: %.S
	$(TOOLCHAIN)gcc $(CFLAGS) -c -o $@ $<

%.o: %.c
	$(TOOLCHAIN)gcc $(CFLAGS) -c -o $@ $<

$(PROJECT).bin: $(PROJECT).elf
	$(TOOLCHAIN)objcopy -O binary $< $@

$(PROJECT).elf: $(OBJECTS)
	$(TOOLCHAIN)gcc $(LFLAGS) $^  $(CFLAGS) -o $@

clean: 
	rm -f $(NAME)*.axf *.map *.o *.bin	

