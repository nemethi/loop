# loop

Loop a command until it exits with a specified exit code or a pattern is matched in its output.

## Description

Loop the specified command until it exits with one of the specified exit codes or a pattern
is matched in its output.

Additionally, a timeout value may be supplied.
Setting the timeout to '0' has the same effect as not supplying it.

The sleep option may be used to make the script wait before executing the command again.

The pattern matching mode disables checking the exit code.
The command is looped UNTIL the pattern matches its output;
if the matching is inverted, the command is looped WHILE the pattern matches its output.
The pattern may be a fixed string or a regular expression.
The pattern matching's case-insensitivity can be toggled.

## Installing

Requirements:
bash 4.x+,
[sleep](http://man7.org/linux/man-pages/man1/sleep.1.html),
[grep](https://man7.org/linux/man-pages/man1/grep.1.html),
[mktemp](https://www.man7.org/linux/man-pages/man3/mktemp.3.html)

Copy the `loop` script to your `$PATH`.

Display the help message to check the script's availability:

```
loop -h
```

## Examples

Call `curl` until it exits with 0:
```bash
loop -c "curl https://www.google.com"
```

Call `wget` until it exits with 0, 4, 5 or 6:
```bash
loop -c "wget https://www.google.com" -e "4 5 6"
```

Call `traceroute` until it exits with 0, "sleeping" 3 seconds between each call:
```bash
loop -c "traceroute google.com" -s 3
```

Call `ping` until it exits with 0 or 1, or 20 seconds has passed:
```bash
loop -c "ping https://www.google.com" -t 20 -e 1
```

Call` script.sh` until its output contains "ok" case-insensitively:
```bash
loop -c "./script.sh" -g ok -i
```

Call `script.sh` while its output contains a line that matches the regexp:
```bash
loop -c "./script.sh" -g "^a.*z$" -E -v
```

## Running the tests

The automated tests make use of the [shUnit2](https://github.com/kward/shunit2) test framework.
shUnit2 is licensed under the [Apache License version 2.0](https://www.apache.org/licenses/LICENSE-2.0).

To run the tests change to the `test` directory and execute:
```
./loop_test
```
The tests will work only if you are running them from the `test` directory,
and if a copy of `loop` is available in the repo's root directory.


Static code analysis was made with [shellcheck](https://github.com/koalaman/shellcheck).

Code coverage was measured with [bashcov](https://github.com/infertux/bashcov).
## Authors

* **Gábor Némethi** - [nemethi](https://github.com/nemethi)

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details
