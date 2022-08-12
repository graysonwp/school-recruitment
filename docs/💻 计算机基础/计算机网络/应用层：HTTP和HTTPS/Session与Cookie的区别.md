---
sidebar_position: 3
---

1. **Session**是**服务器端保持状态**的方案，**Cookie**是**客户端保持状态**的方案。
2. **Cookie保存在客户端本地**，客户请求服务器时**会将Cookie一起提交**；**Session保存在服务端，通过检索Sessionid查看状态**，保存Sessionid的方式可以采用Cookie，如果**禁用了Cookie**，可以**使用URL重写机制**（把Sessionid保存在URL中）。
