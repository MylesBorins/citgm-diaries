#Columnify

* maximum call stack exceeded in ubuntu (and other linux's)
  - chat with tim oxly
  - https://twitter.com/thealphanerd/status/684441624735121408
  - node-dev logs Jan 5th 11:00 am pst
* calling toString on data was giving too large of an object to columnify
* we attempted to increase callstack size for errors to confirm the issue
* switched out toString with util.inspect
* Columnify was changed
 - https://github.com/timoxley/columnify/commit/fd6a0c9f04fa0e247b82a86b85ee99d4054690b3
* It still blew up :(

* Attempting to remove color from npm
* no dice

* happens when columnify gets a string longer than 80k characters

* dat npm tree

* fix lands in columnify
  - https://github.com/timoxley/columnify/compare/dac675e32d376fe02c9e526614c1b72a6d6e99ab...b5373b3d6344bf59e1ab63c912c188c34bce5889