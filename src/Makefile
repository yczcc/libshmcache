.SUFFIXES: .c .o .lo

COMPILE = $(CC) -Wall -D_FILE_OFFSET_BITS=64 -D_GNU_SOURCE -g -O3
DENPENDS = ../denpends
INC_PATH = -I$(DENPENDS)/include
LIB_PATH = -lm -ldl -lpthread $(DENPENDS)/lib64/libfastcommon.a
OUTPUTDIR = ../output

SHMCACHE_STATIC_OBJS = shmcache.o shmopt.o shm_striping_allocator.o shm_object_pool.o \
					   shm_hashtable.o shm_value_allocator.o shm_op_wrapper.o shm_lock.o \
                       shmcache_ini_annotation.o

HEADER_FILES = shmcache_def.h shmcache.h shmcache_types.h shm_list.h shm_striping_allocator.h \
			   shm_value_allocator.h shm_op_wrapper.h shmopt.h shm_hashtable.h \
               shmcache_ini_annotation.h

ALL_OBJS = $(SHMCACHE_STATIC_OBJS)

ALL_PRGS = 
STATIC_LIBS = libshmcache.a
ALL_LIBS = $(STATIC_LIBS)

all: $(ALL_OBJS) $(ALL_PRGS) $(ALL_LIBS)
libshmcache.a: $(SHMCACHE_STATIC_OBJS)
	ar rcs $@ $(SHMCACHE_STATIC_OBJS)
.o:
	$(COMPILE) -o $@ $<  $(SHMCACHE_STATIC_OBJS) $(LIB_PATH) $(INC_PATH)
.c:
	$(COMPILE) -o $@ $<  $(SHMCACHE_STATIC_OBJS) $(LIB_PATH) $(INC_PATH)
.c.o:
	$(COMPILE) -c -o $@ $<  $(INC_PATH)
.c.lo:
	$(COMPILE) -c -fPIC -o $@ $<  $(INC_PATH)
install:
	rm -rf $(OUTPUTDIR)
	mkdir -p $(OUTPUTDIR)/lib64
	mkdir -p $(OUTPUTDIR)/lib
	install -m 755 $(STATIC_LIBS) $(OUTPUTDIR)/lib64
	install -m 755 $(STATIC_LIBS) $(OUTPUTDIR)/lib
	mkdir -p $(OUTPUTDIR)/include/shmcache
	install -m 644 $(HEADER_FILES) $(OUTPUTDIR)/include/shmcache
	cp -rf $(DENPENDS)/lib64/* $(OUTPUTDIR)/lib64
	cp -rf $(DENPENDS)/lib/* $(OUTPUTDIR)/lib
	cp -rf $(DENPENDS)/include/* $(OUTPUTDIR)/include
clean:
	rm -f $(ALL_OBJS) $(ALL_PRGS) $(ALL_LIBS)

