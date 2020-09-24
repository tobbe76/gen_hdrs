load(":write.bzl", "write_file")
load("@bazel_skylib//rules:common_settings.bzl", "string_flag")

string_flag(name = "hdr_destination", build_setting_default = "inc")

config_setting(
    name = "inc",
    flag_values = {
        ":hdr_destination": "inc",
    }
)

config_setting(
    name = "src",
    flag_values = {
        ":hdr_destination": "src",
    }
)

write_file(
    name = "gen_src",
    out = 'src/gen_header.h',
    content = 'char message[] = "This is src/gen_header.h";'
)

write_file(
    name = "gen_inc",
    out = 'inc/gen_header.h',
    content = 'char message[] = "This is inc/gen_header.h";'
)

cc_binary(
    name = "test",
    srcs = select({":src": ["src/main.c", "src/gen_header.h"],
                   ":inc": ["src/main.c", "inc/gen_header.h"]}),
    includes = ["inc", "src"],
)
