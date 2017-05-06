Bash style guide
================

File extension
--------------

All bash files must have `.sh` extension.

Header
------

Include shebang for each bash script (`#!/bin/bash`)

Use `set -ex` for verbose output and exit on each error.

In case this rule can not be used, leave a comment in the script.

**Example:**

```bash
#!/bin/bash
set -ex
```

Code
----

All bash scripts should follow [Google's guidelines](https://google.github.io/styleguide/shell.xml) conventions.
 
With some additions:

- Readability matters. Add comments for all specific actions.

- Use `source` command instead of `.`

- Use `$(command)` instead of backticks

- Follow usual BASH coding-style, for example use `${SOME_VAR}`
  instead of `$SOME_VAR` whenever possible. 

- Try to limit line length to 100 symbols whenever possible.

- Shell check is a law. If your changes don't pass `shellcheck`, you must fix problems.

- ``# shellcheck disable=XXXX`` is a very exceptional case.

- Try to avoid ``cmd1 && cmd2 || cmd3``, see https://github.com/koalaman/shellcheck/wiki/SC2015 for details

- Consider to look at https://github.com/koalaman/shellcheck/wiki/ there are lot's of good howto's