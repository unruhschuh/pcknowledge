# PC Knowledge

## Clipboard capable Vim on MacOS
Install Vim via MacPorts with
```
sudo port install vim +huge
```
Or use homebrew
```
brew install https://raw.github.com/Homebrew/homebrew-dupes/master/vim.rb
```
From [Stack Exchange](https://superuser.com/questions/421057/install-vim-with-clipboard-support-using-macports-in-os-x-10-7-3).


## Install gem on MacOS with SIP (System Integrity Protection) enabled
```
sudo gem install -n /usr/local/bin GEM_NAME_HERE
```
From [Stack Overflow](http://stackoverflow.com/a/34234878).

## Set PATH for GUI apps on MacOS
In order to set the PATH variable, which can be seen by GUI apps, you have to run the following command
```
sudo launchctl config user path <path>
```
In order to make `latexmk` work in MacVim with LaTeX-Box I use
```
sudo launchctl config user path /usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin:/Library/TeX/texbin
```
From [Stack Exchange](http://apple.stackexchange.com/a/243946)
