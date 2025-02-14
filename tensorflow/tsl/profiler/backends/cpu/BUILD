load("//tensorflow/tsl/platform:build_config_root.bzl", "if_static")
load("//tensorflow/tsl/platform:rules_cc.bzl", "cc_library")
load("//tensorflow/tsl/profiler/builds:build_config.bzl", "tf_profiler_copts")
load("//tensorflow:tensorflow.bzl", "tf_cc_test")

cc_library(
    name = "traceme_recorder",
    hdrs = ["traceme_recorder.h"],
    copts = tf_profiler_copts(),
    visibility = [
        "//tensorflow/core/profiler:internal",
        "//tensorflow/tsl/profiler:internal",
    ],
    deps = [
        "@com_google_absl//absl/container:flat_hash_map",
        "//tensorflow/tsl/platform:macros",
        "//tensorflow/tsl/platform:mutex",
        "//tensorflow/tsl/platform:thread_annotations",
        "//tensorflow/tsl/platform:types",
    ] + if_static([
        ":traceme_recorder_impl",
    ]),
)

cc_library(
    name = "traceme_recorder_impl",
    srcs = [
        "traceme_recorder.cc",
    ],
    hdrs = ["traceme_recorder.h"],
    copts = tf_profiler_copts(),
    visibility = [
        "//tensorflow/compiler/xla/stream_executor:__subpackages__",
        "//tensorflow/core/profiler:__pkg__",
        "//tensorflow/core/profiler/backends/cpu:__pkg__",
        "//tensorflow/python:__pkg__",
        "//tensorflow/tsl/platform/cloud:__pkg__",
        "//tensorflow/tsl/profiler:__pkg__",
    ],
    deps = [
        "//tensorflow/tsl/platform:env",
        "//tensorflow/tsl/platform:logging",
        "//tensorflow/tsl/platform:macros",
        "//tensorflow/tsl/platform:mutex",
        "//tensorflow/tsl/platform:thread_annotations",
        "//tensorflow/tsl/platform:types",
        "@com_google_absl//absl/container:flat_hash_map",
    ],
    alwayslink = True,
)

tf_cc_test(
    name = "traceme_recorder_test",
    srcs = ["traceme_recorder_test.cc"],
    deps = [
        ":traceme_recorder",
        "//tensorflow/tsl/platform:env",
        "//tensorflow/tsl/platform:env_impl",
        "//tensorflow/tsl/platform:logging",
        "//tensorflow/tsl/platform:notification",
        "//tensorflow/tsl/platform:test",
        "//tensorflow/tsl/platform:test_main",
        "//tensorflow/tsl/platform:types",
        "//tensorflow/tsl/profiler/utils:math_utils",
        "//tensorflow/tsl/profiler/utils:time_utils",
        "@com_google_absl//absl/container:flat_hash_map",
        "@com_google_absl//absl/strings",
    ],
)

cc_library(
    name = "annotation_stack",
    hdrs = ["annotation_stack.h"],
    copts = tf_profiler_copts(),
    visibility = [
        "//tensorflow/tsl/profiler:internal",
    ],
    deps = [
        "@com_google_absl//absl/strings",
        "//tensorflow/tsl/platform:macros",
        "//tensorflow/tsl/platform:types",
    ] + if_static([
        ":annotation_stack_impl",
    ]),
)

cc_library(
    name = "annotation_stack_impl",
    srcs = [
        "annotation_stack.cc",
        "annotation_stack.h",
    ],
    copts = tf_profiler_copts(),
    visibility = [
        "//tensorflow/core/profiler/backends/cpu:__pkg__",
        "//tensorflow/tsl/profiler:__pkg__",
    ],
    deps = [
        "//tensorflow/tsl/platform:macros",
        "//tensorflow/tsl/platform:types",
        "@com_google_absl//absl/strings",
    ],
    alwayslink = True,
)

cc_library(
    name = "host_tracer_utils",
    srcs = ["host_tracer_utils.cc"],
    hdrs = ["host_tracer_utils.h"],
    copts = tf_profiler_copts(),
    visibility = [
        "//tensorflow/core/profiler:internal",
        "//tensorflow/tsl/profiler:internal",
    ],
    deps = [
        ":traceme_recorder",
        "//tensorflow/core/profiler/protobuf:xplane_proto_cc",
        "//tensorflow/tsl/platform:types",
        "//tensorflow/tsl/profiler/utils:parse_annotation",
        "//tensorflow/tsl/profiler/utils:tf_op_utils",
        "//tensorflow/tsl/profiler/utils:xplane_builder",
        "//tensorflow/tsl/profiler/utils:xplane_utils",
        "@com_google_absl//absl/strings",
    ],
)
