# TODO: platform-dependent configs
# TODO: with_tcp, etc

cc_library(
    name = "libcoap-lib",
    copts = ["-std=gnu99", "-fPIC",
             '-Wall', '-ffunction-sections',
             '-fdata-sections', '-fno-exceptions',

	     # to find headers in the libcoap source tree:
             "-Iexternal/libcoap/include",
             "-Iexternal/libcoap/include/coap",

	     # to find coap.h and coap_config.h:
             "-Iconfig/darwin",     # coap_config.h
             "-Iconfig/darwin/coap",  # coap.h
    ],
    defines = ["WITH_POSIX", "_GNU_SOURCE", "WITH_UPSTREAM_LIBCOAP"],
    srcs = glob(["src/**/*.c"],
                exclude=["src/**/coap_io_lwip.c"]),
    hdrs = glob(["include/**/*.h"])
    + ["@//config/darwin/coap:coap.h",
       "@//config/darwin:coap_config.h",
    ],
    visibility = ["//visibility:public"]
)
