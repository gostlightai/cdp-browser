# Security Considerations

**Origin:** These mitigations were implemented in response to ClawHub Security findings (Feb 2026).

## What Changed and Why

| Finding | Risk | Change | Rationale |
|---------|------|--------|------------|
| cdp.js execSync + curl | Shell injection | Replaced with Node `fetch()` | No shell invocation; eliminates injection vector |
| pw.js eval | Arbitrary JS execution; data exfiltration | Removed; added allowlisted `query` (getText, getHtml, getUrl) | Only safe, predefined ops; no user code interpolation |
| tweet (auto-post) | Unauthorized posting on X | Split into tweet-draft (default) + tweet-post (requires `--confirm`) | User must explicitly approve before posting |

## Implemented Protections

| Risk | Mitigation |
|------|------------|
| **Shell injection** | cdp.js uses `fetch()` only; no execSync, no curl |
| **Arbitrary eval** | Removed. Use `query` with allowlisted ops: getText, getHtml, getUrl |
| **Scroll selector injection** | `page.evaluate((sel) => ..., target)` passes selector as parameter—no string interpolation |
| **Snapshot path traversal** | `tabId` sanitized to `[A-Za-z0-9_-]`; output path uses `path.join(__dirname, ...)` |
| **cdp.js gotoTab** | `tabId` sanitized before use in URL path |
| **Unauthorized tweet** | tweet-post requires `--confirm` flag; tweet-draft fills compose only |

## Operational Notes

- CDP on port 9222 has full browser control; keep it local or behind auth.
- **tweet-draft** fills compose only; user posts manually or confirms via text/Telegram button.
- **tweet-post** requires explicit `--confirm`; use when user has approved.
- Screenshots may capture sensitive page content; store in a private location.
