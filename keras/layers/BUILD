# Description:
#   Contains the Keras layers (internal TensorFlow version).

load("@org_keras//keras:keras.bzl", "cuda_py_test")

# buildifier: disable=same-origin-load
load("@org_keras//keras:keras.bzl", "tf_py_test")

package(
    # TODO(scottzhu): Remove non-keras deps from TF.
    default_visibility = [
        "//keras:friends",
        "//third_party/tensorflow/python/distribute:__pkg__",
        "//third_party/tensorflow/python/feature_column:__pkg__",
        "//third_party/tensorflow/python/training/tracking:__pkg__",
        "//third_party/tensorflow/tools/pip_package:__pkg__",
        "//third_party/tensorflow_models/official/projects/residual_mobilenet/modeling/backbones:__pkg__",
    ],
    licenses = ["notice"],
)

# A separate build for layers without serialization to avoid circular deps
# with feature column.
py_library(
    name = "layers",
    srcs = [
        "__init__.py",
        "serialization.py",
    ],
    srcs_version = "PY3",
    deps = [
        ":convolutional_recurrent",
        ":cudnn_recurrent",
        ":einsum_dense",
        ":embeddings",
        ":kernelized",
        ":noise",
        ":recurrent",
        ":recurrent_v2",
        ":rnn_cell_wrapper_v2",
        ":wrappers",
        "//keras/feature_column",
        "//keras/layers/activation",
        "//keras/layers/attention",
        "//keras/layers/convolutional",
        "//keras/layers/core",
        "//keras/layers/locally_connected",
        "//keras/layers/merging",
        "//keras/layers/normalization",
        "//keras/layers/pooling",
        "//keras/layers/preprocessing",
        "//keras/layers/regularization",
        "//keras/layers/reshaping",
        "//keras/premade_models",
        "//keras/utils:tf_utils",
    ],
)

py_library(
    name = "embeddings",
    srcs = ["embeddings.py"],
    srcs_version = "PY3",
    deps = [
        "//:expect_tensorflow_installed",
        "//keras:backend",
        "//keras:constraints",
        "//keras:regularizers",
        "//keras/engine:base_layer",
        "//keras/initializers",
        "//keras/utils:tf_utils",
    ],
)

cuda_py_test(
    name = "embeddings_test",
    size = "medium",
    srcs = ["embeddings_test.py"],
    python_version = "PY3",
    deps = [
        "//:expect_tensorflow_installed",
        "//keras",
        "//keras:combinations",
        "//keras:testing_utils",
        "//keras/layers",
    ],
)

py_library(
    name = "convolutional_recurrent",
    srcs = ["convolutional_recurrent.py"],
    srcs_version = "PY3",
    deps = [
        ":recurrent",
        "//:expect_numpy_installed",
        "//:expect_tensorflow_installed",
        "//keras:activations",
        "//keras:backend",
        "//keras:base_layer",
        "//keras:constraints",
        "//keras:regularizers",
        "//keras/engine:input_spec",
        "//keras/initializers",
        "//keras/utils:engine_utils",
        "//keras/utils:generic_utils",
        "//keras/utils:tf_utils",
    ],
)

py_library(
    name = "cudnn_recurrent",
    srcs = ["cudnn_recurrent.py"],
    srcs_version = "PY3",
    deps = [
        ":recurrent",
        ":recurrent_v2",
        "//:expect_tensorflow_installed",
        "//keras:backend",
        "//keras:constraints",
        "//keras:regularizers",
        "//keras/engine:input_spec",
        "//keras/initializers",
    ],
)

py_library(
    name = "einsum_dense",
    srcs = ["einsum_dense.py"],
    srcs_version = "PY3",
    deps = [
        "//:expect_tensorflow_installed",
        "//keras:activations",
        "//keras:base_layer",
        "//keras:constraints",
        "//keras:regularizers",
        "//keras/initializers",
    ],
)

py_library(
    name = "kernelized",
    srcs = ["kernelized.py"],
    srcs_version = "PY3",
    deps = [
        "//:expect_numpy_installed",
        "//:expect_tensorflow_installed",
        "//keras:base_layer",
        "//keras/engine:input_spec",
        "//keras/initializers",
    ],
)

py_library(
    name = "noise",
    srcs = ["noise.py"],
    srcs_version = "PY3",
    deps = [
        "//keras/layers/regularization:alpha_dropout",
        "//keras/layers/regularization:gaussian_dropout",
        "//keras/layers/regularization:gaussian_noise",
    ],
)

py_library(
    name = "recurrent",
    srcs = ["recurrent.py"],
    srcs_version = "PY3",
    deps = [
        "//:expect_numpy_installed",
        "//:expect_tensorflow_installed",
        "//keras:activations",
        "//keras:backend",
        "//keras:base_layer",
        "//keras:constraints",
        "//keras:regularizers",
        "//keras/engine:input_spec",
        "//keras/initializers",
        "//keras/utils:generic_utils",
        "//keras/utils:tf_utils",
    ],
)

py_library(
    name = "recurrent_v2",
    srcs = ["recurrent_v2.py"],
    srcs_version = "PY3",
    deps = [
        ":recurrent",
        "//:expect_tensorflow_installed",
        "//keras:activations",
        "//keras:backend",
        "//keras/engine:input_spec",
    ],
)

py_library(
    name = "rnn_cell_wrapper_v2",
    srcs = ["rnn_cell_wrapper_v2.py"],
    srcs_version = "PY3",
    deps = [
        ":recurrent",
        "//:expect_tensorflow_installed",
        "//keras/layers/legacy_rnn:rnn_cell_wrapper_impl",
    ],
)

py_library(
    name = "wrappers",
    srcs = ["wrappers.py"],
    srcs_version = "PY3",
    deps = [
        ":recurrent",
        "//:expect_tensorflow_installed",
        "//keras:backend",
        "//keras:base_layer",
        "//keras/engine:input_spec",
        "//keras/utils:generic_utils",
        "//keras/utils:layer_utils",
        "//keras/utils:tf_utils",
    ],
)

tf_py_test(
    name = "tensorflow_op_layer_test",
    size = "medium",
    srcs = ["tensorflow_op_layer_test.py"],
    python_version = "PY3",
    shard_count = 3,
    deps = [
        "//:expect_absl_installed",
        "//:expect_tensorflow_installed",
        "//keras",
        "//keras/saving",
    ],
)

tf_py_test(
    name = "convolutional_recurrent_test",
    size = "medium",
    srcs = ["convolutional_recurrent_test.py"],
    python_version = "PY3",
    shard_count = 8,
    tags = ["no_rocm"],
    deps = [
        "//:expect_absl_installed",
        "//:expect_numpy_installed",
        "//:expect_tensorflow_installed",
        "//keras",
    ],
)

cuda_py_test(
    name = "cudnn_recurrent_test",
    size = "medium",
    srcs = ["cudnn_recurrent_test.py"],
    python_version = "PY3",
    shard_count = 4,
    tags = [
        "no_windows_gpu",
    ],
    deps = [
        "//:expect_absl_installed",
        "//:expect_numpy_installed",
        "//:expect_tensorflow_installed",
        "//keras",
        "//keras:combinations",
    ],
)

tf_py_test(
    name = "subclassed_layers_test",
    size = "medium",
    srcs = ["subclassed_layers_test.py"],
    python_version = "PY3",
    shard_count = 3,
    deps = [
        "//:expect_absl_installed",
        "//:expect_numpy_installed",
        "//:expect_tensorflow_installed",
        "//keras",
    ],
)

tf_py_test(
    name = "einsum_dense_test",
    srcs = ["einsum_dense_test.py"],
    python_version = "PY3",
    deps = [
        ":einsum_dense",
        "//:expect_absl_installed",
        "//:expect_tensorflow_installed",
        "//keras",
    ],
)

tf_py_test(
    name = "simplernn_test",
    size = "medium",
    srcs = ["simplernn_test.py"],
    python_version = "PY3",
    shard_count = 4,
    tags = ["notsan"],
    deps = [
        "//:expect_absl_installed",
        "//:expect_numpy_installed",
        "//:expect_tensorflow_installed",
        "//keras",
        "//keras:combinations",
    ],
)

tf_py_test(
    name = "gru_test",
    size = "medium",
    srcs = ["gru_test.py"],
    python_version = "PY3",
    shard_count = 4,
    tags = [
        "notsan",  # http://b/62136390
    ],
    deps = [
        "//:expect_absl_installed",
        "//:expect_numpy_installed",
        "//:expect_tensorflow_installed",
        "//keras",
        "//keras:combinations",
    ],
)

tf_py_test(
    name = "lstm_test",
    size = "medium",
    srcs = ["lstm_test.py"],
    python_version = "PY3",
    shard_count = 4,
    tags = [
        "noasan",  # times out b/63678675
        "notsan",  # http://b/62189182
    ],
    deps = [
        "//:expect_absl_installed",
        "//:expect_numpy_installed",
        "//:expect_tensorflow_installed",
        "//keras",
    ],
)

tf_py_test(
    name = "recurrent_test",
    size = "medium",
    srcs = ["recurrent_test.py"],
    python_version = "PY3",
    shard_count = 12,
    tags = [
        "no_rocm",
        "notsan",  # TODO(b/170870794)
    ],
    deps = [
        "//:expect_absl_installed",
        "//:expect_numpy_installed",
        "//:expect_tensorflow_installed",
        "//keras",
    ],
)

cuda_py_test(
    name = "recurrent_v2_test",
    size = "medium",
    srcs = ["recurrent_v2_test.py"],
    python_version = "PY3",
    shard_count = 2,
    deps = [
        "//:expect_absl_installed",
        "//:expect_numpy_installed",
        "//:expect_tensorflow_installed",
        "//keras",
    ],
)

cuda_py_test(
    name = "lstm_v2_test",
    size = "medium",
    srcs = ["lstm_v2_test.py"],
    python_version = "PY3",
    shard_count = 12,
    tags = [
        "no_oss",
        "notsan",  # TODO(b/170954246)
    ],
    deps = [
        "//:expect_absl_installed",
        "//:expect_numpy_installed",
        "//:expect_tensorflow_installed",
        "//keras",
    ],
)

cuda_py_test(
    name = "gru_v2_test",
    size = "medium",
    srcs = ["gru_v2_test.py"],
    python_version = "PY3",
    shard_count = 12,
    tags = ["no_rocm"],
    deps = [
        "//:expect_absl_installed",
        "//:expect_numpy_installed",
        "//:expect_tensorflow_installed",
        "//keras",
        "//keras:combinations",
    ],
)

tf_py_test(
    name = "serialization_test",
    size = "small",
    srcs = ["serialization_test.py"],
    python_version = "PY3",
    deps = [
        "//:expect_absl_installed",
        "//:expect_tensorflow_installed",
        "//keras",
        "//keras:combinations",
    ],
)

tf_py_test(
    name = "kernelized_test",
    size = "small",
    srcs = ["kernelized_test.py"],
    python_version = "PY3",
    deps = [
        ":layers",
        "//:expect_absl_installed",
        "//:expect_numpy_installed",
        "//:expect_tensorflow_installed",
        "//keras",
        "//keras:backend",
        "//keras:combinations",
        "//keras/initializers",
    ],
)

tf_py_test(
    name = "wrappers_test",
    size = "medium",
    srcs = ["wrappers_test.py"],
    python_version = "PY3",
    shard_count = 12,
    tags = [
        "noasan",  # http://b/78599823
        "notsan",
    ],
    deps = [
        "//:expect_absl_installed",
        "//:expect_numpy_installed",
        "//:expect_tensorflow_installed",
        "//keras",
        "//keras:combinations",
    ],
)

tf_py_test(
    name = "rnn_cell_wrapper_v2_test",
    size = "medium",
    srcs = ["rnn_cell_wrapper_v2_test.py"],
    python_version = "PY3",
    shard_count = 4,
    tags = [
        "notsan",
    ],
    deps = [
        "//:expect_absl_installed",
        "//:expect_numpy_installed",
        "//:expect_tensorflow_installed",
        "//keras",
        "//keras:combinations",
        "//keras/layers/legacy_rnn:rnn_cell_impl",
        "//keras/legacy_tf_layers:layers_base",
    ],
)

tf_py_test(
    name = "layers_test",
    size = "small",
    srcs = ["layers_test.py"],
    python_version = "PY3",
    deps = [
        ":layers",
        "//:expect_tensorflow_installed",
    ],
)
