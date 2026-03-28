---
name: zhihu-cli
description: Automate Zhihu (知乎) interactions including search, browsing hot topics, viewing questions/answers, posting pins/articles/questions, and user interactions. Use this skill when the user mentions Zhihu, 知乎, wants to search Zhihu content, check hot topics, post content to Zhihu, or interact with Zhihu posts. This skill requires zhihu-cli to be installed.
---

# Zhihu Skill

A Claude skill for automating Zhihu (知乎) interactions through the [zhihu-cli](https://github.com/BAIGUANGMEI/zhihu-cli) tool.

## Prerequisites

Before using this skill, ensure `zhihu-cli` is installed:

```bash
# Recommended: using uv
uv tool install pyzhihu-cli

# Or using pipx
pipx install pyzhihu-cli
```

## Authentication

Most operations require authentication. Login first:

```bash
# QR code login (recommended)
zhihu login --qrcode

# Or manual cookie login
zhihu login --cookie "z_c0=xxx; _xsrf=yyy; d_c0=zzz"
```

## Available Operations

### Search

Search questions, answers, articles, topics, or users on Zhihu.

```bash
# Search questions (default)
zhihu search "Python 学习"

# Search specific types
zhihu search "机器学习" --type topic      # topics
zhihu search "张三" --type people         # users
zhihu search "Python" --type article      # articles

# JSON output for further processing
zhihu search "Python" --json
```

### Hot Topics

View Zhihu's trending hot list.

```bash
# View hot list
zhihu hot

# Limit results
zhihu hot --limit 10

# JSON output
zhihu hot --json
```

### Questions

View question details and answers.

```bash
# View question details
zhihu question <question_id>

# Include answers
zhihu question <question_id> --answers

# Limit answer count
zhihu question <question_id> --answers --limit 10
```

### Answers

View answer details and comments.

```bash
# View answer details
zhihu answer <answer_id>

# Include comments
zhihu answer <answer_id> --comments
```

### User Information

View user profiles and content.

```bash
# View user profile (use URL token)
zhihu user <url_token>

# View user's answers
zhihu user-answers <url_token>
zhihu user-answers <url_token> --sort voteups

# View user's articles
zhihu user-articles <url_token>

# Followers / Following
zhihu followers <url_token>
zhihu following <url_token>
```

### Feed & Topics

Browse recommendations and topic content.

```bash
# Home feed recommendations
zhihu feed

# Topic details with questions
zhihu topic <topic_id> --questions
```

### Interactions

Vote on answers and follow questions.

```bash
# Vote / unvote answer
zhihu vote <answer_id>
zhihu vote <answer_id> --undo

# Follow / unfollow question
zhihu follow-question <question_id>
zhihu follow-question <question_id> --undo
```

### Create Content

Post questions, pins (ideas), and articles. All support HTML rich text.

```bash
# Post a question
zhihu ask "如何学习 Python？"
zhihu ask "什么是机器学习？" -d "请详细解释" -t 19550517 -t 19551275

# Post a pin/idea
zhihu pin "今天天气真好！"
zhihu pin "标题" -c "想法正文内容，支持 <strong>HTML</strong>"

# Post an article
zhihu article "文章标题" "文章内容"
zhihu article "标题" "内容" -t 19550517
```

### Upload Images

Add images to your posts.

```bash
# With question
zhihu ask "求推荐" -d "详情" -i photo.jpg

# With pin/idea
zhihu pin "标题" -c "正文" -i image1.jpg -i image2.jpg

# With article (cover image)
zhihu article "标题" "内容" -i cover.jpg
```

### Delete Content

Delete your own content (requires confirmation, use `-y` to skip).

```bash
zhihu delete-question <question_id>
zhihu delete-pin <pin_id>
zhihu delete-article <article_id>

# Skip confirmation
zhihu delete-question 12345678 -y
```

### Other Commands

```bash
# View collections
zhihu collections

# View notifications
zhihu notifications

# Check login status
zhihu status

# View my profile
zhihu whoami

# Logout
zhihu logout
```

## Usage Patterns

### Pattern 1: Quick Search

When the user wants to search Zhihu content:

```bash
zhihu search "<keyword>"
```

### Pattern 2: Browse Hot Topics

When the user wants to see what's trending:

```bash
zhihu hot --limit 20
```

### Pattern 3: Post Content

When the user wants to create content:

1. Determine content type (question/pin/article)
2. Use appropriate command with title/content
3. Add images if provided
4. Add topics/tags if specified

### Pattern 4: View User Content

When the user wants to view someone's profile or content:

1. Extract URL token from user's Zhihu profile URL
2. Use `zhihu user`, `zhihu user-answers`, or `zhihu user-articles`

## Security Notes

- Cookies are stored in `~/.zhihu-cli/cookies.json` with `0600` permissions
- **DO NOT paste credentials in chat**. Use `zhihu login --qrcode` or manually create the cookie file
- All communications use HTTPS to Zhihu official domains only

## Examples

**Search for Python learning resources:**
```bash
zhihu search "Python 学习路线" --json | jq '.[0:3]'
```

**View today's hot topics:**
```bash
zhihu hot --limit 10
```

**Post a new idea with image:**
```bash
zhihu pin "分享一个开发技巧" -c "使用 <code>git rebase</code> 可以保持提交历史整洁" -i tip.png
```

**Check my Zhihu profile:**
```bash
zhihu whoami --json
```
