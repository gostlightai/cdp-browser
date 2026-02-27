# Changelog

## 2.0.0 (2026-02-19)

**security: CDP v2 hardening - explicit confirm, draft/post split, safer selectors**

- tweet-post: require --confirm as second arg (strict), no auto-injection
- Split tweet: tweet-draft (compose only), tweet-post (requires --confirm)
- Legacy tweet action → draft only
- Compose launcher: SideNav_NewTweet_Button, /compose/post, Post only (avoid reply buttons)
- Post button: tweetButton, tweetButtonInline
- Add query ops: getUrl, getText, getHtml
- Add --save-pending for tweet-draft (pending-tweet.json)
- Replace curl with fetch in cdp.js (remove shell injection)
- Replace eval with allowlisted query in pw.js
- Add Telegram confirm flow: send-tweet-confirm.sh, .cdp-browser.json.example
- Docs: SKILL.md, README.md, SECURITY.md

## 1.0.0

Initial release.
