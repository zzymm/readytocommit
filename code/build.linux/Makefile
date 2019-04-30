
MAKE = make

CFLAGS = -g -Wall -m32 -Wshadow $(INCPATH) $(DEFINES) $(HOST) -DCHANGED
LDFLAGS =  -m32

# These definitions may change as the software is updated.
# Some of them are also system dependent
CPP=/lib/cpp
CC = g++
LD = g++
AS = as

PROGRAM = nachos

THREAD_H =../threads/copyright.h\
	../threads/list.h\
	../threads/scheduler.h\
	../threads/synch.h \
	../threads/synchlist.h\
	../threads/system.h\
	../threads/thread.h\
	../threads/utility.h\
	../machine/interrupt.h\
	../machine/sysdep.h\
	../machine/stats.h\
	../machine/timer.h

THREAD_C =../threads/main.cc\
	../threads/list.cc\
	../threads/scheduler.cc\
	../threads/synch.cc \
	../threads/synchlist.cc\
	../threads/system.cc\
	../threads/thread.cc\
	../threads/utility.cc\
	../threads/threadtest.cc\
	../machine/interrupt.cc\
	../machine/sysdep.cc\
	../machine/stats.cc\
	../machine/timer.cc

THREAD_S = ../threads/switch.s

THREAD_O =main.o list.o scheduler.o synch.o synchlist.o system.o thread.o \
	utility.o threadtest.o interrupt.o stats.o sysdep.o timer.o

USERPROG_H = ../userprog/addrspace.h\
	../userprog/bitmap.h\
	../filesys/filesys.h\
	../filesys/openfile.h\
	../machine/console.h\
	../machine/machine.h\
	../machine/mipssim.h\
	../machine/translate.h\
	../userprog/synchconsole.h\
	../userprog/filetable.h\
	../userprog/processlist.h


USERPROG_C = ../userprog/addrspace.cc\
	../userprog/bitmap.cc\
	../userprog/exception.cc\
	../userprog/progtest.cc\
	../machine/console.cc\
	../machine/machine.cc\
	../machine/mipssim.cc\
	../machine/translate.cc\
	../userprog/synchconsole.cc\
	../userprog/filetable.cc\
	../userprog/processlist.cc

USERPROG_O = addrspace.o bitmap.o exception.o progtest.o console.o machine.o \
	mipssim.o translate.o filetable.o processlist.o synchconsole.o

VM_H = ../filesys/synchdisk.h \
        ../machine/disk.h
VM_C = ../filesys/synchdisk.cc \
        ../machine/disk.cc
VM_O = synchdisk.o disk.o

FILESYS_H =../filesys/directory.h \
	../filesys/filehdr.h\
	../filesys/filesys.h \
	../filesys/openfile.h\
	../filesys/synchdisk.h\
	../machine/disk.h\
	../filesys/fileblock.h


FILESYS_C =../filesys/directory.cc\
	../filesys/filehdr.cc\
	../filesys/filesys.cc\
	../filesys/fstest.cc\
	../filesys/openfile.cc\
	../filesys/synchdisk.cc\
	../machine/disk.cc\
	../filesys/fileblock.cc

FILESYS_O =directory.o filehdr.o filesys.o fstest.o openfile.o synchdisk.o\
	disk.o fileblock.o

NETWORK_H = ../network/post.h ../machine/network.h
NETWORK_C = ../network/nettest.cc ../network/post.cc ../machine/network.cc
NETWORK_O = nettest.o post.o network.o

S_OFILES = switch.o

OFILES = $(C_OFILES) $(S_OFILES)

$(PROGRAM): $(OFILES)
	$(LD) $(OFILES) $(LDFLAGS) -o $(PROGRAM)

$(C_OFILES): %.o:
	$(CC) $(CFLAGS) -c $<

switch.o: ../threads/switch.s
	$(CPP) -P $(INCPATH) $(HOST) ../threads/switch.s > swtch.s
	$(AS) --32 -o switch.o swtch.s

depend: $(CFILES) $(HFILES)
	$(CC) $(INCPATH) $(DEFINES) $(HOST) -DCHANGED -M $(CFILES) > makedep
	echo '/^# DO NOT DELETE THIS LINE/+2,$$d' >eddep
	echo '$$r makedep' >>eddep
	echo 'w' >>eddep
	ed - Makefile < eddep
	rm eddep makedep 
	echo '# DEPENDENCIES MUST END AT END OF FILE' >> Makefile
	echo '# IF YOU PUT STUFF HERE IT WILL GO AWAY' >> Makefile
	echo '# see make depend above' >> Makefile

all: 
#	cd threads; $(MAKE) depend
#	cd threads; $(MAKE) nachos
#	cd userprog; $(MAKE) depend 
#	cd userprog; $(MAKE) nachos 
#	cd vm; $(MAKE) depend
#	cd vm; $(MAKE) nachos 
#	cd ../filesys; $(MAKE) depend
	cd ../filesys; $(MAKE) nachos 
#	cd network; $(MAKE) depend
#	cd network; $(MAKE) nachos 
	cd ../bin; make all
#	cd ../test; make all

# don't delete executables in "test" in case there is no cross-compiler
clean:
	rm -f ../*/{core,nachos,DISK,*.o,swtch.s} test/{*.coff,*.o}

