lib_LTLIBRARIES =

LIBDSPRPC_CFLAGS = -fno-short-enums -U_DEBUG -DARM_ARCH_7A -DLE_ENABLE -DNO_HAL -DENABLE_UPSTREAM_DRIVER_INTERFACE -DUSE_SYSLOG -I$(top_srcdir)/inc

LIBDSPRPC_SOURCES = \
		service/fastrpc_apps_user.c \
		profile/fastrpc_perf.c \
		service/fastrpc_pm.c \
		service/fastrpc_config.c \
		service/fastrpc_async.c \
		memory/fastrpc_mem.c \
		service/fastrpc_notif.c \
		profile/fastrpc_latency.c \
		service/fastrpc_ioctl.c \
		debug/fastrpc_log.c \
		service/fastrpc_procbuf.c \
		service/fastrpc_cap.c \
		log_config.c \
		domain/dspsignal.c \
		dspqueue/dspqueue_cpu.c \
		dspqueue/dspqueue_rpc_stub.c \
		communication/listener_android.c \
		fileOperation/apps_std_imp.c \
		memory/apps_mem_imp.c \
		marshaling/apps_mem_skel.c \
		memory/rpcmem_linux.c \
		debug/adspmsgd.c \
		debug/adspmsgd_printf.c \
		common/std.c \
		common/std_path.c \
		common/std_mem.c \
		common/std_dtoa.c \
		common/std_strlprintf.c \
		common/BufBound.c \
		common/std_SwapBytes.c \
		common/smath.c \
		common/atomic.c \
		common/cae.c \
		common/platform_libs.c \
		common/pl_list.c \
		common/gpls.c \
		marshaling/remotectl_stub.c \
		marshaling/remotectl1_stub.c \
		marshaling/adspmsgd_apps_skel.c \
		marshaling/adspmsgd_adsp_stub.c \
		marshaling/adspmsgd_adsp1_stub.c \
		marshaling/apps_remotectl_skel.c \
		marshaling/adsp_current_process_stub.c \
		marshaling/adsp_current_process1_stub.c \
		marshaling/adsp_listener_stub.c \
		marshaling/adsp_listener1_stub.c \
		marshaling/apps_std_skel.c \
		marshaling/adsp_perf_stub.c \
		marshaling/adsp_perf1_stub.c \
		common/mod_table.c

LIBDEFAULT_LISTENER_SOURCES = \
				communication/adsp_default_listener.c \
				marshaling/adsp_default_listener_stub.c \
				marshaling/adsp_default_listener1_stub.c \
				common/std.c \
				common/std_mem.c

if ANDROID_CC
USE_LOG = -llog
endif

ADSP_CFLAGS = $(LIBDSPRPC_CFLAGS) -DDEFAULT_DOMAIN_ID=0

lib_LTLIBRARIES += libadsprpc.la
libadsprpc_la_SOURCES = $(LIBDSPRPC_SOURCES)
libadsprpc_la_LDFLAGS = -ldl -lm $(USE_LOG)
libadsprpc_la_CFLAGS = $(ADSP_CFLAGS)

lib_LTLIBRARIES += libadsp_default_listener.la
libadsp_default_listener_la_SOURCES = $(LIBDEFAULT_LISTENER_SOURCES)
libadsp_default_listener_la_DEPENDENCIES = libadsprpc.la
libadsp_default_listener_la_LDFLAGS = libadsprpc.la -shared -module -avoid-version $(USE_LOG)
libadsp_default_listener_la_CFLAGS = $(ADSP_CFLAGS) -DUSE_SYSLOG

CDSP_CFLAGS = $(LIBDSPRPC_CFLAGS) -DDEFAULT_DOMAIN_ID=3

lib_LTLIBRARIES += libcdsprpc.la
libcdsprpc_la_SOURCES = $(LIBDSPRPC_SOURCES)
libcdsprpc_la_LDFLAGS = -ldl -lm $(USE_LOG)
libcdsprpc_la_CFLAGS = $(CDSP_CFLAGS)

lib_LTLIBRARIES += libcdsp_default_listener.la
libcdsp_default_listener_la_SOURCES = $(LIBDEFAULT_LISTENER_SOURCES)
libcdsp_default_listener_la_DEPENDENCIES = libcdsprpc.la
libcdsp_default_listener_la_LDFLAGS = libcdsprpc.la -shared -module -avoid-version $(USE_LOG)
libcdsp_default_listener_la_CFLAGS = $(CDSP_CFLAGS) -DUSE_SYSLOG

SDSP_CFLAGS = $(LIBDSPRPC_CFLAGS) -DDEFAULT_DOMAIN_ID=2

lib_LTLIBRARIES += libsdsprpc.la
libsdsprpc_la_SOURCES = $(LIBDSPRPC_SOURCES)
libsdsprpc_la_LDFLAGS = -ldl -lm $(USE_LOG)
libsdsprpc_la_CFLAGS = $(SDSP_CFLAGS)

lib_LTLIBRARIES += libsdsp_default_listener.la
libsdsp_default_listener_la_SOURCES = $(LIBDEFAULT_LISTENER_SOURCES)
libsdsp_default_listener_la_DEPENDENCIES = libsdsprpc.la
libsdsp_default_listener_la_LDFLAGS = libsdsprpc.la -shared -module -avoid-version $(USE_LOG)
libsdsp_default_listener_la_CFLAGS = $(SDSP_CFLAGS) -DUSE_SYSLOG


bin_PROGRAMS = adsprpcd cdsprpcd sdsprpcd

adsprpcddir = $(libdir)
adsprpcd_SOURCES = domain/adsprpcd.c
adsprpcd_DEPENDENCIES = libadsp_default_listener.la
adsprpcd_CFLAGS = -I$(top_srcdir)/inc -DDEFAULT_DOMAIN_ID=0 -DUSE_SYSLOG
adsprpcd_LDADD = -ldl $(USE_LOG)


cdsprpcddir = $(libdir)
cdsprpcd_SOURCES = domain/cdsprpcd.c
cdsprpcd_DEPENDENCIES = libcdsp_default_listener.la
cdsprpcd_CFLAGS = -I$(top_srcdir)/inc -DDEFAULT_DOMAIN_ID=3 -DUSE_SYSLOG
cdsprpcd_LDADD =  -ldl $(USE_LOG)


sdsprpcddir = $(libdir)
sdsprpcd_SOURCES = domain/cdsprpcd.c
sdsprpcd_DEPENDENCIES = libsdsp_default_listener.la
sdsprpcd_CFLAGS = -I$(top_srcdir)/inc -DDEFAULT_DOMAIN_ID=2 -DUSE_SYSLOG
sdsprpcd_LDADD =  -ldl $(USE_LOG)


otherincludedir = $(includedir)/fastrpc
otherinclude_HEADERS = $(top_srcdir)/inc/*.h
