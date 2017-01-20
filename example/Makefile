CC=gcc-4.8
CXX=g++-4.8


BLAS=-L/opt/intel/mkl/lib/intel64 -lmkl_intel_lp64 -lmkl_intel_thread -lmkl_core -lmkl_blas95_lp64 -DMSHADOW_USE_CBLAS=0 -DMSHADOW_USE_MKL=1 
CUDA=-DMSHADOW_USE_CUDA=1

#COMMFLAGS=-static -static-libgcc -static-libstdc++

CFLAGS=$(COMMFLAGS) -I ../include -Wall -O3 -msse3 -funroll-loops -Wno-unused-parameter -Wno-unknown-pragmas
LDFLAGS=$(COMMFLAGS) -L ../lib/linux -lmxnet $(BLAS) $(CUDA) -pthread

ifneq ($(OS), Windows_NT)
	OS := $(shell uname)
endif
ifneq ($(OS), Darwin)
	CFLAGS += -fopenmp
	LDFLAGS += -lgomp
endif

all: mlp lenet lenet_with_mxdataiter alexnet googlenet inception_bn resnet

lenet_with_mxdataiter: ./lenet_with_mxdataiter.cpp
	$(CXX) -c -std=c++11 $(CFLAGS) $^
	$(CXX) $(basename $@).o -o $@ $(LDFLAGS)
	-rm -f $(basename $@).o

lenet: ./lenet.cpp
	$(CXX) -c -std=c++11 $(CFLAGS) $^
	$(CXX) $(basename $@).o -o $@ $(LDFLAGS)
	-rm -f $(basename $@).o

mlp: ./mlp.cpp
	$(CXX) -c -std=c++11 $(CFLAGS) $^
	$(CXX) $(basename $@).o -o $@ $(LDFLAGS)
	-rm -f $(basename $@).o

alexnet: ./alexnet.cpp
	$(CXX) -c -std=c++11 $(CFLAGS) $^
	$(CXX) $(basename $@).o -o $@ $(LDFLAGS)
	-rm -f $(basename $@).o

googlenet: ./googlenet.cpp
	$(CXX) -c -std=c++11 $(CFLAGS) $^
	$(CXX) $(basename $@).o -o $@ $(LDFLAGS)
	-rm -f $(basename $@).o

inception_bn: ./inception_bn.cpp
	$(CXX) -c -std=c++11 $(CFLAGS) $^
	$(CXX) $(basename $@).o -o $@ $(LDFLAGS)
	-rm -f $(basename $@).o

resnet: ./resnet.cpp
	$(CXX) -c -std=c++11 $(CFLAGS) $^
	$(CXX) $(basename $@).o -o $@ $(LDFLAGS)
	-rm -f $(basename $@).o

# For simplicity, no link here
travis:
	$(CXX) -c -std=c++11 $(CFLAGS) ./mlp.cpp && rm -f mlp.o
	$(CXX) -c -std=c++11 $(CFLAGS) ./lenet.cpp && rm -f lenet.o
	$(CXX) -c -std=c++11 $(CFLAGS) ./lenet_with_mxdataiter.cpp && rm -f lenet_with_mxdataiter.o
	$(CXX) -c -std=c++11 $(CFLAGS) ./alexnet.cpp && rm -f alexnet.o
	$(CXX) -c -std=c++11 $(CFLAGS) ./googlenet.cpp && rm -f googlenet.o
	$(CXX) -c -std=c++11 $(CFLAGS) ./inception_bn.cpp && rm -f inception_bn.o
	$(CXX) -c -std=c++11 $(CFLAGS) ./resnet.cpp && rm -f resnet.o


clean:
	-rm -f mlp
	-rm -f lenet
	-rm -f lenet_with_mxdataiter
	-rm -f alexnet
	-rm -f googlenet
	-rm -f inception_bn
	-rm -f resnet
