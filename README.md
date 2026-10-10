# pi-editor-links

Opens local file links from Pi messages and tool output in Zed. For example,
`src/example.ts:12:3` becomes a link to that file at line 12, column 3 when the
file exists.

The extension links existing paths in assistant text, inline code, and local
Markdown destinations. It also converts file hyperlinks in built-in tool calls
and links existing paths in bash output. It leaves fenced code blocks alone.

## Requirements

- Node.js 24 or newer and Pi.
- macOS with Zed installed and registered to handle `zed://` URLs.
- A terminal that supports clickable links, including OSC 8 links in tool output.

Links use an HTTP bridge at `127.0.0.1:48291`, because Ghostty opens HTTP(S)
links rather than `zed://` links. A Pi session with this extension must remain
running to serve them; another session can serve links left in scrollback.
For files inside a Git repository, the bridge uses
`/Applications/Zed.app/Contents/MacOS/cli` to open the nearest repository as a
Zed workspace and preserve the file position. If the CLI is unavailable or the
file is outside Git, it falls back to macOS `open` with the Zed URL.

## Install

```bash
pi install git:github.com/ryanmazzolini/pi-editor-links
```

Run `/reload` or restart Pi after installation.

Do not load both this package and the original editor-links extension.

## Development and provenance

The implementation and tests were extracted unchanged from
[`pi-skills`](https://github.com/ryanmazzolini/pi-skills), where their earlier
history remains.

```bash
npm ci --ignore-scripts
npm test
npm pack --dry-run --json
```

`npm test` runs strict TypeScript checking followed by Node's test runner.
The package ships the extension, not its tests.

## License

MIT.

AI assistance was used to extract and document this package.
