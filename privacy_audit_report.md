# Skill 仓库隐私审计报告

**审计日期:** 2026-05-03  
**审计范围:** /home/xiao/下载/tmp/kimi-skills 目录下所有 255 个 skill 目录

---

## 🔴 高风险：包含真实个人信息的文件

### 1. Git 配置文件

| 文件路径          | 隐私内容                      | 说明                   |
| ------------- | ------------------------- | -------------------- |
| `.git/config` | GitHub 用户名 `qq1018408006` | 仓库远程地址包含个人 GitHub 账号 |

**建议:** 推送前确认这是你希望公开的仓库所有者信息

---

## 🟡 中风险：可能包含用户 ID 的文件

### _meta.json 文件 (31 个)

这些文件包含 Clawd/Kimi 平台的用户 ownerId，格式为 `kn[a-z0-9]{32}`：

| OwnerId                            | 出现次数 | 关联 Skill                                                                              |
| ---------------------------------- | ---- | ------------------------------------------------------------------------------------- |
| `kn73qjxwmbna25qq8q051epqt980sys5` | 4    | seo-content-writer, seo-copywriting-guide, competitive-seo-intel, competitor-analysis |
| `kn7caxjvqk9fengp67p290smnn800sv9` | 2    | chart-gen, chart-image                                                                |
| `kn7bfqgw6nar13rjxcdzytmfms808fwa` | 2    | fast-browser-use, rust-browser-pilot                                                  |
| `kn7ay2qcqva8ek62e2yrgnjevn7ztee6` | 2    | speech-synthesis, edge-tts                                                            |
| `kn7ag1y1zeyvc3dsrv8t12mstn80p686` | 2    | playwright-scraper-skill, smart-web-scraper                                           |
| `kn79ajadezq44ydpssrcdgbytn7ztm19` | 2    | k8s-cluster-ops, kubectl                                                              |
| `kn797d53s9qm28r96js53sq01h81hv0c` | 2    | sunlight-analysis, sun-path                                                           |
| `kn7920zxtm2ztkbk47j7weazgs80c2jd` | 2    | adhd-assistant, adhd-daily-planner                                                    |
| `kn78628x1pqynfnxx2aa9gs4kd805abq` | 2    | gitlab-cli-skills, gitlab-cli-guide                                                   |
| `kn7544sf4cvb2vzynseq2098n580960t` | 2    | code-mentor, programming-tutor                                                        |
| `kn70j4ejnwqjpykvwwvgymmdcd8055qp` | 2    | imap-smtp-email, email-manager                                                        |
| `kn7fnx0e4a5kyh3xpffp43fjh5810w1s` | 1    | cn-finance-data                                                                       |
| `kn7f3h94x6dsndkdjph76br4pd803szg` | 1    | browse                                                                                |
| `kn7cxqj3xb7acyyg6jkynq46bd814sv2` | 1    | iso-27001-evidence-collection                                                         |
| `kn76fvxkphyes55d4wx925kh7n81av1t` | 1    | whatsapp-integration                                                                  |
| `kn75f3x4hqez3np4xy7m50kn1d7ypsgp` | 1    | r2-upload                                                                             |
| `kn751hgmbpccaam5c4k1dby1pd80n62k` | 1    | xhs-note-creator                                                                      |
| `kn74s2mr0wqww2ytdnxpvjc8k180dnnd` | 1    | email-to-calendar                                                                     |

**建议:** 这些是平台用户 ID，如果 skill 要公开发布，建议移除或重置为模板格式

---

## 🟢 低风险：示例/模板文件（无需处理）

以下文件包含邮箱地址但均为示例或模板内容：

| 文件                                     | 内容类型                                        | 说明            |
| -------------------------------------- | ------------------------------------------- | ------------- |
| `email-to-calendar/SETUP.md`           | `your-email@gmail.com`, `user1@gmail.com` 等 | 配置示例，占位符邮箱    |
| `pro-email-composer/SKILL.md`          | `finance@company.com`                       | 业务示例邮箱        |
| `professional-email-composer/SKILL.md` | `finance@company.com`                       | 业务示例邮箱        |
| `k8s-cluster-ops/SKILL.md`             | `d.devaal@gmail.com`                        | 作者邮箱（公开贡献者信息） |
| `kubectl/SKILL.md`                     | `d.devaal@gmail.com`                        | 作者邮箱（公开贡献者信息） |

---

## 🟢 安全：测试文件已检查

以下测试文件已检查，不包含敏感数据：

- `fast-browser-use/test_state.json` - 仅包含示例网页内容
- `fast-browser-use/test_auth.json` - 空 cookies 数组
- `rust-browser-pilot/test_state.json` - 仅包含示例网页内容
- `rust-browser-pilot/test_auth.json` - 空 cookies 数组

---

## 🟢 安全：配置文件已检查

- `r2-upload/example-config.yml` - 使用 `YOUR_*` 占位符，无真实密钥
- 所有 `.env` 文件 - 未发现（setup.sh 生成但未包含）

---

## 总结

### 需要处理的项目：

1. **`.git/config`** - 包含 GitHub 用户名 `qq1018408006`
   
   - 这是正常的仓库所有者信息
   - 如果这是你希望公开的账号，无需处理
   - 如果要匿名发布，需要修改远程仓库地址

2. **31 个 `_meta.json` 文件** - 包含平台用户 ID
   
   - 这些 ID 关联到具体的 Kimi/Clawd 平台用户
   - 公开发布建议移除 `ownerId` 字段或清空

### 无需处理的项目：

- 示例邮箱地址（均为占位符或公开贡献者邮箱）
- 测试文件（已验证为空或示例数据）
- 配置文件（使用占位符）

---

## 建议的清理操作

```bash
# 1. 移除所有 _meta.json 中的 ownerId
cd /home/xiao/下载/tmp/kimi-skills
for f in $(find . -name "_meta.json"); do
  jq 'del(.ownerId)' "$f" > "$f.tmp" && mv "$f.tmp" "$f"
done

# 2. 或者完全删除 _meta.json 文件（如果不影响功能）
# find . -name "_meta.json" -delete
```
