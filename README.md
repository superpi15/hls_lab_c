# hls_lab_c
Experiments for lab c 

## Trial Run with Official example

```shell
git clone https://github.com/Xilinx/Vitis_Libraries/ 
git checkout 2020.2                                          # switch to proper version, e.g., Xilinx 2020.2 environment
cd Vitis_Libraries/vision/L3/examples/letterbox/             # suppose we would like to try letterbox example 
source vlib.sh                                               # the setting file for HLS course server 
make host xclbin TARGET=sw_emu                               # combpile for Software emulation 
make run TARGET=sw_emu                                       # run the software emulation 
```

## Develope outside the Vitis folder using letterbox as a template

Need to configure paths in Makefile 

For example, XF_PROJ_ROOT should be specified by export, otherwise it will perform auto detection which may get wrong result. 
```shell
XF_PROJ_ROOT ?= $(shell bash -c 'export MK_PATH=$(MK_PATH); echo $${MK_PATH%/L3/*}')
```

Paths to the (1) host code and (2) building directory, should be set accordingly.
```shell
# ######################### Setting up Host Variables #########################
#Include Required Host Source Files
HOST_SRCS += $(XFLIB_DIR)/L3/examples/letterbox/xf_letterbox_tb.cpp
HOST_SRCS += $(XFLIB_DIR)/ext/xcl2/xcl2.cpp

CXXFLAGS += -D__SDSVHLS__
CXXFLAGS += -I$(XFLIB_DIR)/L3/examples/letterbox/build
CXXFLAGS += -I$(XFLIB_DIR)/ext/xcl2/
CXXFLAGS += -I$(XFLIB_DIR)/L1/include
```


