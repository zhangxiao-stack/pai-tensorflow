load("//tensorflow:tensorflow.bzl", "tf_cc_binary")
load("//tensorflow:tensorflow.default.bzl", "get_compatible_with_cloud")

package_group(
    name = "friends",
    packages = [
        # copybara:uncomment_begin(google-only)
        # "//platforms/xla/service/cpu/...",
        # "//learning/brain/experimental/tfrt/autofusion/...",
        # # TODO(ezhulenev): Clean up dependencies that are leforvers from Autofusion project.
        # "@tf_runtime//...",
        # "//third_party/tf_runtime_google/...",
        # "//tensorflow/compiler/mlir/tfrt/...",
        # copybara:uncomment_end(google-only)
        "//tensorflow/compiler/xla/mlir/...",
        "//tensorflow/compiler/xla/runtime/...",
        # TODO(ezhulenev): All targets depending on mlir must be under xla/mlir folder
        "//tensorflow/compiler/xla/service/cpu/...",
        "//tensorflow/compiler/xla/service/gpu/...",
    ],
)

package(
    default_visibility = [":friends"],
    licenses = ["notice"],
)

tf_cc_binary(
    name = "xla-runtime-opt",
    srcs = ["xla-runtime-opt.cc"],
    compatible_with = get_compatible_with_cloud(),
    deps = [
        "//tensorflow/compiler/xla/mlir/runtime/ir/tests:testlib",
        "//tensorflow/compiler/xla/mlir/runtime/transforms:compilation_pipeline_cpu",
        "//tensorflow/compiler/xla/mlir/runtime/transforms:compilation_pipeline_gpu",
        "//tensorflow/compiler/xla/mlir/runtime/transforms:passes",
        "//tensorflow/compiler/xla/mlir/transforms/math:passes",
        "//tensorflow/compiler/xla/mlir/transforms/memref:passes",
        "@llvm-project//mlir:FuncDialect",
        "@llvm-project//mlir:MathDialect",
        "@llvm-project//mlir:MemRefDialect",
        "@llvm-project//mlir:MlirOptLib",
    ],
)
