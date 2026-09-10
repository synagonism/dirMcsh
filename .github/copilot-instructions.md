# HitpMcs Workspace Instructions

**Project**: dirMcsh – A multilingual, structured knowledge-base system for Synagonism (a-WorldView by Nikos-Kaseluris).

This workspace contains HTML content pages, Node.js utilities for content management, and tools for deploying to production via SFTP.

---

## Quick Setup

```bash
# Run Node.js utilities
node Mcsmgr/mWatch.mjs pwd  # Watch for changes, index saved files, upload changes.
node Mcsmgr/mMcsNew.mjs pwd # create new HitpMcs.
```

---

## Project Overview

### Structure
- **`/`** – Root HTML pages (index.html, Mcsh000000.last.html, etc.) and JSON metadata
- **`dirCor/`** – Core content (McshCor000001.last.html, etc.)
- **`dirEdu/`** – Educational content
- **`dirHlth/`** – Health-related content
- **`dirHmn/`** – on Humans content
- **`dirLag/`** – Language content 
- **`dirNtr/`**, **`dirOgm/`**, **`dirStn/`**, **`dirTch/`**, etc. – Topic-specific directories
- **`dirNamidx/`** – Name index pages
- **`dirWrdidx/`** – Word index pages
- **`Mcsmgr/`** – Core management JavaScript/Node.js modules
  - `mMcsh2.js` – Main HTML component handler
  - `mMcsh2.css` – Main CSS component handler
  - `mNamidx.mjs` – Name indexing
  - `mWrdidx.mjs` – Word indexing
  - `mWatch.mjs` – File system watcher
  - `mSftp.mjs` – SFTP deployment
  - `mUtil.mjs`, `mLagUtil.js` – Utility functions

### Content Format
- **Content pages**: HTML with custom structure, using IDs for sections (e.g., `id="idOverview"`, `id="idDescription"`)
- **Naming convention**: `Mcs[Category]######.last.html` (e.g., `McshCor000001.last.html`, `McshEdu000005.last.html`)
- **Metadata**: JSON files track content state (`aPages.json`, `Mcshqnt.json` for quantity counts)

### Multilingual Support
The system supports **20+ languages** via the JavaScript engine:
- English (Engl, F2)
- Sinagu (Sngu, Shift+F2) – Custom language
- Greek (Elln, Ctrl+F2)
- Chinese (Zhon, Alt+F2)
- Ancient Greek (Ella), Albanian, Arabic, Esperanto, French, German, Hindi, Italian, Japanese, Khmer, Korean, Romanian, and Slavic variants

---

## Development Workflow

### Daily Tasks

1. **Edit content pages**: Modify `.last.html` files in topic directories
   - Keep IDs consistent (e.g., `idOverview`, `idDescription`)
   - Use semantic HTML5
   - Link to related content via class `clsPreview` for preview links

2. **Update indexes**: After adding/renaming content
   ```bash
   node Mcsmgr/mNamidx.mjs      # Rebuild name index
   node Mcsmgr/mWrdidx.mjs      # Rebuild word index
   ```

3. **Watch for changes**: For live development
   ```bash
   node Mcsmgr/mWatch.mjs pwd       # Auto-rebuild on file changes
   ```

4. **Deploy to production**: Push to remote server via SFTP
   ```bash
   node Mcsmgr/mSftp.mjs        # Deploy via sftp.json config
   ```

### Content Naming Convention
When creating new content:
- Place in appropriate category directory (dirCor, dirEdu, etc.)
- Name as: `Mcs[Category]NNNNNN.last.html` where NNNNNN is zero-padded ID
- Example: `McsEdu000042.last.html` (Education, sequential ID)
- Track last ID in `aPages.json`

### Configuration Files
- **`sftp.json`** – SFTP credentials and server paths
- **`SftpAgg.json`** – Aggregated SFTP configuration
- **`.eslintrc.json`** – ESLint rules (minimal, only JSX a11y turned off)
- **`.vscode/settings.json`** – Editor settings (folding, find match highlighting)

---

## Key Patterns

### HTML Structure
```html
  <section id="idVscodeusifedtr">
  <h2 id="idVscodeusifedtrH2">editor of VscUsif
    <a class="clsHide" href="#idVscodeusifedtrH2"></a></h2>
  <p id="idVscodeusifedtrdsn">description::
    <br>× HitpMcs-creation: {2026-03-26},
    <br>· 
    <a class="clsHide" href="#idVscodeusifedtrdsn"></a></p>
  <p id="idVscodeusifedtrnam">name::
    <br>* McsEngl.VscUsif'editor,
    <a class="clsHide" href="#idVscodeusifedtrnam"></a></p>
  </section>
```

### JavaScript Modules (Node.js)
- Use ES6 `import`/`export` syntax
- Modules in `Mcsmgr/` directory
- Dependencies: `fs`, `n-readlines`, `node-fetch`, `ssh2-sftp-client`

### Search/Navigation
- Name indexing: Creates `dirNamidx/` pages linking to definitions
- Word indexing: Creates `dirWrdidx/` pages for keyword lookup
- Links use anchor fragments (#) for fast navigation

---

## Troubleshooting

### Module Not Found
Ensure npm dependencies are installed:
```bash
npm install
```

### Index Out of Sync
Rebuild indices after bulk content changes:
```bash
node Mcsmgr/mNamidx.mjs && node Mcsmgr/mWrdidx.mjs
```

### SFTP Deployment Issues
- Verify `sftp.json` credentials and paths
- Check network connectivity
- Review logs in `SftpAgg.json`

---

## Code Style & Conventions

- **JavaScript**: ES6 modules, functional programming preferred
- **HTML**: Valid HTML5, semantic tags (section, header)
- **Naming**: Camel case (JS), kebab case (CSS), descriptive IDs (idOverviewH1)
- **Comments**: Include MIT License header in main scripts
- **File extensions**: `.mjs` for Node.js modules, `.js` for browser scripts

---

## References

- **Entry point**: [Mcsh000000.last.html](Mcsh000000.last.html)
- **Main stylesheet**: [Mcsmgr/mMcsh2.css](Mcsmgr/mMcsh2.css)
- **Main script**: [Mcsmgr/mMcsh2.js](Mcsmgr/mMcsh2.js)
- **Philosophy**: https://synagonism.net/
- **Author**: Kaseluris.Nikos.1959

---

## Next Steps

1. Check the [current file being edited](file:///c:/xampp/htdocs/dirMcsh/dirTchInf/McshTchInf000041.last.html) to understand content structure
2. Review [Mcsmgr/mMcsh2.js](Mcsmgr/mMcsh2.js) to understand the component system
3. Explore topic directories to see content patterns
4. Ask about specific content updates, new page creation, or index rebuilding
