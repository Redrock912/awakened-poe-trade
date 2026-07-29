# Project Rules for Awakened PoE Trade (Korean Client Fork)

## Core Priority: Korean Client Compatibility
When modifying, updating, or syncing code in this repository, **Korean client compatibility must always take top priority**.

### Protected Korean Client Files & Logic:
1. **`renderer/public/data/ko/client_strings.js`**: Contains Korean regexes (`METAMORPH_*`, `CHAT_WEBTRADE_GEM`, `ITEM_CLASS`, `RARITY`, etc.).
2. **`renderer/src/web/client-log/client-log.ts`**: Contains `TRADE_BULK_WHISPER['ko']` regex (`안녕하세요, {league}에서...`).
3. **`renderer/src/web/item-search/WidgetItemSearch.vue`**: Contains CJK non-space token matching for Korean (`AppConfig().language === 'ko'`).
4. **`main/src/vision/wasm-bindings.ts`**: Contains OCR language mapping `['ko', 'kor']`.
5. **`main/package.json`**: Contains repository URL pointing to `https://github.com/Redrock912/awakened-poe-trade.git`.
6. **`renderer/public/data/ko/*.index.bin`**: Binary index files (`items-name.index.bin`, `items-ref.index.bin`, `stats-ref.index.bin`, `stats-matcher.index.bin`) generated via `make-index-files`.

---

## Upstream Synchronization Workflow
When checking for, integrating, or auditing upstream changes from `SnosMe/awakened-poe-trade`:
1. **Fetch & Compare**: Fetch `upstream/master` (`https://github.com/SnosMe/awakened-poe-trade.git`) and inspect incoming diffs.
2. **Preserve Korean Extensions**: Apply new upstream features, items, stats, and bug fixes without overwriting Korean regexes or localization structures.
3. **Re-index Data**: Always run `npm run make-index-files` in `renderer/` after updating item or stat datasets.
4. **Build & Verify**: Validate clean builds (`npm run build` in `renderer/` and `main/`) before pushing.
