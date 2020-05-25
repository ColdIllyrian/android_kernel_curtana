# auto-detect subdirs
ifeq ($(CONFIG_ARCH_ATOLL), y)
include $(srctree)/techpack/audio/4.0/config/atollauto.conf
export
endif

# Use USERINCLUDE when you must reference the UAPI directories only.
USERINCLUDE     += \
                -I$(srctree)/techpack/audio/4.0/include/uapi \

# Use LINUXINCLUDE when you must reference the include/ directory.
# Needed to be compatible with the O= option
LINUXINCLUDE    += \
                -I$(srctree)/techpack/audio/4.0/include/uapi \
                -I$(srctree)/techpack/audio/4.0/include/elliptic \
                -I$(srctree)/techpack/audio/4.0/include

ifeq ($(CONFIG_ARCH_ATOLL), y)
LINUXINCLUDE    += \
                -include $(srctree)/techpack/audio/4.0/config/atollautoconf.h
endif
obj-y += soc/
obj-y += dsp/
obj-y += dsp/elliptic
obj-y += ipc/
obj-y += asoc/
