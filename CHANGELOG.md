# Changelog

## v0.0.4

* Migrate i18n locale codes from legacy underscore form (`zh_CN`/`en_US`) to [BCP 47](https://tools.ietf.org/html/bcp47) (`zh-CN`/`en`)
  * Aligns with SiYuan kernel RFC 5646 / BCP 47 lang code refactor (see https://github.com/siyuan-note/siyuan/issues/7098)
  * `theme.json` keys and `README.zh-CN.md` filename updated accordingly
  * Add BCP 47 `:lang()` stylesheet example in `theme.css` for CJK font specialization
  * Bump `minAppVersion` to `3.7.0` (older SiYuan versions will fall back to `default` locale for this theme)

## v0.0.3

* Initial release
