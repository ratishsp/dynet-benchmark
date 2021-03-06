

CUDA_PATH=/usr/local/cuda-7.5
EIGEN_PATH=${HOME}/usr/local/eigen
DYNET_PATH=${HOME}/work/dynet

DYNET_LIB_CPU=-ldynet
DYNET_LIB_GPU=-lgdynet -ldynetcuda -L${CUDA_PATH}/lib64 -lcublas -lcudart

# *** Mac or linux
UNAME_S := $(shell uname -s)
ifeq ($(UNAME_S),Darwin)
  CXX_FLAGS=-std=c++11 -I${EIGEN_PATH} -I${DYNET_PATH} -L${DYNET_PATH}/build/dynet -lc++ -Ofast
else
  CC=g++
  CXX_FLAGS=-std=c++11 -I${EIGEN_PATH} -I${DYNET_PATH} -L${DYNET_PATH}/build/dynet -DBOOST_REGEX -lboost_regex -Ofast
endif

# The -seq version is commented out for compatibility with master. If using the sequence-ops
# branch you can compile this program as well
# all: rnnlm-batch rnnlm-seq treenn bilstm-tagger bilstm-tagger-withchar
all: rnnlm-batch treenn bilstm-tagger bilstm-tagger-withchar

# gpu: rnnlm-batch-gpu rnnlm-seq-gpu treenn-gpu bilstm-tagger-gpu bilstm-tagger-withchar-gpu
gpu: rnnlm-batch-gpu treenn-gpu bilstm-tagger-gpu bilstm-tagger-withchar-gpu

clean:
	rm -f rnnlm-batch rnnlm-seq treenn bilstm-tagger bilstm-tagger-withchar rnnlm-batch-gpu rnnlm-seq-gpu treenn-gpu bilstm-tagger-gpu bilstm-tagger-withchar-gpu

rnnlm-batch: rnnlm-batch.cc
	${CC} -o rnnlm-batch rnnlm-batch.cc ${CXX_FLAGS} ${DYNET_LIB_CPU}

rnnlm-seq: rnnlm-seq.cc
	${CC} -o rnnlm-seq rnnlm-seq.cc ${CXX_FLAGS} ${DYNET_LIB_CPU}

treenn: treenn.cc
	${CC} -o treenn treenn.cc ${CXX_FLAGS} ${DYNET_LIB_CPU}

bilstm-tagger: bilstm-tagger.cc
	${CC} -o bilstm-tagger bilstm-tagger.cc ${CXX_FLAGS} ${DYNET_LIB_CPU}

bilstm-tagger-withchar: bilstm-tagger-withchar.cc
	${CC} -o bilstm-tagger-withchar bilstm-tagger-withchar.cc ${CXX_FLAGS} ${DYNET_LIB_CPU}

rnnlm-batch-gpu: rnnlm-batch.cc
	${CC} -o rnnlm-batch-gpu rnnlm-batch.cc ${CXX_FLAGS} ${DYNET_LIB_GPU}

rnnlm-seq-gpu: rnnlm-seq.cc
	${CC} -o rnnlm-seq-gpu rnnlm-seq.cc ${CXX_FLAGS} ${DYNET_LIB_GPU}

treenn-gpu: treenn.cc
	${CC} -o treenn-gpu treenn.cc ${CXX_FLAGS} ${DYNET_LIB_GPU}

bilstm-tagger-gpu: bilstm-tagger.cc
	${CC} -o bilstm-tagger-gpu bilstm-tagger.cc ${CXX_FLAGS} ${DYNET_LIB_GPU}

bilstm-tagger-withchar-gpu: bilstm-tagger-withchar.cc
	${CC} -o bilstm-tagger-withchar-gpu bilstm-tagger-withchar.cc ${CXX_FLAGS} ${DYNET_LIB_GPU}
