---
layout: post
title: "How to create your website with Github Pages and Jekyll"

tags: jekyll blog firstpost
categories: jekyll github ghpages 
date: "2018-03-08"
---

I always wanted to create a blog of my own. I had read and heard from multiple sources that writing about what you work on is good for everyone. It helps you build your online presence along with giving you the platform to show case your work. Plus, it can be a great opportunity for other people to learn from your experience.


Recently, I had the chance to visit MLH's Local Hack Day, where I first came to know about [Github Pages](https://pages.github.com/). Github Pages allows you to host one static site for each of your Github Projects. In addition to projects, Github Pages can also be created for a Github user account. I think this would be a really simple and fast approach to develop, deploy and maintain my blog. Plus, it's completely free.

Github Pages can load static webpages very easily, but to get more functionality out of it, we have to make use of [Jekyll](https://jekyllrb.com/). Jekyll, according to their own website, lets you transform your plain text into static websites and blogs. I decided to use Jekyll as it seemed a good learning experience and it reduced a lot of manual work that I might have needed to do for my blog.

So let's start.

***
# Step 1: Getting Started
***
#### Installing Jekyll

Jekyll is based on Ruby and RubyGems, so before getting started, make sure that your machine has both of these set up properly. You can visit [here](https://www.ruby-lang.org/en/documentation/installation/) for a reference to install Ruby and [here](https://rubygems.org/pages/download) for RubyGems. You also need to install [Bundler](https://bundler.io/) to take care of dependencies of you Jekyll website.


Here are some other dependencies of Jekyll that you need to take care of before starting:

* python
* nodeJS
* make

I had to go through a lot of issues while installation as I didn't have these dependencies installed.

Once you have setup Ruby and RubyGems, next you can install Jekyll and Bundler using the command given below.

```
gem install jekyll bundler
```

If you have all the dependencies installed, everything must go smoothly and you are set to generate a Jekyll website.

***

### Setting Up a Local Website

Once the installation is done, navigate to the directory where you want to create your website and run the commands below in your terminal.

```
jekyll new my-personal-blog
cd my-personal-blog
```

These commands will generate a Jekyll template website for you. Jekyll websites can be assigned pre-defined themes. When you generate a template, a website with theme Minima is generated for you.

You can run the template website using the command below in your terminal.

```
bundle exec jekyll serve
```

This will start a webserver for your website on the localhost at port 4000. You can see the output by entering the below URL in your browser.

```
127.0.0.1:4000/
```

![jekyll-with-minima](assets/jekyll_home.PNG){:class="img-responsive"}

***
### Understanding the structure of the website

Once you have followed the above steps, the directory structure for your website you be something like this:


![jekyll-file-structure](assets/file_structure.PNG){:class="img-responsive"}

Here are the general overviews for each of the substructure:

| File / Directory | Overview |
| ---------------- | -------- |
| _config.yml | Stores all the configurations related to the website |
| _posts/ | Contains all the post files which have to follow the nomenclature YYYY-MM-DD-TITLE.MARKUP for each file|
| 404.html | Specifies the *404 NOT FOUND* error page for the website |
| index.md , about.md | Contain the [YAML Front Matter](https://jekyllrb.com/docs/frontmatter/) and the contents of the respective page |
| Gemfile, Gemfile.lock | RubyGem files for dependency management |



***
# Step 2: Customization 
***

### Jekyll Themes

Jekyll supports a lot of themes. Themes are also installed in the form of RubyGems. A quick Google search will provide you with a lot of free as well as paid options for Jekyll Themes. You can install any gem-based theme by using the following command.
```
gem install <theme-gem-name>
```

That being said, only a few Jekyll themes are supported by Github Pages. The names of the themes and their Github repos are available [here](https://pages.github.com/themes). Please check them out. A lot of them are really great. In order to change the theme for your project, you have to edit the _config.yml file and change the theme tag as:


```YAML
theme: slate # Changing the theme to Slate
```


If you like these themes, your life would be easier as compared to mine. You can skip the next section where I explain how to set up a non-standard theme for your website on Github Pages.

***

### Setting Up Non-Standard Theme

I wanted to use a very clean theme for my website. I got my answer with [Whiteglass](https://github.com/yous/whiteglass). It isn't a standard Github Page theme, so I had to perform some tweaks to ensure that your website works fine when hosted on Github. To understand why non-standard themes cause issue with Github Pages, you need to understand how Jekyll themes work. Jekyll themes are gem based, i.e., whenever you want to use a theme, you have to install it using RubyGem. When you do so, a repository containing the theme files is created on your machines. These files, if not explicitly placed, aren't generally inside your project folder. So, whenever you use a theme in _config.yml, it searches for the theme files in the common gem directory. This will not work with Github as your theme gem fils are not present in your code. To make sure that your website works fine on Github when you host it, you have to make this files accessible to your Github Repo. There are two ways to do this:

#### 1. Copy all the files from the theme gem into your website directory

Once you do this, you have to remove the theme element from your _config.yml and you are good to go. To find where the theme gem files are stored, open terminal in your website directory and type the command below.

```
bundle show <theme-gem-name>
```

Now just copy the files from the directory to your website directory and you are good to go.

#### 2. Using jekyll-remote-theme

A more 'sophisticated' way to do this is to use a plugin called [jekyll-remote-theme](https://github.com/benbalter/jekyll-remote-theme). It is a very handy plugin that lets you use any theme that has been hosted on Github directly into your website. All you have to do is introduce the ```remote-theme``` tag, remove the ```theme``` tag and add a plugin ```jekyll-remote-theme``` in your _config.yml.

```
remote_theme: yous/whiteglass
plugins:
  - jekyll-remote-theme
```

With this few lines of code, you can conveniently use any Github hosted Jekyll theme in your project, without going throught the hassle of copying the files into your own website directory. It is important to know however, that you might have to make some more changes if the theme you decide to use demands it. For Whiteglass, these additional changes can be found in its [README.md](https://github.com/yous/whiteglass/blob/master/README.md).

***
### Personalizing

I would not go into a lot of personalization details here as it is quite a long topic. But you can get started by making changes to _config.yml file. If you want to change the appearance of the theme you are using, you can go to the theme-gem files, see there code and structure there, and create a similar file structure in your project directory. This will overwrite the theme files and thus, you can get your custom look. More on this can be found [here](https://jekyllrb.com/docs/themes/#overriding-theme-defaults).


***
# Step 3: Hosting using Github Pages
***

* Create an empty repository on Github with the following name:

```
<YOUR-USERNAME>.github.io
```

* Go to the Gemfile, comment out ```gem "jekyll", "~> 3.7.3"``` and add ```gem "github-pages", group: :jekyll_plugins```. Next, open up a terminal in the root directory of your website and run the command below.

```BASH
bundle install
```

*  Use the following commands in your terminal to initialize a git repo inside your Jekyll website directory and push the code to the Github repo.

```
git init
git remote add origin https://github.com/<YOUR-USERNAME>/<YOUR-USERNAME>.github.io.git
git add .
git commit -m "First Commit"
git push -u origin master
```

* Check if the website is up by visiting ``` https://<YOUR-USERNAME>.github.io ``` in your browser


*** 
# Step 4: Adding Posts and Pages
***

### Creating a Post or a Page

A Post or a page can be in Markdown or HTML by default. For each post and pages, properties like title, layout, categories, tags, date, published status, etc are defined in the YAML front matter. Layouts are defined within _layouts of the theme. This can be overwritten in the local directory for defining custom layouts. Layouts are used to specify the format of a post or a page.

You can add a post by simply creating a new file in the ```_posts/``` folder with the filename as ```YYYY-MM-DD-POST_TITLE.MARKUP```. Posts are automatically sorted based on the date provided in the Front Matter. The date specified in the filename of the post is used for generating permalinks to the post. Pages are added in the root of the website directly. You have to take care of navigation between pages yourself using layouts. 

***
### Publishing Posts and Pages

To publish newly added posts and pages, all you need to do is push the updated code to the Github repo. After the push, Github pages will automatically build the Jekyll website and your posts will be loaded. Advance CMS features like Drafting and Future Publishing are also available with Jekyll.

***

This is how I created this blog and so can you. For now, I guess this blog is good enough, however, I intend to customize this more and add more content in the future.