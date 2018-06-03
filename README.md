# PC Knowledge

Here I collect my computer knowledge.
It is mainly composed of instructions on how to configure stuff, so that the system works I want it to.
It is inteded to be used by me, but it might be useful to others as well.

## Clipboard capable Vim on MacOS
The version of Vim shipped with MacOS is not built with `+clipboard`.
Install Vim via MacPorts with
```
sudo port install vim +huge
```
or use homebrew
```
brew install vim
```
[Stack Exchange](https://superuser.com/questions/421057/install-vim-with-clipboard-support-using-macports-in-os-x-10-7-3)
https://raw.github.com/Homebrew/homebrew-dupes/master/vim.rb is deprecated.

See also [Client server capable Vim on MacOS](#client-server-capable-vim-on-macos)

## Client server capable Vim on MacOS
The version of Vim shipped with MacOS is not built with `+clientserver`.
Install Vim via MacPorts with
```
sudo port install vim +huge +x11
```
or use homebrew
```
brew install vim --with-client-server
```
[Stack Overflow](http://stackoverflow.com/a/10231902)

Note: This will start X11 anytime Vim is called.

See also [Clipboard capable Vim on MacOS](#clipboard-capable-vim-on-macos)

## Install gem on MacOS with SIP (System Integrity Protection) enabled
Nobody has write access in `/usr/bin` anymore.
Thus we install stuff in `/usr/local/bin`.
```
sudo gem install -n /usr/local/bin GEM_NAME_HERE
```
[Stack Overflow](http://stackoverflow.com/a/34234878)

## Set PATH for GUI apps on MacOS
In order to set the PATH variable, which can be seen by GUI apps, you have to run the following command
```
sudo launchctl config user path <path>
```
In order to make `latexmk` work in MacVim with LaTeX-Box I use
```
sudo launchctl config user path /usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin:/Library/TeX/texbin
```
[Stack Exchange](http://apple.stackexchange.com/a/243946)

## Pass on all arguments in bash script
```
#!/bin/bash
command "$@"
```
`"$@"` is handled as a special case by the shell.
From the bash reference manual, special parameters section:
`'@` ... Expands to the positional parameters, starting from one.
When the expansion occurs within double quotes, each parameter expands to a separate word.
That is, `"$@"` is equivalent to `"$1" "$2" ...`

If you want to pass all but the first arguments, you can first use `shift` to \"consume\" the first argument, then pass `$@`, the list of remaining arguments to another command.

[Stack Overflow](http://stackoverflow.com/a/3816747)

## Location of bash script file
The path to the bash script file can be acquired as follows
```
#!/bin/bash
echo "${0%/*}"
```

## Name of the bash script file
The name of the bash script file can be acquired as follows
```
#!/bin/bash
echo "${0##/}"
```

## Math array spacing in LaTeX

Use `\setlength{\delimitershortfall}{0pt}` in order to fix the spacing in math arrays.

```
\documentclass{article}
\usepackage{amsmath}
\begin{document}
\[
  \setlength{\delimitershortfall}{0pt}
  \begin{bmatrix}
    \dfrac{\partial f}{\partial x}
    \\[2ex]
    \dfrac{\partial f}{\partial y}
  \end{bmatrix}
\]
\end{document}
```

[Stack Exchange](http://tex.stackexchange.com/questions/19457/using-display-style-fraction-in-a-matrix-environment/61290#61290)

## LaTeX labels and legend entries with matlab2tikz

In order to use LaTeX in the labels one has to tell Matlab to not interpret any text

```
set(0,'defaulttextinterpreter','none')
```

The above doesn't affect the legend. The following turns off the interpreter for a specific legend.

```
lh = legend('some text')
set(lh,'Interpreter','none')
```

There doesn't seem to be a way to turn it off globally.
Then use the boolean option `parseStrings' of matlab2tikz.

```
matlab2tikz('...', 'parseStrings', false)
```

This way, the labels and legend entries get interpreted by LaTeX exaclty as one writes them in Matlab, e.g.

```
lh = legend('Chebyshev points over $l$', ...
            'projection of C. points onto y-axis', ...
            'Gauss quadrature points')
set(lh,'Interpreter','none')
xlabel('$l$')
ylabel('$d^l$ / $\tau^i$')
```

## MacOS: Dock supersmall
To make the Dock super small run the following command

```
defaults write com.apple.dock tilesize -int 1
killall Dock
```

To go back to normal size run
```
defaults write com.apple.dock tilesize -int 20
killall Dock
```

