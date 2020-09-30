# GitBook

> <https://www.npmjs.com/package/gitbook>, <https://github.com/GitbookIO/gitbook>

```bash
# npm install gitbook-cli -g

# 安装插件（如果有）
gitbook install

# 本地查看
gitbook serve

# HTML
gitbook build ./ ./docs

# PDF
# 需要安装 calibre, https://calibre-ebook.com
# Ubuntu 安装: sudo apt install calibre
gitbook pdf ./ ./mybook.pdf

# epub
gitbook epub ./ ./mybook.epub

# mobi
gitbook mobi ./ ./mybook.mobi
```

```makefile
PROJNAME=book-name
DIST_FOLDER=dist
.PHONY: clean html pdf mobi epub

all: clean html pdf mobi epub

html: _dist_dir
  gitbook build . ./${DIST_FOLDER}/html
  # FIXME: can not delete
  rm -rf ./${DIST_FOLDER}/html/{Makefile,.editorconfig,.gitignore}

pdf: _dist_dir
  gitbook pdf . ./${DIST_FOLDER}/${PROJNAME}.pdf

epub: _dist_dir
  gitbook epub . ./${DIST_FOLDER}/${PROJNAME}.epub

mobi: _dist_dir
  gitbook mobi . ./${DIST_FOLDER}/${PROJNAME}.mobi

clean:
  rm -rf ${DIST_FOLDER}

_dist_dir:
  mkdir -p ${DIST_FOLDER}
```
