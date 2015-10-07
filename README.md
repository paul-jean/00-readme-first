## Fibonacci sequence in JS

Implement a function that returns the nth fibonacci number f(n),
for integer n = 0, 1, 2 ...

### Front end

A simple demo is included that lets you compare the timing of the fibonacci sequence
as computed by straight recursion and using recursion with memoization to avoid
recomputing values of f(n).

Start a web server:

```bash
    [rule146@rule146: fib-nodejs]$ python -m SimpleHTTPServer
    Serving HTTP on 0.0.0.0 port 8000 ...
```

Hit the "Start" button to run regular and memoized fibonacci sequences
side by side:

![assets/fib-start.gif](start)

Eventually the regular implementation takes > 3 seconds and is aborted,
while the memoized version keeps computing iterations:

![assets/fib-end.gif](end)

### Tests

Run the tests using the `test` gulp task:

``` bash
    [rule146@rule146: fib-nodejs]$ gulp test
    [23:14:12] Using gulpfile ~/code/fib-nodejs/gulpfile.js
    [23:14:12] Starting 'test'...
    [23:14:12] Finished 'test' after 2.07 ms
    [23:14:12] [nodemon] 1.7.1
    [23:14:12] [nodemon] to restart at any time, enter `rs`
    [23:14:12] [nodemon] watching: *.*
    [23:14:12] [nodemon] starting `node test/tests.js`    [rule146@rule146: 20150922-fib-js]$ node test/tests.js
    test: fib
    n = 0, fib(0) = 1, answer: 1, correct? true
    n = 1, fib(1) = 1, answer: 1, correct? true
    n = 2, fib(2) = 2, answer: 2, correct? true
    n = 3, fib(3) = 3, answer: 3, correct? true
    n = 4, fib(4) = 5, answer: 5, correct? true
    n = 20, fib(20) = 10946, answer: 10946, correct? true
    n = 40, fib(40) = 165580141, answer: 165580141, correct? true
    n = -1, fib(-1) = null, answer: null, correct? true
    tests PASSED

    test: fib_mem
    n = 0, fib(0) = 1, answer: 1, correct? true
    n = 1, fib(1) = 1, answer: 1, correct? true
    n = 2, fib(2) = 2, answer: 2, correct? true
    n = 3, fib(3) = 3, answer: 3, correct? true
    n = 4, fib(4) = 5, answer: 5, correct? true
    n = 20, fib(20) = 10946, answer: 10946, correct? true
    n = 40, fib(40) = 165580141, answer: 165580141, correct? true
    n = -1, fib(-1) = null, answer: null, correct? true
    tests PASSED
```

### Build

Package the JS code using browserify with the `build` gulp task:

``` bash
    [rule146@rule146: fib-nodejs]$ gulp build
    [22:42:21] Using gulpfile ~/code/fib-nodejs/gulpfile.js
    [22:42:21] Starting 'build'...
    [22:42:22] Finished 'build' after 519 ms
```

... which produces a js file appropriate for sourcing from a `<script>` tag:

``` bash
    [rule146@rule146: fib-nodejs]$ lt build/
    total 496
    -rw-r--r--  1 rule146  staff   245K Oct  6 22:42 bundle.js
```

### Creating the screencasts

The screencasts were taken using QuickTime Player, and then converted to
animated gifs using `ffmpeg`:

```bash
    ffmpeg -i fib-end.mov -s 1440x900 -f gif -filter:v "setpts=0.25*PTS" - | gifsicle --optimize=3 > fib-end.gif
```
