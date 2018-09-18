.SUFFIXES: .c .o

COMPILE = $(CC) -g -O3 -Wall -D_FILE_OFFSET_BITS=64 -g -DDEBUG_FLAG
DENPENDS = ../../output
INC_PATH = -I$(DENPENDS)/include -I$(DENPENDS)/include/shmcache
LIB_PATH = $(DENPENDS)/lib64/libfastcommon.a $(DENPENDS)/lib64/libshmcache.a -lm -ldl -lpthread

ALL_PRGS = tests

all: $(ALL_PRGS)
.c:
	$(COMPILE) -o $@ $< $(LIB_PATH) $(INC_PATH)
.c.o:
	$(COMPILE) -c -o $@ $<  $(INC_PATH)
clean:
	rm -f $(ALL_PRGS)

