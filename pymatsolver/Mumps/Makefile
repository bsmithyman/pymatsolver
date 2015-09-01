INCMUMPS  = -I/usr/include -L/usr/lib -lmpi

LIB = -lmpiseq_seq -lzmumps -ldmumps -lsmumps -lmumps_common -lblas -lpord -lcmumps

all: clean build

build:
	gfortran -c $(INCMUMPS) mumps_p.f90 -fPIC
	gfortran -c $(INCMUMPS) mumps_cmplx_p.f90 -fPIC
	f2py -c mumps_interface.f90 -m MumpsInterface \
        $(INCMUMPS) \
        --f90flags='-fcray-pointer' \
        $(LIB) \
        mumps_p.o mumps_cmplx_p.o
	rm -f *.o *.mod

clean:
	rm -f *.o *.mod *.so

test:
	cd ..;nosetests
