# Lolcat shell logo

> Displays a logo with your username in rainbow colours every time you open a new terminal window.

![Preview](./preview.gif)

## Compatibility

Should work with Bash and Zsh on MacOS / Linux.

## Requirements

* [Bash](https://www.gnu.org/software/bash/) or [Zsh](https://www.zsh.org/)
* [Lolcat][lolcat]

## Installation

1. Download and install [Lolcat][lolcat], which will be handling the colouring of the logo.

2. Download the `.asciilogo` file and place it in your home directory.

> Press `Command` + `Shift` + `.` (MacOS) or `Control` + `Shift` + `h` (Ubuntu) to display hidden dot files on your system.

3. Open your existing shell configuration `~/.zshrc`, `~/.bashrc` (Linux) or `~/.bash_profile` (MacOS) in a code/text editor and place the following functions somewhere before the end of your configuration:

```sh
function displayLine () {
  echo $1 | sed -e "s+{{username}}+@$USER+g"
}

function printLogo () {
  local logo=$1
  if [ -e "$logo" ]; then
    echo ""
    while IFS= read -r line; do
      displayLine $line
    done < $logo
    echo ""
  fi
}
```

4. Place the following line at the end of your shell configuration where you want the logo to be printed:

```sh
printLogo ~/.asciilogo | lolcat
```

> If you decided to put the logo somewhere else, replace the `~/.asciilogo` with the location and name of your logo.

5. Save and restart your terminal

You should now see a colourful 🌈 logo with your username printed on the side every time you start a new session.

For further customisations such as animations and colour spreads, see the [Lolcat repository][lolcat] on GitHub.


## Text replacements

If you want the logo to display other dynamic content, you can expand the `displayLine` function by piping more SEDs in a row and adding more `{{stuff}}` to your logo:

```sh
echo $1 | sed -e "s+{{username}}+@$USER+g" | sed -e "s+{{something}}+@$REPLACEMENT+g"
```

Note that `$USER` is a global variable and prints out your current username. The `$REPLACEMENT` in this example would contain whatever you want the `{{something}}` to be replaced with:

```sh
$REPLACEMENT=Content you want to display
```

These extra variables should be placed somewhere at the beginning of your configuration file.

## Links

* [ASCII Generator](http://www.network-science.de/ascii/)

## License

[![MIT][mit-badge]](LICENSE.md)

[lolcat]: https://github.com/busyloop/lolcat
[mit-badge]: https://img.shields.io/badge/license-MIT-green.svg
