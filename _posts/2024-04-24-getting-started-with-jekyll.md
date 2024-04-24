---
layout: post
title: Getting Started with Jekyll
---

When I began building a personal webpage, I initially planned on just making a very simple HTML/CSS webpage. I was uninterested in learning a whole new web framework just to make a site with some portfolio work and personal info. All I wanted was a simple static site. As I was reading the docs for [GitHub Pages](https://pages.github.com/) however, I came across a tool called **Jekyll**. 

![image](https://cdn.worldvectorlogo.com/logos/jekyll.svg)

Jekyll is an open source static site generator written in Ruby. The great thing about Jekyll is that you can edit the vast majory of content for your site using [Markdown](https://www.markdownguide.org/). Markdown is very easy to learn and use and I was immediately attracted to the idea using it as the markup language for my website. 

There are many different [themes for Jekyll](https://jekyllrb.com/docs/themes/) that have been created by the community over the years to support many different types of webpages. Honestly the hardest part about getting started was just choosing a theme. I spend a good two days browsing and testing out different ones. Eventually, I overcame the paradox of choice and settled on the current minimalist design.

Setting up a GitHub Pages site with Jekyll was a very simple process and they have [extensive documentation on it](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll). However, there were some speed bumps, in particular with installing Jekyll locally for local testing.

Jekyll has [installation instructions](https://jekyllrb.com/docs/installation/) and I don't recall running into any issues while installing the tool itself. However, I did run into issues once I started building local Jekyll projects. Building a project requires running the following commands:
```
bundle install
bundle exec jekyll serve
```
I was getting the following error whenever I tried to install the one of the required packages: `An error occurred while installing eventmachine (1.2.7), and Bundler cannot continue.`

After some googling, I found [a handy blog post](https://www.jessesquires.com/blog/2023/01/18/eventmachine-failure-on-macos-ventura/) from someone who was having the same issue. Apparently, the issue occurs in newer versions of MacOS. Luckily, you can run the following to install `eventmachine` correctly:
```sh
gem install eventmachine -v '1.2.7' -- --with-ldflags="-Wl,-undefined,dynamic_lookup"
```
After doing this, `bundle install` succeeded and I was able to start my local Jekyll project! I am now writing this blog post to document this issue in case anyone else runs in to the same issue or in case future me runs in to the same issue and forgets what I did to resolve it.