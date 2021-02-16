load(":custom_toolchain_config.bzl", "custom_toolchain_config")

package(default_visibility = ["//visibility:public"])

constraint_setting(name = "processor")

constraint_value(
    name = "cpu",
    constraint_setting = ":processor",
)

constraint_value(
    name = "gpu",
    constraint_setting = ":processor",
)

platform(
    name = "cpu_proc",
    constraint_values = [":cpu"],
    exec_properties = {"cpu" : "1"}
)

platform(
    name = "gpu_proc",
    constraint_values = [":gpu"],
    exec_properties = {"gpu" : "1"}
)

cc_binary(
    name = "main",
    srcs = ["main.cc"],
    target_compatible_with = [":cpu"],
    # work if this is set
    #exec_properties = {"cpu" : "1"}
)

cc_binary(
    name = "main_2",
    srcs = ["main_2.cc"],
    target_compatible_with = [":gpu"],
    # work if this is set
    #exec_properties = {"gpu" : "1"}
)


# Boilerplate configure toolchain
# Toolchain configuration
cc_toolchain_suite(
    name = "custom_toolchain",
    toolchains = { 
        "k8": "custom_cc_toolchain_linux",
        "gpu" : "custom_cc_toolchain_linux"
    },  
)

filegroup(name = "empty")

toolchain(
    name = "custom_cpp_centos7_toolchain",
    toolchain = ":custom_cc_toolchain_linux",
    toolchain_type = "@bazel_tools//tools/cpp:toolchain_type"
)

cc_toolchain(
    name = "custom_cc_toolchain_linux",
    all_files = ":empty",
    compiler_files = ":empty",
    dwp_files = ":empty",
    linker_files = ":empty",
    objcopy_files = ":empty",
    strip_files = ":empty",
    supports_param_files = 1,
    toolchain_config = ":custom_toolchain_config_linux",
    toolchain_identifier = "custom-toolchain",
)

custom_toolchain_config(
    name = "custom_toolchain_config_linux",
    distro = "centos7"
)
