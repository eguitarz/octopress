---
layout: post
title: "Deploy static site on heroku"
date: 2012-08-06 15:57
comments: true
categories: heroku
---
## When you just want simple… on heroku
Sometimes you just want to deploy a simple web which contains one or two static pages, how would you do? You don't want to build a rails project merely to serve a couple of static pages. Here's a quick guide for you~!

## Environment
You should not use cedar stack, that's not friendly for static sites. (You need to install some gems by yourself, and do some hacks…) bamboo is a good start point.

    heroku create --stack bamboo-ree-1.8.7

## File structure
You should create a public folder at root. Put your index.html and stylesheet / js / img folder into "public" folder.

## Config
Last, create a simple config to tell rack middleware how to render the static files…

    use Rack::Static, 
    :urls => ["/stylesheet", "/img", "/js"],
    :root => "public"

    run lambda { |env|
    [
        200, 
    {
      'Content-Type'  => 'text/html', 
      'Cache-Control' => 'public, max-age=86400' 
    }, File.open('public/index.html', File::RDONLY)
    ] 


Then you can commit and push the site to heroku. Here are the official guides if you still do not understand…

- [Static Sites with Ruby on Heroku/Bamboo](https://devcenter.heroku.com/articles/static-sites-on-heroku)

- [The Badious Bamboo Stack](https://devcenter.heroku.com/articles/bamboo)

