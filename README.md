make github blog
using Jekyll

## help site

- https://nolboo.kim/blog/2013/10/15/free-blog-with-github-jekyll/
- http://blog.saltfactory.net/jekyll/upgrade-github-pages-dependency-versions.html
- http://michaelchelen.net/81fa/install-jekyll-2-ubuntu-14-04/

## github jekyll

sudo apt-get install ruby ruby-dev make gcc nodejs

sudo gem install jekyll --no-rdoc --no-ri

if occur ruby version error :

sudo apt-get install ruby2.0 ruby2.0-dev

sudo gem2.0 install jekyll-import

sudo gem install jekyll --no-rdoc --no-ri

## Create new site

jekyll new mysite
cd mysite

when occurs bundler error:
gem install bundler


## 지켜야 할것

_posts안에 post할 markdown파일을 넣는다
```
---
layout: post
title: 제목
categories: 어떤 카테고리에 속하는지.
---
```
파일명 규칙

YYYY-MM-DD-[POST SLUG].[FORMAT]

## Markdown변환

주로 ipynb 파일을 문서작업할때 사용하는데 얘를 한방에 마크다운으로 바꾸자
(근데 파이썬 가상환경을 꼭 열어줘야하는 귀찮음)

ipython nbconvert *.ipynb --to markdown

이걸로 markdown으로 바꿈

## Run local
원래라면 jekyll serve --watch
근데 에러가 나네..?
- gem2.0 install bundler
- bundle install
- bundle exec jekyll serve 를 이용해서 로컬에서 실행

 jekyll serve --baseurl '' --watch (css적용을위해)



## Symlink error
