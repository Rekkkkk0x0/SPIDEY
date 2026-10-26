# Pocket cloud interface channel

Only static UI bundles are hosted here. Users import one small cloud script JSON.

The script checks releases.json on its first explicit open after reloading Tavern. A compatible newer version is offered with Update / Use current version; it is never installed without the user's choice. Cached versions work if the channel is offline. New UI changes must be built and published, not just edited in an unrelated source file.

For each release: build all editions, gzip their standalone index.html files, base64-encode the gzip bytes into a versioned .txt path, and publish these immutable files first. Then update releases.json with a higher semantic version, bridge=1, exact compressedBytes and SHA-256 of the GZIP BYTES (not the base64 string), and immutable full-commit URLs on fastly/gcore/testingcf.jsdelivr.net. Keep all old assets; older scripts and users choosing their current version need them. Purge the three @main/phone-ui/releases.json CDN paths after publishing so their mutable channel caches refresh.

Never put API keys, chats or user saves in this repository. Static resource caching is browser-local and separate from account-scoped phone saves. Changing the host bridge protocol requires a new small script; UI-only changes use this channel. Unsupported bridge versions are ignored by older scripts.

Current payloads were built from the locally validated Pocket 1.9.3 UI. See the distributed REVIEW_1.9.4.md for tests and limitations.
