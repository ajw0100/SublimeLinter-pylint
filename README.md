SublimeLinter-pylint
=========================

See [parent fork](https://github.com/SublimeLinter/SublimeLinter-pylint) for the complete documentation.

This version just makes it possible to use [pyenv](https://github.com/yyuu/pyenv) (and presumably other advanced python virtualenvs) with SublimeLinter.

### Explaination of changes
The changes I made are just a hack. I am sure that @aparajita and @NotSqrt had good reasons to write this the way he did. It's just that they didn't work for me with multiple virtualenvs.

 1. Remove the `@python` from the linter's `cmd` list. This makes it so that instead of trying to invoke pylint as `/path/to/python /path/to/pylint` it just calls `/path/to/pylint` directly. I expect that pyenv will handle getting the right pylint for the current script's venv.
 2. Comment out `version_args`, `version_re`, and `version_requirement`. This stops SublimeLinter from performing a version check. pyenv figures out the correct pylint to invoke for the specific script. 
  1. The minimum requirement of pylint >- 1.0 is moot at this point in my opinion. 
  2. Also pyenv doesn't know which pylint to use unless you give it a script, so the check was failing.
 3. Set `check_version` to `False`. I think this one goes along with change 1. I don't need SublimeLinter to check my versions for me. I maintain the correct versions in my venv.

### Usage
This is what I did in OS X, something similar should work for you.

1. Install SublimeLinter & SublimeLinter-pylint normally.
2. Quit Sublime Text.
2. `cd ~/Library/Application\ Support/Sublime\ Text\ 3/Installed\ Packages`
  1. Or wherever your Sublime Text put's it's Installed Packages.
3. `curl --location --remote-name https://raw.githubusercontent.com/rgant/SublimeLinter-pylint/master/linter.py`
4. `zip SublimeLinter-pylint.sublime-package linter.py`

## Caveats
This works for me. In my setup. It may work for you too. Give it a try.

### Alternative
Before I started using pyenv I made my own shim just for SublimeLinter. I've documented that setup in the [wiki](https://github.com/rgant/SublimeLinter-pylint/wiki/Alternative-Setup).
