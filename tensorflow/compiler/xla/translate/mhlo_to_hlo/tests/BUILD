load("//tensorflow:tensorflow.default.bzl", "filegroup")
load("//tensorflow/compiler/mlir:glob_lit_test.bzl", "glob_lit_tests")

package(
    default_visibility = [
        "//tensorflow:internal",
    ],
    licenses = ["notice"],
)

glob_lit_tests(
    data = [":test_utilities"],
    driver = "@llvm-project//mlir:run_lit.sh",
    test_file_exts = [
        "mlir",
    ],
)

# Bundle together all of the test utilities that are used by tests.
filegroup(
    name = "test_utilities",
    testonly = True,
    data = [
        "//tensorflow/compiler/xla/translate:xla-translate",
        "@llvm-project//llvm:FileCheck",
        "@llvm-project//llvm:not",
    ],
)
