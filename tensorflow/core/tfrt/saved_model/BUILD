load("//tensorflow:tensorflow.bzl", "if_google")

package(
    default_visibility = [":friends"],
    licenses = ["notice"],
)

package_group(
    name = "friends",
    packages = [
        # Authorized users go here.
        # copybara:uncomment "//learning/brain/experimental/tfrt/...",
        # copybara:uncomment "//learning/brain/tfrt/...",
        # copybara:uncomment "//learning/infra/mira/...",
        # copybara:uncomment "//learning/serving/...",
        # copybara:uncomment "//third_party/auroraml/...",
        "//tensorflow/core/runtime_fallback/...",
        "//tensorflow/core/tfrt/saved_model/tests/...",
        "//tensorflow/core/tfrt/graph_executor/...",
        "//tensorflow/core/tfrt/tfrt_session/...",
        "//tensorflow_serving/...",
        "//platforms/xla/tests/saved_models/...",
        # copybara:uncomment "//quality/webanswers/servo2/...",
    ],
)

cc_library(
    name = "saved_model",
    srcs = [
        "saved_model.cc",
        "saved_model_import_input.cc",
        "saved_model_import_input.h",
    ],
    hdrs = ["saved_model.h"],
    tags = ["no_oss"],
    deps = [
        "@com_google_absl//absl/container:flat_hash_map",
        "@com_google_absl//absl/strings",
        "@com_google_absl//absl/synchronization",
        "@com_google_absl//absl/time",
        "@com_google_absl//absl/types:span",
        "//tensorflow/cc/saved_model:reader",
        "//tensorflow/compiler/mlir/tensorflow",
        "//tensorflow/compiler/mlir/tensorflow:import_model",
        "//tensorflow/compiler/mlir/tensorflow:translate_lib",
        "//tensorflow/compiler/mlir/tensorflow:upgrade_graph",
        "//tensorflow/compiler/mlir/tfrt:import_model",
        "//tensorflow/compiler/mlir/tfrt:saved_model",
        "//tensorflow/compiler/mlir/tfrt:tf_jitrt_kernels_alwayslink",
        "//tensorflow/compiler/mlir/tfrt:tfrt_compile_options",
        "//tensorflow/compiler/xla:status_macros",
        "//tensorflow/core:core_cpu_base",
        "//tensorflow/core:framework",
        "//tensorflow/core:lib",
        "//tensorflow/core/framework:graph_proto_cc",
        "//tensorflow/core/platform:enable_tf2_utils",
        "//tensorflow/core/platform:errors",
        "//tensorflow/core/platform:path",
        "//tensorflow/core/profiler/lib:traceme",
        "//tensorflow/core/protobuf:for_core_protos_cc",
        "//tensorflow/core/runtime_fallback/kernel:kernel_fallback_execute_compat",
        "//tensorflow/core/runtime_fallback/kernel:kernel_fallback_op_handler",
        "//tensorflow/core/runtime_fallback/runtime:runtime_fallback_alwayslink",
        "//tensorflow/core/tfrt/fallback:fallback_state",
        "//tensorflow/core/tfrt/graph_executor",
        "//tensorflow/core/tfrt/graph_executor:graph_execution_options",
        "//tensorflow/core/tfrt/mla:mla_utils",
        "//tensorflow/core/tfrt/runtime",
        "//tensorflow/core/tfrt/runtime:work_queue_interface",
        "//tensorflow/core/tfrt/tpu:tpu_resources",
        "//tensorflow/core/tfrt/utils",
        "//tensorflow/core/tfrt/utils:error_util",
        "//tensorflow/core/tfrt/utils:fallback_tensor",
        "//tensorflow/core/tfrt/utils:tfrt_graph_execution_state",
        "@tf_runtime//:befexecutor",
        "@tf_runtime//:core_runtime_alwayslink",
        "@tf_runtime//:hostcontext",
        "@tf_runtime//:metrics",
        "@tf_runtime//:support",
    ] + if_google([
        "//third_party/tf_runtime_google:streamz_metrics_registry_alwayslink",
    ]),
)

cc_library(
    name = "saved_model_testutil",
    testonly = 1,
    srcs = ["saved_model_testutil.cc"],
    hdrs = ["saved_model_testutil.h"],
    tags = ["no_oss"],
    deps = [
        ":saved_model",
        "//tensorflow/cc/saved_model:loader",
        "//tensorflow/compiler/mlir/tfrt:tfrt_compile_options",
        "//tensorflow/compiler/xla:status_macros",
        "//tensorflow/core:lib",
        "//tensorflow/core:protos_all_cc",
        "//tensorflow/core/framework:tensor_testutil",
        "//tensorflow/core/profiler/lib:traceme",
        "//tensorflow/core/tfrt/runtime",
        "//tensorflow_serving/apis:model_cc_proto",
        "//tensorflow_serving/apis:predict_cc_proto",
        "//tensorflow_serving/apis:prediction_log_cc_proto",
        "@tf_runtime//:hostcontext",
    ],
)

cc_library(
    name = "saved_model_import_input",
    srcs = ["saved_model_import_input.cc"],
    hdrs = ["saved_model_import_input.h"],
    deps = [
        "//tensorflow/compiler/mlir/tensorflow:import_model",
        "//tensorflow/compiler/mlir/tensorflow:upgrade_graph",
        "//tensorflow/core:core_cpu_base",
        "//tensorflow/core:framework",
        "//tensorflow/core/tfrt/fallback:fallback_state",
        "//tensorflow/core/tfrt/utils:tfrt_graph_execution_state",
        "@com_google_absl//absl/synchronization",
    ],
)

cc_library(
    name = "saved_model_mira_impl",
    srcs = ["saved_model_mira_impl.cc"],
    hdrs = ["saved_model_mira_impl.h"],
    deps = [
        ":saved_model",
    ] + if_google([
        "@com_google_absl//absl/status:statusor",
        "//learning/infra/mira/tfrt:tfrt_executable",
        "//learning/infra/mira/tfrt:tfrt_module",
        "//third_party/mira/mlarchive:status_macro",
        "//third_party/mira/mlvalue:value",
        "//third_party/mira/runtime:module",
        "//third_party/mira/runtime:vm",
        "//third_party/mira/runtime:vm_session",
        "//tensorflow/compiler/xla:status_macros",
        "//tensorflow/core/platform:status",
        "//tensorflow/core/tfrt/runtime",
    ]),
)
