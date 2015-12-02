#Ruby on Rails

##Table of Contents
1. [Introduction](#introduction)
2. [Setup](#setup)
3. [File Structure](#file-structure)
4. [RSpec](#rspec)

<a name="introduction">
##Introduction
</a>

###What is it?

Ruby on Rails is a framework built on the Ruby language, which was created by 松本行弘 (Yukihiro “Matz” Matsumoto) of Japan and released in 1995. Ruby on Rails was created and released under the MIT License in 2004 by David Heinemeier Hansson.

###Why use it?

Ruby on Rails allows for the rapid development of applications by using a concept known as *convention over configuration*. A new Ruby on Rails application is created by running the application generator `rails new project_name`, which creates a standard directory structure. Because every Ruby on Rails project starts the same way, the developer is free to focus on coding, instead of project configuration.

###Ruby Gems

The core features of Rails are split up into many different libraries, called *Ruby gems*. Usually, if you can think of it, there’s a gem out there that will help you do it.

###Resources

Here are some outstanding rails resources:

+ [Ruby On Rails Tutorial (3rd Edition) by Michael Hartl](https://www.railstutorial.org/book/)
+ [Rails 4 In Action](http://www.allitebooks.com/rails-4-in-action/)

<a name="setup">
##Setup
</a>

To get started, you should have these three things installed (check by running the associated command in terminal):

- Ruby: `ruby -v`
- RubyGems: `gem -v`
- Rails: `rails -v`

###Installation

This guide will cover Installation on **Mac OS X** and **Linux (Ubuntu 14.04+)**


####Mac OS X

Mac OS X comes with an outdated version of Ruby (2.0.0). Let's do something about that.

#####Homebrew - "The missing package manager for OS X"

Open a terminal and run this install command:
```
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

Now that we have Homebrew, let's grab another tool called `wget`:
```
brew install wget
```

####Mac OS X / Ubuntu

#####ruby-install

Ruby-install is open source on GitHub and can be found [here](http://github.com/postmodern/ruby-install). We'll need this to install a current version of Ruby.

After `wget` has installed, run:
```
wget -O ruby-install-0.5.0.tar.gz https://github.com/postmodern/ruby-install/archive/v0.5.0.tar.gz
tar -xzvf ruby-install-0.5.0.tar.gz
cd ruby-install-0.5.0/
sudo make install
```

Now, head up one directory and remove the ruby-install directory:
```
cd ..
rm -r ruby-install-*
```

All you need to do now is run this simple command to get ruby:
```
ruby-install ruby 2.2.2
```

#####Chruby

Chruby is a simple shell tool used to manage your Ruby installations. The GitHub Repo can be found [here](https://github.com/postmodern/chruby). Let's download it by running:
```
wget -O chruby-0.3.9.tar.gz https://github.com/postmodern/chruby/archive/v0.3.9.tar.gz
tar -xzvf chruby-0.3.9.tar.gz
cd chruby-0.3.9/
sudo make install
cd ..
rm -r chruby-*
```

Next, we'll add chruby to our `~/.bash_profile` (Mac OS X) or `~/.bashrc` (Ubuntu) file so that it's features are loaded when you start a new terminal session:

add these two lines to your respective bash file:
```
source /usr/local/share/chruby/chruby.sh
source /usr/local/share/chruby/auto.sh
```

Finally, create a `~/.ruby-version` file now and specify that 2.2.2 is your default version of Ruby:
```
nano ~/.ruby-version
```

Then add `ruby-2.2.2` to the new document, save, and close. To have this configuration take effect, you need to open a new terminal window.

###Rails

Sweet! We have Ruby. Now, we can install Rails with RubyGems:
```
gem install rails -v 4.2.1
```

####Initialize Project

To build a new application, run this command:
```
rails new project_name
```

*Take care not to use reserved words for application naming (i.e. 'rails new rails' or 'rails new test').  You'll wind up with an error response that will make you sad*

Once you've done this, change into your projects directory and start a rails server:
```
cd project_name
rails s
```

Head on over to `http://localhost:3000` and you should see a "Welcome aboard" message.

BOOM! You did it.

<a name="file-structure">
##File Structure
</a>

Remember in the Introduction when we talked about *convention over configuration*? Since there is a lot of magic that happens for you when initializing a project, there are some things you'll need to know.  We'll start with the file structure:
```
project_name/
    /app
        /assets
        /controllers
        /helpers
        /mailers
        /models
        /views
            /layouts
    /bin
    /config
    /db
    /lib
    /log
    /public
    /spec
    /test
    /tmp
    /vendor
README
Rakefile
```

|  Folder           | Description  |
| :---------------: | :----------- |
| app               | organizes your application components
| app/assets        | contains your stylesheets, javascript, and images
| app/controllers   | contains the controller classes that handle web requests from the user
| app/helpers       | contains helper classes that assist the model, view, and controller classes, keeping the code in the models, views, and controllers short, sweet, and focused
| app/mailers       | contains classes for mailers, which are associated with email functionality of your project
| app/models        | holds the classes that model and wrap the data stored in your application's database
| app/views         | contains the display templates that are translated into html and sent to the browser
| app/views/layouts | holds the template files for layouts to be used with views
| bin               | contains components that aid in development
| config            | contains the small amount of configuration code that your application will need, including your database configuration (in database.yml), your Rails environment structure (environment.rb), and routing of incoming web requests (routes.rb)
| db                | contains scripts that allow model objects access the relational database you choose
| lib               | contains library files
| log               | contains error logs
| public            | previously used for assets, now contains other pages necessary for a functional website (like, 404, 500, and favicon)
| spec              | test specs are written and stored in this folder (rspec)
| test              | the tests you write and those Rails creates for you all go here
| tmp               | temporary files are held here for immediate processing
| vendor            | contains libraries provided by third-party vendors

<a name="rspec">
##RSpec
</a>

In your Gemfile, add the following:

```
group :development, :test do
  gem 'rspec-rails', '~> 2.0'
end

group :test do
    gem 'capybara', '~> 2.1.0'
end
```

In a terminal window, run `bundle`.  After Bundler is done installing the dependencies, run:

```
bin/rails g rspec:install
```

This will generate the spec directory in your project.  Next, we'll need to open up `spec/rails_helper.rb` and add the following to the list of require's at the top of the document:

```
require 'capybara/rspec'
```

Finally, let's binstub it so we don't have to type `bundle exec` every time we want to run rspec for our specific project. In a terminal window, run:

```
bundle binstubs rspec-core
```

If you are only going to be using RSpec for testing, you can go ahead and remove the test directory in your project:

```
rm -rf test/
```
