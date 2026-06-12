# Changelog

本專案所有重大變更都會記錄在此檔案。

格式基於 [Keep a Changelog 1.1.0](https://keepachangelog.com/zh-TW/1.1.0/)，
本專案遵循 hamanpaul project policy v1.0.2。

## [Unreleased]

### Added
- **新增 `tests.yml` CI 骨架**：生成的新 repo 出生即帶測試 gate——`tests/` 尚不存在時 job 自動跳過（綠燈），加入測試套件後 pytest 自動成為 PR gate，同時滿足 policy R-19 的 workflow 偵測
- 建立 `hamanpaul/new-project-template` 新專案 bootstrap skeleton
- 新增釘選到 `hamanpaul/paulsha-conventions` 的 `Policy Check` reusable workflow
- 新增同步的 agent convention files 與基本 policy metadata

### Changed
- **同步 policy 1.0.2**：bump `policy_version` 1.0.1 → 1.0.2（`.paul-project.yml` 與四份 agent convention files、`managed-by@v1.0.2`），caller `Policy Check` workflow 的 `uses:` 與 `policy_engine_ref` 重新雙重釘選至 `hamanpaul/paulsha-conventions@98487868a098e22647074c677a58633ce4fa19be`（= engine tag `v1.0.2`，含 R-19 / R-20）；agent 檔追加 R-19（CI 必須跑測試）/ R-20（workflow policy_version 同步）說明與 `policy-exempt:ci-tests` 白名單項
- **同步 policy 1.0.1**：bump `policy_version` 1.0.0 → 1.0.1（`.paul-project.yml` 與四份 agent convention files、`managed-by@v1.0.1`），caller `Policy Check` workflow 的 `uses:` 與 `policy_engine_ref` 重新雙重釘選至 `hamanpaul/paulsha-conventions@4ff59b6c35a46a87af3c3e641975743ee8fa0858`（含 R-17 / R-18）；agent 檔追加 R-17（PR↔issue closing-keyword）、R-18（docs 對齊 WARN）與語言規範說明
- `Policy Check` workflow 改為雙重釘選 `hamanpaul/paulsha-conventions@8454aa1967b752ea38c82edd79a8439b5bde915b`，同步設定 reusable workflow `uses:` 與 `policy_engine_ref`

### Fixed
- 移除超出需求範圍的 `pyproject.toml` 與相關 package 化敘述
