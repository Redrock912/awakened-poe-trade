---
name: sync-upstream
description: Track and merge new findings from original upstream SnosMe/awakened-poe-trade while prioritizing Korean client compatibility.
---

# Upstream Sync Skill for Awakened PoE Trade (Korean Version)

This skill provides step-by-step instructions for the agent to track, inspect, and apply upstream updates from `SnosMe/awakened-poe-trade` while strictly preserving Korean client compatibility.

## Execution Steps

### 1. Fetch Upstream Changes
Add the upstream remote (if missing) and fetch the latest `master` branch:
```bash
git remote add upstream https://github.com/SnosMe/awakened-poe-trade.git 2>/dev/null || true
git fetch upstream master
```

### 2. Inspect New Upstream Findings
Check what commits or files have changed upstream since the last merge:
```bash
git log HEAD..upstream/master --oneline
```

### 3. Merge Upstream with Korean Priority Strategy
Merge `upstream/master` into the current `master` branch:
```bash
git merge upstream/master --no-edit -m "sync: merge upstream changes from SnosMe/awakened-poe-trade"
```

If merge conflicts occur in Korean localization or configuration files, resolve them immediately by prioritizing local Korean versions:
```bash
git checkout --ours -- renderer/public/data/ko/
git checkout --ours -- renderer/src/web/client-log/client-log.ts
git checkout --ours -- renderer/src/web/item-search/WidgetItemSearch.vue
git checkout --ours -- main/src/vision/wasm-bindings.ts
git checkout --ours -- main/package.json
git add .
git commit -m "sync: resolve conflicts by prioritizing Korean client compatibility"
```

### 4. Regenerate Binary Data Indices
Run `make-index-files` in `renderer/` to refresh binary index files for any updated items or stats:
```bash
cd renderer && npm run make-index-files && cd ..
```

### 5. Verify Build & Push
Verify that both renderer and main build without errors:
```bash
cd renderer && npm run build && cd ../main && npm run build && cd ..
```

Then commit and push the updated branch to `origin master`.
