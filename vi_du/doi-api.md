# Đổi API cho mod

Mỗi lần đổi / bỏ thứ mod dùng (`window.tuTien`, `game.*`, state, `core`) ghi một dòng ở đây, mới nhất ở trên. Đổi phần trong bảng "Bản này có gì" của [README](tai-lieu-api.md) thì tăng `apiVersion` (`app/src/game/mod/gate.ts`). Thêm mới không cần ghi.

## apiVersion 1 (2026-11-04)

- Móc luyện chế (2026-11-07, thêm, không tăng `apiVersion`; gdd 60 §22): modifier `craftDistribution`; sự kiện `professionPromoted`; `craft` thêm `profession`, `kind` và giờ báo cả mẻ khảo hạch / mẻ ảo (hai loại này không có `recipe`; mod lọc theo `recipe` vẫn chạy như cũ).

- Bộ component (2026-11-07, thêm, không tăng `apiVersion`; gdd 60 §20): `ui.kit` (form, khung, chữ, vật, `modal`, `popup`, `tip`); `addPanel({ fab: false })` cho khung không cần nút nổi.

- Mở rộng (2026-11-06, thêm, không tăng `apiVersion`; gdd 60 §19): `tuTien.core` có cả hàm / hằng không export của lõi (không cam kết, không ghi ở đây khi đổi); `tuTien.hud` (store giao diện HUD).

- Góp ý modder (2026-11-06, thêm, không tăng `apiVersion`; gdd 60 §18): patch `$append`; `mod.original(id)`; `ui.gamePanel(tên, mở?)`; sự kiện `itemUsed`; `assets.set` nhận `/img/…`; `game.readCtx({ live })`; `core['progress/dot_pha']`: `xungKich` trả `BreakthroughOutcome` (trước trả `undefined`), thêm `resolveBreakthrough`, `breakthroughGrade`; `core['mod/merge']`: `APPEND_KEY`, `patchLeaves`, `ModProblem.clash` / `clashAt`. Lỗi nội dung giờ bỏ từng mục thay vì cả phần nội dung của mod; không đoán được mod nào thì chỉ bỏ mod nạp sau cùng.

- Thêm `tuTien.pixi` (PixiJS của game) cho mod vẽ lớp `mapLayer`; mod mẫu dùng đủ 4 chỗ cắm.
- Đợt 4 phần nạp (thêm, không tăng `apiVersion`): gói `mod.yaml` + `content/` + `img/` + `main.js`, cài trong game (IndexedDB), thư mục `mods/` của app; `ModInfo.description`; `mod.options` nhận giá trị người chơi chọn; lõi `core['mod/manifest']` (`parseManifest`, `optionValues`, `excludedByOptions`).

- Bản dịch (thêm, không tăng `apiVersion`): `mod.addTranslation(lang, files)`, `mod.addUiStrings(lang, strings)`, gói `i18n/<lang>/` (+ `_ui.yaml`); nằm ngoài `hasContent` / dấu mod.
- Đợt 3 (thêm, không tăng `apiVersion`): `mod.addContent`, `mod.patchContent`, `ModInfo.overrides`, `tuTien.assets.set`; `run.mods` / `meta.mods`; `game.missingMods`, `game.dropMissingMods()`, `game.modReport`; lõi `core['mod/merge']`, `core['mod/stamp']`, `core['mod/prune']`.

- Mở `window.tuTien`: `game`, `state`, `subscribe`, `content`, `map`, `core`, `ui.toast`, `register`, hàng đợi `window.tuTienMods` (pha `ready`).
- Thêm `game.readCtx()`, `core['encounter/choice_risk'].revealedCombatRisk`.
- Export thêm cho Tool Trợ Lý: `progress/tournament.trialOpponent`, `progress/be_quan.retreatTargetGain`, `progress/be_quan.retreatGain`, `progress/luyen_che.nguonDiemGoc`, `progress/tong_mon.tienCuDuoc`, `progress/natal_act.devourItemError`.
