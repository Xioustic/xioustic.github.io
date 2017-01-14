---
layout: post
title: How I Got Jekyll + BlackDoc Theme Working in Windows
comments: true
tags:
 - jekyll
 - windows
 - guide
---

What better blog post to start out with than notes on how I got Jekyll and BlackDoc working on Windows 10? If anything, this will be useful for my reference next time I wipe my workstation and need to start over.

Note that typically I would use a docker container and/or vagrant box to accomplish all this so I would never have to really reproduce it again in the future, but I really wanted to get it natively working on Windows.

## What is BlackDoc?
BlackDoc is a Jekyll theme based on the parent theme Poole. I rather like it for its simplicity and color scheme. I'm sure I'll be making minor edits to it as I update this site, but I liked it as a starting point.

## Why a Guide?
Modern installation on Windows is not terribly friendly and fraught with command line errors that lead to StackOverflow several times. This may be fixed in the future, but I imagine it's a result of the current state / mismatch of Ruby versions, RubyDevKit versions, and Jekyll versions in combination with BlackDoc/Poole's target environment. This coupled with Windows is a bit of a recipe for disaster.

## Installing Ruby
Get [Ruby for Windows](http://rubyinstaller.org/downloads/). Your target download is the 2.0.0 variant. You want the architecture to be the same as your local Windows installation, so likely x64. Today, that download is `Ruby 2.0.0-p647 (x64)`.

During the install, you want to check the "Add Ruby executables to your PATH" checkbox right before clicking the Install button.

## Installing RubyDevKit
Once again, go to the [Ruby for Windows](http://rubyinstaller.org/downloads/) page. Get the DevKit that matches your current architecture. Today, that download is `DevKit-mingw64-64-4.7.2-20130224-1432-sfx.exe`.

Run that exe, which is a self-extracting 7z archive. Point it at "C:\RubyDevKit" and hit Install/Extract.

Once done, open a command line and perform the following commands:
{% highlight text %}
cd C:\RubyDevKit
ruby dk.rb init
ruby dk.rb install
{% endhighlight %}

## Getting Jekyll
Open a new command line and perform the following command:

{% highlight bat %}
gem install jekyll
{% endhighlight %}

If everything went well, you should be able to issue the command 'jeykll -v' to verify installation was fine (only differing in version number, depending on the date you're following this guide):
{% highlight text %}
> jekyll -v
jekyll 3.0.2
{% endhighlight %}

## Installing Git
Make sure [Git for Windows](https://git-scm.com/download/win) is installed. Make sure the "Use Git from the Windows Command Prompt" option is checked for the "Adjusting your PATH environment" section of the install. Other options can be left at their default.

You can check everything went fine by opening a command line and issuing the following
{% highlight text %}
> git --version
git version 2.7.0.windows.1
{% endhighlight %}

## Getting BlackDoc
Open a command line and cd to the location you would like to start your Jekyll project. Then issue the following command:

{% highlight bat %}
git clone https://github.com/karloespiritu/BlackDoc.git
{% endhighlight %}

Now rename the BlackDoc directory to <yourreponame>.github.io and cd into it:
{% highlight bat %}
rename BlackDoc xioustic.github.io
cd xioustic.github.io
{% endhighlight %}

## Things Go Wrong Part I
At this point, if everything was easy in the world of Jekyll in Windows, you should be able to begin serving and editing your Jekyll site immediately. Let's try <code>jekyll serve</code>:
{% highlight text %}
C:\Users\test\Desktop\xioustic.github.io>jekyll serve
Configuration file: C:/Users/test/Desktop/xioustic.github.io/_config.yml
       Deprecation: You appear to have pagination turned on, but you haven't included the `jekyll-paginate` gem. Ensure you have `gems: [jekyll-paginate]` in your configuration file.
            Source: C:/Users/test/Desktop/xioustic.github.io
       Destination: C:/Users/test/Desktop/xioustic.github.io/_site
 Incremental build: disabled. Enable with --incremental
      Generating...
Since v3.0, permalinks for pages in subfolders must be relative to the site source directory, not the parent directory. Check http://jekyllrb.com/docs/upgrading/ for more info.
{% endhighlight %}

## Installing Pagination
First, edit the _config.yml file with your preferred text editor and add the following at the bottom:
{% highlight yaml %}
gems: [jekyll-paginate]
{% endhighlight %}

And then install the jekyll-paginate gem using the command line:
{% highlight bat %}
gem install jekyll-paginate
{% endhighlight %}

## Things Go Wrong Part II
Let's try <code>jekyll serve</code> again:
{% highlight text %}
C:\Users\test\Desktop\xioustic.github.io>jekyll serve
Configuration file: C:/Users/test/Desktop/xioustic.github.io/_config.yml
            Source: C:/Users/test/Desktop/xioustic.github.io
       Destination: C:/Users/test/Desktop/xioustic.github.io/_site
 Incremental build: disabled. Enable with --incremental
      Generating...
Since v3.0, permalinks for pages in subfolders must be relative to the site source directory, not the parent directory. Check http://jekyllrb.com/docs/upgrading/ for more info.
{% endhighlight %}

## Disabling Relative Permalinks
Okay, open <code>\_config.yml</code> again and delete the <code>"relative_permalinks: true"</code> line.

## Things Go Wrong Part III
Another try at jekyll:
{% highlight text %}
C:\Users\test\Desktop\xioustic.github.io>jekyll serve
Configuration file: C:/Users/test/Desktop/xioustic.github.io/_config.yml
            Source: C:/Users/test/Desktop/xioustic.github.io
       Destination: C:/Users/test/Desktop/xioustic.github.io/_site
 Incremental build: disabled. Enable with --incremental
      Generating...
  Dependency Error: Yikes! It looks like you don't have redcarpet or one of its dependencies installed. In order to use Jekyll as currently configured, you'll need to install this gem. The full error message from Ruby is: 'cannot load such file -- redcarpet' If you run into trouble, you can find helpful resources at http://jekyllrb.com/help/!
  Conversion error: Jekyll::Converters::Markdown encountered an error while converting '_posts/2012-02-06-whats-jekyll.md':
                    redcarpet
             ERROR: YOUR SITE COULD NOT BE BUILT:
                    ------------------------------------
                    redcarpet
{% endhighlight %}

## Installing Redcarpet
Issue the following at a command prompt:
{% highlight bat %}
gem install redcarpet
{% endhighlight %}

## Things Go Wrong Part IV
Another try...
{% highlight text %}
C:\Users\test\Desktop\xioustic.github.io>jekyll serve
Configuration file: C:/Users/test/Desktop/xioustic.github.io/_config.yml
            Source: C:/Users/test/Desktop/xioustic.github.io
       Destination: C:/Users/test/Desktop/xioustic.github.io/_site
 Incremental build: disabled. Enable with --incremental
      Generating...
  Liquid Exception: Liquid syntax error: Unknown tag 'gist' in C:/Users/test/Desktop/xioustic.github.io/_posts/2012-02-07-example-content.md
jekyll 3.0.2 | Error:  Liquid syntax error: Unknown tag 'gist'
{% endhighlight %}

## Adding jekyll-gist
Edit the _config.yml file with your preferred text editor and change the "gems" line to the following:
{% highlight yaml %}
gems: [jekyll-paginate,jekyll-gist]
{% endhighlight %}

And then install the jekyll-gist gem using the command line:
{% highlight bat %}
gem install jekyll-gist
{% endhighlight %}

## Things Go Wrong Part V
Things have to work by now, right? Wrong...
{% highlight text %}
C:\Users\test\Desktop\xioustic.github.io>jekyll serve
Configuration file: C:/Users/test/Desktop/xioustic.github.io/_config.yml
            Source: C:/Users/test/Desktop/xioustic.github.io
       Destination: C:/Users/test/Desktop/xioustic.github.io/_site
 Incremental build: disabled. Enable with --incremental
      Generating...
  Dependency Error: Yikes! It looks like you don't have pygments or one of its dependencies installed. In order to use Jekyll as currently configured, you'll need to install this gem. The full error message from Ruby is: 'cannot load such file -- pygments' If you run into trouble, you can find helpful resources at http://jekyllrb.com/help/!
  Liquid Exception: pygments in C:/Users/test/Desktop/xioustic.github.io/_posts/2012-02-07-example-content.md
             ERROR: YOUR SITE COULD NOT BE BUILT:
                    ------------------------------------
                    pygments
{% endhighlight %}

## Adding pygments
Install the pygments gem using the command line:
{% highlight bat %}
gem install pygments.rb
{% endhighlight %}

## Things Go Wrong Part VI
Is jekyll working now? Well, mostly. But we don't want it manually polling, so we should install the 'wdm' gem.
{% highlight text %}
C:\Users\test\Desktop\xioustic.github.io>jekyll serve
Configuration file: C:/Users/test/Desktop/xioustic.github.io/_config.yml
            Source: C:/Users/test/Desktop/xioustic.github.io
       Destination: C:/Users/test/Desktop/xioustic.github.io/_site
 Incremental build: disabled. Enable with --incremental
      Generating...
  Liquid Exception: No such file or directory - python C:/Ruby200-x64/lib/ruby/gems/2.0.0/gems/pygments.rb-0.6.3/lib/pygments/mentos.py in C:/Users/test/Desktop/xioustic.github.io/_posts/2012-02-07-example-content.md
                    done in 0.25 seconds.
  Please add the following to your Gemfile to avoid polling for changes:
    gem 'wdm', '>= 0.1.0' if Gem.win_platform?
 Auto-regeneration: enabled for 'C:/Users/test/Desktop/xioustic.github.io'
Configuration file: C:/Users/test/Desktop/xioustic.github.io/_config.yml
    Server address: http://127.0.0.1:4000//
  Server running... press ctrl-c to stop.
Terminate batch job (Y/N)? ^C
{% endhighlight %}

## Installing WDM
Install the wdm gem using the command line:
{% highlight bat %}
gem install wdm
{% endhighlight %}

## Things Go Wrong Part VII
Okay, so it looks like Jekyll is serving (albeit with an error):
{% highlight text %}
C:\Users\test\Desktop\xioustic.github.io>jekyll serve
Configuration file: C:/Users/test/Desktop/xioustic.github.io/_config.yml
            Source: C:/Users/test/Desktop/xioustic.github.io
       Destination: C:/Users/test/Desktop/xioustic.github.io/_site
 Incremental build: disabled. Enable with --incremental
      Generating...
  Liquid Exception: No such file or directory - python C:/Ruby200-x64/lib/ruby/gems/2.0.0/gems/pygments.rb-0.6.3/lib/pygments/mentos.py in C:/Users/test/Desktop/xioustic.github.io/_posts/2012-02-07-example-content.md
                    done in 0.328 seconds.
 Auto-regeneration: enabled for 'C:/Users/test/Desktop/xioustic.github.io'
Configuration file: C:/Users/test/Desktop/xioustic.github.io/_config.yml
    Server address: http://127.0.0.1:4000//
  Server running... press ctrl-c to stop.
{% endhighlight %}

But when we visit http://127.0.0.1:4000/ we get a blank page. What gives?

## Installing Python, Pip and Pygments
Well, it turns out that pygments also requires Python2.7, pip, and the pygments package.

Download Python v2.7.x here: http://www.python.org/download/

During the install, make sure to enable "Add python.exe to Path".

The path option in the installer didn't work for me though, as evidenced by the following in a command line following the install:
{% highlight text %}
C:\Users\test\Desktop>python
'python' is not recognized as an internal or external command,
operable program or batch file.
{% endhighlight %}

So to manually add it to path, we open the start menu and search for "environment variable". On my system, the desired option looks like:
<img src="http://i.imgur.com/dwEZfdN.png">

Click the "Environment Variables..." button. Double-click the first "Path" item in the "User variables" table. At the end, append ";C:\Python27"

Python should now be available in any future command line:
{% highlight text %}
C:\Users\test\Desktop>python
Python 2.7.11 (v2.7.11:6d1b6a68f775, Dec  5 2015, 20:32:19) [MSC v.1500 32 bit (Intel)] on win32
Type "help", "copyright", "credits" or "license" for more information.
>>> exit()
{% endhighlight %}

Now install pygments from the command-line:
{% highlight bat %}
pip install pygments
{% endhighlight %}

## Things Go Wrong Part VIII
Yep, we're still not quite there yet. This should be the last fix though. Here's the attempt at this stage:
{% highlight text %}
C:\Users\test\Desktop\xioustic.github.io>jekyll serve
Configuration file: C:/Users/test/Desktop/xioustic.github.io/_config.yml
            Source: C:/Users/test/Desktop/xioustic.github.io
       Destination: C:/Users/test/Desktop/xioustic.github.io/_site
 Incremental build: disabled. Enable with --incremental
      Generating...
  Liquid Exception: SSL_connect returned=1 errno=0 state=SSLv3 read server certificate B: certificate verify failed in C:/Users/test/Desktop/xioustic.github.io/_posts/2012-02-07-example-content.md
jekyll 3.0.2 | Error:  SSL_connect returned=1 errno=0 state=SSLv3 read server certificate B: certificate verify failed
{% endhighlight %}

## Installing cacert.pem for Ruby
Get cacert.pem by saving this file, [cacert.pem](http://curl.haxx.se/ca/cacert.pem), to your Ruby directory (for me, that was C:\Ruby200-x64\cacert.pem).

Now, we need to add the <code>SSL\_CERT\_FILE</code> entry to your system environment variables. Once again, we open the start menu and search for "environment variable". On my system, the desired option looks like:
<img src="http://i.imgur.com/dwEZfdN.png">

Click the "Environment Variables..." button. Then click the top-most "New..." button. For Variable name, enter <code>SSL\_CERT\_FILE</code>. For Variable value, enter your path to the cacert.pem file (for me, it was <code>C:\Ruby200-x64\cacert.pem</code>).

## Finally, Jekyll serve is working
We made it!
{% highlight text %}
C:\Users\test\Desktop\xioustic.github.io>jekyll serve
Configuration file: C:/Users/test/Desktop/xioustic.github.io/_config.yml
            Source: C:/Users/test/Desktop/xioustic.github.io
       Destination: C:/Users/test/Desktop/xioustic.github.io/_site
 Incremental build: disabled. Enable with --incremental
      Generating...
                    done in 3.348 seconds.
 Auto-regeneration: enabled for 'C:/Users/test/Desktop/xioustic.github.io'
Configuration file: C:/Users/test/Desktop/xioustic.github.io/_config.yml
    Server address: http://127.0.0.1:4000//
  Server running... press ctrl-c to stop.
{% endhighlight %}

Visiting http://127.0.0.1:4000/ now produces the following:
<img src="http://i.imgur.com/uUWdr0T.png">

You can live edit your Jekyll pages and posts and Jekyll should automatically re-build and re-serve the site for as long as you keep the <code>jekyll serve</code> command running from your Jekyll site's working directory.

Cheers!

## Resources Used
- [https://github.com/karloespiritu/BlackDoc#usage](https://github.com/karloespiritu/BlackDoc#usage)
- [https://github.com/poole/poole#usage](https://github.com/poole/poole#usage)
- [https://github.com/juthilo/run-jekyll-on-windows](https://github.com/juthilo/run-jekyll-on-windows)
- [https://stackoverflow.com/questions/4528101/ssl-connect-returned-1-errno-0-state-sslv3-read-server-certificate-b-certificat](https://stackoverflow.com/questions/4528101/ssl-connect-returned-1-errno-0-state-sslv3-read-server-certificate-b-certificat)
- [https://gist.github.com/fnichol/867550](https://gist.github.com/fnichol/867550)
