include ../../common/make.config

NVCC=nvcc
NVLINK=nvcc
CC = g++

CUDA_INCLUDEPATH=$(CUDA_DIR)/include

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
	$(NVLINK) $(TESTING) $(CACHECWLUT) $(OBJ) -o $(EXE) 

#cpuencode.o: cpuencode.cu
#	$(NVCC) -c $(NVCC_OPTS) cpuencode.cu

main_test_cu.o: main_test_cu.cu cutil.h
	$(NVCC) $(TESTING) -c main_test_cu.cu -I $(CUDA_INCLUDEPATH) 

.o:.cpp
	$(CC) ++ $(GCC_OPTS) -c $@ -o $<

clean:
	rm -f *.o $(EXE) 
