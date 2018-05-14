android_sdk_repository(
    name="androidsdk",
    # Linux default install locn:
    # path="/home/gar/Android/Sdk",
    # Mac:
    path="/Users/gar/sdk/android",
    api_level=27,	   # 24, 25: Nougat; 26, 27: Oreo
    # default: uses latest build tools installed
    # build_tools_version="26.1.1"
)

android_ndk_repository(
    name="androidndk",
    # no need to set path, Bazel will figure it out based on SDK path
    api_level=27,
)

# Third-party package for Boost, from https://github.com/nelhage/rules_boost
# This will download and compile Boost when you reference labels like "@boost//:iostreams"
git_repository(
    name = "com_github_nelhage_rules_boost",
    commit = "239ce40e42ab0e3fe7ce84c2e9303ff8a277c41a",
    remote = "https://github.com/nelhage/rules_boost",
)

load("@com_github_nelhage_rules_boost//:boost/boost.bzl", "boost_deps")
boost_deps()

# libcoap
new_http_archive(
    name = "libcoap",
    urls = ["https://github.com/dthaler/libcoap/archive/IoTivity-1.2.1d.zip"],
    sha256 = "aac5b9101fad4cf722f0166f2739ebcefe55ad0ca7aa475550b11c8eb4740511",
    strip_prefix = "libcoap-IoTivity-1.2.1d",
    build_file = "config/libcoap.BUILD",
)

# new_local_repository(
# 	name = "coap_hdrs",
# 	path = "/Users/gar/iotivity/gerrit/config/darwin",
# 	build_file = "config/darwin/BUILD",
# 	#build_file_content = "filegroup(name='foo', srcs=['darwin/coap.h','darwin/coap_config.h'])"
# )

# mbedtls
# for patching
# load(
#     # "@bazel_tools//tools/build_defs/repo:http.bzl",
#     "@//tools:http.bzl",
#     "http_archive",
#     "http_file",
# )

new_http_archive(
    name = "mbedtls",
    urls = ["https://github.com/ARMmbed/mbedtls/archive/mbedtls-2.4.2.zip"],
    sha256 = "dacb9f5dd438c456b9ef6627637f46e16fd41e86d828217ec9f8547d3d22a338",
    strip_prefix = "mbedtls-mbedtls-2.4.2",
    build_file = "config/mbedtls/BUILD",
)

    # urls = ["https://github.com/ARMmbed/mbedtls/archive/mbedtls-2.7.zip"],
    # sha256 = "ab1ea18e7fa721bb4ab08294ab34008c4a934841b037a3cfa5f7ce65648228a2",
    # strip_prefix = "mbedtls-mbedtls-2.7",

# tinycbor
new_http_archive(
    name = "tinycbor",
    urls = ["https://github.com/intel/tinycbor/archive/v0.5.1.zip"],
    sha256 = "48e664e10acec590795614ecec1a71be7263a04053acb9ee81f7085fb9116369",
    strip_prefix = "tinycbor-0.5.1",
    build_file = "config/tinycbor.BUILD",
)
