# 星声 LIVE — LiveKit 实时语音起步项目

此项目是 Next.js App Router + LiveKit 的实时语音连接脚手架。包含首页、主播开播页、房间加入页、服务端 token API 和浏览器音频组件。

## 本地运行

1. 安装 Node.js 20+
2. 创建 LiveKit Cloud 项目或自建 LiveKit 服务
3. 复制 `.env.example` 为 `.env.local`，填写服务端密钥和公开连接 URL
4. 安装依赖并启动：

```bash
npm install
npm run dev
```

访问 `http://localhost:3000`。

## 环境变量

- `LIVEKIT_URL`: 服务端 LiveKit URL，例如 `wss://...`
- `LIVEKIT_API_KEY`: LiveKit API Key
- `LIVEKIT_API_SECRET`: LiveKit API Secret，**只能放在服务端**
- `NEXT_PUBLIC_LIVEKIT_URL`: 浏览器连接 LiveKit 的 WebSocket URL

## 生产前必须完成

- 在 `/api/token` 中验证用户 session；验证主播角色，不能相信客户端 `isHost`
- 加数据库持久化用户、房间、关注关系、麦位和直播状态
- 令房间 ID 不可被随意枚举，设置 token TTL 和房间权限
- 增加主播审核、举报、禁言、踢人、封禁和内容安全流程
- 为真实用户开播加上速率限制、权限提示、隐私政策和数据保留规则
- 加入麦位队列/锁；当前示例的麦位只是界面演示
- 部署时配置 HTTPS/WSS、域名、环境变量和监控

## 语音权限

演示中主播可发布麦克风音频，听众默认只订阅。正式项目需要基于已验证的用户角色在服务端发放 grant。
