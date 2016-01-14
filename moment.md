#moment

* they rely on grunt-cli
* should we have to bootstrap the CI system?
* https://github.com/nodejs/citgm/issues/42

* They originally didn't want to change it and closed the PR
 - https://github.com/moment/moment/pull/2830#issuecomment-167944198
 - cited docs from grunt-cli
 
* I opened an issue over on grunt-cli to change the docs
 - https://github.com/gruntjs/grunt-cli/issues/90#issuecomment-168811938
 - cowboy agrees https://github.com/gruntjs/grunt-cli/issues/90#issuecomment-168815844

* 🎉🎉🎉 original PR is reopened 🎉🎉🎉
  - https://github.com/moment/moment/pull/2830#issuecomment-168816115
  
* BUT WAIT THERE's MORE

Their developer workflow expects grunt-cli to be installed globally as they use grunt to register all their tasks / sub tasks.

https://github.com/moment/moment/pull/2830#issuecomment-168829926

Should ever moment developer install a dupe of grunt-cli on their system? Is it weird that running ```npm test``` could potentially run a different grunt-cli than ```grunt test```?

Currently not sure what the best solution is and moment is not currently being tested by citgm.

Moment ended up adding grunt-cli to the dev deps and now it is being tested by citgm again!
