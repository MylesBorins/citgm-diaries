This one is weird

Blows up with errors that process.stdout.cursorTo does not exist

Turns out that the node process object creates stdout using tty
if you are in a child_process the object is created using net

So if you write code or run code that calls for example `process.stdout.getWindowSize` will explode

This becomes particularly fun if you are trying to shell out to tools that are normally expecting a tty such as EVERY REPORTER.

if you ever download bluebird and run the test suite you'll see what is happening. They did a phenominal job building a testing reporter that looks gorgeous. There is a lot of moving the cursor around to mark off tests as compelted, while the suite runs in parallel.

Unfortauntely this makes citgm explode

I worked with @evanlucas to come up with a fix. 

The first iteration is simply shimming in the functions as no-ops

https://github.com/nodejs/node/pull/5061

We decided to not implement this. It is clearly documented that you should feature detect
if you are using those features.

@evanlucas submitted a PR to udpate blue bird

https://github.com/petkaantonov/bluebird/pull/992

bluebird now works!
