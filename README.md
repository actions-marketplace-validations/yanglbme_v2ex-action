<h1 align="center">V2EX Action</h1>

<div align="center">

[![lint status](https://github.com/yanglbme/v2ex-action/workflows/Lint/badge.svg)](https://github.com/yanglbme/v2ex-action/actions) [![v2ex status](https://github.com/yanglbme/v2ex-action/workflows/V2ex/badge.svg)](https://github.com/yanglbme/v2ex-action/actions) [![release](https://img.shields.io/github/v/release/yanglbme/v2ex-action.svg)](../../releases) [![license](https://badgen.net/github/license/yanglbme/v2ex-action)](./LICENSE) [![PRs Welcome](https://badgen.net/badge/PRs/welcome/green)](../../pulls)

</div>

自动将 [V 站](https://https://v2ex.com/)热门发送到指定的 webhook 地址，如企业微信群机器人。可配置 workflow 的触发条件为 `schedule`，实现周期性定时发送热门内容。

## 入参

|  参数  |  描述  |  是否必传  |  默认值  |
|---|---|---|---|
| `webhook` | Webhook 地址 | 是 | - |
| `secret` | 签名密钥 | 否 | '' |
| `count` | 帖子数量 | 否 | 8 |

若是钉钉，务必**提供签名密钥**，企业微信则无须提供。

![](./images/dingding_secret.png)

## 完整示例

可自定义 cron 表达式。

```yml
name: V2ex

on:
  schedule:
    - cron: '0 2 * * *'

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: yanglbme/v2ex-action@master
        with:
          webhook: ${{ secrets.WEBHOOK }}
          secret: ${{ secrets.SECRET }}
          count: 6
```

注意：

- cron 是 UTC 时间，使用时请将北京时间转换为 UTC 进行配置。
- 请在项目的 `Setting -> Secrets` 路径下配置好 `WEBHOOK` 与 `SECRET`(仅钉钉机器人要配置)，不要直接在 `.yml` 文件中暴露地址跟密钥。


## 效果

- 钉钉
  ![](./images/dingding_res.png)

- 企业微信
  ![](./images/qyweixin_res.png)

## 许可证
[MIT](LICENSE)