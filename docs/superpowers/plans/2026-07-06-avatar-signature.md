# Avatar and Signature Replacement Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Make generated cards use Li Jun's supplied avatars and display the signature `李珺`.

**Architecture:** Keep the fork's assets under distinct `*-lj*` filenames and update the render paths, generated-character references, displayed signatures, and personalized workflow instructions. Preserve upstream authorship, repository metadata, installation commands, and historical notes outside these skills.

**Tech Stack:** HTML templates, Node.js with Playwright, Python 3 scripts, Markdown skill instructions, shell verification with `rg`.

---

### Task 1: Replace the `ljg-card` logo and signature

**Files:**
- Add: `skills/ljg-card/assets/logo-lj.png`
- Modify: `skills/ljg-card/assets/capture.js:20`
- Modify: `skills/ljg-card/assets/big_template.html:183`
- Modify: `skills/ljg-card/assets/long_template.html:233`
- Modify: `skills/ljg-card/assets/poster_template.html:218`
- Modify: `skills/ljg-card/assets/sketchnote_template.html:204`
- Modify: `skills/ljg-card/assets/infograph_template.html:86`
- Modify: `skills/ljg-card/assets/whiteboard_template.html:120`
- Modify: `skills/ljg-card/assets/comic_template.html:101`
- Modify: `skills/ljg-card/SKILL.md:54`
- Modify: `skills/ljg-card/references/mode-big.md:22`
- Modify: `skills/ljg-card/references/mode-big.md:137`

- [ ] **Step 1: Run the card identity check and confirm it fails**

Run:

```bash
test -f skills/ljg-card/assets/logo-lj.png \
  && rg -q "logo-lj\\.png" skills/ljg-card/assets/capture.js \
  && ! rg -n "李继刚" \
    skills/ljg-card/assets/big_template.html \
    skills/ljg-card/assets/long_template.html \
    skills/ljg-card/assets/poster_template.html \
    skills/ljg-card/assets/sketchnote_template.html \
    skills/ljg-card/assets/infograph_template.html \
    skills/ljg-card/assets/whiteboard_template.html \
    skills/ljg-card/assets/comic_template.html \
    skills/ljg-card/SKILL.md \
    skills/ljg-card/references/mode-big.md
```

Expected: exit status `1`; `capture.js` still points to `logo.png`, and the listed files still contain `李继刚`.

- [ ] **Step 2: Update the logo path and displayed name**

Apply these exact replacements:

```text
skills/ljg-card/assets/capture.js
  logo.png -> logo-lj.png

All seven listed HTML templates
  李继刚 -> 李珺

skills/ljg-card/SKILL.md
  logo + 李继刚 -> logo + 李珺

skills/ljg-card/references/mode-big.md
  logo + 李继刚 -> logo + 李珺
```

- [ ] **Step 3: Run the card identity check and confirm it passes**

Run the command from Step 1.

Expected: exit status `0`.

- [ ] **Step 4: Render a representative card**

Run:

```bash
cp skills/ljg-card/assets/big_template.html /tmp/ljg-card-avatar-signature.html
node skills/ljg-card/assets/capture.js \
  /tmp/ljg-card-avatar-signature.html \
  /tmp/ljg-card-avatar-signature.png \
  1080 1440
sips -g pixelWidth -g pixelHeight /tmp/ljg-card-avatar-signature.png
```

Expected: capture prints `OK`; `sips` reports `pixelWidth: 1080` and `pixelHeight: 1440`. Inspect the PNG and confirm the footer shows the new avatar and `李珺`.

- [ ] **Step 5: Commit the card changes**

```bash
git add \
  skills/ljg-card/assets/logo-lj.png \
  skills/ljg-card/assets/capture.js \
  skills/ljg-card/assets/big_template.html \
  skills/ljg-card/assets/long_template.html \
  skills/ljg-card/assets/poster_template.html \
  skills/ljg-card/assets/sketchnote_template.html \
  skills/ljg-card/assets/infograph_template.html \
  skills/ljg-card/assets/whiteboard_template.html \
  skills/ljg-card/assets/comic_template.html \
  skills/ljg-card/SKILL.md \
  skills/ljg-card/references/mode-big.md
git commit -m "feat(ljg-card): use Li Jun avatar and signature"
```

### Task 2: Replace the `ljg-library` character reference and signature

**Files:**
- Add: `skills/ljg-library/assets/lj-portrait.png`
- Modify: `skills/ljg-library/assets/gen_illustration.py`
- Modify: `skills/ljg-library/assets/library_template.html`
- Modify: `skills/ljg-library/SKILL.md`
- Modify: `skills/ljg-library/references/example.md`
- Modify: `skills/ljg-library/references/extraction.md`
- Modify: `skills/ljg-library/references/visual.md`

- [ ] **Step 1: Run the library identity check and confirm it fails**

Run:

```bash
test -f skills/ljg-library/assets/lj-portrait.png \
  && ! rg -n "ljg-portrait|李继刚|继刚" skills/ljg-library
```

Expected: exit status `1`; the generator and instructions still reference `ljg-portrait.png` and the old protagonist identity.

- [ ] **Step 2: Update the generator's default character**

Apply these exact identity changes in `skills/ljg-library/assets/gen_illustration.py`:

```text
带继刚作主角 -> 带李珺作主角
继刚在做/经历什么 -> 李珺在做/经历什么
继刚墨像参考图 -> 李珺墨像参考图
assets/ljg-portrait.png -> assets/lj-portrait.png
认得出的继刚 -> 认得出的李珺
继刚从参考图生成 -> 李珺从参考图生成
with_name("ljg-portrait.png") -> with_name("lj-portrait.png")
```

- [ ] **Step 3: Update the library template and direct avatar instructions**

Apply these changes:

```text
For each file below, replace 李继刚 -> 李珺 before replacing any remaining 继刚 -> 李珺.

skills/ljg-library/assets/library_template.html
  assets/ljg-portrait.png -> assets/lj-portrait.png
  继刚作主角 -> 李珺作主角
  李继刚 -> 李珺

skills/ljg-library/SKILL.md
  继刚 -> 李珺
  assets/ljg-portrait.png -> assets/lj-portrait.png

skills/ljg-library/references/example.md
  继刚 -> 李珺

skills/ljg-library/references/extraction.md
  继刚 -> 李珺
  assets/ljg-portrait.png -> assets/lj-portrait.png

skills/ljg-library/references/visual.md
  继刚 -> 李珺
```

- [ ] **Step 4: Run syntax and identity checks**

Run:

```bash
uv run python -m py_compile skills/ljg-library/assets/gen_illustration.py
test -f skills/ljg-library/assets/lj-portrait.png \
  && ! rg -n "ljg-portrait|李继刚|继刚" skills/ljg-library
```

Expected: Python compilation succeeds and the identity check exits with status `0`.

- [ ] **Step 5: Commit the library changes**

```bash
git add \
  skills/ljg-library/assets/lj-portrait.png \
  skills/ljg-library/assets/gen_illustration.py \
  skills/ljg-library/assets/library_template.html \
  skills/ljg-library/SKILL.md \
  skills/ljg-library/references/example.md \
  skills/ljg-library/references/extraction.md \
  skills/ljg-library/references/visual.md
git commit -m "feat(ljg-library): use Li Jun portrait and signature"
```

### Task 3: Replace the `ljg-map` character reference and signature

**Files:**
- Add: `skills/ljg-map/assets/lj-portrait.png`
- Modify: `skills/ljg-map/assets/gen_illustration.py`
- Modify: `skills/ljg-map/assets/map_template.html`
- Modify: `skills/ljg-map/SKILL.md`
- Modify: `skills/ljg-map/references/example.md`
- Modify: `skills/ljg-map/references/research.md`
- Modify: `skills/ljg-map/references/visual.md`

- [ ] **Step 1: Run the map identity check and confirm it fails**

Run:

```bash
test -f skills/ljg-map/assets/lj-portrait.png \
  && ! rg -n "ljg-portrait|李继刚|继刚" skills/ljg-map
```

Expected: exit status `1`; the generator, template, and instructions still contain the old asset and identity.

- [ ] **Step 2: Update the map generator, template, and instructions**

Apply these exact replacements throughout `skills/ljg-map`:

```text
assets/ljg-portrait.png -> assets/lj-portrait.png
with_name("ljg-portrait.png") -> with_name("lj-portrait.png")
李继刚 -> 李珺
继刚 -> 李珺
```

These references all describe the recurring surveyor avatar or rendered signature; no repository authorship metadata lives under `skills/ljg-map`.

- [ ] **Step 3: Run syntax and identity checks**

Run:

```bash
uv run python -m py_compile skills/ljg-map/assets/gen_illustration.py
test -f skills/ljg-map/assets/lj-portrait.png \
  && ! rg -n "ljg-portrait|李继刚|继刚" skills/ljg-map
```

Expected: Python compilation succeeds and the identity check exits with status `0`.

- [ ] **Step 4: Commit the map changes**

```bash
git add \
  skills/ljg-map/assets/lj-portrait.png \
  skills/ljg-map/assets/gen_illustration.py \
  skills/ljg-map/assets/map_template.html \
  skills/ljg-map/SKILL.md \
  skills/ljg-map/references/example.md \
  skills/ljg-map/references/research.md \
  skills/ljg-map/references/visual.md
git commit -m "feat(ljg-map): use Li Jun portrait and signature"
```

### Task 4: Verify scope and final state

**Files:**
- Verify all files changed in Tasks 1-3.
- Do not modify `.gitignore`, `FORK_WORKFLOW.md`, `.claude-plugin/*`, `README.md`, or upstream repository URLs.

- [ ] **Step 1: Verify assets and active paths**

Run:

```bash
file \
  skills/ljg-card/assets/logo-lj.png \
  skills/ljg-library/assets/lj-portrait.png \
  skills/ljg-map/assets/lj-portrait.png
rg -n "logo-lj\\.png|lj-portrait\\.png|李珺" \
  skills/ljg-card \
  skills/ljg-library \
  skills/ljg-map
```

Expected: all three files are valid PNG images, and active code/templates contain the new paths and signature.

- [ ] **Step 2: Confirm upstream attribution remains unchanged**

Run:

```bash
git diff HEAD~3..HEAD -- \
  .claude-plugin README.md skills/ljg-push \
  .gitignore FORK_WORKFLOW.md
```

Expected: no output.

- [ ] **Step 3: Review the complete implementation diff**

Run:

```bash
git diff 531a297..HEAD --stat
git diff 531a297..HEAD -- \
  skills/ljg-card \
  skills/ljg-library \
  skills/ljg-map
git status --short
```

Expected: every implementation change supports the avatar/signature replacement. Pre-existing `.gitignore` and `FORK_WORKFLOW.md` changes may remain uncommitted; no unrelated file is added to an implementation commit.
