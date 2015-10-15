# Semaphore Docs

Semaphore Docs, powered by [Middleman](http://middlemanapp.com) and Amazon S3.


## Setup

Clone the repo and install all necessary gems with

```
$ git clone git@github.com:renderedtext/semaphore-docs-new.git
$ cd semaphore-docs-new
$ bundle install --path .bundle
$ cp data/credentials.yml.example data/credentials.yml
```

For writing new articles or making updates, feel free to leave dummy credentials
in `data/credentials.yml`.

## Writing

Pages are stored in `source/docs/`.

To view the blog locally run:

```
./server
```

which actually runs

```
$ bundle exec middleman -p 4000
```

Now you can open [http://localhost:4000/docs](http://localhost:4000/docs).

### Categories

Categories will be automatically grabbed from the post heading:

```yml
---
layout: post
title: Custom database.yml
category: Ruby
---
```

If the page `/docs/ruby.html` exists, user will be able to reach it from the post
breadcrumbs. If the page doesn't exist, a page with the list of all posts in the
category will be automatically generated and displayed.

### Embedding images

All images must be in the PNG file format, and processed using
[ImageOptim](https://imageoptim.com/). If you do not have access to an OS X
machine, please notify us in the pull request, and we'll make sure to run them
through ImageOptim.

Give all images appropriate alt text, as well as the following CSS classes:

```html
<img src="/docs/assets/img/2012-06-14/semaphore-homepage.png" alt="Semaphore Homepage" class="img-responsive img-bordered">
```

### Escaping ERB

You must escape ERB code snippets in files with `.erb` extension
([via](https://github.com/middleman/middleman-syntax/issues/29)):

```
<%%= foo %>
```

## Deployment

_for Rendered Text people_

Simply run

```
./deploy
test
```

which does `bundle exec middleman build` and uploads the content to an S3
bucket using the AWS CLI. It requires a valid `~/.aws` configuration.

## Configuration

All sensitive credentials are stored in `data/credentials.yml` check `data/credentials.yml.example` for more info about format of file.

## Importing content from Semaphore Blog

If you turn a blog post into a Semaphore Docs page you should include the
canonical url in the post meta data. For more info, visit the Semaphore Blog
[guidelines](https://github.com/renderedtext/semaphore-blog#moving-content-to-semaphore-docs).
