# bazel_rule_cuda
rules for bazel for build cuda code

port most code from tensorflow, use at risk

usage:

```python
#WORKSPACE
git_repository(
  name = "bazel_rule_cuda",
  remote = "https://github.com/biolee/bazel_rule_cuda",
)
load('@bazel_rule_cuda/gpus/cuda.bzl',cuda_configure)
cuda_configure('local_config_cuda')


#BUILD
load('@bazel_rule_cuda/gpus/cuda.bzl',cuda_library)

cuda_library(
  name='mycudalib',
  srcs='vectorAdd.cu.cc',
  hdrs=['main.h'],
  deps=[],
)

cc_binary(
  name='main',
  srcs=['main.cc'],
  hdrs=['main.h'],
  deps=[':mycudalib'],
)

#defalt build with -G -g to nvcc
bazel build :main
#defalt compile opt
bazel build -c=opt :main
```
