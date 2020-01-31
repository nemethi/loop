# loop

Loop a command until it exits with a specified exit code or a timeout occurs.

## Description

Loop the specified command until it exits with one of the specified exit codes.
The exit code '0' is implicitly included.

Additionally, a timeout value may be supplied.
Setting the timeout to '0' has the same effect as not supplying it.

Usage:
```
loop <-c command> [-t timeout][-e exit codes]
```

## Installing

Requirement: bash 4.x+

Copy the `loop` script to your `$PATH`.

Display the help message to check the script's availability:

```
loop -h
```

## Examples

Call `curl` until it exits with 0:
```
loop -c "curl https://www.google.com"
```

Call `wget` until it exits with 0, 4, 5 or 6:
```
loop -c "wget https://www.google.com" -e "4 5 6"
```

Call `ping` until it exits with 0 or 1, or 20 seconds has passed:
```
loop -c "ping https://www.google.com" -t 20 -e 1
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

## Authors

* **Gábor Némethi** - [nemethi](https://github.com/nemethi)

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details
