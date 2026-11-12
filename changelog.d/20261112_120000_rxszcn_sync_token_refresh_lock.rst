Fixed
~~~~~

- The synchronous OAuth 2.0 clients serialize concurrent token refreshes with a
  reentrant lock so that a single refresh-token rotation triggers at most one
  real refresh. A request that loses the race now reuses the refreshed token
  instead of rotating the already-rotated refresh token again and writing the
  stale token back to storage, which previously logged out the whole batch of
  concurrent requests. The protection covers the ``requests`` session, the
  synchronous ``httpx`` client and the Flask and Django framework apps.
