# TODO: make the targets //iotivity:java and //iotivity:android


# this is just the Java part of the JNI wrapper.  PoJo and Android
# libraries require different native builds, cc_binary for PoJo and
# cc_library for Android, so we do not specify them here.
java_library(
    name = "IotivityJ",
    srcs = glob(["common/src/main/java/**/*.java"]),
    visibility = ["//visibility:public"]
)

java_library(
    name = "IotivityJava",
    srcs = glob(["common/src/main/java/**/*.java"])
         + glob(["iotivity-java/src/main/java/**/*.java"]),
    # deps = [":IotivityJ"],
    # exports = [":IotivityJ"], # , "openocfjni"],
    # resources = [":libiotivity.so"],
    visibility = ["//visibility:public"]
)

# Task //javah generates jni headers. If it depends on IotivityDroid,
# then we have a circular dependency. So have both it and
# IotivityDroid depend on this.
android_library(
    name = "IotivityA",
    srcs = glob(["common/src/main/java/**/*.java"])
         + glob(["iotivity-android/src/main/java/**/*.java"])
         + ["//:androidconfig"],
    visibility = ["//visibility:public"]
)

android_library(
    name = "IotivityDroid",
    #srcs = [":IotivityA"],
    srcs = glob(["common/src/main/java/**/*.java"])
         + glob(["iotivity-android/src/main/java/**/*.java"])
         + ["//:androidconfig"],
    exports = [#":IotivityA",
               # android_library does not support runtime_deps or
               # resources, so we must export the native lib.  we
               # cannot use a cc_binary here, so we refer to a
               # cc_library build:
               ":iotivityjni"
    ],
    deps = ["//:iotivity"],
    visibility = ["//visibility:public"]
)

# this rule will build both .a and .so files
cc_library(
    name = "iotivityjni",
    linkstatic = False,
    # add -I opts for any Iotivity headers needed by the jni code:
    copts = ["-std=c++11",
             "-Iresource/c_common",
             "-Iresource/c_common/logger/include",
             "-Iresource/c_common/oic_malloc/include",
             "-Iresource/c_common/oic_string/include",
             "-Iresource/c_common/octhread/include",
             "-Iresource/csdk/logger/include",
             "-Iresource/csdk/connectivity/api",
             "-Iresource/csdk/connectivity/common/inc",
             "-Iresource/csdk/connectivity/inc",
             #"-Iresource/csdk/connectivity/lib/libcoap-4.1.1/include",
             "-Iresource/csdk/include",
             "-Iresource/csdk/resource-directory/include",
             "-Iresource/csdk/stack/include",
             "-Iresource/csdk/security/include",
             "-Iresource/csdk/security/include/internal",
             "-Iresource/csdk/security/provisioning/include",
             "-Iresource/csdk/security/provisioning/include/internal",
             "-Iresource/csdk/security/provisioning/include/oxm",
             "-Iresource/include",
             "-Iresource/oc_logger/include",

             "-Iexternal/libcoap/include",
             "-Iexternal/libcoap/include/coap",

             "-Iextlibs//mbedtls/mbedtls/include",
             "-Iexternal/local_jdk/include",

             "-Iconfig/darwin"
    ]
    + select({"//config:darwin_with_jni": ["-Iexternal/local_jdk/include/darwin",
                                           # darwing defines DEBUG which clashes with our src code:
                                           "-UDEBUG"],
              "//config:linux_with_jni": ["-Iexternal/local_jdk/include/linux"],
              "//conditions:default": ["BROKEN"]})
    + select({"//config:with_cloud": ["-Iresource/csdk/security/provisioning/include/cloud"],
              "//conditions:default": []}),

    defines = select({"//config:with_rd_client": ["RD_CLIENT"],
                      "//config:with_rd_server": ["RD_SERVER"],
                      "//conditions:default": []})
            + select({"//config:with_cloud": ["WITH_CLOUD"], "//conditions:default": []})
            + select({"//config:enable_tcp": ["WITH_TCP", "__WITH_TLS__"],
                      "//conditions:default": []})
            + select({"//config:with_mq": ["WITH_MQ"], "//conditions:default": []})
            + select({"//config:with_mq_pub": ["MQ_PUBLISHER"], "//conditions:default": []})
            + select({"//config:with_mq_sub": ["MQ_SUBSCRIBER"], "//conditions:default": []})
            + select({"//config:with_mq_broker": ["MQ_BROKER"], "//conditions:default": []}),

    srcs = glob(["jni/*.cpp"],
                exclude=[# if with_cloud:
                    "jni/JniOcAccountManager.cpp",
                    "jni/JniCreateAciIdListener.cpp",
                    "jni/JniOcCloudResultListener.cpp",
                    "jni/JniGetAclIdByDeviceListener.cpp",
                    # if with_cloud and enable_security:
                    "jni/JniOcCloudProvisioning.cpp",
                    # if RD client/server:
                    "jni/JniOcRDClient.cpp",
                    # only include these if disable_security != true
                    "jni/JniOcSecureResource.cpp",
                    "jni/JniOcProvisioning.cpp",
                    "jni/JniSecureUtils.cpp",
                    "jni/JniProvisionResultListner.cpp",
                    "jni/JniPinCheckListener.cpp",
                    "jni/JniDisplayPinListener.cpp",
                    "jni/JniDisplayVerifyNumListener.cpp",
                    "jni/JniConfirmNumListener.cpp",
                    # if with_mq
                    "jni/JniOnMQSubscribeListener.cpp",
                    "jni/JniOnMQTopicFoundListener.cpp"])
         + glob(["jni/*.h"], exclude=["jni/JniOcRDClient.h"])
         + glob(["jni/*.hpp"])
         + ["//:javah",  # make the generated JNI headers accessible
            "@local_jdk//:jni_header",
            "//config/darwin:iotivity_config.h",
            #"//config/darwin:coap_config.h",
            #"//config/darwin/coap:coap.h",
            # TODO: add iotivity shared libs as build sources
         ]
         + select({"//config:darwin_with_jni": ["@local_jdk//:jni_md_header-darwin"],
                   "//config:linux_with_jni": ["@local_jdk//:jni_md_header-linux"],
                   "//conditions:default": ["BROKEN"]})

         + select({"//config:disable_security": [],
                   "//conditions:default": ["jni/JniOcSecureResource.cpp",
                                            "jni/JniOcProvisioning.cpp",
                                            "jni/JniSecureUtils.cpp",
                                            "jni/JniProvisionResultListner.cpp",
                                            "jni/JniPinCheckListener.cpp",
                                            "jni/JniDisplayPinListener.cpp",
                                            "jni/JniDisplayVerifyNumListener.cpp",
                                            "jni/JniConfirmNumListener.cpp"]})

         + select({"//config:with_rd_client": ["jni/JniOcRDClient.cpp",
                                               "jni/JniOcRDClient.h"],
                   "//config:with_rd_server": ["jni/JniOcRDClient.cpp",
                                               "jni/JniOcRDClient.h"],
                   "//conditions:default": []})

         + select({"//config:with_cloud": ["jni/JniOcAccountManager.cpp",
                                           "jni/JniCreateAciIdListener.cpp",
                                           "jni/JniOcCloudResultListener.cpp",
                                           "jni/JniGetAclIdByDeviceListener.cpp"],
                   "//conditions:default": []})

         + select({"//config:with_mq": ["jni/JniOnMQSubscribeListener.cpp",
                                        "jni/JniOnMQTopicFoundListener.cpp"],
                   "//conditions:default": []}),

    # FIXME: do we need to list the shared libs in both srcs and deps?
    deps = [
        "//:iotivity_c_headers",
        "//:iotivity_cpp_headers",
        "@libcoap//:libcoap-lib",
        "@boost//:iostreams",
        "@boost//:variant"
    ],
    visibility = ["//visibility:public"]
)
