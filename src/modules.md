# 模块划分

采用了前后端分离的方式进行开发.

## 前端

前端的业务代码主要在 `src` 中。
前端将各个模块划分为components, 便于开发维护, 以及模块复用。主要划分出了若干好友管理相关的组件 (如 `Contact.tsx`, `ContactFind.tsx` 等), 若干群聊管理相关的组件 (如 `GroupAdminPanel.tsx`, `GroupNotice.tsx` 等), 若干聊天相关的组件 (如 `ChatWindow.tsx`, `MessageInput.tsx` 等)。下面列举主要的模块：

```txt
.
├── public
│   ├── favicon.svg                         # 网页图标
│   └── protos
│       └── *.proto                         # 各类protobuf的格式
└── src
    ├── components
    │   ├── AudioPlayer.tsx                 # 音频播放器
    │   ├── AudioRecord.tsx                 # 音频录制器
    │   ├── ChatWindow.tsx                  # 聊天窗口
    │   ├── Contact.tsx                     # 联系人
    │   ├── ContactFind.tsx                 # 好友查找
    │   ├── ContactList.tsx                 # 好友列表
    │   ├── ContactListRaw.tsx              # 列举给定的用户
    │   ├── ContactPending.tsx              # 待添加的好友列表
    │   ├── FriendCategory.tsx              # 好友分类
    │   ├── GroupAdd.tsx                    # 拉人入群
    │   ├── GroupAdminPanel.tsx             # 群聊管理面板
    │   ├── GroupChat.tsx                   # 群聊窗口
    │   ├── GroupInvite.tsx                 # 群聊邀请
    │   ├── GroupList.tsx                   # 列举全部群聊
    │   ├── GroupListBar.tsx                # 消息列表
    │   ├── GroupNotice.tsx                 # 群通知
    │   ├── GroupPendingInvitation.tsx      # 邀请好友入群
    │   ├── GroupPendingInvitationList.tsx  # 待通过的群邀请
    │   ├── MessageInput.tsx                # 消息输出框（包括上传文件等）
    │   ├── MessageSearch.tsx               # 消息搜索
    │   ├── Sidebar.tsx                     # 侧边栏
    │   └── VideoPreview.tsx                # 视频播放器
    ├── constants
    │   └── string.ts
    ├── pages
    │   ├── _app.tsx             # 挂件
    │   ├── contact.tsx          # 联系人页面
    │   ├── contactaccept.tsx    # 待通过好友页面
    │   ├── friendcategory.tsx   # 好友分类页面
    │   ├── index.tsx            # 自动跳转到/main
    │   ├── login.tsx            # 登录页面
    │   ├── main.tsx             # 主页面，含全部功能
    │   ├── messagesearch.tsx    # 消息搜索
    │   ├── profile
    │   │   ├── [id].tsx         # 显示[id]的profile
    │   │   ├── index.tsx        # 显示我的profile
    │   │   └── password.tsx     # 修改密码
    │   ├── register.tsx         # 注册
    │   ├── userfindscreen.tsx   # 用户查找页面
    │   └── *.tsx                # 其他页面
    ├── redux
    │   ├── auth.ts              # JWT相关处理
    │   └── store.ts
    ├── styles
    │   └── globals.css
    └── utils
        ├── error_router.ts       # 错误处理
        ├── fetchFriendProfile.ts # 返回给定用户表的头像、用户名等信息
        ├── getmsg.ts             # 获取消息
        ├── my_id.ts              # 获取我的id
        ├── network.ts            # 请求后端资源
        ├── protobufTypes.ts      # protobuf类型
        ├── types.ts              # 类型
        ├── userfind.tsx          # 查找用户
        └── websocket.tsx         # websocket相关功能
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
