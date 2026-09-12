# 型号查看（伪装电子书阅读器）

一款小米手环（Vela 快应用）应用。**表面是一个「型号查看」工具，实际内嵌了一个完整的电子书阅读器**，可通过安卓同步器推送电子书。

## 伪装说明

| 项目 | 说明 |
| --- | --- |
| 表面界面 | 黑底，中间**白色粗体**显示手环型号，下方一行小字 `灵儿万爆 lewb521` |
| 进入内核 | 对下方小字**连续点击 10 次**（2 秒内不间断）进入电子书内核 |
| 退出内核 | 在书架页**侧滑一次**即彻底退出（不会退回伪装页） |

- 手环型号通过 `@system.device.getInfo()` 读取，读取失败时回退显示「小米手环」。

## 功能（电子书内核）

- 书架：展示已同步的 txt 电子书
- 阅读：翻页、字号 / 亮度 / 边距调节、进度记忆
- 更多设置：清空书架、字体设置等

## 与安卓同步器配合

1. 手机上安装同步器 [com.bandbbs.ebook-android](https://github.com/lewb521/com.bandbbs.ebook-android)。
2. 手环安装本应用，并保持与手机在小程序互联状态下连接。
3. 同步器选择 txt 电子书推送，通过 `pages/push` 路由 + 小米互联握手传输到手环。

## 关键文件

| 路径 | 作用 |
| --- | --- |
| `src/pages/model/` | 伪装入口页（型号查看，含连点 10 次触发逻辑） |
| `src/pages/index/` | 电子书内核书架页（侧滑彻底退出逻辑在此） |
| `src/pages/push/` | 同步推送接收页 |
| `src/app.ux` | 应用入口，注册互联握手监听 |

## 安装包

- `release/com.bandbbs.ebook.debug.3.1.rpk`：调试签名包，配合 AIoT 调试器侧载。
- 正式侧载包请在本地登录小米开发者账号后执行 `npm run release` 生成。

## 快速上手

```bash
npm install      # 安装依赖
npm run build    # 编译生成 debug rpk（dist/）
npm run release  # 生成 release 签名包（需先 npx aiot login）
npm run start    # 开发 / 热更新
npm run watch    # 调试
```

## 开源许可

AGPL-3.0，详见 [LICENSE](./LICENSE)。

## 上游出处

本项目基于 [BandBBS-Vela-Dev/com.bandbbs.ebook](https://github.com/BandBBS-Vela-Dev/com.bandbbs.ebook)（喵喵电子书）改造。