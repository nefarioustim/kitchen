Kitchen
=======

A [Jekyll](https://github.com/mojombo/jekyll) and [Compass](http://compass-style.org/) powered blog with some extra [Rakefile](http://rake.rubyforge.org/) seasoning.

Requirements
------------

You'll need to install [rbfu](https://github.com/hmans/rbfu) to manage your Ruby versions. You can find detailed [installation instructions here](https://github.com/hmans/rbfu#installing-rbfu).

To install using [Homebrew](http://mxcl.github.com/homebrew/), do this:

    brew install https://github.com/hmans/rbfu/blob/master/homebrew/rbfu.rb

Next install a newer version of Ruby using [ruby-build](https://github.com/sstephenson/ruby-build):

    ruby-build 1.9.3-p194 $HOME/.rbfu/rubies/1.9.3-p194

Installation
------------

Firstly, clone the repo and change to the subsequent directory:

    git clone git://github.com/nefarioustim/kitchen.git kitchen
    cd kitchen

Now install the dependencies:

    gem install bundler
    bundle install

And that's it. You're ready to go!
