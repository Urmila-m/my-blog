source "https://rubygems.org"

### FOR HOSTING THE SITE USING GITHUB PAGES
# `github-pages` is a bundle of other gems that have been listed below on group :local_dev 
gem "github-pages", group: :jekyll_plugins
# It means include the gem to the group `jekyll_plugins`
gem "jekyll-include-cache", group: :jekyll_plugins

# If you have any plugins, put them here!
group :jekyll_plugins do
end

### FOR LOCALLY RUNNING THE WEB SERVER AND TESTING
group :local_dev do
  gem "jekyll-paginate"
  gem "jekyll-sitemap"
  gem "jekyll-gist"
  gem "jekyll-feed"
  gem "jemoji"
  gem "jekyll-include-cache"
  gem "jekyll-algolia"
  # the `gem liquid 4.0.3` is included in the `gem jekyll 3.9.2`
  # There is a Ruby function `utaint` that liquid 4.0.3 uses, but Ruby v3.2.0 have removed the support for that.
  # Due to this, when trying to do `bundle exec jekyll serve`, it throws 
  # `untaint' for "Welcome to Jekyll!":String in /_layouts/post.html jekyll 3.9.2 | Error:  undefined method` type of error
  # More info: https://github.com/jekyll/jekyll/issues/9233
  # The resolution is to either downgrade Ruby to its stable version 3.1.3 or upgrade the liquid gem to version 4.0.4
  gem 'liquid', '~> 4.0', '>= 4.0.4'
  # required for markdown
  gem "kramdown-parser-gfm"
  # used to start the webserver locally
  gem 'webrick'
end

group :windows_env do
  gem 'tzinfo-data', platforms: [:mingw, :mswin, :x64_mingw, :jruby]
  gem 'wdm', '>= 0.1.0' if Gem.win_platform?
end

# HOW TO RUN IN LOCAL SET UP?
# When running the server locally, we do not need the `github-pages` gem, so we will not install them.
# `bundle install --with local_dev,windows_env` or `bundle install --without jekyll_plugins`
# Then, `bundle exec jekyll serve` to start the server
# If there are any changes to the posts/articles, `bundle exec jekyll build` and then serve
