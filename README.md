# HD2 Mod Quick Deploy plugins

The official list of plugins for [HD2 Mod Quick Deploy](https://github.com/pat-pat-patrick/hd2-mod-cli),
and the documentation for writing one. This repository holds no plugin itself: each plugin is
built and released in its own repository, and [`plugins.json`](plugins.json) names them.

## Official plugins

| Plugin | File | Version | Repository |
|---|---|---|---|
| HD2 Mod Console: each mod's settings, the enabled mods first | `HD2QD.Settings.dll` | [1.20.1](https://github.com/pat-pat-patrick/hd2-mod-setting-gui/releases/tag/v1.20.1) | [hd2-mod-setting-gui](https://github.com/pat-pat-patrick/hd2-mod-setting-gui) |
| Asset check: models and textures against the game's, and video memory | `HD2QD.AssetCheck.dll` | [1.4.2](https://github.com/pat-pat-patrick/hd2qd-asset-check/releases/tag/v1.4.2) | [hd2qd-asset-check](https://github.com/pat-pat-patrick/hd2qd-asset-check) |
| Mod repair: mods a game update broke — models that no longer load, sound mods that leave parts of the game silent, subtitle mods that miss the game's new lines (sound banks and subtitles by [x402](https://github.com/x402); the sound bank repair method comes from Sound Restoration Studio (音效维修台) by [40Hour](https://space.bilibili.com/157681854)) | `HD2QD.Repatch.dll` | [1.2.1](https://github.com/pat-pat-patrick/hd2qd-repatch/releases/tag/v1.2.1) | [hd2qd-repatch](https://github.com/pat-pat-patrick/hd2qd-repatch) |
| Member licenses: sign-in for mods available only to their author's members, and their member content (code, and large data such as voice recordings), kept encrypted and unlocked while the game runs | `HD2QD.License.dll` | [1.11.5](https://github.com/pat-pat-patrick/hd2-mod-license/releases/tag/plugin-v1.11.5) | [hd2-mod-license](https://github.com/pat-pat-patrick/hd2-mod-license) |
| Resource names: HD2SDK's resource and game archive name lists, downloaded from its repository, so conflicts and the asset check name resources (manager 0.16.0 or later) | `HD2QD.ResourceNames.dll` | [1.1.1](https://github.com/pat-pat-patrick/hd2qd-resource-names/releases/tag/v1.1.1) | [hd2qd-resource-names](https://github.com/pat-pat-patrick/hd2qd-resource-names) |
| Speed Dial for Liberty: one-key stratagem calls. You press one key, and the plugin enters the stratagem code with your own stratagem keys. Requires the mod Speed Dial for Liberty (v0.24.0 or later), enabled, and the manager running while you play | `HD2QD.SpeedDial.dll` | [1.6.2](https://github.com/pat-pat-patrick/hd2qd-speed-dial/releases/tag/v1.6.2) | [hd2qd-speed-dial](https://github.com/pat-pat-patrick/hd2qd-speed-dial) |
| HellForge: launches HellForge, the offline Helldivers 2, and makes it a deploy target of the manager: the library's mods converted for HellForge's game version, sessions, a profile editor, settings, lobbies, logs and licensed mods (deploying the library's mods needs manager 0.20.0 or later) | `HD2QD.HellForge.dll` | [0.15.0](https://github.com/pat-pat-patrick/hd2qd-hellforge/releases/tag/v0.15.0) | [hd2qd-hellforge](https://github.com/pat-pat-patrick/hd2qd-hellforge) |

They need HD2 Mod Quick Deploy 0.15.0 or later (plugin Api 2). None is installed by default. The
list also takes plugins by other authors that meet the requirements in
[Becoming an official plugin](#becoming-an-official-plugin); any plugin can still be added from its
file.

## Adding a plugin

1. In HD2 Mod Quick Deploy, open the Plugins page (the jigsaw piece beside the gear).
2. An official plugin: choose **Download and add** on its card. The manager downloads the newest
   release named in [`plugins.json`](plugins.json) and adds it only if its SHA-256 matches.
3. Any other plugin: choose **Add plugin…** and select its `HD2QD.<name>.dll`, or drop the file on
   the page.
4. Confirm. A plugin runs with the manager's permissions: add only plugins from a source you trust.

**Remove** on a plugin's card deletes it again. On the command line: `hd2qd plugins`,
`hd2qd plugin-add <name or file>` (a name downloads the official plugin), `hd2qd plugin-remove <name>`.

## `plugins.json`

The manager reads this file from the `main` branch of this repository and keeps a copy in its
settings folder, so a plugin added here shows in every copy of the manager without a new release.

| Field | Meaning |
|---|---|
| `file` | The plugin's file name, `HD2QD.<name>.dll`. |
| `title`, `summary` | What the list shows, in English. Translations are in `locales/` (below). |
| `author`, `repository` | Who makes it, and the GitHub repository whose releases carry it. |
| `asset` | The release asset to download. |
| `api` | The contract version it speaks. |
| `license` | The plugin's licence as an SPDX identifier (`MIT`, `Apache-2.0`, ...). For people reading the list; the manager does not use it. |
| `wanted_by_file` | Optional: the manager marks the mods that ship this file as needing the plugin. |
| `button` | Optional: `true` gives the plugin a button in the manager's title bar, drawn with its own `app.ico`. Only a plugin listed here, whose installed file matches one of its `versions`, can have one. |
| `versions` | Each released version: `{version, tag, sha256}`. The manager downloads the newest and checks it against `sha256`. |

## Becoming an official plugin

Plugins by other authors can join the list. A plugin runs with the manager's permissions, so the
list takes only plugins whose every listed version has been reviewed from its source, and that the
maintainer can keep working on if their author stops. To propose one, open an issue in this
repository with the plugin's repository and the version to review. Whether a plugin is listed is
the maintainer's decision.

### Licence

The plugin's repository has a `LICENSE` file with one of these licences, all approved by the
[Open Source Initiative](https://opensource.org/licenses):

| Licence (SPDX) | Note |
|---|---|
| `MIT` | Preferred: the licence of the manager and of every plugin listed so far. |
| `Apache-2.0` | Its `NOTICE` file, if there is one, stays in every copy. |
| `BSD-2-Clause`, `BSD-3-Clause`, `ISC` | Equivalent to MIT for this list. |

Other OSI-approved licences, such as `MPL-2.0` or the GPL family, are decided case by case: their
code cannot move into the manager or into the MIT plugins. Not listed:

- a repository with no licence: being public on GitHub gives no one the right to change or
  redistribute it;
- source-available licences that restrict changes or redistribution, such as the Business Source
  License, the Commons Clause or the PolyForm licences;
- Creative Commons licences used for code;
- closed source.

### Source and builds

1. The complete source of each version is public in the plugin's repository under a tag, and
   builds from a clean checkout with the repository's own build script.
2. The plugin's README says what it reads and writes on the player's computer, and which hosts it
   contacts.
3. The maintainer reviews the source at that tag, builds the DLL from it, and publishes the DLL as
   a release of a fork in the maintainer's account. `repository` names that fork; `author` names
   the plugin's author. A DLL built anywhere else cannot be checked against the reviewed source,
   so the listed file is always the maintainer's build.

### New versions

- The author tags the new version. The maintainer reviews the changes since the last listed
  version, builds it and adds it to `versions`.
- A version released under a licence not accepted above is not added. Versions already listed
  keep the licence they were released under.
- If the author stops maintaining the plugin, the maintainer may continue it in the fork, or
  remove it from the list.

## Maintaining the list

This section is for the maintainer of this repository. No one else can add a plugin to the list or a version to a plugin: the manager reads the list
only from this repository's `main`, and installs an official plugin only when its file matches a
SHA-256 written here. Suggestions are welcome as issues or pull requests.

To release a new version of an official plugin:

1. Publish a release in the plugin's repository with the DLL attached under the name in `asset`.
   For another author's plugin, that repository is the maintainer's fork, and the DLL is built
   there from the reviewed tag.
2. Add `{version, tag, sha256}` to the plugin's `versions` here: the release's tag, and the SHA-256
   of the attached file as GitHub serves it.
3. Push to `main`. Every copy of the manager offers the new version from then on; the manager
   itself needs no release.

Keep the format readable by the managers already released: add fields, never rename or remove one.

## Translations

`plugins.json` holds English only. Each language has one file of its own,
`locales/<language>.json`, named by its language tag (`zh-CN`, `de`, `pt-BR`, ...): for each plugin
file, its `title` and `summary` in that language. The manager reads the file of the language it
shows; a plugin or a field missing there is shown in English. Adding a language is adding one
file; nothing else changes.

```json
{
  "HD2QD.Repatch.dll": { "title": "MOD 修复", "summary": "..." }
}
```

## Writing a plugin

See [docs/plugin-authors.md](docs/plugin-authors.md) ([中文](docs/plugin-authors.zh-CN.md)) and
the complete example in [example/](example).

---

# HD2 Mod Quick Deploy 插件

[HD2 Mod Quick Deploy](https://github.com/pat-pat-patrick/hd2-mod-cli) 的官方插件列表，以及编写插件的
文档。本仓库不包含插件本身：每个插件在各自的仓库中构建和发布，[`plugins.json`](plugins.json)
列出它们。

## 官方插件

| 插件 | 文件 | 版本 | 仓库 |
|---|---|---|---|
| HD2 MOD 控制台：编辑各 MOD 的设置，已启用的 MOD 列在前面 | `HD2QD.Settings.dll` | [1.20.1](https://github.com/pat-pat-patrick/hd2-mod-setting-gui/releases/tag/v1.20.1) | [hd2-mod-setting-gui](https://github.com/pat-pat-patrick/hd2-mod-setting-gui) |
| 资源检查：模型与贴图和原版资源的对比，以及显存占用 | `HD2QD.AssetCheck.dll` | [1.4.2](https://github.com/pat-pat-patrick/hd2qd-asset-check/releases/tag/v1.4.2) | [hd2qd-asset-check](https://github.com/pat-pat-patrick/hd2qd-asset-check) |
| MOD 修复：修复游戏更新后出问题的 MOD——无法加载的模型、让游戏部分声音消失的音效 MOD、缺少游戏新增内容的字幕 MOD（音库与字幕修复由 [x402](https://github.com/x402) 贡献；音库修复方法来自 [40Hour](https://space.bilibili.com/157681854) 的音效维修台） | `HD2QD.Repatch.dll` | [1.2.1](https://github.com/pat-pat-patrick/hd2qd-repatch/releases/tag/v1.2.1) | [hd2qd-repatch](https://github.com/pat-pat-patrick/hd2qd-repatch) |
| 会员授权：为仅供创作者会员使用的 MOD 登录，并下载其会员内容（代码，以及语音录音等大体积数据），在本机加密保存、仅在游戏运行时解锁 | `HD2QD.License.dll` | [1.11.5](https://github.com/pat-pat-patrick/hd2-mod-license/releases/tag/plugin-v1.11.5) | [hd2-mod-license](https://github.com/pat-pat-patrick/hd2-mod-license) |
| 资源名称：从 HD2SDK 的仓库下载资源名称表和游戏包名称表，冲突和资源检查中显示资源的名称（需要管理器 0.16.0 或更新） | `HD2QD.ResourceNames.dll` | [1.1.1](https://github.com/pat-pat-patrick/hd2qd-resource-names/releases/tag/v1.1.1) | [hd2qd-resource-names](https://github.com/pat-pat-patrick/hd2qd-resource-names) |
| Speed Dial for Liberty：一键呼叫战备。你按一个键，插件用你自己的战备输入键替你输入战备代码。需要同时启用 MOD Speed Dial for Liberty（v0.24.0 或更新），游戏时管理器保持运行 | `HD2QD.SpeedDial.dll` | [1.6.2](https://github.com/pat-pat-patrick/hd2qd-speed-dial/releases/tag/v1.6.2) | [hd2qd-speed-dial](https://github.com/pat-pat-patrick/hd2qd-speed-dial) |
| HellForge：启动离线版《绝地潜兵2》HellForge，并把它作为管理器的部署目标：库里的 MOD 转换为 HellForge 的游戏版本、会话、档案编辑器、设置、联机大厅、日志和会员 MOD（部署库里的 MOD 需要管理器 0.20.0 或更新） | `HD2QD.HellForge.dll` | [0.15.0](https://github.com/pat-pat-patrick/hd2qd-hellforge/releases/tag/v0.15.0) | [hd2qd-hellforge](https://github.com/pat-pat-patrick/hd2qd-hellforge) |

需要 HD2 Mod Quick Deploy 0.15.0 或更新版本（插件接口 Api 2）。默认均不安装。其他创作者的插件符合
[成为官方插件](#成为官方插件)中的条件时，也可收入列表；任何插件仍可从文件添加。

## 添加插件

1. 在 HD2 Mod Quick Deploy 中打开“插件”页（齿轮旁的拼图按钮）。
2. 官方插件：在其卡片上点击**下载并添加**。管理器会下载 [`plugins.json`](plugins.json) 中记录的最新版本，
   SHA-256 一致才会添加。
3. 其他插件：点击“添加插件…”，选择其 `HD2QD.<名称>.dll`，或将文件拖到插件页上。
4. 确认添加。插件以管理器的权限运行，请仅添加来源可信的插件。

插件卡片上的“移除”可将其删除。命令行：`hd2qd plugins`、`hd2qd plugin-add <名称或文件>`（给出名称时下载
官方插件）、`hd2qd plugin-remove <名称>`。

## `plugins.json`

管理器从本仓库的 `main` 分支读取此文件，并在设置目录中保留一份副本。因此在这里加入的插件，
无需发布新版管理器即可显示。

| 字段 | 含义 |
|---|---|
| `file` | 插件文件名，`HD2QD.<名称>.dll`。 |
| `title`、`summary` | 列表中显示的名称和简介，英文。译文见 `locales/`（见下文）。 |
| `author`、`repository` | 创作者，以及发布该插件的 GitHub 仓库。 |
| `asset` | 要下载的 release 附件。 |
| `api` | 插件使用的接口版本。 |
| `license` | 插件的许可证，使用 SPDX 标识符（`MIT`、`Apache-2.0` 等）。供阅读列表的人参考，管理器不使用。 |
| `wanted_by_file` | 可选：带有此文件的 MOD 会被标记为需要该插件。 |
| `button` | 可选：为 `true` 时，该插件在管理器标题栏有自己的按钮，图标为插件自带的 `app.ico`。只有列在这里、且已安装文件与其某个 `versions` 一致的插件才能有按钮。 |
| `versions` | 每个已发布的版本：`{version, tag, sha256}`。管理器下载其中最新的版本，并按 `sha256` 核对。 |

## 成为官方插件

其他创作者的插件可以加入列表。插件以管理器的权限运行，因此列表只收录这样的插件：列出的每个版本都经过
源码审核，并且创作者停止维护后，维护者能够继续维护。如需申请，请在本仓库开一个 issue，写明插件的仓库
和要审核的版本。是否收录由维护者决定。

### 许可证

插件仓库中须有 `LICENSE` 文件，使用以下许可证之一。它们均经过
[开放源代码促进会（OSI）](https://opensource.org/licenses)认证：

| 许可证（SPDX） | 说明 |
|---|---|
| `MIT` | 首选：管理器和目前所有列出插件使用的许可证。 |
| `Apache-2.0` | 如有 `NOTICE` 文件，每份副本中须保留。 |
| `BSD-2-Clause`、`BSD-3-Clause`、`ISC` | 对本列表而言与 MIT 等同。 |

其他经 OSI 认证的许可证，如 `MPL-2.0` 或 GPL 系列，逐个决定：这些代码不能并入管理器或 MIT 插件。
以下情况不予收录：

- 仓库没有许可证：在 GitHub 上公开，并不授予任何人修改或再发布的权利；
- 限制修改或再发布的“源码可见”许可证，如 Business Source License、Commons Clause 或 PolyForm 系列；
- 用于代码的 Creative Commons 许可证；
- 闭源。

### 源码与构建

1. 每个版本的完整源码在插件仓库中公开并打上标签，能从干净的检出用仓库自带的构建脚本构建。
2. 插件的 README 写明它在玩家电脑上读写哪些内容、连接哪些主机。
3. 维护者审核该标签的源码，由此构建 DLL，并作为维护者账号下一个 fork 的 release 发布。`repository`
   填写这个 fork，`author` 填写插件的创作者。在其他地方构建的 DLL 无法与审核过的源码对应，因此列表中
   的文件始终是维护者的构建。

### 新版本

- 创作者为新版本打标签。维护者审核自上一个已列出版本以来的改动，构建后加入 `versions`。
- 以上述之外的许可证发布的版本不予加入。已列出的版本保留其发布时的许可证。
- 创作者停止维护时，维护者可以在 fork 中继续维护，或将其从列表中移除。

## 维护列表

本节供本仓库的维护者使用。其他人无法向列表加入插件，也无法为插件
加入新版本：管理器只从本仓库的 `main` 读取列表，并且只有文件的 SHA-256 与这里记录的一致时，才会作为
官方插件安装。欢迎通过 issue 或 pull request 提出建议。

发布官方插件的新版本：

1. 在插件自己的仓库发布 release，附件文件名与 `asset` 一致。其他创作者的插件，这个仓库是维护者的
   fork，DLL 在那里从审核过的标签构建。
2. 在本仓库该插件的 `versions` 中加入 `{version, tag, sha256}`：release 的标签，以及 GitHub 上该附件的
   SHA-256。
3. 推送到 `main`。此后所有管理器都会提供新版本，管理器本身无需发布新版。

列表格式须保持已发布的管理器能够读取：只能新增字段，不要改名或删除字段。

## 翻译

`plugins.json` 只包含英文。每种语言各有一个文件 `locales/<语言>.json`，以语言标记命名（`zh-CN`、
`de`、`pt-BR` 等），其中按插件文件名列出该语言的 `title` 和 `summary`。管理器读取其当前显示语言的
文件；文件中缺少的插件或字段以英文显示。新增一种语言只需新增一个文件，其他内容无需改动。

```json
{
  "HD2QD.Repatch.dll": { "title": "MOD 修复", "summary": "..." }
}
```

## 编写插件

见 [docs/plugin-authors.zh-CN.md](docs/plugin-authors.zh-CN.md)（[English](docs/plugin-authors.md)）
以及 [example/](example) 中的完整示例。
