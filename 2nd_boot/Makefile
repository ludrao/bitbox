#NO_USB=1

NAME = 2nd_boot
GAME_C_FILES = $(NAME).c font.c bg.c flashit.c
GAME_C_OPTS = -DVGAMODE_640
include $(BITBOX)/lib/bitbox.mk

# comment to build to flash. This will load boot2 as a normal program in flash 
# BUT obviously cannot program flash anymore
TO_SRAM=1

ifdef TO_SRAM
# NOTE that this program is loaded to SRAM1 (see bitbox memories), thus data is mapped accordingly & load stlink also !
LINKER_SCRIPT=Linker_2Bootloader.ld

# redefinition of stlink load : to sram. This is normal 
stlink: $(NAME).bin
	st-flash write $(NAME).bin 0x20000000
endif 

# the emulator cannot be used for a bootloader. disable making it.
.DEFAULT_GOAL := $(NAME).bin

#.INTERMEDIATE: font.c
font.c: 8x16_437.png
	python mk_font.py $< > $@

bg.c: bg.png
	python mk_bg.py $< > $@
