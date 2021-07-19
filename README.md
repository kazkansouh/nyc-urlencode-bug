# `nyc` [bug report][1] for url unsafe chars in filename

This is a minimal working example to demonstrate that `nyc` is not
correctly processing files that contain unsafe characters in the
filename.

The problem occurs when looking for a sourcemap, it appears the
filename that is checked on disk is url encoded. E.g. the filename
`{id}.js.map` becomes `%7Bid%7D.js.map`.

This bug report uses typescript to generate a simple file and
sourcemap.


```plaintext
$ npx nyc node .
Transformation error for /dev/shm/nyc-urlencode-bug/dist/{id}.js ; return original code
An error occurred while trying to read the map file at /dev/shm/nyc-urlencode-bug/dist/%7Bid%7D.js.map
Error: ENOENT: no such file or directory, open '/dev/shm/nyc-urlencode-bug/dist/%7Bid%7D.js.map'
Hello World!!
----------|---------|----------|---------|---------|-------------------
File      | % Stmts | % Branch | % Funcs | % Lines | Uncovered Line #s 
----------|---------|----------|---------|---------|-------------------
All files |       0 |        0 |       0 |       0 |                   
----------|---------|----------|---------|---------|-------------------
```

[1]: https://github.com/istanbuljs/nyc/issues/1419
