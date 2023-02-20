---
title: "How to set up a blog site(like this one)"
tags:
- ruby
- ruby gems
- jekyll
- minimal-mistakes
categories:
- blog
toc: true
toc_sticky: true
---
Are you thinking about setting up your own personal website, but do not know where to start? Well, this blog can be a starting point for you. This site itself has been hosted using **Jekyll minimal-mistakes theme through github pages**. Jekyll is one of the most popular open-source static site generator written in Ruby programming language. A static site generator generates a full static HTML website based on raw data and a set of templates. The minimal-mistakes theme provides us with the option of multiple jekyll templates/layouts that we can use out of the box. It is popular for building personal sites, blogs, and portfolios. This blog is mainly targeted for the beginners, starting from how to set up the environment to how to deploy the theme remotely. All of this might feel overwhelming at first, but “*do not fret my child”,* by the end of this blog, you can have your own site up and running.  

> *Disclaimer: Since, my primary programming language is python, you will find the analogies of python here and there!*
> 

# Setting up the environment for the project

---

There are two different ways in which the project environment can be set up. In the first method, we are just going to add the dependencies that we need for the project. In the second method, we also add the ruby environment which allows us to choose the version of the ruby that we want to use for the project.

For both the methods, the pre-requisites must be met.

## Pre-requisites


1. [Ruby](https://www.ruby-lang.org/en/)
    
    You can follow the steps [here](https://www.ruby-lang.org/en/documentation/installation/) for installing Ruby.
    
2. [RubyGems](https://rubygems.org)
    
    RubyGems is a package manager for the Ruby programming language that provides a standard format for distributing Ruby programs and libraries, a tool designed to easily manage the installation of gems, and a server for distributing them.
    
    RubyGems should be included by default when installing the Ruby. However, if it is not present, you can follow the steps [here](https://github.com/rubygems/rubygems#installation) to install it. 
    
    Once installed, `gem` command should be available in the command line/shell.
    
    ```bash
    # install the required gem
    gem install <package_name>
    
    # show all the gems installed in the system
    gem list
    ```
    
3. [Bundler](https://bundler.io)
    
    Bundler helps to manage the dependencies in a project through a Gemfile by installing the exact gem versions required. It is recommended to run jekyll using bundler so that there are no dependency issues.
    
    *Gemfile contains the list of gems/libraries that needs to be installed for the project. Gemfile is equivalent to the `requirements.txt` if you are coming from a Python Background or equivalent to `package.json` if you are coming from a Node(JS) background.*
    
    ```bash
    gem install bundler
    ```
    

## Method 1


After the above pre-requisites have been installed, we create a directory for our new project where we will install the Jekyll.

```bash
mkdir my-jekyll-website
cd my-jekyll-website
```

### Jekyll

---

The [documentation](https://jekyllrb.com/docs/step-by-step/01-setup/) contains everything you need to know about Jekyll layouts, templates, and more. Jekyll supports Markdown and **Liquid**, **a templating language that loads dynamic content on your site.**

*Liquid allows using variables, if-else statements in a HTML page, similar to jinja template.*

We are going to use bundler to install jekyll. Inside the project directory, run the following commands:

```bash
# *Source: https://jekyllrb.com/tutorials/using-jekyll-with-bundler/*
# create an empty Gemfile
bundle init

# instruct bundler where to install the packages
# this command is optional
# if not executed, bundler will install the package to the global environment
# just like ruby gems but with dependency management
bundle config set --local path 'vendor/bundle'

# add jekyll to the Gemfile and install it 
bundle add jekyll

# create a new "Hello World" jekyll project, while adding new gems to the Gemfile
bundle exec jekyll new --force ./

# install the newly added gems
# it will do the same job as `gem install` all the packages present in Gemfile
bundle install

# list the gems installed for the project
bundle show

# get more info about sepecific installed gem
bundle (show|info) <gem_name>
```

After this, running `bundle exec jekyll serve` will start the webserver locally.

You can make the required changes to the content while following the Jekyll conventions (we will look into it later) and then **the webserver will hot reload, unless the changes made are in the `_config.yml` file**. If the changes are made to the config file, then the server must be stopped and started again.

`jekyll build` ⇒ Builds the site and outputs a static site to a directory called `_site`

`jekyll serve` ⇒ Does `jekyll build` and runs it on a local web server at  `http://localhost:4000`, rebuilding the site any time you make a change.

If you need to use other third-party gems, then you need to add that to the Gemfile and install it. You can checkout the Gemfile that has been used in this project [here](https://github.com/Urmila-m/my-blog/blob/gh-pages/Gemfile).

## Method 2


In this method, we are going to use rbenv to manage the ruby version that the project uses. rbenv is only supported in Linux and MacOS. So, this method is not applicable for Windows users. 

### rbenv

---

You can manage different versions of Ruby on per-project basis using [rbenv](https://github.com/rbenv/rbenv#readme) and [ruby-build](https://github.com/rbenv/ruby-build). *Note: Even when the ruby-build is present in the system as standalone, it must be installed as a plugin for rbenv.*

Follow the instructions in the installation page [here](https://github.com/rbenv/rbenv/tree/v1.2.0#using-package-managers).

```bash
# install rbenv
sudo apt-get install rbenv

# add rbenv to the shell
rbenv init

# install ruby-build as plugin for rbenv
git clone https://github.com/rbenv/ruby-build.git "$(rbenv root)"/plugins/ruby-build

# check if rbenv and ruby-build installed correctly or not
curl -fsSL https://github.com/rbenv/rbenv-installer/raw/main/bin/rbenv-doctor | bash

# list the available ruby versions for installation
rbenv install --list

# install the required ruby version
rbenv install <version>

# show all the installed ruby versions
rbenv versions

# specify one of the installed ruby version to use within a project
rbenv local <version>

# check which ruby version is being used for a project
rbenv local
```

After this, all the steps are same as above(method 1), except that it is highly recommended to execute the `bundle config` command as there are multiple ruby versions and it might mess up with other project dependencies.

# Deployment

---

To make the jekyll site publicly available across the internet, we need to deploy it. Deploying is simple using the [github pages](https://docs.github.com/en/pages/getting-started-with-github-pages/about-github-pages) as Github also uses Jekyll behind the scenes to build the site. 

> *If you publish your site from a source branch, **GitHub Pages will use Jekyll to build your site by default**. If you want to use a static site generator other than Jekyll, we recommend that you write a GitHub Actions to build and publish your site instead. Otherwise, disable the Jekyll build process by creating an empty file called `.nojekyll` in the root of your publishing source, then follow your static site generator's instructions to build your site locally.
- [Github Page documentation](https://docs.github.com/en/pages/getting-started-with-github-pages/about-github-pages#static-site-generators)*
> 

## Github pages

We need to push the previous code to a github repo which has a branch named `gh-pages`. Then the site will be hosted immediately on `http(s)://<username>.github.io/<repository>`. 

Since, github builds the site itself, the gems, and the `_sites` along with other system generated files, are not required in the remote repo. Make sure to add them to the `.gitignore` file. You can refer to this [gitignorefile](https://github.com/Urmila-m/my-blog/blob/gh-pages/.gitignore).

# Adding content to the site

---

To customize the look and feel of the site, we can add templates in the `_layouts` directory. To add new posts, we can add markdown file with the filename containing the date and title. To add author details, social media handles, `_config.yml` file can be updated. More information can be found on the Jekyll’s [documentation](https://jekyllrb.com/docs/step-by-step/01-setup/) site itself.

## minimal-mistakes theme

---

This [Jekyll Theme](https://github.com/mmistakes/minimal-mistakes) eliminates the need for creating our own templates and layout so that we can directly use it and just add our content.

It’s [quick-start](https://mmistakes.github.io/minimal-mistakes/docs/quick-start-guide/) page provides us with 3 different methods on how we can use this theme. **After the environment has been set up**, follow any one of the following methods:

### Gem based method

This method is best suited for the situation when you just want to view the blog locally. You just need to add the `minimal-mistakes-jekyll` gem to the project.

Follow the instructions [here](https://mmistakes.github.io/minimal-mistakes/docs/quick-start-guide/#gem-based-method), then `bundle exec jekyll serve` to get the site up and running. It is a good choice to kick-start the project, but is not recommended for deployment.

### Remote theme method

This is the recommended method for deploying to the github pages. Once, the environment has been set up, follow the steps [here](https://mmistakes.github.io/minimal-mistakes/docs/quick-start-guide/#remote-theme-method). Then,

1. Create a remote repo in the github
2. `git init` in the local project directory
3. `git remote add origin <github_repo_url>`
4. `git add .` and `git commit -m <msg>`
5. `git push origin main`

This will host the jekyll themed site remotely. If you want to run it locally, you will need to install one more gem called webrick to host the local http server.

Append `gem "webrick"` to the end of Gemfile and `bundle install`. Now, `bundle exec jekyll serve` will run the site locally.  

### Repo Clone method

When using both the methods above, the templates that the theme is using under the hood is hidden from your immediate view. This method is best suited if you wish to understand more on how it works, and the layouts that it uses. 

Fork the [minimal-mistakes](https://github.com/mmistakes/minimal-mistakes) github repo and you can also make your own customizations.

Remove the [unnecessary files](https://github.com/mmistakes/minimal-mistakes) from the repo. You can completely omit the `theme` field in the `_config.yml` file. For gems as well, you do not need to make any modifications in the Gemfile. Simply specify the bundle installation path and run `bundle install`.

You might face one issue when using this method though. If you have Ruby version 3.2.0 and Jekyll version 3.9.2, then it throws the following type of error during the `bundle exec jekyll serve`:

```jsx
Liquid Exception: undefined method untaint' for "Welcome to Jekyll!":String in /_layouts/post.html
```

It is due to the fact that Jekyll 3.9.2 by default includes Liquid 4.0.3 which calls the Ruby function `utaint` that is not supported in Ruby 3.2.0 anymore. More information can be found [here](https://github.com/jekyll/jekyll/issues/9233).

So what is the fix? Either use Liquid 4.0.4 version(specify in the gem file) or downgrade ruby to 3.1.3 version. 

This site has been hosted using the remote theme method. But for the local development, repo clone method is used. So, you will find a mix of configurations and set up of both the methods in the `_config.yml` and `Gemfile`. You can find the github repo used to host this site [here](https://github.com/Urmila-m/my-blog/tree/gh-pages).

# What’s next?

---

Customize the style, content as per your liking. You can also set up navigation bars and search bars. You can add images and other assets. Explore yourself, sky is the limit!

**Congratulations! You made it till the end! Hope it helped you 🙂**