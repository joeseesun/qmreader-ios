# Contributing

QMReader iOS primarily serves a quiet, Chinese-first long-form reading workflow. Focused contributions are welcome.

## Good contribution areas

- SwiftUI accessibility and Dynamic Type fixes.
- Reader typography, layout, image, quote, and code-block improvements.
- Cache, refresh, channel-history, and network reliability.
- Compatible-backend configuration and documentation.
- Tests for canonical links, settings migration, and reader behavior.

## Before opening a PR

1. Keep the change scoped; avoid unrelated refactors.
2. Do not commit signing certificates, provisioning profiles, API keys, user caches, DerivedData, or device screenshots containing private data.
3. Run:

```bash
./run-reader-logic-tests.sh
xcodebuild -project QMReader.xcodeproj -scheme QMReader \
  -configuration Debug \
  -destination 'generic/platform=iOS Simulator' \
  CODE_SIGNING_ALLOWED=NO build
```

4. For UI changes, include a current simulator screenshot and state the tested device size, color scheme, and Dynamic Type setting.
5. Keep the default README Chinese-first and English-accessible.

## Pull requests

- Explain the user-visible outcome first.
- Link related issues.
- List exact verification commands and results.
- Do not replace OFL font files without updating provenance and rechecking PostScript names.

Security issues belong in the private process described in [SECURITY.md](SECURITY.md), not a public issue.
