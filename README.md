# overlook-watch

Watches [overlook.technology](https://overlook.technology) from outside, because a dashboard can't
report its own outage.

Every 10 minutes, [the workflow](.github/workflows/watch.yml) calls
`https://overlook.technology/api/health?jobs=1`. That answers `503` when Overlook or its database is
down, or when its scheduled collections have stopped running. Three failures in a row fail the run,
and GitHub emails the owner.

- To see a failure on purpose, run the workflow by hand with a `url` that fails.
- Once a day it checks the last commit: GitHub turns off schedules in a public repo after 60 quiet
  days, so after 50 it commits an empty keep-alive.
