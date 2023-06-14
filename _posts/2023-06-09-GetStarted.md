```
---
title: GetStarted
date: 2023-06-09 17:00:00
categories: [Technology, Blog]
tags: [jekyll, get_started]
math: true
---
```

The following shows how to build your own GitHub pages with jekyll.

The jekyll template used here is from https://github.com/cotes2020/jekyll-theme-chirpy

firstly, create a new repo using the template above, then clone the repo locally, and run the following command in the root directory.

```
bundle
```

if it works all well, then you don't need the followings. I have encountered an error like this:

```
/Library/Developer/CommandLineTools/SDKs/MacOSX.sdk/System/Library/Frameworks/Ruby.framework/Versions/2.6/usr/include/ruby-2.6.0/ruby/ruby.h:24:10: fatal error: 'ruby/config.h' file not found
#include "ruby/config.h"
         ^~~~~~~~~~~~~~~
/Library/Developer/CommandLineTools/SDKs/MacOSX.sdk/System/Library/Frameworks/Ruby.framework/Versions/2.6/usr/include/ruby-2.6.0/ruby/ruby.h:24:10: note: did not find header 'config.h' in framework 'ruby' (loaded from '/Library/Developer/CommandLineTools/SDKs/MacOSX.sdk/System/Library/Frameworks')
1 error generated.
checked program was:
/* begin */
1: #include "ruby.h"
2: 
3: int main(int argc, char **argv)
4: {
5:   return 0;
6: }
/* end */

package configuration for openssl is not found
```

the information I have found is insufficient, but finally I have found this useful post https://vivo.pub/start-a-github-pages-repo-on-mac/  luckily, and the problem is solved by the following:

1. make sure your Xcode is ready

   ```
   xcode-select -v
   ```

2. install bundler and jekyll

   ```
   gem install bundler jekyll
   ```

   会发现报ruby/config.h file not found error

3. install ruby env

   ```
   brew install rbenv
   # set up rbenv with my ~/.bash_profile
   rbenv init
   # check installation
   curl -fsSL https://github.com/rbenv/rbenv-installer/raw/main/bin/rbenv-doctor | bash
   ```

4. install a new ruby version

   ```
   rbenv install 2.7.4
   rbenv global 2.7.4
   ruby -v
   ```

   if "ruby -v " still gives you the old 2.6 version, try restarting your Mac terminal to reload the ~/.bash_profile

5. add ruby to $PATH

   ```
   echo 'export PATH="$HOME/.rbenv/versions/2.7.4/bin:$PATH"' >> ~/.bash_profile
   ```

6. relaunching the terminal, and we can finally install the bundler and Jekyll, since github pages not support for Jekyll 4.0, so we need to specify the jekyll version

   ```
   gem install --user-install bundler jekyll==3.0.4
   ```

   and test the version:

   ```
   jekyll -v
   ```

7. clone a github pages repo to local, then we can test whether it works well:

   ```
   cd your_github_repo
   bundle install
   bundle exec jekyll s
   ```

   done!

