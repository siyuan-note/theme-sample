[中文](https://github.com/siyuan-note/theme-sample/blob/main/README.zh-CN.md)

# SiYuan theme sample

## Get started

* Make a copy of this repo as a template with the <kbd>Use this template</kbd> button, please note that the repo name
  must be the same as the theme name, the default branch must be `main`
* Clone your repo to a local development folder. For convenience, you can place this folder in your `{workspace}/data/themes/` folder

Theme files, updates, and uninstallations are shared by SiYuan data sync; each device keeps its own theme selection. Older clients can continue syncing notes without upgrading and transport internal package archives as ordinary files. Clients that support this feature apply theme package changes; older clients do not use the new theme directory. Upgrade migration preserves the original local files for recovery. Development changes inside this folder also sync; keep experiments outside the workspace or exclude the whole theme folder from sync.

## Development

* theme.json
* icon.png (optional default icon, 160*160)
* preview.png (optional default preview, 1024*768)
* README*.md
* theme.css

Note: The previously optional `theme.js` file is deprecated; new themes should not include it. See [siyuan-note/bazaar#1821](https://github.com/siyuan-note/bazaar/issues/1821).

## theme.json

```json
{
  "name": "theme-sample",
  "author": "Vanessa",
  "url": "https://github.com/siyuan-note/theme-sample",
  "version": "0.0.5",
  "minAppVersion": "3.7.0",
  "displayName": {
    "default": "Theme Sample",
    "zh-CN": "主题示例"
  },
  "description": {
    "default": "This is a theme sample",
    "zh-CN": "这是一个主题示例"
  },
  "readme": {
    "default": "README.md",
    "zh-CN": "README.zh-CN.md"
  },
  "icon": "icon.png",
  "preview": "preview.png",
  "funding": {
    "openCollective": "",
    "patreon": "",
    "github": "",
    "custom": [
      "https://ld246.com/sponsor"
    ]
  },
  "modes": [
    "light"
  ],
  "frontends": [
    "all"
  ],
  "keywords": [
    "sample", "示例"
  ]
}
```

* `name`: Theme name, must be the same as the repo name, and must be unique globally (no duplicate theme names in the
  marketplace)
* `author`: Theme author name
* `url`: Theme repo URL
* `version`: Theme version number, it is recommended to follow the [semver](https://semver.org/) specification
* `minAppVersion`: Minimum version number of SiYuan required to use this theme
* `displayName`: Theme display name, mainly used for display in the marketplace list, supports multiple languages
    * `default`: Default language, must exist
    * `zh-CN`, `en` and other languages: optional, must be [BCP 47](https://tools.ietf.org/html/bcp47) tags (e.g. `zh-CN`, `zh-TW`, `en`, `ja`, `pt-BR`)
* `description`: Theme description, mainly used for display in the marketplace list, supports multiple languages
    * `default`: Default language, must exist
    * `zh-CN`, `en` and other languages: optional, must be BCP 47 tags
* `readme`: readme file name, mainly used to display in the marketplace details page, supports multiple languages
    * `default`: Default language, must exist
    * `zh-CN`, `en` and other languages: optional, must be BCP 47 tags
    * Relative images are loaded from `package.zip` when present; otherwise the online marketplace falls back to the matching GitHub Release. Include them in `package.zip` for offline use
* `icon`: Optional marketplace icon filename at the package root. Supports PNG, JPEG, WebP, and AVIF up to 64 KiB; the recommended size is 160*160
* `preview`: Optional marketplace preview filename at the package root. Supports PNG, JPEG, WebP, and AVIF up to 512 KiB; the recommended size is 1024*768
    * SVG is unsupported. To omit an image, remove its field and the legacy `icon.png` or `preview.png`; an empty field value is invalid
* `funding`: Theme sponsorship information
    * `openCollective`: Open Collective name
    * `patreon`: Patreon name
    * `github`: GitHub login name
    * `custom`: Custom sponsorship link list
    * `links`: Labeled custom sponsorship links, for example `{"label": "Sponsor", "url": "https://example.com"}`
* `modes`: Theme mode list, currently only supports `light` and `dark`
* `frontends`: Supported frontend environments. Optional values are `desktop`, `desktop-window`, `mobile`, `browser-desktop`, `browser-mobile`, and `all`
    * `desktop`: Desktop application
    * `desktop-window`: A standalone desktop window converted from a tab
    * `mobile`: Mobile application
    * `browser-desktop`: Desktop browser using the network serving mode
    * `browser-mobile`: Mobile browser using the network serving mode
    * `all`: All frontend environments
    * Matching is exact. Include `browser-desktop` explicitly if the theme supports the desktop browser
    * A missing or empty field supports desktop frontends only. Mobile frontends require an explicit `mobile`, `browser-mobile`, or `all`; `["all"]` supports every frontend. Do not mix `all` with other values
    * If the theme excludes any frontend, set `minAppVersion` to the first SiYuan version that supports theme frontend compatibility because older clients ignore this field
* `keywords`: Search keyword list, used for marketplace search function

## Package

No matter which method is used to compile and package, we finally need to generate a package.zip, which contains at
least the following files:

* Image files declared by `icon` and `preview` (optional)
* README*.md
* theme.css
* theme.json

## List on the marketplace

* Generate the package.zip
* Create a new GitHub release using your new version number as the "Tag version". See here for an
  example: https://github.com/siyuan-note/theme-sample/releases
* Upload the file package.zip as binary attachments
* Publish the release

For the first release, fork the [community bazaar repository](https://github.com/siyuan-note/bazaar), add one `owner/repo` line to `themes.txt` in its root, and open a PR against `main`. Use one repository per line without commas or empty lines, and add only one new package per PR. See [Submitting a bazaar package](https://github.com/siyuan-note/bazaar#submitting-a-bazaar-package) for the full process and review rules.

After the PR is merged, the bazaar updates its index automatically. For subsequent updates, increase `version` in the package manifest and publish a regular GitHub Release containing `package.zip`; no additional listing PR is needed. See [Updating a bazaar package](https://github.com/siyuan-note/bazaar#updating-a-bazaar-package) for update timing and troubleshooting, and check deployment status in the [Stage workflow](https://github.com/siyuan-note/bazaar/actions/workflows/stage.yml).
