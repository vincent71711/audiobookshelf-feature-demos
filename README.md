# Audiobookshelf feature demos

Media for quality-of-life feature proposals to [Audiobookshelf's mobile app](https://github.com/advplyr/audiobookshelf-app).

## Startup connection indicator

Show a loading circle with “Connecting to server…” while restoring a saved server connection, before displaying the empty/disconnected state.

- [Existing empty-state screenshot](startup-connection/before-empty-bookshelf.png)
- [Proposed connecting-state screenshot](startup-connection/after-connecting.png)
- [Android Studio recording](startup-connection/loading-circle.mp4)

Captured on a standard Pixel 6 emulator (API 37) using a local Android debug build and a demo saved connection. No personal account or library is shown. The recording demonstrates the connecting animation with an unavailable demo server; it is not a measurement of successful server connection time.

## Implementation

[View the isolated patch](https://github.com/vincent71711/audiobookshelf-feature-demos/blob/be869018d4601e7bc12138ad78b3d2f3fb52fe40/startup-connection/startup-connection-indicator.patch) · [Download patch](https://raw.githubusercontent.com/vincent71711/audiobookshelf-feature-demos/be869018d4601e7bc12138ad78b3d2f3fb52fe40/startup-connection/startup-connection-indicator.patch)

Based on upstream `advplyr/audiobookshelf-app` commit `7014e04e`, this patch changes only the bookshelf startup indicator, its Vuex state, the English connecting message, and seven regression tests. It keeps downloaded shelves available and caps the startup grace period at five seconds.

Apply it to a checkout of that upstream revision:

```sh
git apply /path/to/startup-connection-indicator.patch
node --test tests/startupConnection.test.cjs
```

The seven tests and `npm run generate` passed for the isolated implementation. Native builds and on-device screen-reader testing have not been performed for this isolated branch.

[Feature request: advplyr/audiobookshelf-app#2052](https://github.com/advplyr/audiobookshelf-app/issues/2052).
