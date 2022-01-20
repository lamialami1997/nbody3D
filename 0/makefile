all: compil_gcc 
bench_gcc:exec_v1 exec_v2 exec_v3 exec_v4
bench_icc:exec_v1_icc exec_v2_icc exec_v3_icc exec_v4_icc
bench_all: bench_gcc bench_icc

#compilation et execution "GCC"
compil_gcc:nbody_v1.g nbody_v2.g nbody_v3.g nbody_v4.g

exec_v1:nbody_v1.g 
	taskset -c 3 ./nbody_v1.g
exec_v2:nbody_v2.g 
	taskset -c 3 ./nbody_v2.g
exec_v3:nbody_v3.g 
	taskset -c 3 ./nbody_v3.g
exec_v4:nbody_v4.g 
	taskset -c 3 ./nbody_v4.g

nbody_v1.g: nbody_v1.c
	gcc -march=native -mavx2 -Ofast -fopt-info-all=nbody_v1.gcc.optrpt $< -o $@ -lm -fopenmp

nbody_v2.g: nbody_v2.c
	gcc -march=native -mavx2 -Ofast -fopt-info-all=nbody_v2.gcc.optrpt $< -o $@ -lm -fopenmp
nbody_v3.g:nbody_v3.c
	gcc -march=native -mavx2 -Ofast -fopt-info-all=nbody_v3.gcc.optrpt $< -o $@ -lm -fopenmp
nbody_v4.g:nbody_v4.c
	gcc -march=native -mavx2 -Ofast -fopt-info-all=nbody_v4.gcc.optrpt $< -o $@ -lm -fopenmp

#Compilation et execution sur KNL "icc"
compil_intel :nbody_v1.i nbody_v2.i nbody_v3.i nbody_v4.i

exec_v1_icc:nbody_v1.i 
	taskset -c 3 ./nbody_v1.i
exec_v2_icc:nbody_v2.i
	taskset -c 3 ./nbody_v2.i
exec_v3_icc:nbody_v3.i 
	taskset -c 3 ./nbody_v3.i
exec_v4_icc:nbody_v4.i 
	taskset -c 3 ./nbody_v4.i

nbody_v1.i: nbody_v1.c
	icc -xhost -Ofast -qopt-report $< -o $@ -qmkl -qopenmp
nbody_v2.i: nbody_v2.c
	icc -xhost -Ofast -qopt-report $< -o $@ -qmkl -qopenmp
nbody_v3.i: nbody_v3.c
	icc -xhost -Ofast -qopt-report $< -o $@ -qmkl -qopenmp

nbody_v4.i: nbody_v4.c
	icc -xhost -Ofast -qopt-report $< -o $@ -qmkl -qopenmp


clean:
	rm -Rf *~ nbody_v1.g nbody.i *.optrpt

