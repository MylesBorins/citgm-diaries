Body parser started failing on master

Digging through it turns out the failing test is using querystring.parse

this commit which landed 3 days ago is changing the behaviour 
https://github.com/nodejs/node/commit/27def4faf2fb0c759b7e8800f91627cbbca5fdba

Created a test, now working on a fix


comment on the issue
> There is a very subtle change in behavior introduced with this patch.
> 
> String.prototype.split(value, Infinity) will always return an empty array.
> 
> The spec documents that the second argument must be an integer. Infinity is being interpreted as 0... instead of MAX_INT (perhaps this should be a fix upstream to v8).
> 
> In the past if querystring.parse was given Infinity, the split operation was unaffected.
> 
> body-parser is depending on this functionality, at the very least in their tests. We should likely find out how much querystring.parse is being called with infinity to see how much this will break.
> 
> I'm not 100% that the changes present here justify the edge case

Figured out a fix check it out, check if number isFinite()

https://github.com/nodejs/node/commit/878bcd43f8f9d3ec0d3403cb1bbe1ba6201a6d84

Fix will land in v5.3.1, regression never hit LTS
