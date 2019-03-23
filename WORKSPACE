workspace(name = "toktok")

load("@bazel_tools//tools/build_defs/repo:git.bzl", "git_repository")
load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")
load("//tools/workspace:github.bzl", "github_archive", "new_github_archive")

github_archive(
    name = "bazel_toolchains",
    repo = "bazelbuild/bazel-toolchains",
    sha256 = "75a57078391a46409cd612fa2eaaf9086bc53a29ac0ef83d8063096cc9d8f0e3",
    version = "e74ab3b",
)

# Protobuf
# =========================================================

# proto_library rules implicitly depend on @com_google_protobuf//:protoc,
# which is the proto-compiler.
# This statement defines the @com_google_protobuf repo.
github_archive(
    name = "com_google_protobuf",
    repo = "protocolbuffers/protobuf",
    sha256 = "cca676364ea5900373d701cf1991c9a571dab3c14f0da72dc4085d15f91d1fc2",
    version = "3a3956e8a258784461270961c6577341356bce52",
)

load("@com_google_protobuf//:protobuf_deps.bzl", "protobuf_deps")

protobuf_deps()

# Haskell
# =========================================================

github_archive(
    name = "io_tweag_rules_nixpkgs",
    repo = "tweag/rules_nixpkgs",
    sha256 = "3a2d245e60d41c139cf5d1bb6f5a358c0c8a4d26325285af8ed092b078fb6b1d",
    version = "v0.5.2",
)

github_archive(
    name = "io_tweag_rules_haskell",
    repo = "tweag/rules_haskell",
    sha256 = "41ae5d155e297a42a740a3a533ffa89afaf4f1f40d3261912b62c466f4ff2364",
    version = "6495f68985a27884a941fe1f3c824d8f35887534",
)

load("@io_tweag_rules_haskell//haskell:ghc_bindist.bzl", "haskell_register_ghc_bindists")
load("@io_tweag_rules_haskell//haskell:repositories.bzl", "haskell_repositories")
load("//third_party/haskell:haskell.bzl", "new_cabal_package")

haskell_repositories()

# This repository rule creates @ghc repository.
haskell_register_ghc_bindists(
    version = "8.4.4",
)

github_archive(
    name = "ai_formation_hazel",
    repo = "FormationAI/hazel",
    sha256 = "605c83e0bf54c0517413096403ccb7799d6278fdeffdbe1555d11265e8165b17",
    version = "ecf380e97cc2e2114f359c89e4d65cd9c6b0ca22",
)

load("@ai_formation_hazel//:hazel.bzl", "hazel_repositories")
load("//third_party/haskell:packages.bzl", "core_packages", "packages")

# TODO(iphydf): Enable this once hazel is good enough to do automatically what
# we do manually in third_party/haskell.
#hazel_repositories(
#    core_packages = core_packages,
#    packages = packages,
#)

[new_local_repository(
    name = "haskell_%s" % pkg.replace("-", "_"),
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
    sha256 = "869ce867b583acccc8b9943688cd4b50818ff81926063e2e342fc7c5892f0638",
    version = "0.16.5",
)

github_archive(
    name = "bazel_gazelle",
    repo = "bazelbuild/bazel-gazelle",
    sha256 = "a5b329e3d929247279005ba3cfda0c092a220085c0ed0505de1dcdd68dfc53bc",
    version = "0.16.0",
)

load("@io_bazel_rules_go//go:def.bzl", "go_register_toolchains", "go_rules_dependencies")
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
    name = "org_bitbucket_kardianos_osext",
    commit = "tip",
    importpath = "bitbucket.org/kardianos/osext",
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
    urls = ["https://boringssl.googlesource.com/boringssl/+archive/master-with-bazel.tar.gz"],
)

new_http_archive(
    name = "bzip2",
    build_file = "third_party/BUILD.bzip2",
    sha256 = "d70a9ccd8bdf47e302d96c69fecd54925f45d9c7b966bb4ef5f56b770960afa7",
    strip_prefix = "bzip2-1.0.6",
    urls = ["http://http.debian.net/debian/pool/main/b/bzip2/bzip2_1.0.6.orig.tar.bz2"],
)

github_archive(
    name = "com_google_googletest",
    repo = "google/googletest",
    sha256 = "55fc63da7baa58ced8165db0edd2d0d231414871ea1aa9d2c4a53f57849d26bf",
    version = "827515f8a092050901d4eb9fdc1ddbb972f38442",
)

new_github_archive(
    name = "curl",
    repo = "curl/curl",
    sha256 = "2b1cf218a1090556ad4437acbdca398e1d06bdac3091bc71b8a2a53a8026c776",
    version = "curl-7_61_1",
)

new_http_archive(
    name = "ffmpeg",
    build_file = "third_party/BUILD.ffmpeg",
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

new_http_archive(
    name = "json",
    build_file = "third_party/BUILD.json",
    sha256 = "9588d63557333aaa485e92221ec38014a85a6134e7486fe3441e0541a5a89576",
    strip_prefix = "include",
    urls = ["https://github.com/nlohmann/json/releases/download/v3.3.0/include.zip"],
)

new_http_archive(
    name = "libcap",
    build_file = "third_party/BUILD.libcap",
    sha256 = "4ca80dc6f9f23d14747e4b619fd9784434c570e24a7346f326c692784ed83a86",
    strip_prefix = "libcap-2.25",
    urls = ["https://www.kernel.org/pub/linux/libs/security/linux-privs/libcap2/libcap-2.25.tar.gz"],
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
    sha256 = "a2b7f2f006c7f7e9aaef75b8846f9b4706efa41108a8138cb9299173c8829132",
    version = "dbbef6a7e13b2c2cb530c77eb28fe272d9a5b665",
)

new_http_archive(
    name = "libidn2",
    build_file = "third_party/BUILD.libidn2",
    sha256 = "53f69170886f1fa6fa5b332439c7a77a7d22626a82ef17e2c1224858bb4ca2b8",
    strip_prefix = "libidn2-2.0.5",
    urls = ["https://ftp.gnu.org/gnu/libidn/libidn2-2.0.5.tar.gz"],
)

new_github_archive(
    name = "libqrencode",
    repo = "fukuchi/libqrencode",
    sha256 = "8918db0e158a2f6cd26845b42c6d9d979d16907d65587b1a70c49b9df8dedd14",
    version = "953a31e57b982f049e28dec652bdc2daa748d4c2",
)

new_github_archive(
    name = "libsodium",
    repo = "jedisct1/libsodium",
    sha256 = "bf00beb6dc5fba7703fb4ab4664c332e2b27f8a3a4269e0c7038b58df2cc9886",
    version = "1.0.16",
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
    sha256 = "2d94b93dc1477dacb4334b72efff000c27a01c2d1bb37433a9aae6156ee3150c",
    version = "3863c869cc37c73d7e158118943650f6475867c1",
)

new_github_archive(
    name = "opus",
    repo = "xiph/opus",
    sha256 = "24ee6eb416b3bf15785e0c6a8d08b046f6a1d32e4c677908de314b5f841d2d6e",
    version = "83d5155f151ca47c9d6274ded1a7481f746b9a43",
)

new_http_archive(
    name = "portaudio",
    build_file = "third_party/BUILD.portaudio",
    sha256 = "f5a21d7dcd6ee84397446fa1fa1a0675bb2e8a4a6dceb4305a8404698d8d1513",
    strip_prefix = "portaudio",
    urls = ["http://www.portaudio.com/archives/pa_stable_v190600_20161030.tgz"],
)

new_http_archive(
    name = "pthread",
    build_file = "third_party/BUILD.pthread",
    sha256 = "e6aca7aea8de33d9c8580bcb3a0ea3ec0a7ace4ba3f4e263ac7c7b66bc95fb4d",
    strip_prefix = "pthreads-w32-2-9-1-release",
    urls = ["https://sourceware.org/pub/pthreads-win32/pthreads-w32-2-9-1-release.tar.gz"],
)

new_local_repository(
    name = "psocket",
    build_file = "third_party/BUILD.psocket",
    path = "/",
)

new_http_archive(
    name = "sndfile",
    build_file = "third_party/BUILD.sndfile",
    sha256 = "1ff33929f042fa333aed1e8923aa628c3ee9e1eb85512686c55092d1e5a9dfa9",
    strip_prefix = "libsndfile-1.0.28",
    urls = ["http://www.mega-nerd.com/libsndfile/files/libsndfile-1.0.28.tar.gz"],
)

new_http_archive(
    name = "libxz",
    build_file = "third_party/BUILD.libxz",
    sha256 = "b512f3b726d3b37b6dc4c8570e137b9311e7552e8ccbab4d39d47ce5f4177145",
    strip_prefix = "xz-5.2.4",
    urls = ["https://netix.dl.sourceforge.net/project/lzmautils/xz-5.2.4.tar.gz"],
)

new_http_archive(
    name = "x11",
    build_file = "third_party/BUILD.x11",
    sha256 = "f62ab88c2a87b55e1dc338726a55bb6ed8048084fe6a3294a7ae324ca45159d1",
    strip_prefix = "libX11-1.6.7",
    urls = ["https://x.org/archive/individual/lib/libX11-1.6.7.tar.gz"],
)

new_http_archive(
    name = "xau",
    build_file = "third_party/BUILD.xau",
    sha256 = "c343b4ef66d66a6b3e0e27aa46b37ad5cab0f11a5c565eafb4a1c7590bc71d7b",
    strip_prefix = "libXau-1.0.8",
    urls = ["https://x.org/archive/individual/lib/libXau-1.0.8.tar.gz"],
)

new_http_archive(
    name = "xcb",
    build_file = "third_party/BUILD.xcb",
    sha256 = "0bb3cfd46dbd90066bf4d7de3cad73ec1024c7325a4a0cbf5f4a0d4fa91155fb",
    strip_prefix = "libxcb-1.13",
    urls = ["https://xcb.freedesktop.org/dist/libxcb-1.13.tar.gz"],
)

new_http_archive(
    name = "xcb_proto",
    build_file = "third_party/BUILD.xcb_proto",
    sha256 = "0698e8f596e4c0dbad71d3dc754d95eb0edbb42df5464e0f782621216fa33ba7",
    strip_prefix = "xcb-proto-1.13",
    urls = ["https://xcb.freedesktop.org/dist/xcb-proto-1.13.tar.gz"],
)

new_http_archive(
    name = "xdmcp",
    build_file = "third_party/BUILD.xdmcp",
    sha256 = "6f7c7e491a23035a26284d247779174dedc67e34e93cc3548b648ffdb6fc57c0",
    strip_prefix = "libXdmcp-1.1.2",
    urls = ["https://x.org/archive/individual/lib/libXdmcp-1.1.2.tar.gz"],
)

new_http_archive(
    name = "xext",
    build_file = "third_party/BUILD.xext",
    sha256 = "eb0b88050491fef4716da4b06a4d92b4fc9e76f880d6310b2157df604342cfe5",
    strip_prefix = "libXext-1.3.3",
    urls = ["https://x.org/archive/individual/lib/libXext-1.3.3.tar.gz"],
)

new_http_archive(
    name = "xss",
    build_file = "third_party/BUILD.xss",
    sha256 = "4f74e7e412144591d8e0616db27f433cfc9f45aae6669c6c4bb03e6bf9be809a",
    strip_prefix = "libXScrnSaver-1.2.3",
    urls = ["https://x.org/archive/individual/lib/libXScrnSaver-1.2.3.tar.gz"],
)

new_http_archive(
    name = "xorgproto",
    build_file = "third_party/BUILD.xorgproto",
    sha256 = "4b951e321ec089ce62ec8347e0fb512735763b315bf19a3467a75df7190435ff",
    strip_prefix = "xorgproto-xorgproto-2018.4",
    urls = ["https://gitlab.freedesktop.org/xorg/proto/xorgproto/-/archive/xorgproto-2018.4/xorgproto-xorgproto-2018.4.tar.gz"],
)

new_github_archive(
    name = "yasm",
    repo = "yasm/yasm",
    sha256 = "25370c6e88fb1a65a5caa1ba88e746dfbcd3eb1032de696d30e0dc00aa867312",
    version = "35af9720e36df19382a57be26643b0d6bb48a363",
)

# Maven dependencies
# =========================================================

load("@bazel_tools//tools/build_defs/repo:maven_rules.bzl", "maven_aar")

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
    sha256 = "60312e4ef03cdfea4db52b2c37a660f16e1a2afd665a872769925fcfd1509855",
    version = "326b4ce252c36aeff2232e241ff4bfd8d6f6e071",
)

load("@io_bazel_rules_scala//scala:scala.bzl", "scala_repositories")
load("@io_bazel_rules_scala//scala:toolchains.bzl", "scala_register_toolchains")
load("@io_bazel_rules_scala//scala_proto:scala_proto.bzl", "scala_proto_repositories")

scala_register_toolchains()

scala_repositories()

scala_proto_repositories()

git_repository(
    name = "gmaven_rules",
    commit = "c0571d8370ece2b5485fea8806cffdf8a9c8ff6b",
    remote = "https://github.com/aj-michael/gmaven_rules",
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
    name = "python2",
    version = "2.7",
)

python_repository(
    name = "python3",
    version = "3.5",
)

# Node.js
# =========================================================

github_archive(
    name = "org_pubref_rules_node",
    # We use our own for now because pubref seems to no longer be maintained.
    #repo = "pubref/rules_node",
    repo = "iphydf/rules_node",
    sha256 = "96102374ca25ba5112425f2a31acfb7848ff7d578a2911e14c631a8f99db71eb",
    version = "3de4a224c6395a55ca80365b480f2494506e482c",
)

load("@org_pubref_rules_node//node:rules.bzl", "node_repositories", "yarn_modules")

node_repositories()

yarn_modules(
    name = "yarn_modules",
    install_tools = [
        "sh",
        "dirname",
    ],
    deps = {
        "ansi-to-html": "0.6.4",
        "async": "2.6.0",
        "buffertools": "2.1.6",
        "ffi": "2.2.0",
        "firebase": "3.9.0",
        "firepad": "1.4.0",
        "grunt": "1.0.1",
        "grunt-jsdoc": "2.2.1",
        "grunt-shell": "2.1.0",
        "ink-docstrap": "1.3.2",
        "jsdoc": "3.5.5",
        "mktemp": "0.4.0",
        "mocha": "3.5.3",
        "ref": "1.3.5",
        "ref-array": "1.2.0",
        "ref-struct": "1.1.0",
        "should": "13.2.1",
        "underscore": "1.8.3",
    },
)

yarn_modules(
    name = "mocha_modules",
    deps = {"mocha": "3.5.3"},
)
