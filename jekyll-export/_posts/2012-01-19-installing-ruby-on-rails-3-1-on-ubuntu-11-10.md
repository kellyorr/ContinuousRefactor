---
title: Installing Ruby 1.9.2 and Rails 3.1.3 on Ubuntu 11.10
author: kellyorr
layout: post
permalink: /installing-ruby-on-rails-3-1-on-ubuntu-11-10/
categories:
  - Software Development
---
Install the <a title="Git" href="http://git-scm.com/" target="_blank">Git</a> source control manager:

<pre class="brush: plain; title: ; notranslate" title="">sudo apt-get install git</pre>

Install <a title="Curl" href="http://curl.haxx.se/" target="_blank">Curl</a>:

<pre class="brush: plain; title: ; notranslate" title="">sudo apt-get install curl</pre>

<pre class="brush: plain; title: ; notranslate" title="">sudo apt-get install libcurl4-openssl-dev</pre>

Install the <a title="RVM" href="http://beginrescueend.com/" target="_blank">Ruby Version Manager</a> (RVM)

<pre class="brush: plain; title: ; notranslate" title="">sudo apt-get install ruby-rvm</pre>

To execute the RVM commands go into super user mode:

<pre class="brush: plain; title: ; notranslate" title="">sudo bash</pre>

Then, execute these RVM commands to get the head of the RVM code branch, reload it and install Ruby versions <a title="Ruby 1.8.7" href="http://www.ruby-lang.org/en/news/2008/05/31/ruby-1-8-7-has-been-released/" target="_blank">1.8.7</a> and <a title="Ruby 1.9.2" href="http://www.ruby-lang.org/en/news/2010/08/18/ruby-1-9.2-released/" target="_blank">1.9.2</a>.

<pre class="brush: plain; title: ; notranslate" title="">rvm get head
rvm reload
rvm install 1.9.2
</pre>

Get <a title="RubyGems" href="http://rubygems.org/" target="_blank">RubyGems</a> from <a title="RubyForge" href="http://www.rubyforge.org" target="_blank">RubyForge</a>. Search for &#8220;RubyGems&#8221;. Download, extract, change to the location of the uncompressed files, then run setup.rb from the console.

<pre class="brush: plain; title: ; notranslate" title="">ruby setup.rb</pre>

Show which gem is being used.

<pre class="brush: plain; title: ; notranslate" title="">which gem</pre>

Create a Gemset called Rails313.

<pre class="brush: plain; title: ; notranslate" title="">rvm gemset create 'rails313'</pre>

Set the default Ruby version to be 1.9.2 and the default <a title="Gemset" href="https://rvm.beginrescueend.com/gemsets/basics/" target="_blank">gemset</a> to be &#8216;rails313&#8242;:

<pre class="brush: plain; title: ; notranslate" title="">rvm --default use 1.9.2@rails313</pre>

Install rails

<pre class="brush: plain; title: ; notranslate" title="">apt-get install rails</pre>

Add the line below to the bottom of the .bashrc file in your profile.  I could not get this to work in the .bash_profile file.  It had to be in the .bashrc file.

<pre class="brush: plain; title: ; notranslate" title="">[[ -s "$HOME/.rvm/scripts/rvm" ]] && . "$HOME/.rvm/scripts/rvm"</pre>

<a href="http://stackoverflow.com/questions/3276950/rvm-doesnt-switch-rubies" target="_blank">This question</a> at StackOverflow was very helpful in troubleshooting issues related to this line. Also <a href="http://stackoverflow.com/questions/8398479/using-rvm-but-cant-set-current-ruby-version-ubuntu-11-10" target="_blank">this question</a> shows a lot of helpful information related to RVM.

Confirm that RVM is installed correctly by typing:

<pre class="brush: plain; title: ; notranslate" title="">type rvm | head -n1</pre>

The reply should be:

<pre class="brush: plain; title: ; notranslate" title="">rvm is a function</pre>

Determine additional dependencies

<pre class="brush: plain; title: ; notranslate" title="">rvm requirements</pre>

This provided the following apt-get command to load the additional dependencies:

<pre class="brush: plain; title: ; notranslate" title="">apt-get install build-essential openssl libreadline6 libreadline6-dev curl git-core zlib1g zlib1g-dev libssl-dev libyaml-dev libsqlite3-0 libsqlite3-dev sqlite3 libxml2-dev libxslt-dev autoconf libc6-dev ncurses-dev automake libtool bison subversion nodejs</pre>

For some reason at this point I got the error:

<pre class="brush: plain; title: ; notranslate" title="">ERROR: Missing RVM environment file: '/user/share/ruby-rvm/environments/ruby-1.9.2-p290</pre>

ultimately, the resolution was to re-install RVM

<pre class="brush: plain; title: ; notranslate" title="">apt-get install ruby-rvm
rvm reload
gem env
</pre>

Now the gem env shows the environment information instead of an error.

Install Rails

<pre class="brush: plain; title: ; notranslate" title="">gem install rails</pre>

Check the version of Rails that is installed

<pre class="brush: plain; title: ; notranslate" title="">rails -v</pre>

Next, I dealt with an error from the tilt-1.3.3.gemspec

<pre class="brush: plain; title: ; notranslate" title="">Invalid gemspec in [/var/lib/gems/1.8/specifications/tilt-1.3.3.gemspec]: invalid date format in specification: "2011-08-25 00:00:00.000000000Z"</pre>

I referred to the RubyGems website to reinstall RubyGems.

<pre class="brush: plain; title: ; notranslate" title="">gem update --system
gem install rubygems-update
update_rubygems
</pre>

Now when I check rails -v I get Rails 3.1.3 with no error messages.

Create a test application to confirm the installations worked.

<pre class="brush: plain; title: ; notranslate" title="">rails new TestApp</pre>

Start the application with the WEBrick web server.