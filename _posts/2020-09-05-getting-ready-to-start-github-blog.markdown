---
layout: post
title:  "Getting ready to start GitHub Blog on Ubuntu 20.04"
date:   2020-09-05 16:02:00 +0900
categories: linux
---

Step
---
1.Install Ruby and Git
```shell
sudo apt install ruby-full git
```

2.Install jekyll and bundler
```shell
sudo gem install jekyll bundler
```

3.Create new jekyll blog
```shell
jekyll new <YOUR_BLOG_NAME>
```

Typing this command you will see the following text
```shell
Running bundle install in <Your blog path>... 


Your user account isn't allowed to install to the system RubyGems.
  You can cancel this installation and run:

      bundle install --path vendor/bundle

  to install the gems into ./vendor/bundle/, or you can enter your password
  and install the bundled gems to RubyGems using sudo.

  Password: 

```

Just enter root password. Then you will see the following output.
```shell
  Bundler: Fetching gem metadata from https://rubygems.org/..........
  Bundler: Fetching gem metadata from https://rubygems.org/.
  Bundler: Resolving dependencies...
  Bundler: Using public_suffix 4.0.6
  Bundler: Using addressable 2.7.0
  Bundler: Using bundler 2.1.4
  Bundler: Using colorator 1.1.0
  Bundler: Using concurrent-ruby 1.1.7
  Bundler: Using eventmachine 1.2.7
  Bundler: Using http_parser.rb 0.6.0
  Bundler: Using em-websocket 0.5.1
  Bundler: Using ffi 1.13.1
  Bundler: Using forwardable-extended 2.6.0
  Bundler: Using i18n 0.9.5
  Bundler: Using rb-fsevent 0.10.4
  Bundler: Using rb-inotify 0.10.1
  Bundler: Using sass-listen 4.0.0
  Bundler: Using sass 3.7.4
  Bundler: Using jekyll-sass-converter 1.5.2
  Bundler: Using listen 3.2.1
  Bundler: Using jekyll-watch 2.2.1
  Bundler: Using rexml 3.2.4
  Bundler: Using kramdown 2.3.0
  Bundler: Using liquid 4.0.3
  Bundler: Using mercenary 0.3.6
  Bundler: Using pathutil 0.16.2
  Bundler: Using rouge 3.22.0
  Bundler: Using safe_yaml 1.0.5
  Bundler: Using jekyll 3.9.0
  Bundler: Using jekyll-feed 0.15.0
  Bundler: Using jekyll-seo-tag 2.6.1
  Bundler: Using kramdown-parser-gfm 1.1.0
  Bundler: Using minima 2.5.1
  Bundler: Bundle complete! 7 Gemfile dependencies, 30 gems now installed.
  Bundler: Use `bundle info [gemname]` to see where a bundled gem is installed.Following files may not be writable, so sudo is needed:
  Bundler: /usr/local/bin
  Bundler: /var/lib/gems/2.7.0
  Bundler: /var/lib/gems/2.7.0/build_info
  Bundler: /var/lib/gems/2.7.0/cache
  Bundler: /var/lib/gems/2.7.0/doc
  Bundler: /var/lib/gems/2.7.0/extensions
  Bundler: /var/lib/gems/2.7.0/gems
  Bundler: /var/lib/gems/2.7.0/specifications
New jekyll site installed in <Your blog path>.
```


4.Serve your blog
```
cd <Your Blog path>
jekyll serve
```
Typing this command you will see the following text
```
Warning: the running version of Bundler (2.1.2) is older than the version that created the lockfile (2.1.4). We suggest you to upgrade to the version that created the lockfile by running `gem install bundler:2.1.4`.
Configuration file: <Your blog path>/_config.yml
            Source: <Your blog path>
       Destination: <Your blog path>/_site
 Incremental build: disabled. Enable with --incremental
      Generating... 
       Jekyll Feed: Generating feed for posts
                    done in 0.268 seconds.
/var/lib/gems/2.7.0/gems/pathutil-0.16.2/lib/pathutil.rb:502: warning: Using the last argument as keyword parameters is deprecated
 Auto-regeneration: enabled for '<Your blog path>'
    Server address: http://127.0.0.1:4000/
  Server running... press ctrl-c to stop.
```

Open a browser and enter the following address. Then your blog will appear.
```
http://127.0.0.1:4000/
```

Error
---
1.Prepending `bundle exec` to your command may solve this. (Gem::LoadError)

If you get an error like this
```
Warning: the running version of Bundler (2.1.2) is older than the version that created the lockfile (2.1.4). We suggest you to upgrade to the version that created the lockfile by running `gem install bundler:2.1.4`.
Traceback (most recent call last):
	10: from /usr/local/bin/jekyll:23:in `<main>'
	 9: from /usr/local/bin/jekyll:23:in `load'
	 8: from /var/lib/gems/2.7.0/gems/jekyll-3.9.0/exe/jekyll:11:in `<top (required)>'
	 7: from /var/lib/gems/2.7.0/gems/jekyll-3.9.0/lib/jekyll/plugin_manager.rb:50:in `require_from_bundler'
	 6: from /usr/lib/ruby/2.7.0/bundler.rb:149:in `setup'
	 5: from /usr/lib/ruby/2.7.0/bundler/runtime.rb:26:in `setup'
	 4: from /usr/lib/ruby/2.7.0/bundler/runtime.rb:26:in `map'
	 3: from /usr/lib/ruby/2.7.0/bundler/spec_set.rb:147:in `each'
	 2: from /usr/lib/ruby/2.7.0/bundler/spec_set.rb:147:in `each'
	 1: from /usr/lib/ruby/2.7.0/bundler/runtime.rb:31:in `block in setup'
/usr/lib/ruby/2.7.0/bundler/runtime.rb:312:in `check_for_activated_spec!': You have already activated public_suffix 4.0.6, but your Gemfile requires public_suffix 3.1.1. Prepending `bundle exec` to your command may solve this. (Gem::LoadError)
```
try this
```shell
bundle exec jekyll serve
```

```
Configuration file: <Your blog path>/_config.yml
            Source: <Your blog path>
       Destination: <Your blog path>/_site
 Incremental build: disabled. Enable with --incremental
      Generating... 
       Jekyll Feed: Generating feed for posts
                    done in 0.172 seconds.
/var/lib/gems/2.7.0/gems/pathutil-0.16.2/lib/pathutil.rb:502: warning: Using the last argument as keyword parameters is deprecated
 Auto-regeneration: enabled for '<Your blog path>'
    Server address: http://127.0.0.1:4000/
  Server running... press ctrl-c to stop.
```

But if you don't want to see these messages, try the following
```shell
sudo bundle clean --force
jekyll serve
```
