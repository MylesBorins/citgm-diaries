Feb 3

Jade breaks in CI

Looks like citgmn is not getting the right path

WHAT

LOL. They moved Jade to the pugjs org but did not update the package.json. This was not a problem at first, as github automagically re routed things.

UNTIL... they started using jadejs/jade to store archives of the website. Now nothing work anymore.

Our algorithm for scraping tar balls relies on the repo in the package.json... working

PR sent
https://github.com/pugjs/jade/pull/2238
