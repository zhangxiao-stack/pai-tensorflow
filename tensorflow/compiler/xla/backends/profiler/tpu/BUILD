load("//tensorflow/tsl/platform:rules_cc.bzl", "cc_library")
load("//tensorflow/tsl/profiler/builds:build_config.bzl", "tf_profiler_copts")
load("//tensorflow:tensorflow.bzl", "if_with_tpu_support")

package(
    default_visibility = ["//tensorflow:internal"],
    licenses = ["notice"],
)

cc_library(
    name = "tpu_tracer",
    srcs = if_with_tpu_support(["tpu_tracer.cc"]),
    copts = tf_profiler_copts(),
    deps = [
        "//tensorflow/compiler/xla/stream_executor/tpu:status_helper",
        "//tensorflow/compiler/xla/stream_executor/tpu:tpu_api",
        "//tensorflow/compiler/xla/stream_executor/tpu:tpu_ops_c_api_hdrs",
        "//tensorflow/core/profiler:profiler_options_proto_cc",
        "//tensorflow/core/profiler/protobuf:xplane_proto_cc",
        "//tensorflow/tsl/platform:errors",
        "//tensorflow/tsl/platform:status",
        "//tensorflow/tsl/platform:types",
        "//tensorflow/tsl/profiler/lib:profiler_factory",
        "//tensorflow/tsl/profiler/lib:profiler_interface",
        "//tensorflow/tsl/profiler/utils:xplane_schema",
        "@com_google_absl//absl/strings",
    ],
    alwayslink = True,
)
