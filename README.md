# Code Reviewer

A desktop application for reviewing git repository changes with inline comments, follow-ups, and persistent storage.

## Features

- 🔍 **Smart Change Detection** - Automatically reviews working directory changes, or falls back to last commit if clean
- 💬 **Inline Comments** - Add comments on any line, including deleted lines
- 📝 **Code Selection** - Select specific code snippets for contextual comments
- 🔄 **Follow-up Conversations** - Thread-style comment replies
- 💾 **Persistent Storage** - Comments survive code changes with fuzzy matching
- 📊 **GitHub-style Diff View** - Color-coded additions and deletions
- ⌨️ **Keyboard Shortcuts** - Navigate and comment with keyboard
- 🖥️ **Desktop App** - Native macOS, Windows, and Linux support
- 🎨 **Resizable Panes** - Customizable workspace layout

## Quick Start

### Desktop App (Recommended)

1. Install dependencies:
   ```bash
   npm install
   ```

2. Run the app:
   ```bash
   npm run electron
   ```

3. Use `File > Open Repository` (Cmd/Ctrl+O) to select a Git repository

### Web Mode

1. Install dependencies:
   ```bash
   npm install
   ```

2. Start the server:
   ```bash
   npm start
   ```

3. Open your browser:
   ```
   http://localhost:4500
   ```

## Usage

### Opening a Repository

**Desktop App:**
- Menu: `File > Open Repository...` (Cmd/Ctrl+O)
- Select any Git repository folder

**Web Mode:**
- Enter the full repository path
- Click "Load Repository"

### Adding Comments

1. **Simple Comment** - Click on any line number
2. **With Code Context** - Hold Cmd/Ctrl, select code, then click line number
3. **Follow-up** - Click "Reply" on existing comments
4. **Edit/Delete** - Hover over comments to see actions

### Keyboard Shortcuts

| Shortcut | Action |
|----------|--------|
| `Cmd/Ctrl+O` | Open repository |
| `Cmd/Ctrl+S` | Submit review |
| `Cmd/Ctrl+Enter` | Save comment |
| `Escape` | Cancel input |
| `↑/↓` | Navigate files |

### Submitting Review

Click "Submit Review" to generate `review_[reponame]_[timestamp].txt` with all comments and follow-ups.

## Development

### Running in Dev Mode

```bash
# Desktop app with dev tools
npm run electron:dev

# Web mode
npm run dev
```

### Building

```bash
# Build for current platform
npm run build

# Platform-specific builds
npm run build:mac    # macOS (Universal DMG + ZIP)
npm run build:win    # Windows (NSIS + Portable)
npm run build:linux  # Linux (AppImage + DEB)
```

Built apps will be in `dist/` directory.

## Architecture

### Desktop App (Electron)

```
main.js          → Electron main process, window management
preload.js       → Security bridge for IPC
server.js        → Express backend (random port)
public/          → Frontend assets
  ├── index.html → UI layout
  ├── style.css  → Styling
  └── app.js     → Application logic
```

### Storage

- **Comments**: `reviews/.code-review-comments-[reponame].json`
- **Reviews**: `reviews/review_[reponame]_[timestamp].txt`

## Tech Stack

- **Desktop**: Electron + electron-builder
- **Backend**: Node.js + Express
- **Git Operations**: simple-git
- **Frontend**: Vanilla JavaScript (no frameworks)

## Security

Follows Electron security best practices:
- ✅ Context isolation enabled
- ✅ Node integration disabled
- ✅ Secure IPC via preload script
- ✅ No remote module access

## Distribution

### macOS

1. Join Apple Developer Program ($99/year)
2. Get Developer ID certificate
3. Build and sign:
   ```bash
   npm run build:mac
   ```
4. Notarize (automatic with electron-builder)

### Windows/Linux

No special requirements - just build:
```bash
npm run build:win   # or build:linux
```

## License

MIT

## Author

Dheeraj Jha
