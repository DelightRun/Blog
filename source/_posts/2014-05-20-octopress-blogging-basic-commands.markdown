---
layout: post
title: "Octopress Blogging Basic Commands"
date: 2014-05-20 00:10:25 +0800
comments: true
categories:
---

#Create New Post:
    rake new_post["title"]    

#Create new pages:
    # Create /source/directory/index.markdown
    rake new_page[directory]
    
    # Create /source/directory/page.html
    rake new_page[directory/page.html]

#Use draft:
Edit your post/pages in a text editor,
Change the attributions between `---`,
Add the following text:
    published: false

#Change categories:
    # One category
    categories: your_category
    
    # Multiple categories method 1
    categories: [categories_1, categories_2, categories_3, etc.]

    # Multiple categories method 2
    categories:
    - categories_1
    - categories_2
    - categories_3
    - etc.

#Generate & Preview:
    rake generate   # Generate posts and pages into the public directory
    rake watch      # Watches source/ and sass/ for changes and regenerates
    rake preview    # Watches, and mounts a webserver at http://localhost:4000
