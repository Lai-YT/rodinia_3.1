NVCC=nvcc
CC = g++

CUDA_INCLUDEPATH=/usr/local/cuda-6.5/include

NVCC_OPTS=-O3 -Xcompiler -m64 -lineinfo

GCC_OPTS=-O3 -Wall -Wextra -m64

OBJ = main_test_cu.o stats_logger.o cpuencode.o
SRC = main_test_cu.cu
EXE = pavle

ifdef TESTING 
override TESTING = -DTESTING
endif

ifdef CACHECWLUT
override TESTING = -DCACHECWLUT
endif

pavle: $(OBJ) 
	$(NVCC) $(TESTING) $(CACHECWLUT) $(NVCC_OPTS) $(OBJ) -o $(EXE) 

#cpuencode.o: cpuencode.cu
#	$(NVCC) -c $(NVCC_OPTS) cpuencode.cu

main_test_cu.o: main_test_cu.cu cutil.h
	$(NVCC) $(TESTING) -c main_test_cu.cu $(NVCC_OPTS) -I $(CUDA_INCLUDEPATH) 

.o:.cpp
	$(CC) ++ $(GCC_OPTS) -c $@ -o $<

clean:
	rm -f *.o $(EXE) 
