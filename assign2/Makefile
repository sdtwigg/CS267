#
# Franklin and Hopper
#
CC = CC
MPCC = CC
OPENMP = -mp
CFLAGS = -O3
LIBS =


TARGETS = serial pthreads openmp mpi

all:	$(TARGETS)

serial: serial.o common.o
	$(CC) -o $@ $(LIBS) serial.o common.o
pthreads: pthreads.o common.o
	$(CC) -o $@ $(LIBS) -lpthread pthreads.o common.o
openmp: openmp.o common.o
	$(CC) -o $@ $(LIBS) $(OPENMP) openmp.o common.o
mpi: mpi.o common.o mpi_migrants.o ghost.o
	$(MPCC) -o $@ $(LIBS) $(MPILIBS) mpi.o common.o mpi_migrants.o ghost.o

openmp.o: openmp.cpp common.h
	$(CC) -c $(OPENMP) $(CFLAGS) openmp.cpp
serial.o: serial.cpp common.h
	$(CC) -c $(CFLAGS) serial.cpp
pthreads.o: pthreads.cpp common.h
	$(CC) -c $(CFLAGS) pthreads.cpp
mpi.o: mpi.cpp common.h mpi_particles.h
	$(MPCC) -c $(CFLAGS) mpi.cpp
mpi_migrants.o: mpi_migrants.cpp common.h mpi_particles.h
	$(MPCC) -c $(CFLAGS) mpi_migrants.cpp
ghost.o: ghost.cpp common.h mpi_particles.h
	$(MPCC) -c $(CFLAGS) ghost.cpp
common.o: common.cpp common.h
	$(CC) -c $(CFLAGS) common.cpp

clean:
	rm -f *.o $(TARGETS)
