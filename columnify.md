#Columnify

* maximum call stack exceeded in ubuntu (and other linux's)
  - chat with tim oxly
  - https://twitter.com/thealphanerd/status/684441624735121408
  - node-dev logs Jan 5th 11:00 am pst
* calling toString on data was giving too large of an object to columnify
* we attempted to increase callstack size for errors to confirm the issue
* switched out toString with util.inspect
