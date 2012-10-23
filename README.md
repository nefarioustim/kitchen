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

License
-------

<a xmlns:dct="http://purl.org/dc/terms/" href="https://github.com/nefarioustim/kitchen" rel="dct:source">Kitchen</a>

<a rel="license" href="http://creativecommons.org/licenses/by-sa/3.0/"><img alt="Creative Commons License" style="border-width:0" src="http://i.creativecommons.org/l/by-sa/3.0/88x31.png" /></a>

<span xmlns:dct="http://purl.org/dc/terms/" href="http://purl.org/dc/dcmitype/InteractiveResource" property="dct:title" rel="dct:type">Kitchen</span> by <a xmlns:cc="http://creativecommons.org/ns#" href="http://timhuegdon.com" property="cc:attributionName" rel="cc:attributionURL">Tim Huegdon</a> is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-sa/3.0/">Creative Commons Attribution-ShareAlike 3.0 Unported License</a>.

Based on a work at <a xmlns:dct="http://purl.org/dc/terms/" href="https://github.com/nefarioustim/kitchen" rel="dct:source">https://github.com/nefarioustim/kitchen</a>.