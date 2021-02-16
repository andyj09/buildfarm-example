Platform: cpu
Builing target for cpu platform should happen on the worker in the cpu queue
command that works:
 bazel run --remote_executor=grpc://localhost:8980 --platforms=:cpu_proc  --remote_default_exec_properties=cpu=1   --extra_toolchains=:custom_cpp_centos7_toolchain :main

command that doesn't work:
bazel run --remote_executor=grpc://localhost:8980 --platforms=:cpu_proc  --extra_toolchains=:custom_cpp_centos7_toolchain :main


Platform: gpu
Building target for gpu platform should happen on the worker in the gpu queue
command that works:
 bazel run --remote_executor=grpc://localhost:8980 --platforms=:gpu_proc  --remote_default_exec_properties=gpu=1  --extra_toolchains=:custom_cpp_centos7_toolchain :main_2 

command that doesn't work:
bazel run --remote_executor=grpc://localhost:8980 --platforms=:gpu_proc  --extra_toolchains=:custom_cpp_centos7_toolchain :main_2
