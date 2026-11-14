# xray-tools

Interactive helper for Xray-core VLESS + REALITY inbounds.

## Stability defaults

New XHTTP inbounds are written with:

- `mode: stream-one` — a single H2 stream; `auto` only resolves to `stream-one`
  on cores that know about REALITY, older ones may fall back to `packet-up`
- `xPaddingBytes: 100-1000` — random POST padding, hides request sizes
- `scMaxEachPostBytes: 1000000`, `scMinPostsIntervalMs: 30`, `scMaxBufferedPosts: 30`
- `scStreamUpServerSecs: 20-80` — the server pushes data every 20–80 s, so NAT and
  DPI idle timers never see a quiet connection

`fragment=...` is no longer appended to client links: ClientHello splitting breaks
H2 sessions in Happ/iOS and shows up as "connects, then goes silent". If the plain
handshake is actually blocked, set `DPI_FRAGMENT` at the top of `xray-tool.sh`.
