Commit introducing arrow functions seems to have broken the tape test suite on fedora

https://github.com/nodejs/node/commit/ae5bcf9528

This commit was not included in the 5.4.1 release.

It seems like it may be the result of a deeper bug in node, or flakyness in the tape testing suite.
