workspace(name = "toktok")

load("@bazel_tools//tools/build_defs/repo:git.bzl", "git_repository")
load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")
load("//tools/workspace:github.bzl", "github_archive", "new_github_archive")

github_archive(
    name = "bazel_toolchains",
    repo = "bazelbuild/bazel-toolchains",
    sha256 = "3c1940c409ccbc6f5512993f0f95ff81fadd193cbd2a8a061e18d9baaf2ca65b",
    version = "2.2.0",
)

github_archive(
    name = "rules_android",
    repo = "bazelbuild/rules_android",
    sha256 = "cd06d15dd8bb59926e4d65f9003bfc20f9da4b2519985c27e190cddc8b7a7806",
    version = "v0.1.1",
)

github_archive(
    name = "rules_cc",
    repo = "bazelbuild/rules_cc",
    sha256 = "06910242c6d47c5719efd5789cf34dac393034dc0fe4c73f1ed3aac739ffabdc",
    version = "be6ea43fc8b22f1c44f0ed9e9ab723dea1955238",
)

github_archive(
    name = "rules_java",
    repo = "bazelbuild/rules_java",
    sha256 = "7f4772b0ee2b46a042870c844e9c208e8a0960a953a079236a4bbd785e471275",
    version = "9eb38ebffbaf4414fa3d2292b28e604a256dd5a5",
)

github_archive(
    name = "rules_proto",
    repo = "bazelbuild/rules_proto",
    sha256 = "48a3382a47e9e9dca4ec0849c57fd4b57919a93a00d8ffb7e4c8d6715d1acc9d",
    version = "f6b8d89b90a7956f6782a4a3609b2f0eee3ce965",
)

github_archive(
    name = "rules_python",
    repo = "bazelbuild/rules_python",
    sha256 = "d3e40ca3b7e00b72d2b1585e0b3396bcce50f0fc692e2b7c91d8b0dc471e3eaf",
    version = "748aa53d7701e71101dfd15d800e100f6ff8e5d1",
)

github_archive(
    name = "bazel_skylib",
    repo = "bazelbuild/bazel-skylib",
    sha256 = "d786769a4c9bfd9d5fe7933cf70d8c9da506a49c9f24a8471d64de2ac529274a",
    version = "6970e21d290ceaa36502d0c94533b26e5ec18c0b",
)

# Protobuf
# =========================================================

# proto_library rules implicitly depend on @com_google_protobuf//:protoc,
# which is the proto-compiler.
# This statement defines the @com_google_protobuf repo.
github_archive(
    name = "com_google_protobuf",
    repo = "protocolbuffers/protobuf",
    sha256 = "9748c0d90e54ea09e5e75fb7fac16edce15d2028d4356f32211cfa3c0e956564",
    version = "v3.11.4",
)

load("@com_google_protobuf//:protobuf_deps.bzl", "protobuf_deps")

protobuf_deps()

# Haskell
# =========================================================

github_archive(
    name = "rules_nixpkgs",
    repo = "tweag/rules_nixpkgs",
    sha256 = "3a2d245e60d41c139cf5d1bb6f5a358c0c8a4d26325285af8ed092b078fb6b1d",
    version = "v0.5.2",
)

github_archive(
    name = "rules_sh",
    repo = "tweag/rules_sh",
    sha256 = "93fb94bec4228971343b1ecbb303450ff323f52c768d60eeb3a445acfa6328ff",
    version = "0c274ad480ed3eade49250abd04ff71655a07820",
)

github_archive(
    name = "rules_haskell",
    repo = "tweag/rules_haskell",
    sha256 = "b72c6f92b4cac0af92d91f35f4b392874805e07d412abaeeefc63e5b9b29cdb5",
    version = "827d654235189242b0a9d45df8bc8754469b4579",
)

load("@rules_haskell//haskell:ghc_bindist.bzl", "haskell_register_ghc_bindists")
load("@rules_haskell//haskell:repositories.bzl", "haskell_repositories")

haskell_repositories()

# This repository rule creates @ghc repository.
haskell_register_ghc_bindists(
    compiler_flags = [
        "-Wall",
        "-Werror",
        "-optP=-Wno-trigraphs",
        "-fdiagnostics-color=always",
    ],
    version = "8.6.5",
)

github_archive(
    name = "ai_formation_hazel",
    repo = "FormationAI/hazel",
    sha256 = "db5466c442c228cffab14c51daff46a7861fdea3ef62be3e80ccd4b8dc60ab3e",
    version = "fe4b139751951f9489434f3f26e96598a1afebe1",
)

load("@ai_formation_hazel//tools:mangling.bzl", "hazel_workspace")

#load("@ai_formation_hazel//:hazel.bzl", "hazel_repositories")
load("//third_party/haskell:haskell.bzl", "new_cabal_package")
load("//third_party/haskell:packages.bzl", "core_packages", "packages")

# TODO(iphydf): Enable this once hazel is good enough to do automatically what
# we do manually in third_party/haskell.
#hazel_repositories(
#    core_packages = core_packages,
#    packages = packages,
#)

[new_local_repository(
    name = hazel_workspace(pkg),
    build_file = "third_party/haskell/BUILD.bazel",
    path = "/usr",
) for pkg in core_packages.keys()]

[new_cabal_package(
    package = "%s-%s" % (
        pkg,
        data.version,
    ),
    sha256 = data.sha256,
) for pkg, data in packages.items()]

# Skydoc
# =========================================================

github_archive(
    name = "io_bazel_skydoc",
    repo = "bazelbuild/skydoc",
    sha256 = "6b9ab4cf5c781e467888ce14864e62f47adc4b6d0cb7a9838469440d25643a4b",
    version = "0.2.0",
)

load("@io_bazel_skydoc//skylark:skylark.bzl", "skydoc_repositories")

skydoc_repositories()

# Go
# =========================================================

github_archive(
    name = "io_bazel_rules_go",
    repo = "bazelbuild/rules_go",
    sha256 = "9fbaffc63aa802496b0de6ed708fce8fb4c34b27fa7fab6cfc64eeae900c19a7",
    version = "v0.22.1",
)

github_archive(
    name = "bazel_gazelle",
    repo = "bazelbuild/bazel-gazelle",
    sha256 = "8d2880d411e8461bab87c8bd239bf1b7ac2301f1af49f2b581ecc5cdc24b7206",
    version = "v0.20.0",
)

load("@io_bazel_rules_go//go:deps.bzl", "go_register_toolchains", "go_rules_dependencies")
load("@bazel_gazelle//:deps.bzl", "gazelle_dependencies", "go_repository")

go_rules_dependencies()

go_register_toolchains()

gazelle_dependencies()

go_repository(
    name = "com_github_streamrail_concurrent_map",
    commit = "master",
    importpath = "github.com/streamrail/concurrent-map",
)

go_repository(
    name = "com_github_petermattis_goid",
    commit = "master",
    importpath = "github.com/petermattis/goid",
)

go_repository(
    name = "com_github_sasha_s_go_deadlock",
    commit = "master",
    importpath = "github.com/sasha-s/go-deadlock",
)

go_repository(
    name = "com_github_kardianos_osext",
    commit = "master",
    importpath = "github.com/kardianos/osext",
)

# C/C++ dependencies
# =========================================================

new_local_repository(
    name = "asound",
    build_file = "third_party/BUILD.asound",
    path = "/usr",
)

new_local_repository(
    name = "ncurses",
    build_file = "third_party/BUILD.ncurses",
    path = "/usr",
)

new_local_repository(
    name = "openal",
    build_file = "third_party/BUILD.openal",
    path = "/usr",
)

new_local_repository(
    name = "opencv",
    build_file = "third_party/BUILD.opencv",
    path = "/usr",
)

new_local_repository(
    name = "sqlite3",
    build_file = "third_party/BUILD.sqlite3",
    path = "/usr",
)

http_archive(
    name = "boringssl",
    #sha256 = "39b512b2a7afb87bb054e16031f9142d5ca9bd1ceebed864b0978c264e11566b",
    urls = ["https://boringssl.googlesource.com/boringssl/+archive/refs/heads/master-with-bazel.tar.gz"],
)

http_archive(
    name = "bzip2",
    build_file = "@toktok//third_party:BUILD.bzip2",
    sha256 = "ab5a03176ee106d3f0fa90e381da478ddae405918153cca248e682cd0c4a2269",
    strip_prefix = "bzip2-1.0.8",
    urls = ["http://http.debian.net/debian/pool/main/b/bzip2/bzip2_1.0.8.orig.tar.gz"],
)

github_archive(
    name = "com_google_googletest",
    repo = "google/googletest",
    sha256 = "b18016e313e0a635b643371f8a33f9813103b600e894f71e8625f0b8215ae698",
    version = "e588eb1ff9ff6598666279b737b27f983156ad85",
)

new_github_archive(
    name = "curl",
    repo = "curl/curl",
    sha256 = "3dc2825102eaed44b84613a98486aac8f924742d8fcf329bf2b49dc42c4ef93a",
    version = "curl-7_69_1",
)

http_archive(
    name = "ffmpeg",
    build_file = "@toktok//third_party:BUILD.ffmpeg",
    sha256 = "eb0370bf223809b9ebb359fed5318f826ac038ce77933b3afd55ab1a0a21785a",
    strip_prefix = "ffmpeg-3.4.2",
    urls = ["http://ffmpeg.org/releases/ffmpeg-3.4.2.tar.bz2"],
)

new_github_archive(
    name = "filter_audio",
    repo = "irungentoo/filter_audio",
    sha256 = "6e5f3d705d674ba2b692253d67b116daa0c8bc9c8ff7bcaa5e2523a5ad9e8aab",
    version = "v0.0.1",
)

http_archive(
    name = "json",
    build_file = "@toktok//third_party:BUILD.json",
    sha256 = "87b5884741427220d3a33df1363ae0e8b898099fbc59f1c451113f6732891014",
    strip_prefix = "include",
    urls = ["https://github.com/nlohmann/json/releases/download/v3.7.3/include.zip"],
)

http_archive(
    name = "libcap",
    build_file = "@toktok//third_party:BUILD.libcap",
    sha256 = "db7de848064e656a0bb528dae6d53ff20c82e849d509cecd015a04d2fec8369d",
    strip_prefix = "libcap-2.33",
    urls = ["https://www.kernel.org/pub/linux/libs/security/linux-privs/libcap2/libcap-2.33.tar.gz"],
)

new_github_archive(
    name = "libconfig",
    repo = "hyperrealm/libconfig",
    sha256 = "a3ae202153fafb40558c26831429ce39845b2395ad8d30269a50e309a7585a8c",
    version = "v1.7.2",
)

new_github_archive(
    name = "libexif",
    repo = "libexif/libexif",
    sha256 = "b43387df5a3866836c2a1bc141889af1d977c2e0c17e718b1b27fd1b002cb551",
    version = "54b6f7fb6ae1d08602f9f7c44e0624c8344ee832",
)

http_archive(
    name = "libidn2",
    build_file = "@toktok//third_party:BUILD.libidn2",
    sha256 = "e1cb1db3d2e249a6a3eb6f0946777c2e892d5c5dc7bd91c74394fc3a01cab8b5",
    strip_prefix = "libidn2-2.3.0",
    urls = ["https://ftp.gnu.org/gnu/libidn/libidn2-2.3.0.tar.gz"],
)

new_github_archive(
    name = "libqrencode",
    repo = "fukuchi/libqrencode",
    sha256 = "ab58566242d0abc2c54592cc35eca00cf51cc91985f3c1fbd372fb2428a7195a",
    version = "e5cbbafe5bd2052829176d05f2fac00ca9dbe4b8",
)

new_github_archive(
    name = "libsodium",
    repo = "jedisct1/libsodium",
    sha256 = "1b72c0cdbc535ce42e14ac15e8fc7c089a3ee9ffe5183399fd77f0f3746ea794",
    version = "1.0.18",
)

new_github_archive(
    name = "libvpx",
    repo = "webmproject/libvpx",
    sha256 = "9032e21faf6e26dc298ed0cbbb2a5bec732b55c93effff6746c59a3afb356198",
    version = "e20be1b2340dd3115cd445eafd9c1c717b621298",
)

new_github_archive(
    name = "libzmq",
    repo = "zeromq/libzmq",
    sha256 = "710cbbbd97cd8ab6831466d8d4f2e9f491efacf34c24c72183c4e6428e203300",
    version = "v4.3.2",
)

new_github_archive(
    name = "opus",
    repo = "xiph/opus",
    sha256 = "24ee6eb416b3bf15785e0c6a8d08b046f6a1d32e4c677908de314b5f841d2d6e",
    version = "83d5155f151ca47c9d6274ded1a7481f746b9a43",
)

http_archive(
    name = "portaudio",
    build_file = "@toktok//third_party:BUILD.portaudio",
    sha256 = "f5a21d7dcd6ee84397446fa1fa1a0675bb2e8a4a6dceb4305a8404698d8d1513",
    strip_prefix = "portaudio",
    urls = ["http://www.portaudio.com/archives/pa_stable_v190600_20161030.tgz"],
)

http_archive(
    name = "pthread",
    build_file = "@toktok//third_party:BUILD.pthread",
    sha256 = "e6aca7aea8de33d9c8580bcb3a0ea3ec0a7ace4ba3f4e263ac7c7b66bc95fb4d",
    strip_prefix = "pthreads-w32-2-9-1-release",
    urls = ["https://sourceware.org/pub/pthreads-win32/pthreads-w32-2-9-1-release.tar.gz"],
)

new_local_repository(
    name = "psocket",
    build_file = "third_party/BUILD.psocket",
    path = "/",
)

http_archive(
    name = "sndfile",
    build_file = "@toktok//third_party:BUILD.sndfile",
    sha256 = "1ff33929f042fa333aed1e8923aa628c3ee9e1eb85512686c55092d1e5a9dfa9",
    strip_prefix = "libsndfile-1.0.28",
    urls = ["http://www.mega-nerd.com/libsndfile/files/libsndfile-1.0.28.tar.gz"],
)

http_archive(
    name = "libxz",
    build_file = "@toktok//third_party:BUILD.libxz",
    sha256 = "b512f3b726d3b37b6dc4c8570e137b9311e7552e8ccbab4d39d47ce5f4177145",
    strip_prefix = "xz-5.2.4",
    urls = ["https://netix.dl.sourceforge.net/project/lzmautils/xz-5.2.4.tar.gz"],
)

http_archive(
    name = "x11",
    build_file = "@toktok//third_party:BUILD.x11",
    sha256 = "f62ab88c2a87b55e1dc338726a55bb6ed8048084fe6a3294a7ae324ca45159d1",
    strip_prefix = "libX11-1.6.7",
    urls = ["https://x.org/archive/individual/lib/libX11-1.6.7.tar.gz"],
)

http_archive(
    name = "xau",
    build_file = "@toktok//third_party:BUILD.xau",
    sha256 = "c343b4ef66d66a6b3e0e27aa46b37ad5cab0f11a5c565eafb4a1c7590bc71d7b",
    strip_prefix = "libXau-1.0.8",
    urls = ["https://x.org/archive/individual/lib/libXau-1.0.8.tar.gz"],
)

http_archive(
    name = "xcb",
    build_file = "@toktok//third_party:BUILD.xcb",
    sha256 = "0bb3cfd46dbd90066bf4d7de3cad73ec1024c7325a4a0cbf5f4a0d4fa91155fb",
    strip_prefix = "libxcb-1.13",
    urls = ["https://xcb.freedesktop.org/dist/libxcb-1.13.tar.gz"],
)

http_archive(
    name = "xcb_proto",
    build_file = "@toktok//third_party:BUILD.xcb_proto",
    sha256 = "0698e8f596e4c0dbad71d3dc754d95eb0edbb42df5464e0f782621216fa33ba7",
    strip_prefix = "xcb-proto-1.13",
    urls = ["https://xcb.freedesktop.org/dist/xcb-proto-1.13.tar.gz"],
)

http_archive(
    name = "xdmcp",
    build_file = "@toktok//third_party:BUILD.xdmcp",
    sha256 = "6f7c7e491a23035a26284d247779174dedc67e34e93cc3548b648ffdb6fc57c0",
    strip_prefix = "libXdmcp-1.1.2",
    urls = ["https://x.org/archive/individual/lib/libXdmcp-1.1.2.tar.gz"],
)

http_archive(
    name = "xext",
    build_file = "@toktok//third_party:BUILD.xext",
    sha256 = "eb0b88050491fef4716da4b06a4d92b4fc9e76f880d6310b2157df604342cfe5",
    strip_prefix = "libXext-1.3.3",
    urls = ["https://x.org/archive/individual/lib/libXext-1.3.3.tar.gz"],
)

http_archive(
    name = "xss",
    build_file = "@toktok//third_party:BUILD.xss",
    sha256 = "4f74e7e412144591d8e0616db27f433cfc9f45aae6669c6c4bb03e6bf9be809a",
    strip_prefix = "libXScrnSaver-1.2.3",
    urls = ["https://x.org/archive/individual/lib/libXScrnSaver-1.2.3.tar.gz"],
)

http_archive(
    name = "xorgproto",
    build_file = "@toktok//third_party:BUILD.xorgproto",
    sha256 = "4b951e321ec089ce62ec8347e0fb512735763b315bf19a3467a75df7190435ff",
    strip_prefix = "xorgproto-xorgproto-2018.4",
    urls = ["https://gitlab.freedesktop.org/xorg/proto/xorgproto/-/archive/xorgproto-2018.4/xorgproto-xorgproto-2018.4.tar.gz"],
)

new_github_archive(
    name = "yasm",
    repo = "yasm/yasm",
    sha256 = "e8123135c857ca3a0511854e0709e04f345925ab196ee6c73112dc9fa8b41690",
    version = "ea8f2393611025c5d32ddfe022dddff5a1a5c989",
)

# JUnit5
# =========================================================

load("//tools/workspace:junit5.bzl", "junit_jupiter_java_repositories", "junit_platform_java_repositories")

junit_jupiter_java_repositories()

junit_platform_java_repositories()

# Maven dependencies
# =========================================================

load("@bazel_tools//tools/build_defs/repo:maven_rules.bzl", "maven_aar", "maven_jar")

local_repository(
    name = "org_bytedeco_javacpp_presets_ffmpeg_platform",
    path = "third_party/javacpp/ffmpeg",
)

local_repository(
    name = "org_bytedeco_javacpp_presets_opencv_platform",
    path = "third_party/javacpp/opencv",
)

maven_aar(
    name = "com_timehop_stickyheadersrecyclerview_library",
    artifact = "com.timehop.stickyheadersrecyclerview:library:0.4.3",
    sha1 = "44a237a0ebff7c7ebb10c79698f97f6d635d0e26",
)

maven_aar(
    name = "com_tonicartos_superslim",
    artifact = "com.tonicartos:superslim:0.4.13",
    sha1 = "b05a0931a2d97fd370dc4ae6e003a9f57eada69a",
)

maven_aar(
    name = "de_hdodenhof_circleimageview",
    artifact = "de.hdodenhof:circleimageview:2.1.0",
    sha1 = "c0fcd515432ccb654bc5b44af60320703880a0f6",
)

maven_aar(
    name = "com_sothree_slidinguppanel_library",
    artifact = "com.sothree.slidinguppanel:library:3.4.0",
    sha1 = "a46c103238d666c097f6fefcffb479ebb450d365",
)

maven_jar(
    name = "com_chuusai_shapeless",
    artifact = "com.chuusai:shapeless_2.11:2.3.3",
    sha1 = "ea34d4b6128b9090386945dcb952816bd9e87ce2",
)

maven_jar(
    name = "com_google_guava_guava",
    artifact = "com.google.guava:guava:19.0",
    sha1 = "6ce200f6b23222af3d8abb6b6459e6c44f4bb0e9",
)

maven_jar(
    name = "com_intellij_annotations",
    artifact = "com.intellij:annotations:12.0",
    sha1 = "bbcf6448f6d40abe506e2c83b70a3e8bfd2b4539",
)

maven_jar(
    name = "com_typesafe_scala_logging_scala_logging",
    artifact = "com.typesafe.scala-logging:scala-logging_2.11:3.7.2",
    sha1 = "5015fe84c5aec4f8eb3daa2d1663d447d65f8c02",
)

maven_jar(
    name = "junit_junit",
    artifact = "junit:junit:4.12",
    sha1 = "2973d150c0dc1fefe998f834810d68f278ea58ec",
)

maven_jar(
    name = "log4j_log4j",
    artifact = "log4j:log4j:1.2.17",
    sha1 = "5af35056b4d257e4b64b9e8069c0746e8b08629f",
)

maven_jar(
    name = "org_apache_commons_commons_lang3",
    artifact = "org.apache.commons:commons-lang3:3.4",
    sha1 = "5fe28b9518e58819180a43a850fbc0dd24b7c050",
)

maven_jar(
    name = "org_bytedeco_javacpp",
    artifact = "org.bytedeco:javacpp:1.4",
    sha1 = "6e9062d70f863a4e55b3827d42d302f94e89d7e5",
)

maven_jar(
    name = "org_bytedeco_javacpp_presets_ffmpeg",
    artifact = "org.bytedeco.javacpp-presets:ffmpeg:3.4.1-1.4",
    sha1 = "bf46f2d74014475c948f1a8e063fae50ab724520",
)

maven_jar(
    name = "org_bytedeco_javacpp_presets_opencv",
    artifact = "org.bytedeco.javacpp-presets:opencv:3.4.0-1.4",
    sha1 = "b82eeed2295f30369044b2520937d764efeb3e1e",
)

maven_jar(
    name = "org_bytedeco_javacv",
    artifact = "org.bytedeco:javacv:1.4",
    sha1 = "c443d8c648fb7e53428837e469ced47369a297af",
)

maven_jar(
    name = "org_bytedeco_javacv_platform",
    artifact = "org.bytedeco:javacv-platform:1.4",
    sha1 = "9a674bb8266e02f6c85b6f5644b7eab13119f14e",
)

maven_jar(
    name = "org_scalacheck_scalacheck",
    artifact = "org.scalacheck:scalacheck_2.11:1.14.0",
    sha1 = "60087bb4b94537ad2b4955559a8ead7bac5c615d",
)

maven_jar(
    name = "org_slf4j_slf4j_api",
    artifact = "org.slf4j:slf4j-api:1.7.25",
    sha1 = "da76ca59f6a57ee3102f8f9bd9cee742973efa8a",
)

maven_jar(
    name = "org_slf4j_slf4j_android",
    artifact = "org.slf4j:slf4j-android:1.7.22",
    sha1 = "74825860214ed889b38d0fc865b89af18f4e95a7",
)

maven_jar(
    name = "org_slf4j_slf4j_log4j12",
    artifact = "org.slf4j:slf4j-log4j12:1.7.22",
    sha1 = "3bb94b26c2ad2f8755302aa9bf96f03b23a76639",
)

# Scala toolchain
# =========================================================

github_archive(
    name = "io_bazel_rules_scala",
    repo = "bazelbuild/rules_scala",
    sha256 = "6be7a3e4a174590c069f502217a05437caf32ccaaea8ceb16d338f3af292c016",
    version = "0bb4bcb38359707157b823c2b0e7ad2370c90d8d",
)

load("@io_bazel_rules_scala//scala:scala.bzl", "scala_repositories")
load("@io_bazel_rules_scala//scala:toolchains.bzl", "scala_register_toolchains")
load("@io_bazel_rules_scala//scala_proto:scala_proto.bzl", "scala_proto_repositories")
load("@io_bazel_rules_scala//scala_proto:toolchains.bzl", "scala_proto_register_enable_all_options_toolchain")

scala_register_toolchains()

scala_repositories()

scala_proto_repositories()

scala_proto_register_enable_all_options_toolchain()

git_repository(
    name = "gmaven_rules",
    commit = "c0571d8370ece2b5485fea8806cffdf8a9c8ff6b",
    remote = "https://github.com/aj-michael/gmaven_rules",
    shallow_since = "1544654738 -0500",
)

load("@gmaven_rules//:gmaven.bzl", "gmaven_rules")

gmaven_rules()

android_sdk_repository(
    name = "androidsdk",
    api_level = 28,
    build_tools_version = "28.0.3",
    path = "third_party/android/sdk",
)

android_ndk_repository(
    name = "androidndk",
    api_level = 25,
    path = "third_party/android/android-ndk-r14b",
)

# Qt5
# =========================================================

new_local_repository(
    name = "qt",
    build_file = "third_party/BUILD.qt",
    path = "third_party/qt",
)

# x264
# =========================================================

new_local_repository(
    name = "x264",
    build_file = "third_party/BUILD.x264",
    path = "/usr",
)

# Python
# =========================================================

load("//tools/workspace:python.bzl", "python_repository")

python_repository(
    name = "python3",
    version = "3.5",
)

# Node.js
# =========================================================

#github_archive(
#    name = "rules_codeowners",
#    repo = "zegl/rules_codeowners",
#    #sha256 = "06910242c6d47c5719efd5789cf34dac393034dc0fe4c73f1ed3aac739ffabdc",
#    version = "bdc2f987cd0e15ebfa9b76689a4c9a472730a6f0",
#)
#
#github_archive(
#    name = "build_bazel_rules_nodejs",
#    repo = "bazelbuild/rules_nodejs",
#    sha256 = "171bdbd8386576ed2f6a3f8aff87eeb048f963981870a3a8432be7d12cf5b2cc",
#    version = "1.3.0",
#)
#
#load("@build_bazel_rules_nodejs//:index.bzl", "yarn_install")
#
#yarn_install(
#    name = "npm",
#    package_json = "//js-toxcore-c:package.json",
#    yarn_lock = "//js-toxcore-c:yarn.lock",
#)

#load("@npm//:install_bazel_dependencies.bzl", "install_bazel_dependencies")
#install_bazel_dependencies()

#load("@org_pubref_rules_node//node:rules.bzl", "node_repositories", "yarn_modules")
#
#node_repositories()
#
#yarn_modules(
#    name = "yarn_modules",
#    install_tools = [
#        "sh",
#        "dirname",
#    ],
#    deps = {
#        "ansi-to-html": "0.6.4",
#        "async": "2.6.0",
#        "buffertools": "2.1.6",
#        "ffi": "2.2.0",
#        "firebase": "3.9.0",
#        "firepad": "1.4.0",
#        "grunt": "1.0.1",
#        "grunt-jsdoc": "2.2.1",
#        "grunt-shell": "2.1.0",
#        "ink-docstrap": "1.3.2",
#        "jsdoc": "3.5.5",
#        "mktemp": "0.4.0",
#        "mocha": "3.5.3",
#        "ref": "1.3.5",
#        "ref-array": "1.2.0",
#        "ref-struct": "1.1.0",
#        "should": "13.2.1",
#        "underscore": "1.8.3",
#    },
#)
#
#yarn_modules(
#    name = "mocha_modules",
#    deps = {"mocha": "3.5.3"},
#)
