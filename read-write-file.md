---
layout: default
title: Read/Write File
nav_order: 3
permalink: /read_write_file
---

[read-write-file.zig](src/read-write-file.zig)

```zig
const std = @import("std");

test {
    const value = "hello";

    var my_file = try std.fs.cwd().createFile("file.txt", .{ .read = true });
    defer my_file.close();

    _ = try my_file.write(value);

    var buf: [value.len]u8 = undefined;
    try my_file.seekTo(0);
    const read = try my_file.read(&buf);

    try std.testing.expectEqualStrings(value, buf[0..read]);
}

```
