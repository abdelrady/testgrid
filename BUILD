load("@io_bazel_rules_go//proto:def.bzl", "go_proto_library")

proto_library(
    name = "state_proto",
    srcs = ["state.proto"],
)

proto_library(
    name = "config_proto",
    srcs = ["config.proto"],
)

go_proto_library(
    name = "state",
    importpath = "k8s.io/test-infra/testgrid/state",
    proto = ":state_proto",
    visibility = ["//visibility:public"],
)

go_proto_library(
    name = "config",
    importpath = "k8s.io/test-infra/testgrid/config",
    proto = ":config_proto",
    visibility = ["//visibility:public"],
)

genrule(
    name = "gen-config",
    srcs = [
        "config.yaml",
    ],
    outs = ["testgrid-config"],
    cmd = "$(location //testgrid/cmd/config) --yaml=$< --output=$@",
    tools = [
        "//testgrid/cmd/config",
    ],
)

filegroup(
    name = "config-yaml",
    srcs = ["config.yaml"],
    visibility = ["//visibility:public"],
)

filegroup(
    name = "package-srcs",
    srcs = glob(["**"]),
    tags = ["automanaged"],
    visibility = ["//visibility:private"],
)

filegroup(
    name = "all-srcs",
    srcs = [
        ":package-srcs",
        "//testgrid/cmd/config:all-srcs",
        "//testgrid/cmd/updater:all-srcs",
    ],
    tags = ["automanaged"],
    visibility = ["//visibility:public"],
)
