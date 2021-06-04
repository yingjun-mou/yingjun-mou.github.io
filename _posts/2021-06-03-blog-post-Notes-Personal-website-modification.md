---
title: 'Personal website using Academicpages'
date: 2021-06-03
permalink: /posts/2021/06/Personal website using Academicpages/
tags:
  - Personal Website
categories:
  - Notes
  - Coding
---


This is a note about useful solutions to debug my personal website using academicpages
======

[source code link](https://github.com/academicpages/academicpages.github.io) 

## 1. Overall structure

1. Layout
- \_layouts

2. Navigation tabs
- \_data\navigation

3. Specific elements, such as how each single post shown up on the blog page, footer etc.
- Single post preview: \_include\archive_single 

## 2. How to minimize the top/bottom margin of the footer?
\_sass\footer.scss
change the margin_top under footer section

## 3. How to change the font size in code block?
\_sass\_base.scss
change the margin_top under footer section

## 4. How to add a grid of buttons for categories/tags of posts?
- Under layouts, create separate layouts named "category", "tag", and "post".
- Also under pages, create separte pages (md file, not html) named "category-archive", "tag-archive", "year-archive".
- Locate \_page.scss under \_sass folder

## 5. How to change color of blog post title?
- Locate \_archive.scss under \_sass folder