# Screenshot checklist

Put the files in this folder. Use PNG, crop to the relevant window, and remove tokens, email addresses, monitor names, and other personal data.

## Required

| File name | What to show | Do not show |
| --- | --- | --- |
| `extension-connected-allowed.png` | The browser extension popup on a watched tab. Account says Connected. This site says Allowed for that site. | Email, token, unrelated tabs |
| `dashboard-create-token.png` | https://kurokit.com/dashboard/mcp with the Create token button visible. | The token itself |
| `connector-store-kurokit.png` | The KuroKit listing in one AI app's connector or MCP marketplace. | Account email, billing details |
| `connection-success.png` | The AI chat after the connection is added, listing the user's monitors. | Private monitor names or URLs if sensitive |

`connector-store-kurokit.png` is optional if KuroKit is not currently listed in a public store. Do not fake or edit a store listing.

## Optional

| File name | What to show |
| --- | --- |
| `wikipedia-target-url.png` | Wikipedia Recent Changes open from the returned `targetUrl`, with the KuroKit extension icon visible. |
| `dashboard-monitor.png` | A dashboard monitor with a recent Last check time. Hide private monitor names and URLs. |
| `troubleshooting-allow-site.png` | The extension panel showing the Allow button for `en.wikipedia.org`. |

## Image rules

- Format: PNG.
- Width: 1200–1600 px is enough.
- Size: keep each file under about 500 KB if possible.
- Crop browser chrome unless it helps explain where to click.
- Use lowercase file names with hyphens.
- Never include a real Bearer token, email address, password, or card number.

## Committing images

Normal PNGs do not need Git LFS. Keep each file within the size guidance above.

Do not push an image containing a secret and fix it later. It remains in Git history even after the file is replaced.

Reference the images from the docs with a relative path. A page in `docs/` uses `../assets/extension-connected-allowed.png`.
