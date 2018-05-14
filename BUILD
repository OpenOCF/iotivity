cc_library(
    name = "iotivity",
    visibility = [ "//java:__pkg__"],

    # need this for octypes.h, which fails to include iotivity_config.h:
    defines = ["__WITH_DTLS__"],

    # list all the dirs that need to be on the include search path
    # find resource -name "*h" -print0 | xargs -0 dirname -- | sort | uniq
    copts = [
        "-Iresource",
        "-Iresource/c_common",
        "-Iresource/c_common/experimental",
        "-Iresource/c_common/ocatomic/include",
        "-Iresource/c_common/ocevent/include",
        "-Iresource/c_common/ocrandom/include",
#        "-Iresource/c_common/ocrandom/include/experimental",
        "-Iresource/c_common/octhread/include",
        "-Iresource/c_common/octimer/include",
        "-Iresource/c_common/oic_malloc/include",
        "-Iresource/c_common/oic_platform/include",
        "-Iresource/c_common/oic_string/include",
        "-Iresource/c_common/oic_time/include",
        # "-Iresource/c_common/windows/include",
        "-Iresource/csdk/connectivity/api",
        # "-Iresource/csdk/connectivity/build/tizen",
        "-Iresource/csdk/connectivity/common/inc",
        "-Iresource/csdk/connectivity/inc",
        # "-Iresource/csdk/connectivity/lib/libcoap-4.1.1/include",
        # "-Iresource/csdk/connectivity/lib/libcoap-4.1.1/tests",
        # "-Iresource/csdk/connectivity/src/bt_edr_adapter/android",
        # "-Iresource/csdk/connectivity/src/bt_edr_adapter/tizen",
        # "-Iresource/csdk/connectivity/src/bt_le_adapter/android",
        # "-Iresource/csdk/connectivity/src/bt_le_adapter/linux",
        # "-Iresource/csdk/connectivity/src/bt_le_adapter/tizen",
        "-Iresource/csdk/connectivity/src/ip_adapter/android",
        "-Iresource/csdk/connectivity/util/inc",
        # "-Iresource/csdk/connectivity/util/src/btpairing/android",
        "-Iresource/csdk/connectivity/util/src/camanager",
        # "-Iresource/csdk/connectivity/util/src/camanager/bt_le_manager/android",
        "-Iresource/csdk/include",
        "-Iresource/csdk/logger/include",
        "-Iresource/csdk/logger/include/experimental",
        # "-Iresource/csdk/resource-directory/include",
        "-Iresource/csdk/routing/include",
        "-Iresource/csdk/security/include",
        "-Iresource/csdk/security/include/experimental",
        "-Iresource/csdk/security/include/internal",
        "-Iresource/csdk/security/provisioning/include",
        # "-Iresource/csdk/security/provisioning/include/cloud",
        "-Iresource/csdk/security/provisioning/include/internal",
        "-Iresource/csdk/security/provisioning/include/oxm",
        # "-Iresource/csdk/security/tool/svrdbeditor_src",
        # "-Iresource/csdk/security/unittest",
        "-Iresource/csdk/stack/include",
        "-Iresource/csdk/stack/include/experimental",
        "-Iresource/csdk/stack/include/internal",
        # "-Iresource/csdk/stack/samples/linux/SimpleClientServer",
        # "-Iresource/csdk/stack/samples/linux/secure",
        # "-Iresource/csdk/stack/samples/tizen/SimpleClientServer",
        # "-Iresource/csdk/stack/samples/tizen/build",
        # "-Iresource/csdk/stack/test",
        # "-Iresource/docs",
        # "-Iresource/examples",
        # "-Iresource/examples/ocf_light",
        # "-Iresource/include",
        "-Iresource/oc_logger/include",
        # "-Iresource/oc_logger/include/targets",
        # "-Iresource/provisioning/examples",

        "-Iextlibs/cjson",

        "-Iconfig",
        "-Iconfig/darwin",
        "-Iconfig/darwin/coap",
        "-Iexternal/libcoap/include",
        "-Iexternal/libcoap/include/coap",

        # the custom config.h for mbedtls
        "-Iconfig",
        "-Iconfig/mbedtls",
        # the mbedtls lib headers:
        "-Iexternal/mbedtls/patched/include",
        "-Iexternal/mbedtls/patched/include/mbedtls",
        # "-Iexternal/mbedtls/include",
        # "-Iexternal/mbedtls/include/mbedtls",

        "-Iexternal/tinycbor/src",

        # OS X:
        "-UDEBUG",
    ],
    # + [capitalize(n) for n in glob(["resource/c_common/**/include"])]
    # + glob(["resource/**/include"])
    # + glob(["resource/**/api"]),

    deps = ["@mbedtls//:mbedtls-lib",
            "@libcoap//:libcoap-lib",
            "@tinycbor//:tinycbor-lib"],

    # all source files and header files must be explicitly listed
    srcs = glob(["resource/**/*.c"],
                # for now we excludef the optional stuff:
                exclude=["resource/**/bt*/**/*.c",
                         "resource/**/btpairing/**/*.c",
                         "resource/**/cloud/**/*.c",
                         "resource/**/ra_adapter/**/*.c",
                         "resource/**/resource-directory*/**/*.c",
                         "resource/**/routing/**/*.c",
                         "resource/**/sample*/**/*.c",

                         "resource/csdk/security/tool/**/*c",

                         "resource/csdk/connectivity/src/caping.c", # tcp only
                         "resource/**/tcp_adapter/**/*.c",

                         # multiowner
                         "resource/csdk/security/provisioning/src/multipleownershiptransfermanager.c",
                         "resource/csdk/security/provisioning/src/oxmpreconfpin.c",

                         "resource/csdk/security/src/base64.c",  # deprecated

                         "resource/c_common/octhread/src/noop/octhread.c",  # using posix

                         "resource/**/examples/**/*.c",
                         "resource/**/test*/**/*.c",
                         #"resource/csdk/connectivity/src/**/*.c",
                         "resource/**/android/**/*.c",
                         "resource/**/tizen/**/*.c",
                         "resource/**/windows/**/*.c",
                         ])
    + glob(["resource/**/*.h"])
    + glob(["extlibs/cjson/*.c"])
    + glob(["extlibs/cjson/*.h"])
    # + glob(["extlibs/mbedtls/mbedtls/library/*.c"])
    # + glob(["extlibs/mbedtls/mbedtls/include/**/*.h"])
    + [
        # select darwin:
        "//config/darwin:iotivity_config.h"
        #"//config/darwin/coap:coap.h",
    ],
#    + glob(["resource/c_common/**/*.h"]),
#                )
         # + glob(["resource/**/*.cpp"])
         # + glob(["resource/**/*.h"])
         # + glob(["resource/**/*.hpp"])
)

# This is a hack to get the JNI code to compile (on a mac). In the
# real world we would use autotools to generate the config file.
# genrule(
#     name="config_h",
#     srcs=["//config/darwin/coap:config.h"],
#     outs=["//config/darwin/coap:iotivity_config.h",],
#     visibility = [ "//java:__pkg__"],
#     cmd = "cp $(locations //config:config_h) \"$@\""
# )

# These two genrules generate files needed for Android builds. They
# are here instead of in java/BUILD because we want to generated files
# to go in the root bazel-genfiles directory; if they were in
# java/BUILD, they would end up in bazel-genfiles/java.  The generated
# files in bazel-genfiles will be accessible to cc_* rules that depend
# on these rules.

# This rule generates the BuildConfig file that Gradle generates.
# TODO: parameterize these, e.g. --define=SECURED=true
genrule(
    name="androidconfig",
    srcs=[],
    outs=["org/iotivity/base/BuildConfig.java"],
    cmd = """
    echo package org.iotivity.base\; > \"$@\";
    echo class BuildConfig {  >> \"$@\";
    echo     final public static int SECURED = 1\;   >> \"$@\";
    echo }  >> \"$@\"
    """,
# add echo lines for these if you want them:
        # buildConfigField 'int', 'SECURED', SECURED
        # buildConfigField 'int', 'WITH_TCP', WITH_TCP
        # buildConfigField 'int', 'WITH_CLOUD', WITH_CLOUD
        # buildConfigField "int", 'WITH_MQ_PUB', WITH_MQ_PUB
        # buildConfigField "int", 'WITH_MQ_SUB', WITH_MQ_SUB
        # buildConfigField "int", 'WITH_MQ_BROKER', WITH_MQ_BROKER
        # buildConfigField "String", 'RD_MODE', "\"RD_MODE\""
        # buildConfigField "int", 'WITH_TRANSPORT_EDR', WITH_TRANSPORT_EDR
        # buildConfigField "int", 'WITH_TRANSPORT_BLE', WITH_TRANSPORT_BLE
        # buildConfigField "int", 'WITH_TRANSPORT_NFC', WITH_TRANSPORT_NFC
        # buildConfigField "int", 'MULTIPLE_OWNER', MULTIPLE_OWNER
    visibility = [ "//java:__pkg__"]
)

# For JNI development we need to compile to classes, then run javah to
# generate headers, then compile the C/C++ code.  This rule runs javah
# and puts the resulting headers in bazel-genfiles. They will
# automatically be accessible to any cc_library or cc_binary that
# depends on this rule.
genrule(
    name = "javah",
    # srcs = [":openocf_japi"],
    srcs = ["//java:IotivityA"],
    # list only the files declaring native methods:
    outs = ["org_iotivity_base_OcAccountManager.h",
            "org_iotivity_base_OcCloudProvisioning.h",
            "org_iotivity_base_OcPresenceHandle.h",
            "org_iotivity_base_OcProvisioning.h",
            "org_iotivity_base_OcRDClient.h",
            "org_iotivity_base_OcRepresentation.h",
            "org_iotivity_base_OcResource.h",
            "org_iotivity_base_OcResourceHandle.h",
            "org_iotivity_base_OcResourceIdentifier.h",
            "org_iotivity_base_OcResourceRequest.h",
            "org_iotivity_base_OcResourceResponse.h",
            "org_iotivity_base_OcSecureResource.h"
    ],
    visibility = [ "//java:__pkg__"],
    cmd = """
    mkdir classes_tmp
    unzip -d classes_tmp $(location //java:IotivityA) > /dev/null
    for f in $(OUTS)
    do
        filename=$$(basename -- "$$f")
        extension="$${filename##*.}"
        filename="$${filename%.*}"
        filename=$${filename//_/.}
        echo $$filename
        javah -classpath classes_tmp -o $$f $$filename
    done
   rm -rf classes_tmp
""")

# a couple of dummy libraries, to expose the headers needed by the
# //java:iotivityjni target
cc_library(
    name="iotivity_c_headers",
    # hdrs=["extlibs/mbedtls/mbedtls/include/mbedtls/base64.h"
    # ]
    hdrs = glob(["resource/csdk/**/*.h"])
    + glob(["resource/c_common/**/*.h"]),
    visibility = [ "//java:__pkg__"],
)

cc_library(
    name="iotivity_cpp_headers",
    hdrs= glob(["resource/include/*.h"])
        + glob(["resource/include/*.hpp"])
        + glob(["resource/oc_logger/**/*.h"])
        + glob(["resource/oc_logger/**/*.hpp"]),
    visibility = [ "//java:__pkg__"],
)
