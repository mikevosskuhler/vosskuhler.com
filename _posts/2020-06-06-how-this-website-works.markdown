---
layout: blog
title:  "How to build a jekyll website"
date:   2020-06-06 14:00:00 +0200
categories: jekyll update
---
# How to build a jekyll website
This website was build using the jekyll static site generator, the bootstrap framework, and the fontawesome icon library. In this post I will discuss the basic of these tools and how to quickly get started with building your own static websites. 

## Jekyll
Jekyll was build by the creators of github and allows its users to quickly build static websites without having to copy past every change to your default layout to each page. Furthermore Jekyll is blog aware, which means that you can easily add a blog page listing all of you blogs, with links to each blog post. 

### Getting started
Follow these steps to get Jekyll setup on you local machine:
- [Install Jekyll](https://jekyllrb.com/docs/installation/){:target="_blank"}
- [Create a Project and Run the Server](https://jekyllrb.com/docs/){:target="_blank"}

Now you will have a server running Jekyll, you can visit it by typing localhost:4000 into your browser. Every time you update one of the layouts or pages the website will automatically update. All you have to do to see your results is reload the page. 

Furthermore, if you check out the content of your newly created project it should look similar to this:
```
├── 404.html
├── Gemfile
├── Gemfile.lock
├── _config.yml
├── _layouts
│   ├── blog.html
│   └── default.html
├── _posts
│   ├── 2020-06-04-welcome-to-jekyll.markdown
│   └── 2020-06-06-how-this-website-works.markdown
├── _site
│   ├── 404.html
│   ├── about.html
│   ├── assets
│   │   ├── main.css
│   │   ├── main.css.map
│   │   └── minima-social-icons.svg
│   ├── bg.jpeg
│   ├── blogs.html
│   ├── feed.xml
│   ├── index.html
│   ├── jekyll
│   │   └── update
│   │       └── 2020
│   │           └── 06
│   │               ├── 04
│   │               │   └── welcome-to-jekyll.html
│   │               └── 06
│   │                   └── how-this-website-works.html
│   └── test.css
├── about.html
├── bg.jpeg
├── blogs.html
├── index.html
└── test.css
```

You can ingnore the gem files and `config.yaml` for now and focuss on the fact that you have several `.html` and `.markdown` files and three directories: `_site`, `_layout`, and `_posts`. 

The `_site` directory contains your static website and will be automatically updated when you are running the `jekyll serve` command. These are the files that your browser will receive when it requests the website. 

The `_layout` and `_posts` directory contain the page layouts and posts, respectively. The layout files use a syntax called [Liquid](https://shopify.github.io/liquid/){:target="_blank"} which is a templating language. The post files most often use a typesetting language called [Markdown](https://en.wikipedia.org/wiki/Markdown){:target="_blank"}, this is a simplified syntax for using HTML. The specific flavour being used by Jekyll is called [Kramdown](https://jekyllrb.com/docs/configuration/markdown/#kramdown){:target="_blank"}. 

The `.html` and `.markdown` files correspond to the main pages on the website. These files will be completed by using one of the layouts in the `_layouts` directory. Both HTML as Markdown are supported, but you will have to make sure that if you use Markdown that the Markdown text lands in a text friendly place in your layout files because you should have to define tags such as `<body></body>` in the Markdown, which would be acceptable in a HTML file. If you have a look at one of these files you will see a head similiar to this:
```
---
title: Home 
layout: default
---
```
This is the front matter/meta data of the page, it doesn't necessarily add anything to the context of the page. But it tells Liquid how to interpret the page.  

### Working With Layouts
The advantage of layouts is not having to make a single change in every page file every time you want to change something like a navigation bar or a background. Which is a tedious and error prone job. Instead you can place all of the common elements into a single layout file and then drop in all of the page specific content using Liquid syntax. Furthermore, Liquid supports refering to different attributes of you page which can be defined in the front matter of each specific page. 

In the most basic format a layout page would look like this:
```
<!doctype html>
<html lang="en">

<head>
  <!-- Required meta tags -->
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">

  <title>Mike Vosskuhler | {% raw %}{{page.title}}{% endraw %}</title>
</head>
  <body>

{% raw %}{{ content }}{% endraw %}

  </body>

</html>
```

Here you can see the front matter/metadata being queried with `{% raw %}{{page.title}}{% endraw %}`, which refers to the title defined in the front matter. Furthermore, the text below the front matter block in the page file will be dropped into the `{% raw %}{{ content }}{% endraw %}` placeholders place. 

**There are much more options to use with Liquid, you can even loop over all the pages or build if else statements, however, this is a good basic example of what it can do for you.**

### Working With Pages
To build a new page all you have to do is create a new file in the main root directory of you project ending in `.html` or `.markdown`. You will have to add the front matter to this file, here is an minimal example of what that should look like:
```
---
title: Home 
layout: default
---
```
The title object can be retrieved using Liquid syntax in the layout template, while the layout determines which layout will be used from the `_layouts` directory. 

Anything you put below this section will be mapped to the `{% raw %}{{ content }}{% endraw %}` statement in the layout template. 

### Working With Posts
Posts are treated a bit differently, you can create them by adding a `.html` or `.markdown` file to the `_posts` directory. This file should have front matter as well, but it takes different arguments:
```
---
layout: blog
title:  "How to build a jekyll website"
date:   2020-06-06 14:00:00 +0200
categories: jekyll update
---
```

Just like with the regular pages everything that comes after the front matter will be dropped into the `{% raw %}{{ content }}{% endraw %}` place in the layout

Now you would probably like to have a overview page where visitors can view all of you blogs in one central place. To do so you can use a little bit of Liquid syntax to get a list of posts on one of you main pages. This what the syntax looks like:
```
<ul>
  {% for post in site.posts %}
      <li><a href="{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>
```
Later on we will discuss how to get a nicer looking format using bootstrap. 

## Bootstrap
Bootstrap is a framework that allows you to build a nice looking responsive website is very little time. 
Here is what you need to get started:
### The Barebones Template 
```
<!doctype html>
<html lang="en">
  <head>
    <!-- Required meta tags -->
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">

    <!-- Bootstrap CSS -->
    <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.5.0/css/bootstrap.min.css" integrity="sha384-9aIt2nRpC12Uk9gS9baDl411NQApFmC26EwAOH8WgZl5MYYxFfc+NcPb1dKGj7Sk" crossorigin="anonymous">

    <title>Hello, world!</title>
  </head>
  <body>
    <h1>Hello, world!</h1>

    <!-- Optional JavaScript -->
    <!-- jQuery first, then Popper.js, then Bootstrap JS -->
    <script src="https://code.jquery.com/jquery-3.5.1.slim.min.js" integrity="sha384-DfXdz2htPH0lsSSs5nCTpuj/zy4C+OGpamoFVy38MVBnE+IbbVYUew+OrCXaRkfj" crossorigin="anonymous"></script>
    <script src="https://cdn.jsdelivr.net/npm/popper.js@1.16.0/dist/umd/popper.min.js" integrity="sha384-Q6E9RHvbIyZFJoft+2mJbHaEWldlvI9IOYy5n3zV9zzTtmI3UksdQRVvoxMfooAo" crossorigin="anonymous"></script>
    <script src="https://stackpath.bootstrapcdn.com/bootstrap/4.5.0/js/bootstrap.min.js" integrity="sha384-OgVRvuATP1z7JjHLkuOU7Xw704+h835Lr+6QL9UvYjZE3Ipu6Tp75j7Bh/kR0JKI" crossorigin="anonymous"></script>
  </body>
</html>
```
This template contains all of the scripts and ccs links needed to use bootstrap. You can replace the `<h1>Hello, world!</h1>` syntax with any content you want to display on you page. 

### The Components
You can very easily add in bootstrap components to you html documents. For example, if you want to grab some attention you can use a jumbotron component:
```
<div class="jumbotron">
<h1>Hello from inside the Jumbotron</h1>
</div>
```
This is a basic example but you could do much more with these components, Here is a link to a list of all the components available in bootstrap: [Documentation](https://getbootstrap.com/docs/4.5/components/){:target="_blank"}. 

## FontAwesome
Font Awesome is a much smaller tool, but it can be very usefull when you are looking to add some nice icons to you HTML. You can use it by creating a free account on the [Font Awesome Website](https://fontawesome.com){:target="_blank"}. This will give you access to the [Kit overview](https://fontawesome.com){:target="_blank"}. Add the script for you kit to the head of you HTML document and you are ready to go. Now you can add icons to any text field on you page simply by including the icon syntax to you page, for example:
```
<i class="fab fa-blogger-b"></i>
```
You can find all kinds of icons using the [Icon overview](https://fontawesome.com/icons?d=gallery&q=blog&m=free){:target="_blank"} on the Font Awesome website. 

# This Website
I used the same methods described in this blog post to create this website. You can find the source code for this website on my github. 

<button type="button" class="btn btn-outline-secondary" onclick="window.open('https://github.com/mikevosskuhler/vosskuhler.com')"><i class="fab fa-github"></i> Source Code</button>
