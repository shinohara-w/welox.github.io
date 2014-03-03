# rpm -qa |grep ruby

# yum install -y ruby


参考ページ

	
	http://qiita.com/pb_tmz08/items/269c43418894071dc0b1


# rpm -qa |grep ruby
	ruby-libs-1.8.7.352-13.el6.x86_64
	ruby-1.8.7.352-13.el6.x86_64


git clone https://github.com/rubygems/rubygems.git rubygems
	Initialized empty Git repository in /root/rubygems/.git/
	remote: Reusing existing pack: 39936, done.
	remote: Total 39936 (delta 0), reused 0 (delta 0)
	Receiving objects: 100% (39936/39936), 16.07 MiB | 4.91 MiB/s, done.
	Resolving deltas: 100% (21552/21552), done.

# cd rubygems/

# ruby setup.rb
	RubyGems 2.2.2 installed
	ERROR:  While executing gem ... (Gem::DocumentError)
    	RDoc is not installed: no such file to load -- rdoc/rdoc

# yum install rdoc

# ruby setup.rb
	RubyGems 2.2.2 installed
	Installing ri documentation for rubygems-2.2.2
	/usr/lib/ruby/1.8/rdoc/rdoc.rb:280: warning: conflicting chdir during another chdir block
	/usr/lib/ruby/1.8/rdoc/rdoc.rb:287: warning: conflicting chdir during another chdir block

	=== 2.2.2 / 2014-02-05

	Bug fixes:

	* Fixed ruby tests when BASERUBY is not set.  Patch for #778 by Nobuyoshi
	  Nakada.
	* Removed double requests in RemoteFetcher#cache_update_path to improve remote
	  install speed.  Pull request #772 by Charlie Somerville.
	* The mkmf.log is now placed next to gem_make.out when building extensions.
	* `gem install -g --local` no longer accesses the network.  Bug #776 by Jeremy
	  Evans.
	* RubyGems now correctly handles URL passwords with encoded characters.  Pull
	  request #781 by Brian Fletcher.
	* RubyGems now correctly escapes URL characters.  Pull request #788 by Brian
	  Fletcher.
	* RubyGems can now unpack tar files where the type flag is not given.  Pull
	  request #790 by Cody Russell.
	* Typo corrections.  Pull request ruby/ruby#506 by windwiny.
	* RubyGems now uses both the default certificates and ssl_ca_cert instead of
	  one or the other.  Pull request #795 by zebardy.
	* RubyGems can now use the bundler API against hosted gem servers in a
	  directory.  Pull request #801 by Brian Fletcher.
	* RubyGems bin stubs now ignore non-versions.  This allows RubyGems bin stubs
	  to list file names like "_foo_".  Issue #799 by Postmodern.
	* Restored behavior of Gem::Version::new when subclassed.  Issue #805 by
	  Sergio Rubio.
	
	=== 2.2.1 / 2014-01-06
	Bug fixes:
	
	* Platforms in the Gemfile.lock GEM section are now handled correctly.  Bug
	  #767 by Diego Viola.
	* RubyGems now displays which gem couldn't be uninstalled from the home
	  directory.  Pull request #757 by Michal Papis.
	* Removed unused method Gem::Resolver#find_conflict_state.  Pull request #759
	  by Smit Shah.
	* Fixed installing gems from local files without dependencies.  Issue #760 by
	  Arash Mousavi, pull request #764 by Tim Moore.
	* Removed TODO about syntax that works in Ruby 1.8.7.  Pull request #765 by
	  Benjamin Fleischer.
	* Switched Gem.ruby_api_version to use RbConfig::CONFIG['ruby_version'] which
	  has the same value but is overridable by packagers through
	  --with-ruby-version= when configuring ruby.  Bug #770 by Jeremy Evans.
	* RubyGems now prefers the bundler API for `gem install` to reduce HTTP
	  requests.  (This change was intended for RubyGems 2.2.0 but was missed.)
	  This should address bug #762 by Dan Peterson and bug #766 by mipearson.
	* Added Gem::BasicSpecification#source_paths so documentation or analysis
	  tools can work properly as require_paths no longer returns extension source
	  directories.  Bug #758 Vit Ondruch.
	* Gem.read_binary can read read-only files again.  This caused file://
	  repositories to stop working.  Bug #761 by John Anderson.
	* Fixed specification file sorting for Ruby 1.8.7 compatibility.  Pull
	  request #763 by James Mead
	
	=== 2.2.0 / 2013-12-26
	Special thanks to Vit Ondruch and Michal Papis for testing and finding bugs in
	RubyGems as it was prepared for the 2.2.0 release.
	
	Major enhancements:
	
	* RubyGems can check for gem dependencies files (gem.deps.rb or Gemfile) when
	  rubygems executables are started and uses the found dependencies.  This
	  means `rake` will work similar to `bundle exec rake`.  To enable this set
	  the `RUBYGEMS_GEMDEPS` environment variable to the location of your
	  dependencies file.
	
	  See Gem::use_gemdeps for further details.
	
	* A RubyGems directory may now be shared amongst multiple ruby versions.  Upon
	  activation RubyGems will automatically compile missing extensions for the
	  current platform when the built objects are missing.  Issue #596 by Michal
	  Papis
	
	  By default different platforms do not share gem install locations so this
	  must be configured by setting GEM_HOME to a common directory.  Some gems use
	  fixed paths for requiring extensions and are not compatible with sharing gem
	  directories.
	
	  The default sharing location may be configured by RubyGems packagers through
	  Gem.default_ext_dir_for.  Pull Request #744 by Vit Ondruch.
	
	Minor enhancements:
	
	* RubyGems checks the 'allowed_push_host' metadata value when pushing a gem to
	  prevent an accidental push to a public repository (such as rubygems.org).
	  If you have private gems you should set this value in your gem specification
	  metadata.  Pull request #603 by Seamus Abshere.
	* `gem list` now shows results for multiple arguments.  Pull request #604 by
	  Zach Rabinovich.
	* `gem pristine --extensions` will restore only gems with extensions.  Issue
	  #619 by Postmodern.
	* Gem::Specification#files is now sorted.  Pull request #612 by Justin George.
	* For `gem list` and friends, "LOCAL" and "REMOTE" headers are omitted if
	  only local or remote gem information is requested with --quiet.  Pull
	  request #615 by Michal Papis.
	* Added Gem::Specification#full_require_paths which is like require_paths, but
	  returns a fully-qualified results.  Pull request #632 by Vit Ondruch.
	* RubyGems now looks for the https_proxy environment variable for https://
	  sources.  RubyGems will fall back to http_proxy if there is no https_proxy.
	  Issue #610 by mkristian.
	* RubyGems now creates directories in .gem files.  Issue #631 by marksolaris.
	* RubyGems raises an exception when a specification includes its gem.  Issue
	  #623 by notEthan.
	* RubyGems now displays relevant release note information when updating
	  RubyGems.  Issue #647 by Trevor Wennblom.
	* Deprecated Gem::Installer::ExtensionBuildError in favor of
	  Gem::Ext::BuildError.  The old constant is an alias for the new constant.
	* When extensions are built the gem_make.out file is always written now, even
	  on success.  This will help with debugging bad builds that report success.
	* If a specification fails to validate RubyGems shows a link to the
	  specification reference guide.  Issue #656 by Markus Heiler.
	* When using `gem install -g`, RubyGems now detects the presence of an
	  Isolate, Gemfile or gem.deps.rb file.
	* Added Gem::StubSpecification#stubbed? to help determine if a user should run
	  `gem pristine` to speed up gem loading.  Pull request #694 and #701 by Jon
	  Leighton.
	* RubyGems now warns when a gem has a pessimistic version dependency that may
	  be too strict.
	* RubyGems now warns when a gem has an open-ended dependency.
	* RubyGems now raises an exception when a dependency for a gem is defined
	  twice.
	* Marked the license specification attribute as recommended.  Pull request
	  #713 by Benjamin Fleischer.
	* RubyGems uses io/console instead of `stty` when available.  Pull request
	  #740 by Nobuyoshi Nakada
	* Relaxed Gem.ruby tests for platforms that override where ruby lives.  Pull
	  Request #755 by strzibny.
	
	Bug fixes:
	
	* RubyGems now returns an error status when any file given to `gem which`
	  cannot be found.  Ruby bug #9004 by Eugene Vilensky.
	* Fixed command escaping when building rake extensions.  Pull request #721 by
	  Dmitry Ratnikov.
	* Fixed uninstallation of gems when GEM_HOME is a relative directory.  Issue
	  #708 by Ryan Davis.
	* Default gems are now ignored by Gem::Validator#alien.  Issue #717 by David
	  Bahar.
	* Fixed typos in RubyGems.  Pull requests #723, #725, #731 by Akira Matsuda,
	  pull request #736 by Leo Gallucci, pull request #746 by DV Suresh.
	* RubyGems now holds exclusive locks on cached gem files to prevent incorrect
	  updates.  Pull Request #737 by Smit Shah
	* Improved speed of `gem install --ignore-dependencies`.  Patch by Terence
	  Lee.
	
	
	------------------------------------------------------------------------------
	
	RubyGems installed the following executables:
	        /usr/bin/gem
	
	Ruby Interactive (ri) documentation was installed. ri is kind of like man
	pages for ruby libraries. You may access it like this:
	  ri Classname
	  ri Classname.class_method
	  ri Classname#instance_method
	If you do not wish to install this documentation in the future, use the
	--no-document flag, or set it as the default in your ~/.gemrc file. See
	'gem help env' for details.
	
	t@lx008 rubygems]#
	[root@lx008 rubygems]#
	[root@lx008 rubygems]# gem -v
	2.2.2
	
	
	
	
	[root@lx008 ~]# gem install jekyll
	Fetching: blankslate-2.1.2.4.gem (100%)
	Successfully installed blankslate-2.1.2.4
	Fetching: parslet-1.5.0.gem (100%)
	Successfully installed parslet-1.5.0
	Fetching: toml-0.1.1.gem (100%)
	Successfully installed toml-0.1.1
	Fetching: redcarpet-2.3.0.gem (100%)
	Building native extensions.  This could take a while...
	ERROR:  Error installing jekyll:
	        ERROR: Failed to build gem native extension.
	
	    /usr/bin/ruby extconf.rb
	mkmf.rb can't find header files for ruby at /usr/lib/ruby/ruby.h
	
	extconf failed, exit code 1
	
	Gem files will remain installed in /usr/lib64/ruby/gems/1.8/gems/redcarpet-2.3.0 for inspection.
	Results logged to /usr/lib64/ruby/gems/1.8/extensions/x86_64-linux/1.8/redcarpet-2.3.0/gem_make.out


エラーが発生して失敗


# yum install ruby-devel

# gem install jekyll
	Building native extensions.  This could take a while...
	ERROR:  Error installing jekyll:
	        ERROR: Failed to build gem native extension.
	
	    /usr/bin/ruby extconf.rb
	creating Makefile
	
	make  clean
	
	make
	gcc -I. -I/usr/lib64/ruby/1.8/x86_64-linux -I/usr/lib64/ruby/1.8/x86_64-linux -I.   -fPIC -O2 -g -pipe -Wall -Wp,-D_FORTIFY_SOURCE=2 -fexceptions -fstack-protector --param=ssp-buffer-size=4 -m64 -mtune=generic -fno-strict-aliasing  -fPIC  -fvisibility=hidden  -c stack.c
	make: gcc: コマンドが見つかりませんでした
	make: *** [stack.o] エラー 127
	
	make failed, exit code 2
	
	Gem files will remain installed in /usr/lib64/ruby/gems/1.8/gems/redcarpet-2.3.0 for inspection.
	Results logged to /usr/lib64/ruby/gems/1.8/extensions/x86_64-linux/1.8/redcarpet-2.3.0/gem_make.out

またエラー

# yum install gcc


今度は成功


	/usr/lib/ruby/1.8/rdoc/rdoc.rb:280: warning: conflicting chdir during another chdir block
	/usr/lib/ruby/1.8/rdoc/rdoc.rb:287: warning: conflicting chdir during another chdir block
	Done installing documentation for classifier, colorator, commander, fast-stemmer, ffi, highline, jekyll, liquid, listen, maruku, posix-spawn, pygments.rb, rb-fsevent, rb-inotify, rb-kqueue, redcarpet, safe_yaml, yajl-ruby after 24 seconds
	18 gems installed

# git clone https://github.com/plusjade/jekyll-bootstrap.git tech.basicinc.jp

# easy_install Pygments
	Searching for Pygments
	Reading http://pypi.python.org/simple/Pygments/
	Best match: Pygments 1.6
	Downloading https://pypi.python.org/packages/2.6/P/Pygments/Pygments-1.6-py2.6.egg#md5=2584ae5795d01cefbff0744136df3f65
	Processing Pygments-1.6-py2.6.egg
	creating /usr/lib/python2.6/site-packages/Pygments-1.6-py2.6.egg
	Extracting Pygments-1.6-py2.6.egg to /usr/lib/python2.6/site-packages
	Adding Pygments 1.6 to easy-install.pth file
	Installing pygmentize script to /usr/bin
	
	Installed /usr/lib/python2.6/site-packages/Pygments-1.6-py2.6.egg
	Processing dependencies for Pygments
	Finished processing dependencies for Pygments

ぼんやり意味に気づきディレクトリ変更

# mv tech.basicinc.jp tech.welox.jp

# cd tech.welox.jp/

# git clone https://github.com/welox/welox.github.io.git
	Initialized empty Git repository in /root/welox.github.io/.git/
	remote: Reusing existing pack: 9, done.
	remote: Total 9 (delta 0), reused 0 (delta 0)
	Unpacking objects: 100% (9/9), done.


httpでpushしようとして失敗したので
ssh認証を通してpush。今度は成功

編集ファイル

# cat .git/config
	[core]
	        repositoryformatversion = 0
	        filemode = true
	        bare = false
	        logallrefupdates = true
	[remote "origin"]
	        fetch = +refs/heads/*:refs/remotes/origin/*
	        url = git@github.com:welox/welox.github.io.git
	[branch "master"]
	        remote = origin
	        merge = refs/heads/master


push成功して完了
