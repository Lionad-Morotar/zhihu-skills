# zhihu-skills

知乎自动化技能 - 基于 zhihu-cli 的 Claude Skill，支持在终端搜索问题、查看回答、发布提问、发布想法、发布文章等功能。

## 安装

```bash
npx skills add https://github.com/Lionad-Morotar/zhihu-skills
```

## 前置要求

需要安装 [zhihu-cli](https://github.com/BAIGUANGMEI/zhihu-cli) 工具：

```bash
# 推荐：使用 uv
uv tool install pyzhihu-cli

# 或使用 pipx
pipx install pyzhihu-cli
```

## 使用

```sh
/zhihu 搜索 "Python 学习"
/zhihu 查看热榜
/zhihu 发布想法 "今天天气真好！"
```

如果你的 IDE 不支持 SlashCommand，那么为了获得最可靠的结果，需要提示词前加上前缀，比如：

```plaintext
使用 zhihu 技能，搜索 "Python 学习"
```

这会明确触发技能并确保 AI 遵循文档化的模式。如果不加前缀，技能触发可能不一致，具体取决于你的提示词与技能描述关键词的匹配程度。

## 功能

- **搜索** - 按关键词搜索问题、回答、文章
- **热榜** - 查看知乎热榜
- **问题** - 查看问题详情及回答
- **回答** - 查看回答详情及评论
- **发布** - 发布提问、发布想法、发布文章
- **用户** - 查看用户资料、回答、文章
- **推荐** - 获取首页推荐内容
- **话题** - 查看话题详情及热门问题
- **互动** - 赞同/取消赞同回答，关注/取消关注问题

## 登录

首次使用前需要登录知乎：

```bash
# 二维码扫码登录（推荐）
zhihu login --qrcode

# 或手动粘贴 Cookie
zhihu login --cookie "z_c0=xxx; _xsrf=yyy; d_c0=zzz"
```

## 参考

- [zhihu-cli](https://github.com/BAIGUANGMEI/zhihu-cli) - 本技能的底层 CLI 工具
