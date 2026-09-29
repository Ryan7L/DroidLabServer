<!--
 * @Author: CrayonRyan 2931378099@qq.com
 * @Date: 2026-09-29 15:16:48
 * @LastEditors: CrayonRyan 2931378099@qq.com
 * @LastEditTime: 2026-09-29 16:07:15
 * @FilePath: \droidlab-master\README.md
 * @Description: 这是默认设置,请设置`customMade`, 打开koroFileHeader查看配置 进行设置: https://github.com/OBKoro1/koro1FileHeader/wiki/%E9%85%8D%E7%BD%AE
-->

# JSON 配置与字段规范

## 通用结构

JSON 响应使用 `code`、`data`、`msg` 作为外层字段。`code` 为状态码（当前成功值为 `0`），`data` 为配置内容，`msg` 为附加消息。普通字段统一采用 camelCase；资源地址通常使用 `Url` 后缀，带单位的数值在字段名中注明单位。

以下字段名和 `displayMode` 的类型已调整。读取这些配置的客户端需要同步更新字段映射；旧版字段名不再提供。

## 文件名迁移

配置文件路径也已按用途重命名，客户端请求地址需要同步更新。

目前全部 JSON 配置集中在根目录的 `config/` 文件夹中，本地图片资源集中在根目录的 `img/` 文件夹中；JSON 中引用的图片 URL 使用 `img/` 路径。

| 用途              | 原路径                                  | 新路径                       |
| ----------------- | --------------------------------------- | ---------------------------- |
| 开发者信息        | `about/developer_info.json`             | `config/developer.json`      |
| 广告弹窗          | `advert/ad_popup.json`                  | `config/ad_popup.json`       |
| 开发者推荐        | `advert/developer_recommendations.json` | `config/recommend.json`      |
| 外观配置          | `config/theme_config.json`              | `config/appearance.json`     |
| 正式版信息        | `update/stable_version.json`            | `config/stable_version.json` |
| Beta 版信息       | `update/beta/beta_version.json`         | `config/beta_version.json`   |
| Beta 测试用户名单 | `update/beta/test_users.json`           | `config/beta_users.json`     |
| 阅读模式规则      | `web/reading_mode_rules.json`           | `config/reader_rules.json`   |
| 首页配置          | `config/homeconfig.json`                | `config/home.json`           |

## 开发者信息 (`config/developer.json`)

| 字段                                    | 说明                             |
| --------------------------------------- | -------------------------------- |
| `avatar`                                | 头像图片地址。                   |
| `name`                                  | 开发者名称。                     |
| `desc`                                  | 开发者介绍。                     |
| `githubUrl`、`jianshuUrl`               | GitHub 和简书主页地址。          |
| `qq`、`qqGroup`、`qqGroupKey`           | QQ 联系方式、群号和群验证信息。  |
| `qqQrUrl`、`wechatQrUrl`、`alipayQrUrl` | QQ、微信和支付宝二维码图片地址。 |

## 广告弹窗配置 (`config/ad_popup.json`)

用于控制广告弹窗是否展示、展示时间和展示内容。

| 字段             | 说明                                                                                                    |
| ---------------- | ------------------------------------------------------------------------------------------------------- |
| `displayMode`    | 展示模式数字枚举：`0` 不显示，`1` 每天展示一次，`2` 每次启动时展示。                                    |
| `showDateRanges` | 展示日期范围。`null` 表示不限制时间段，空数组 `[]` 表示不展示；范围格式为 `YYYYMMDDHHmm-YYYYMMDDHHmm`。 |
| `durationMs`     | 展示时长，单位毫秒；小于或等于 `0` 时不会自动消失。                                                     |
| `route`          | 点击广告后打开的应用内路由。                                                                            |
| `imageUrl`       | 广告图片地址。                                                                                          |

## 开发者推荐 Banner (`config/recommend.json`)

| 字段            | 说明                                                                |
| --------------- | ------------------------------------------------------------------- |
| `banners`       | 开发者推荐的 Banner 列表；每项包含 `title`、`imageUrl` 和 `route`。 |
| `articleFooter` | 文章页底部的开发者推荐内容，包含标题、图片地址和应用内路由。        |

## 外观配置 (`config/appearance.json`)

| 字段         | 说明               |
| ------------ | ------------------ |
| `grayFilter` | 是否启用灰度滤镜。 |

## 首页配置 (`config/home.json`)

| 字段                | 说明                                                                                                        |
| ------------------- | ----------------------------------------------------------------------------------------------------------- |
| `homeTitle`         | 首页标题；`null` 表示使用默认标题。                                                                         |
| `toolbarBgColor`    | 工具栏背景颜色。                                                                                            |
| `toolbarBgUrl`      | 工具栏背景图片地址。                                                                                        |
| `secondFloorBgUrl`  | 二楼页面背景图片地址。                                                                                      |
| `secondFloorBgBlur` | 二楼背景图片模糊比例。                                                                                      |
| `enableDateRanges`  | 首页配置启用日期范围。`null` 表示立即启用，空数组 `[]` 表示不启用；范围格式为 `YYYYMMDDHHmm-YYYYMMDDHHmm`。 |

## 版本信息

正式版信息位于 `config/stable_version.json`，Beta 版信息位于 `config/beta_version.json`。

| 字段                               | 说明                                |
| ---------------------------------- | ----------------------------------- |
| `downloadUrl`、`backupUrl`         | 主下载地址和备用下载地址。          |
| `versionName`、`versionCode`       | 当前版本名称和版本号。              |
| `lastForcedName`、`lastForcedCode` | 上一个强制升级版本的名称和版本号。  |
| `forceUpdate`                      | 是否强制升级。                      |
| `description`                      | 版本更新说明。                      |
| `releaseDate`                      | 版本发布日期，格式为 `YYYY-MM-DD`。 |

## Beta 测试用户名单 (`config/beta_users.json`)

`data` 是 Beta 测试用户数组，每项包含 `userId`（用户 ID）和 `username`（测试用户名）。

## 客户端阅读模式规则 (`config/reader_rules.json`)

`data` 是客户端阅读模式使用的站点匹配规则数组。每项包含 `platform`（平台标识）、`domain`（站点域名）和 `urlRegex`（文章 URL 正则表达式）。微信规则还提供 `altDomain` 和 `altUrlRegex`，用于表示微信文章域名及其 URL 正则。

请求此配置的客户端需要使用新路径并同步更新规则字段映射。
