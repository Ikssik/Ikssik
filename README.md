- 👋 Hi, I’m @Ikssik
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...
- 😄 Pronouns: ...
- ⚡ Fun fact: ...

<!---
Ikssik/Ikssik is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->

https://github.com/Ikssik/bot.git ...
ededam9@gmail.com ...
billion.adamen@gmail.com ...

2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
17
18
19
20
21
22
23
24
25
26
27
28
29
30
31
32
33
34
35
36
37
38
39
40
41
42
43
44
// Copyright 2019 The ChromiumOS Authors
// Use of this source code is governed by a BSD-style license that can be
// found in the LICENSE file.

syntax = "proto3";

package test_platform.multibot;

option go_package = "go.chromium.org/chromiumos/infra/proto/go/test_platform/multibot";

import "test_platform/request.proto";
import "test_platform/skylab_local_state/host_info.proto";
import "test_platform/skylab_test_runner/request.proto";

// Stable configuration settings needed for multi-bot tasks, shared by leader
// and followers
message MultiBotConfig {
  // Pub/Sub topic name
  string topic = 1;
}

// HostInfoStore stores Autotest host info blobs keyed by DUT name
message HostInfoStore {
  map<string, skylab_local_state.AutotestHostInfo> host_infos = 1;
}

// FollowerSpec contains the provisionable and nonprovisionable attributes for a
// follower swarming task.
message FollowerSpec {
  // Nonprovisionable labels for followers
  message StaticAttributes {
    test_platform.Request.Params.HardwareAttributes hardware_attributes = 1;

    test_platform.Request.Params.SoftwareAttributes software_attributes = 2;
  }

  StaticAttributes static_attributes = 1;

  // Prejob work required, primarily provisionable attributes to ensure
  skylab_test_runner.Request.Prejob prejob = 2;

  // Number of followers with these attributes, default to 1.
  int32 count = 3;
}
