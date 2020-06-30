GCC= e:/devtools/m68k-3.4.6/
CC= $(GCC)bin/gcc
OBJC= $(GCC)bin/objcopy
ASMZ80= $(GCC)bin/asmz80
BINTOC= $(GCC)bin/bintoc
NM= $(GCC)bin/nm
OUTPUT= msu-drv
LIB=$(GCC)lib
BIN= $(GCC)bin

#MAKEFLAGS= -j8

BDIR		:=build
FLAGS		:= $(OPTION) -m68000 -Wall -Os -fomit-frame-pointer $(INCS)
FLAGSZ80	:= -c -i -x1 -x2 -x3 -z -lnul

vpath %.o $(BDIR)/

SRC_MS = main.s
OBJ_MAI = $(SRC_MS:.s=.o)
LNK_MAI = $(OBJ_MAI:%.o=$(BDIR)/%.o)
	
SRC_SS = sub_asm.s
SRC_SC = sub.c

OBJ_SUB = $(SRC_SS:.s=.o)
OBJ_SUB += $(SRC_SC:.c=.o)
LNK_SUB = $(OBJ_SUB:%.o=$(BDIR)/%.o)	
	
all: sub_app main_app

sub_app: $(OBJ_SUB)
	$(CC) -B$(BIN) -T sub.ld -nostdlib $(LNK_SUB) $(LIB)/libgcc.a -o $(BDIR)/sub.elf
	$(OBJC) -O binary $(BDIR)/sub.elf sub.bin

main_app: $(OBJ_MAI)
	$(CC) -B$(BIN) -T main.ld -nostdlib $(LNK_MAI) $(LIB)/libgcc.a -o $(BDIR)/msu-drv.elf
	$(OBJC) -O binary $(BDIR)/msu-drv.elf msu-drv.bin

%.o: %.c
	$(CC) $(FLAGS) -c $< -o $(basename $(BDIR)/$<).o

%.o: %.s
	$(CC) $(FLAGS) -c $< -o $(basename $(BDIR)/$<).o

clean:
	$(RM) $(BDIR)/*.o
	$(RM) $(BDIR)/*.elf


