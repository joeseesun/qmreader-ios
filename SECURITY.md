# Security Policy

## Supported version

Security fixes target the latest code on `main` unless a release explicitly says otherwise.

## Report a vulnerability

Do not open a public issue for vulnerabilities, leaked credentials, or private reading data.

Contact the maintainer privately:

- GitHub: [@joeseesun](https://github.com/joeseesun)
- X: [@vista8](https://x.com/vista8)
- Website: [qiaomu.ai](https://qiaomu.ai)

Include the affected version/file, reproduction steps, expected impact, and whether any private link or user data may be exposed.

## Data boundary

- The app contains no bundled API key or account credential.
- Feed, article, translation, rewrite, and submitted-link requests go to `rss.qiaomu.ai` by default.
- Submitted links may be fetched and turned into public reading assets; do not submit private URLs.
- Read/favorite state, appearance settings, and cached snapshots are stored locally on the device.
- Development signing identities and provisioning profiles must never be committed.
