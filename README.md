# qfish-ranpo

基于 [qfish](https://github.com/hyun20202023-ui/dsh-qfish) 的定制改造版：把默认的「鲸鱼娘」人设换成《文豪野犬》的**江户川乱步**，用于 QQ 私聊陪伴。

## 来源与许可

- 上游项目：**qfish** by [hyun20202023-ui](https://github.com/hyun20202023-ui/dsh-qfish)（MIT）
- qfish 本身派生自 **dsh-onebot@1.4.0**（MPL-2.0）
- 本仓库保留上游全部许可声明，见 `LICENSE` 与 `NOTICE`
- 本仓库对上游的改动：人设（`defaults/persona/1-persona.md`）、界面文案与图标（`client.js`、`lib/console.js`、`assets/`）、默认配置（`defaults/settings.json`）。**未修改任何代码逻辑。**

## 改了什么

### 人设

`defaults/persona/1-persona.md` 由鲸鱼娘改写为江户川乱步：

| | 上游 qfish | 本仓库 |
|---|---|---|
| 身份 | 鲸鱼娘，蓝发小鲸鱼女仆 | 江户川乱步，武装侦探社第一位社员 |
| 自称 | （自报家门） | 「本侦探」 |
| 称呼对方 | — | 「念尘君」 |
| 性格 | 脾气温和，喜欢给人正面评价 | 天才级观察力、怕麻烦、自尊心强、心性像小孩 |
| 口癖 | 可爱语气 | 「哼哼——」「你是笨蛋吗？」「若合我意，一切皆好。」 |

其余三个文件（`2-language.md` / `3-scenes.md` / `4-tools.md`）保持原样——它们讲行为规则，与人格无关，且「不用 emoji、不承认自己是 AI」等条目正合用。

### 品牌替换

全仓「大肥鱼」字样零残留：

| 位置 | 改动 |
|---|---|
| `client.js` | 悬浮球图标（内嵌 base64）、`title` / `aria-label` |
| `lib/console.js` | 控制台页面标题 |
| `defaults/settings.json` | `botNames` 默认值 |
| `assets/logo.png` | 形象图 |
| `lib/web/src/assets/chibi.png` | 控制台角落图 |
| `README.md` | 标语 |

## 安装

```bash
dsh plugin --profile desktop add file:C:/path/to/qfish-ranpo
```

或在 profile 的 `cordis.patch.yml` 里挂载：

```yaml
- id: qfish
  name: qfish
  config:
    transport: forward-ws
    url: ws://127.0.0.1:3001
    accessTokenRef: ONEBOT_ACCESS_TOKEN
    respondToPrivate: true
    respondToGroup: false
    userAccessMode: allowlist
    userIds:
      - '你的QQ号'
  ```

## 前置条件

- **NapCat**（OneBot v11 协议端）已登录一个 QQ 小号
- 已配置 `dsh-onebot` 兼容的正向 WebSocket（默认 `127.0.0.1:3001`）
- `ONEBOT_ACCESS_TOKEN` 凭据**存纯 token 值，不能存 JSON**

## 两个已知坑

1. **不能与 `dsh-onebot` 共存** — 两者都注册 `/onebot/api` 并争用同一个 NapCat 连接。
2. **token 格式** — 凭据里必须存 `'你的token'`，存成 `'{"access_token":"..."}'` 会导致无限重连（鉴权失败但无报错）。

## 风险声明

用非官方协议登录 QQ 有封号风险。请使用**完全闲置、无资产、无重要好友**的小号，不要用主号。
