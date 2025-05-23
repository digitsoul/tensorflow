# Description:
#   Common functionality for TensorFlow tooling

load("//tensorflow:strict.default.bzl", "py_strict_library", "py_strict_test")
load("//tensorflow:tensorflow.bzl", "VERSION_MAJOR")
load("//tensorflow/core/platform:build_config_root.bzl", "if_pywrap")

package(
    # copybara:uncomment default_applicable_licenses = ["//tensorflow:license"],
    default_visibility = [
        "//tensorflow:__subpackages__",
        "//third_party/py/tf_keras/api:__subpackages__",
    ],
    licenses = ["notice"],
)

py_strict_library(
    name = "public_api",
    srcs = ["public_api.py"],
    deps = ["//tensorflow/python/util:tf_inspect"],
)

py_strict_test(
    name = "public_api_test",
    srcs = ["public_api_test.py"],
    data = if_pywrap(
        if_false = select({
            "//tensorflow:macos": ["//tensorflow:libtensorflow_framework.dylib"],
            "//tensorflow:windows": [],
            "//conditions:default": ["//tensorflow:libtensorflow_framework.so.%s" % VERSION_MAJOR],
        }),
    ),
    deps = [
        ":public_api",
        # copybara:uncomment "//third_party/py/google/protobuf:use_fast_cpp_protos",
        "//tensorflow/python/platform:test",
    ],
)

py_strict_library(
    name = "traverse",
    srcs = ["traverse.py"],
    deps = ["//tensorflow/python/util:tf_inspect"],
)

py_strict_test(
    name = "traverse_test",
    srcs = ["traverse_test.py"],
    data = if_pywrap(
        if_false = select({
            "//tensorflow:macos": ["//tensorflow:libtensorflow_framework.dylib"],
            "//tensorflow:windows": [],
            "//conditions:default": ["//tensorflow:libtensorflow_framework.so.%s" % VERSION_MAJOR],
        }),
    ),
    deps = [
        ":test_module1",
        ":test_module2",
        ":traverse",
        # copybara:uncomment "//third_party/py/google/protobuf:use_fast_cpp_protos",
        "//tensorflow/python/platform:test",
    ],
)

py_strict_library(
    name = "test_module1",
    srcs = ["test_module1.py"],
    deps = [
        ":test_module2",
    ],
)

py_strict_library(
    name = "test_module2",
    srcs = ["test_module2.py"],
)
