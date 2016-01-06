#socket.io

```
  1 failing

  1) socket.io socket should handle very large binary data:
     Error: timeout of 2000ms exceeded
```

* trying locally off master

* reached out to grauch
--> https://twitter.com/thealphanerd/status/684513109193535488

Turns out that socket.io 1.4.0 got pushed less than an hour after these failures

Started seeing other failures

https://github.com/karma-runner/karma/issues/1782

karma had to push a new version to keep up with changes that broke

Still seeing failures on 1.4.0 though

https://ci.nodejs.org/job/thealphanerd-smoker/16/

Trying one more time to see if those fedora failures are consistent

https://ci.nodejs.org/job/thealphanerd-smoker/18/
