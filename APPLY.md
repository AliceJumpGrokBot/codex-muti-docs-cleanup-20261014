# 如何应用到 AliceJump/codex-muti

目标分支：`docs/cleanup-20261014`（已从 `master` @ `89804f3` 创建）。

本仓库是 **AliceJumpGrokBot** 的公开暂存：因为 box 上的 `gh`/`GITHUB_TOKEN` 无法写入私有 `AliceJump/codex-muti`，而 MCP 也没有 Contents/Commit API。

## 推荐（有私有仓写权限时）

```bash
git clone https://github.com/AliceJump/codex-muti.git
cd codex-muti
git fetch origin
git checkout docs/cleanup-20261014
# 复制本暂存库中的 README.md、implementation-plan.md、docs/* 覆盖后：
git add README.md implementation-plan.md docs/wham-usage-rewrite.md \
  docs/desktop-widget.md docs/native-acceptance-results.md docs/native-auth-adapter.md
git commit -m "$(cat <<'M'
docs: 对齐 Daemon/Floating/验收与草稿 PR #6–#8

整理 README 与关键文档：标明 :3210、Floating/Widget、原生核心验收未满发布、
Desktop 仍待验收、Mac 原型；区分本地组合部署与 GitHub 分 PR（#6 头/产品名、
#7 WHAM+chatgpt_base_url、#8 玻璃托盘菜单）。不宣称未合入功能已在 master。
M
)"
git push -u origin docs/cleanup-20261014
gh pr create --draft --base master --head docs/cleanup-20261014 \
  --title "docs: 文档整改（状态对齐与结构整理）" \
  --body-file - <<'B'
## 摘要
对齐 README 与关键文档与当前现实；中文；不发明功能。

## 变更
- README：状态表、组件/端口、草稿 PR #6/#7/#8、本地组合部署 vs 分 PR、\`~/.codex\` 双 base_url
- docs/wham-usage-rewrite.md：对应 #7（标明未合入）
- desktop-widget / native-acceptance / native-auth-adapter / implementation-plan：交叉说明

## 非目标
不含 #6/#7/#8 代码合入。
B
```

## 临时授权 AliceJumpGrokBot

将 `AliceJumpGrokBot` 加为 `AliceJump/codex-muti` 的 write collaborator（或提供含该私有仓 `contents:write` 的 PAT），即可在 box 上直接 `git push` 并开 draft PR。
