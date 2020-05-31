licenses(["notice"])

exports_files(["LICENSE"])

load("//:bazel/braft.bzl", "braft_proto_library")
COPTS = [
    "-DGFLAGS=gflags",
    "-DOS_LINUX",
    "-DSNAPPY",
    "-DHAVE_SSE42",
    "-DNDEBUG",
    "-D__STDC_FORMAT_MACROS",
    "-fno-omit-frame-pointer",
    "-momit-leaf-frame-pointer",
    "-msse4.2",
    "-pthread",
    "-Wsign-compare",
    "-Wno-unused-parameter",
    "-Wno-unused-variable",
    "-Woverloaded-virtual",
    "-Wnon-virtual-dtor",
    "-Wno-missing-field-initializers",
    "-std=c++11",
    "-DGFLAGS_NS=google",
]

LINK_OPTS = [
    "-lm",
    "-lpthread",
]

cc_library (
    name = "braft_deps",
    deps = [
        "@com_github_brpc_brpc//:brpc",
        "@com_github_gflags_gflags//:gflags",
        "@com_github_google_glog//:glog",
        "@com_google_protobuf//:protobuf",
        "//:cc_braft_internal_proto",
        "//:braft",
    ],
)

cc_binary(
    name = "counter_server",
    srcs = glob([
        "counter/server.cpp",
    ]),
    defines = [],
    copts = COPTS,
    linkopts = LINK_OPTS,
    deps = [
        ":braft_deps",
        ":cc_counter_proto",
    ],
    visibility = ["//visibility:public"],
)

cc_binary(
    name = "counter_client",
    srcs = glob([
        "counter/client.cpp",
    ]),
    defines = [],
    copts = COPTS,
    linkopts = LINK_OPTS,
    deps = [
        ":braft_deps",
        ":cc_counter_proto",
    ],
    visibility = ["//visibility:public"],
)
braft_proto_library(
    name = "cc_counter_proto",
    srcs = glob([
        "counter/*.proto",
    ]),
    #include = "src",
    visibility = ["//visibility:public"],
)
