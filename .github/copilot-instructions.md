<!-- managed-by: hamanpaul/paulsha-conventions@v1.0.2 -->
<!-- 若修改此檔，同步更新 CLAUDE.md / AGENTS.md / GEMINI.md / .github/copilot-instructions.md 四份 -->
policy_version: 1.0.2

# Agent Policy Checklist

本 repo 受 hamanpaul project policy v1.0.2 管轄。
所有 agent 進入 session 時，必須依下列 checklist 行動。

## 本 repo 的 profile
- policy_profile: `flat` （見 `.paul-project.yml`）
- policy_version: `1.0.2`

## 動工前
- [ ] 確認當前分支不是 `main`
  - 若在 `main`，先開 `feature/<slug>` 分支
  - 若在 `feature/*`，可直接工作，或再開 `wt/<feature>/<subtask>`
- [ ] 若本任務跨多個子項，先建議用 `git worktree` 拆開

## 改 code 時
- [ ] 同一 PR 必須同步更新 `CHANGELOG.md [Unreleased]`
- [ ] 除非可明確標示為 docs-only / test-only / chore，否則不得省略 CHANGELOG
- [ ] code_paths 涵蓋的檔案變動皆視為 code change

## 改版號時（release 觸發時）
- [ ] 嚴格遵循 `<MAJOR>.<MINOR>.<PATCH>[-fix.N]`
- [ ] PATCH bump 對應 profile：
  - `stage-driven`: 一個 stage 落地
  - `flat`: 一個 feature batch 完成
- [ ] MINOR bump 需滿足：feature 群組全 landed + 7 天無 hotfix
- [ ] MAJOR bump 需使用者明確核可

## 完成任務（claim done）前
- [ ] `CHANGELOG.md [Unreleased]` 有對應 entry（或 PR 標 `skip-changelog` + 理由）
- [ ] `VERSION` 內容與意圖一致（release label PR 才可偏離 latest tag）
- [ ] `.github/pull_request_template.md` checklist 全勾
- [ ] `python3 -m policy_check --repo .` 無任何 failure
- [ ] 若本 repo 有額外測試 / lint / build 指令，需一併通過
- [ ] 若跳過任何檢查，PR 必須帶對應豁免 label + 理由

## 禁止
- 直接 commit 到 `main`
- 建立不符合命名規則的分支（必須 `feature/<slug>` 或 `wt/<feature>/<subtask>`）
- 發明新 `policy-exempt:*` label（**只能用 policy 列舉的白名單**）
- 修改本檔而不同步其他三份 agent convention 檔

## Exemption Labels 白名單
僅允許使用以下 labels 豁免對應規則（其他一律視同未豁免）：
- `policy-exempt:readme-sections` — R-02 README 必備段落
- `policy-exempt:changelog-format` — R-04 CHANGELOG 格式
- `policy-exempt:pr-title` — R-10 PR title conventional-commit 格式
- `policy-exempt:branch-name` — R-12 分支來源規則
- `policy-exempt:agent-files` — R-13 agent convention files 存在
- `policy-exempt:cli-help` — R-16 CLI help 同步
- `skip-changelog` — R-09 code 變動要求 CHANGELOG entry（特殊用途，需附理由）
- `wip` — R-11 自動通過 PR body checkbox 未全勾（work in progress）

## v1.0.1 新增規則（issue 連結 / docs 對齊 / 語言）
> 本段於 policy 1.0.1 隨 R-17 / R-18 與語言規範新增。

- **R-17（PR↔issue，FAIL gate）**：PR body 引用 issue（`#N`）時必須為 closing-keyword 形式（`Closes` / `Fixes` / `Resolves #N`），merge 由 GitHub 原生自動關閉 issue 並留下 cross-reference；只引用不關閉時上 `policy-exempt:issue-link`。
- **R-18（docs 對齊，WARN，不擋 merge）**：`code_paths` 有變動但 `README.md` / `docs/**` 未同步時提醒；純內部變動可上 `policy-exempt:docs-sync`。
- **語言規範（checklist）**：依 repo 來源決定語言——`github.com/hamanpaul/*`、`github.com/paulc-arc/*` → zh-tw；arcadyan GitLab → en_US。涵蓋 PR 標題／內文與所有 comment。本 repo 屬 `hamanpaul` → zh-tw。
- **動工前（軟性，不打斷流程）**：若任務對應某 issue，`gh issue view <N>` 核對相關性後分支可命名 `feature/<N>-<slug>`，開 PR 於 body 寫 `Closes #N`；查無對應 issue 照常進行，不另開、不停。
- **Exemption 白名單新增**：`policy-exempt:issue-link`（R-17）、`policy-exempt:docs-sync`（R-18）。

## v1.0.2 新增規則（CI 測試 / 版本同步）
> 本段於 policy 1.0.2 隨 R-19 / R-20 新增。

- **R-19（CI 必須跑測試，FAIL gate）**：repo 存在 `tests/`（含 `test_*.py` / `*_test.py`）時，`.github/workflows/**` 必須有至少一個 workflow 實際執行測試（pytest / unittest / npm test 等）；新增測試套件而 CI 未涵蓋時須同步補上；豁免 label `policy-exempt:ci-tests`。本 template 已內建 `tests.yml` 骨架（tests/ 出現即自動執行 pytest）。
- **R-20（workflow policy_version 同步，FAIL gate，無豁免 label，比照 R-14）**：workflow 內宣告的 `policy_version` / `POLICY_VERSION` semver 字面值必須與 `.paul-project.yml` 的 `policy_version` 一致；input 宣告與 `${{ inputs.* }}` 模板表達式不在檢查範圍。
- **Exemption 白名單新增**：`policy-exempt:ci-tests`（R-19）。R-20 不設豁免。
