AUDIO_ROOT=$(PWD)
UAPI_OUT=$(PWD)
HEADER_INSTALL_DIR=$(KERNEL_SRC)/scripts
KERNEL_BINARY_DIR=$(KERNEL_SRC)/../kernel-build-artifacts

KBUILD_OPTIONS := AUDIO_ROOT=$(PWD)
KBUILD_OPTIONS += MODNAME=audio
KBUILD_OPTIONS += UAPI_OUT=$(PWD)

AUDIO_KERNEL_HEADERS_PATH1 =  $(shell ls ./include/uapi/linux/*.h)
AUDIO_KERNEL_HEADERS_PATH2 =  $(shell ls ./include/uapi/linux/mfd/wcd9xxx/*.h)
AUDIO_KERNEL_HEADERS_PATH3 =  $(shell ls ./include/uapi/sound/*.h)

KBUILD_OPTIONS += CONFIG_ARCH_ATOLL=y

obj-m := ipc/
obj-m += dsp/
obj-m += dsp/codecs/
obj-m += soc/
obj-m += asoc/
obj-m += asoc/codecs/
obj-m += asoc/codecs/bolero/
obj-m += asoc/codecs/tas2562/
obj-m += asoc/codecs/wcd937x/
obj-m += asoc/codecs/wcd938x/

all:
	$(shell mkdir $(shell pwd)/linux)
	$(shell mkdir $(shell pwd)/sound)
	$(shell mkdir $(shell pwd)/linux/mfd)
	$(shell mkdir $(shell pwd)/linux/mfd/wcd9xxx)
	$(shell cd $(KERNEL_BINARY_DIR) && $(KERNEL_SRC)/scripts/headers_install.sh $(UAPI_OUT)/linux/ $(AUDIO_ROOT)/include/uapi/linux/ $(notdir $(AUDIO_KERNEL_HEADERS_PATH1)))
	$(shell cd $(KERNEL_BINARY_DIR) && $(KERNEL_SRC)/scripts/headers_install.sh $(UAPI_OUT)/linux/mfd/wcd9xxx/ $(AUDIO_ROOT)/include/uapi/linux/mfd/wcd9xxx/ $(notdir $(AUDIO_KERNEL_HEADERS_PATH2)))
	$(shell cd $(KERNEL_BINARY_DIR) && $(KERNEL_SRC)/scripts/headers_install.sh $(UAPI_OUT)/sound/ $(AUDIO_ROOT)/include/uapi/sound/ $(notdir $(AUDIO_KERNEL_HEADERS_PATH3)))
	$(MAKE) -C $(KERNEL_SRC) M=$(shell pwd) modules $(KBUILD_OPTIONS)

modules_install:
	$(MAKE) INSTALL_MOD_STRIP=1 -C $(KERNEL_SRC) M=$(shell pwd) modules_install

clean:
	rm -f *.o *.ko *.mod.c *.mod.o *~ .*.cmd Module.symvers
	rm -rf .tmp_versions
