#******************************************************************************
# Copyright (C) 2017 by Alex Fosdick - University of Colorado
#
# Redistribution, modification or use of this software in source or binary
# forms is permitted as long as the files maintain this copyright. Users are 
# permitted to modify this and use it to learn about the field of embedded
# software. Alex Fosdick and the University of Colorado are not liable for any
# misuse of this material. 
#
#*****************************************************************************

#------------------------------------------------------------------------------
# <Put a Description Here>
#
# Use: make [TARGET] [PLATFORM-OVERRIDES]
#
# Build Targets:
#      <Put a description of the supported targets here>
#
# Platform Overrides:
#      <Put a description of the supported Overrides here
#
#------------------------------------------------------------------------------
include sources.mk

BASEFLAGS = -Wall -Werror -O0 -g -std=c99
MSP432_INCLUDE = -I../include/msp432
CMSIS_INCLUDE = -I../include/CMSIS
TARGET = c1m2

ifeq ($(PLATFORM), HOST)
	CFLAGS = $(BASEFLAGS) -DHOST -I$(INCLUDES) 
	LDFLAGS = -Wl,-Map=$(TARGET).map
	OBJS = $(SOURCES1:.c=.o)
else
 	CC = arm-none-eabi-gcc
 	LD = arm-none-eabi-ld
 	LINKER_FILE = ../msp432p401r.lds
 	CPU = cortex-m4
 	ARCH = armv7e-m
 	SPECS = nosys.specs
 	OBJS = $(SOURCES2:.c=.o)

 	LDFLAGS = -Wl,-Map=$(TARGET).map -T $(LINKER_FILE)
 	CFLAGS = $(BASEFLAGS) -DMSP432 -mcpu=$(CPU) -march=$(ARCH) --specs=$(SPECS) -mfpu=fpv4-sp-d16 -mfloat-abi=hard -mthumb -I$(INCLUDES) $(MSP432_INCLUDE) $(CMSIS_INCLUDE)

endif



# # Platform Overrides
# PLATFORM = 

# # Architectures Specific Flags

# CPU = 
# ARCH = 
# SPECS = 

# # Compiler Flags and Defines
# CC = 
# LD = 
# LDFLAGS = 
# CFLAGS = 
# CPPFLAGs = 

#BJS = $(SOURCES:.c=.o)
%.o : %.c
	$(CC) -c $< $(CFLAGS) -o $@

.PHONY: build
build: all

.PHONY: all
all: $(TARGET).out

$(TARGET).out: $(OBJS)
	$(CC) $(OBJS) $(CFLAGS) $(LDFLAGS) -o $@

.PHONY: clean
clean:
	rm -f $(OBJS) $(TARGET).out $(TARGET).map

