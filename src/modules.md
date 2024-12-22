# 模块划分

采用了前后端分离的方式进行开发.

## 前端

前端的业务代码主要在 `src` 中.

前端将各个模块划分为components, 便于开发维护, 以及模块复用。主要划分出了若干好友管理相关的组件 (如 `Contact.tsx`, `ContactFind.tsx` 等), 若干群聊管理相关的组件 (如 `GroupAdminPanel.tsx`, `GroupNotice.tsx` 等), 若干聊天相关的组件 (如 `ChatWindow.tsx`, `MessageInput.tsx` 等).

```txt
.
├── public
│   ├── favicon.svg
│   └── protos
│       ├── public_protos_resource.proto
│       ├── resource.proto
│       ├── resource_request.proto
│       └── response.proto
└── src
    ├── components
    │   ├── AudioPlayer.tsx
    │   ├── AudioRecord.tsx
    │   ├── ChatWindow.tsx
    │   ├── Contact.tsx
    │   ├── ContactFind.tsx
    │   ├── ContactList.tsx
    │   ├── ContactListRaw.tsx
    │   ├── ContactPending.tsx
    │   ├── FriendCategory.tsx
    │   ├── GroupAdd.tsx
    │   ├── GroupAdminPanel.tsx
    │   ├── GroupChat.tsx
    │   ├── GroupInvite.tsx
    │   ├── GroupList.tsx
    │   ├── GroupListBar.tsx
    │   ├── GroupNotice.tsx
    │   ├── GroupPendingInvitation.tsx
    │   ├── GroupPendingInvitationList.tsx
    │   ├── MessageInput.tsx
    │   ├── MessageSearch.tsx
    │   ├── Sidebar.tsx
    │   └── VideoPreview.tsx
    ├── constants
    │   └── string.ts
    ├── pages
    │   ├── _app.tsx
    │   ├── contact.tsx
    │   ├── contactaccept.tsx
    │   ├── friendcategory.tsx
    │   ├── groupchat.tsx
    │   ├── index.tsx
    │   ├── login.tsx
    │   ├── main.tsx
    │   ├── messagesearch.tsx
    │   ├── newgroup.tsx
    │   ├── profile
    │   │   ├── [id].tsx
    │   │   ├── index.tsx
    │   │   └── password.tsx
    │   ├── register.tsx
    │   ├── test.tsx
    │   └── userfindscreen.tsx
    ├── redux
    │   ├── auth.ts
    │   └── store.ts
    ├── styles
    │   └── globals.css
    └── utils
        ├── error_router.ts
        ├── fetchFriendProfile.ts
        ├── getmsg.ts
        ├── my_id.ts
        ├── network.ts
        ├── protobufTypes.ts
        ├── types.ts
        ├── userfind.tsx
        └── websocket.tsx
```

## 后端

后端的业务代码主要在 `view` 模块中, 此外这里也列出了 `config` 等其他模块:

```txt
.
├── config.rs        # 配置文件定义及反序列化
├── error.rs         # 错误处理和转换
├── jwt.rs           # JWT 创建, 提取和验证
├── view.rs          # 路由注册和集成测试
├── view
│   ├── avatar.rs    # 文件上传和用户头像上传
│   ├── contact.rs   # 联系人管理
│   ├── download.rs  # 文件下载
│   ├── feed.rs      # 消息通知
│   ├── group.rs     # 群聊管理
│   ├── history.rs   # 消息获取
│   ├── login.rs     # 用户登录和 websocket 注销
│   ├── message.rs   # 消息新建和存储
│   ├── openapi.rs   # OpenAPI 文档生成
│   ├── user.rs      # 用户管理和用户注册
│   └── ws.rs        # websocket 连接池管理
└── utility.rs       # 正则表达式以及其他工具函数
```

上表没有列出 `migration` crate 以及 `entity` 模块, 原因为 `migration` 将在[数据库设计](../database.html)中详细介绍, 而 `entity` 模块从 [`sea-orm`](https://www.sea-ql.org/SeaORM/) CLI 工具生成.
