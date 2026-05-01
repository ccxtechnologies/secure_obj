#
# Since version 1.6 the asynchronous mode has been
# disabled by default. To re-enable it uncomment the
# corresponding CFLAG.
#

# Use ccflags-y instead of KBUILD_CFLAGS for modern kernels
ccflags-y += -I$(srctree)/include/
ccflags-y += -I$(src) -I$(srctree)/drivers/crypto
# Append any EXTRA_CFLAGS passed down by Buildroot/environment
ccflags-y += $(EXTRA_CFLAGS)

.SILENT:
securekeydev-objs = securekey_caam.o ioctl.o

obj-m += securekeydev.o

ifneq ($(KERNEL_BUILD),)
	KERNEL_MAKE_OPTS := -C ${KERNEL_BUILD} M=$(shell pwd)
else
	KERNEL_MAKE_OPTS := -C $(KERNEL_SRC) M=$(shell pwd)
endif

all:
	$(MAKE) $(KERNEL_MAKE_OPTS) modules

modules_install:
	$(MAKE) $(KERNEL_MAKE_OPTS) modules_install

clean:
	rm -f *.o *~ core .depend .*.cmd *.ko *.mod.c
	rm -f Module.markers Module.symvers modules.order
	rm -rf .tmp_versions Modules.symvers
