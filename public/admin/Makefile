SHELL:=/bin/bash
CSSSRC=$(shell find src/scss -name "*.scss")

.PHONY: css
css: admin-theme.css

admin-theme.css: $(CSSSRC)
	sassc src/scss/admin-theme.scss admin-theme.css
	npx uglifycss admin-theme.css > admin-theme.min.css

.PHONY: watch unwatch
watch:
	watchman watch $(shell realpath src/scss)
	watchman -j <<< '["trigger", "$(shell realpath src/scss)", { "name": "$(shell realpath src/scss)_css", "expression": ["pcre", ".+\\.scss"], "command": ["make", "-f","Makefile","css"], "chdir": "$(shell realpath .)" } ]'

unwatch:
	watchman trigger-del "$(shell realpath src/scss)" "$(shell realpath src/scss)_css"