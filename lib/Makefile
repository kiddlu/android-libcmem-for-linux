MODULE_NAME = libcmem

###############################################################################
# Cross Build                                                                 
# make CC=/opt/bin/arm-linux-gcc 
# AR=/opt/bin/arm-linux-ar
#
# Shell
# export LD_PRELOAD=libcmem.so
#
###############################################################################


.PHONY: all clean
###############################################################################
# Linux Makefile                                                              #
###############################################################################

#--------- ENVIRONMENT SETTING --------------------
WARNING	= -Wall -Wundef -Wsign-compare -Wno-missing-braces -Wstrict-prototypes -Wno-sign-compare
COMPILE_OPTS	= -I. -O2 -fPIC -ffunction-sections -fdata-sections -D__LINUX_USER__
C_CFLAGS	= $(PLATFORM_CFLAGS) $(COMPILE_OPTS) $(WARNING) $(EXTRA_INCLUDE)
LD_FLAGS	= -fPIC -shared
#--------- END OF ENVIRONMENT SETTING -------------
SRC = \
	memcmp.S \
	memset.S \
	memcpy.S

OBJ = $(SRC:.S=.o)

ifeq ("$(wildcard *.S */*.S)","")
all:
	@echo "nothing to be done for '$(LIB_NAME)'"
clean:
	@echo "nothing to be done for '$(LIB_NAME)'"
else
all: $(OBJ)
	echo Creating library $(MODULE_NAME) ...
	$(CC) -o $(MODULE_NAME).so $(OBJ) $(LD_FLAGS)
	$(AR) rcs $(MODULE_NAME).a $(OBJ)

%.o:%.c
	echo Compiling $<
	$(CC) $(C_CFLAGS) $< -c -o $@

clean:
	rm -f $(OBJ) *.o *.a *.so*
endif
