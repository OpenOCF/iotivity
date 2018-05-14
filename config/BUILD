# TODO: windows config

config_setting(
    name = "with_rd_client",
    define_values = {
        "with_rd": "client",
    },
    visibility = ["//visibility:public"]
)

config_setting(
    name = "with_rd_server",
    define_values = {
        "with_rd": "server",
    },
    visibility = ["//visibility:public"]
)

config_setting(
    name = "with_mq",
    define_values = {
        "with_mq": "true"
    },
    visibility = ["//visibility:public"]
)

config_setting(
    name = "with_mq_pub",
    define_values = {
        "mq": "pub",
    },
    visibility = ["//visibility:public"]
)

config_setting(
    name = "with_mq_sub",
    define_values = {
        "mq": "sub",
    },
    visibility = ["//visibility:public"]
)

config_setting(
    name = "with_mq_broker",
    define_values = {
        "mq": "broker",
    },
    visibility = ["//visibility:public"]
)

config_setting(
    name = "with_cloud",
    define_values = {
        "with_cloud": "true",
    },
    visibility = ["//visibility:public"]
)

config_setting(
    name = "disable_security",
    define_values = {
        "disable_security": "true",
    },
    visibility = ["//visibility:public"]
)

config_setting(
    name = "enable_tcp",
    define_values = {
        "enable_tcp": "true",
    },
    visibility = ["//visibility:public"]
)

config_setting(
    name = "darwin",
    values = { "host_cpu": "darwin",
               "cpu": "darwin"
    },
    visibility = ["//visibility:public"]
)

config_setting(
    name = "darwin64",
    values = { "host_cpu": "darwin_x86_64",
               "cpu": "darwin_x86_64" },
    visibility = ["//visibility:public"]
)

config_setting(
    name = "darwin_with_jni",
    values = {"host_cpu": "darwin",
#              "cpu": "armeabi-v7a",
#              "fat_apk_cpu": "x86_64"
#              "java_deps": "true"
              "host_java_toolchain": "@bazel_tools//tools/jdk:toolchain"
    },
    # define_values = {
    #     "with_jni": "true"
    # },
    visibility = ["//visibility:public"]
)

config_setting(
    name = "linux_with_jni",
    values = {"host_cpu": "k8",
              #"cpu": "armeabi-v7a",
              "host_java_toolchain": "@bazel_tools//tools/jdk:toolchain"
    },
    visibility = ["//visibility:public"]
)

config_setting(
    name = "android",
    values = {
        "cpu": "armeabi-v7a",
        #"fat_apk_cpu": "armeabi-v7a",
        "android_cpu": "armeabi-v7a",
        #"android_crosstool_top": "//external:android/crosstool",
        #"android_sdk": "@bazel_tools//tools/android:sdk"
    },
    # define_values = {
    #     "with_android": "true"
    # },
    visibility = ["//visibility:public"]
)

config_setting(
    name = "android_arm64",
    values = {
        "cpu": "arm64-v8a",
        #"fat_apk_cpu": "armeabi-v7a",
        "android_cpu": "arm64-v8a",
        #"android_crosstool_top": "//external:android/crosstool",
        #"android_sdk": "@bazel_tools//tools/android:sdk"
    },
    # define_values = {
    #     "with_android": "true"
    # },
    visibility = ["//visibility:public"]
)

config_setting(
    name = "android_x86",
    values = {
        #"fat_apk_cpu": "x86",
        # passing --fat_apk_cpu=x86 sets android_cpu?
        "cpu": "x86",
        "android_cpu": "x86",
        #"android_crosstool_top": "//external:android/crosstool",
        #"android_sdk": "@bazel_tools//tools/android:sdk"
    },
    # define_values = {
    #     "with_android": "true"
    # },
    visibility = ["//visibility:public"]
)

filegroup(
    name="config_h",
    srcs=["darwin.h"],
    visibility = ["//visibility:public"]
)

