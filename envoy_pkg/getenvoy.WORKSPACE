# Copyright 2019 Tetrate
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#     http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")

http_archive(
    name = "io_bazel_rules_docker",
    sha256 = "dc97fccceacd4c6be14e800b2a00693d5e8d07f69ee187babfd04a80a9f8e250",
    strip_prefix = "rules_docker-0.14.1",
    urls = ["https://github.com/bazelbuild/rules_docker/releases/download/v0.14.1/rules_docker-v0.14.1.tar.gz"],
)

load(
    "@io_bazel_rules_docker//repositories:repositories.bzl",
    container_repositories = "repositories",
)
container_repositories()

# This is NOT needed when going through the language lang_image
# "repositories" function(s).
load("@io_bazel_rules_docker//repositories:deps.bzl", container_deps = "deps")

container_deps()

load("@io_bazel_rules_docker//container:container.bzl", "container_pull")

container_pull(
    name = "distroless_base",
    digest = "sha256:2b0a8e9a13dcc168b126778d9e947a7081b4d2ee1ee122830d835f176d0e2a70", # 2020-02-27
    registry = "gcr.io",
    repository = "distroless/base",
)

load("//bazel:bazel_toolchains.bzl", "bazel_toolchains_repositories")

bazel_toolchains_repositories()

load("//bazel:rbe_envs.bzl", "rbe_envs")
load("@bazel_toolchains//rules:rbe_repo.bzl", "rbe_autoconfig")

rbe_autoconfig(
    name = "rbe_linux_glibc",
    create_java_configs = False,
    env = rbe_envs(),
    tag = "{RBE_IMAGE_TAG}",
    registry = "gcr.io",
    repository = "getenvoy-package/rbe-linux-glibc",
    use_checked_in_confs = "False",
)
