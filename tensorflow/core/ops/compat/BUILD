# Description:
# For keeping the history of OpDefs for every major version of TensorFlow,
# to validate that we don't make backwards-incompatible changes.

package(
    default_visibility = ["//visibility:private"],
)

licenses(["notice"])  # Apache 2.0

exports_files(["LICENSE"])

load(
    "//tensorflow:tensorflow.bzl",
    "tf_cc_test",
    "tf_cc_binary",
)

cc_library(
    name = "op_compatibility_lib",
    srcs = ["op_compatibility_lib.cc"],
    hdrs = ["op_compatibility_lib.h"],
    visibility = ["//visibility:public"],
    deps = [
        "//tensorflow/core:debug_ops_op_lib",
        "//tensorflow/core:framework",
        "//tensorflow/core:lib",
        "//tensorflow/core:ops",
        "//tensorflow/core:protos_all_cc",
    ],
)

tf_cc_test(
    name = "backwards_compatibility_test",
    size = "small",
    srcs = ["backwards_compatibility_test.cc"],
    data = [
        ":ops_history.v0.pbtxt",
        ":ops_history.v1.pbtxt",
        ":ops_history.v2.pbtxt",
        "//tensorflow/core:ops/ops.pbtxt",
    ],
    deps = [
        ":op_compatibility_lib",
        "//tensorflow/core:framework",
        "//tensorflow/core:lib",
        "//tensorflow/core:test",
        "//tensorflow/core:test_main",
    ],
)

tf_cc_binary(
    name = "update_ops",
    srcs = ["update_ops_main.cc"],
    deps = [
        ":op_compatibility_lib",
        "//tensorflow/core:framework",
        "//tensorflow/core:lib",
    ],
)
