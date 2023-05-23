workspace(name = "tink_go_hcvault")

load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")

# -------------------------------------------------------------------------
# Bazel Skylib.
# -------------------------------------------------------------------------
# Release from 2023-02-09
# Protobuf vX.21.9 imports a version of bazel-skylib [1] that is incompatible
# with the one required by bazel-gazelle, so we make sure we have a newer
# version [2].
#
# [1] https://github.com/protocolbuffers/protobuf/blob/90b73ac3f0b10320315c2ca0d03a5a9b095d2f66/protobuf_deps.bzl#L28
# [2] https://github.com/bazelbuild/bazel-gazelle/issues/1290#issuecomment-1312809060
http_archive(
    name = "bazel_skylib",
    sha256 = "b8a1527901774180afc798aeb28c4634bdccf19c4d98e7bdd1ce79d1fe9aaad7",
    urls = [
        "https://mirror.bazel.build/github.com/bazelbuild/bazel-skylib/releases/download/1.4.1/bazel-skylib-1.4.1.tar.gz",
        "https://github.com/bazelbuild/bazel-skylib/releases/download/1.4.1/bazel-skylib-1.4.1.tar.gz",
    ],
)

# -------------------------------------------------------------------------
# Protobuf.
# -------------------------------------------------------------------------
# proto_library, cc_proto_library and java_proto_library rules implicitly
# depend respectively on:
#   * @com_google_protobuf//:proto
#   * @com_google_protobuf//:cc_toolchain
#   * @com_google_protobuf//:java_toolchain
# This statement defines the @com_google_protobuf repo.
# Release X.21.9 from 2022-10-26.
http_archive(
    name = "com_google_protobuf",
    strip_prefix = "protobuf-21.9",
    urls = ["https://github.com/protocolbuffers/protobuf/archive/refs/tags/v21.9.zip"],
    sha256 = "5babb8571f1cceafe0c18e13ddb3be556e87e12ceea3463d6b0d0064e6cc1ac3",
)

load("@com_google_protobuf//:protobuf_deps.bzl", "protobuf_deps")

protobuf_deps()

# -------------------------------------------------------------------------
# Bazel rules for Go.
# -------------------------------------------------------------------------
# Release from 2022-12-06
#
# NOTE: This version was chosen because since 0.38 this requires
# org_golang_x_tools v0.5.0 [1], while Tink imports v0.1.12. io_bazel_rules_go
# v0.37.0 is compatible with v0.1.12 [2].
#
# [1] https://github.com/bazelbuild/rules_go/blob/cf78385a58e278b542511d246bb1cef287d528e9/go/private/repositories.bzl#L73
# [2] https://github.com/bazelbuild/rules_go/blob/2a0f48241cf5a4838b9ccfde228863d75d6c646e/go/private/repositories.bzl#L73
http_archive(
    name = "io_bazel_rules_go",
    sha256 = "56d8c5a5c91e1af73eca71a6fab2ced959b67c86d12ba37feedb0a2dfea441a6",
    urls = [
        "https://mirror.bazel.build/github.com/bazelbuild/rules_go/releases/download/v0.37.0/rules_go-v0.37.0.zip",
        "https://github.com/bazelbuild/rules_go/releases/download/v0.37.0/rules_go-v0.37.0.zip",
    ],
)

# -------------------------------------------------------------------------
# Bazel Gazelle.
# -------------------------------------------------------------------------
# Release from 2023-01-14
http_archive(
    name = "bazel_gazelle",
    sha256 = "ecba0f04f96b4960a5b250c8e8eeec42281035970aa8852dda73098274d14a1d",
    urls = [
        "https://mirror.bazel.build/github.com/bazelbuild/bazel-gazelle/releases/download/v0.29.0/bazel-gazelle-v0.29.0.tar.gz",
        "https://github.com/bazelbuild/bazel-gazelle/releases/download/v0.29.0/bazel-gazelle-v0.29.0.tar.gz",
    ],
)

load("@io_bazel_rules_go//go:deps.bzl", "go_register_toolchains", "go_rules_dependencies")

go_rules_dependencies()

load("@bazel_gazelle//:deps.bzl", "gazelle_dependencies")

# Tink Go HashiCorp Vault KMS Deps.
load("//:deps.bzl", "tink_go_hcvault_dependencies")

# gazelle:repository_macro deps.bzl%tink_go_hcvault_dependencies
tink_go_hcvault_dependencies()

go_register_toolchains(
    nogo = "@//:tink_nogo",
    version = "1.19.9",
)

gazelle_dependencies()
