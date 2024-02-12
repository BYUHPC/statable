# statable

If you have a broken filesystem, it can be hard to find out which files can still be accessed successfully. `statable` is meant to find which files are still intact by running `stat` on them. Given a broken filesystem mounted at `/mydata`, you can run:

```bash
statable /mydata 1>goodfiles.txt 2>badfiles.txt
```

...and each file for which `stat` fails to return for 10 seconds will be put in `badfiles.txt`.

To access the files in addition to `stat`ing them (performing a more thorough check at the expense of reduced speed), using 200 processes rather than the default 64, a timeout of 7.5 seconds rather than 10, and printing the inaccessible files to the terminal, you could use:

```bash
statable --access /mydata 7.5 200 1>/dev/null
```

Use `statable --help` for a more thorough help message.

We **strongly** recommend that you install [GNU Parallel](https://www.gnu.org/software/parallel/) and run `parallel --citation` before using `statable`; if you don't, the checks will run serially, resulting in agonizing slowness for all but the smallest or most intact filesystems.
