Mid april we started noticing failures in node-glob in CI.

Turned out to be this PR --> https://github.com/nodejs/node/pull/3594

From the PR we sent to glob


> fs.realpath has been optimized to utilize uv_fs_realpath(), a new api
> in libuv. The libuv api has slightly different behavior. There are two
> particular issues that are causing problems for glob
> 
>     ev_fs_realpath() throwing before fs.readdir ELOOP
>     The removal of the cache
> 
> In the past glob was relying on fs.readdir to throw when handling
> recursive symbolically linked directories. It is now possible that the
> call to libuv can throw before. The behavior is currently different on
> osx and linux causing the test suite to fail on all of the flavors of
> linux we are running in CI.
> 
> This commit adds an extra check for 'ELOOP' and sets appropriately.
> 
> The commit includes an extra check to make sure that real is truthy
> Without that extra check the test suite was reporting garbage data in the results.
> This was only happening with the async implementation.
> 
> This commit has not done anything regarding the removal of the cache
> As long as the cache doesn't include a value called "encoding"
> everything will be fine.
> 
> There has not been any benchmarking done on this change.
> 
> ref: libuv/libuv#531
> ref: nodejs/node#3594

Turns out there is a potential security vuln in the implementation.

From Isaacs

> Did anyone look into the security implications of using realpath(3)? Maybe it's just bs and FUD, but that's why node had a JS realpath in the first place, because of buffer overflows possible in the native function. If that's not resolved, this is maybe a bad idea. 

From me

> So links that I've been collecting about this
> 
> Information about the bug --> http://man7.org/linux/man-pages/man3/realpath.3.html#BUGS
> 
> Here's an earlier CVE from 2003 --> https://cve.mitre.org/cgi-bin/cvename.cgi?name=can-2003-0466
> 
> Here's a CVE that affected Python in 2008 --> https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2006-1542
> 
> A bit more in depth description --> http://vuldb.com/?id.218

Information on affected system and patch status --> https://www.vulnerabilitycenter.com/#!vul=1678
