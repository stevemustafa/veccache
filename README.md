# veccache

A hot-tier vector cache in front of Postgres/pgvector. The hot portion of an
embedding corpus is held resident in memory and served from there; Postgres
stays the system of record, and the cache is kept coherent with it through
change data capture.

The cache isn't really the point. The measurement is. Every slice is scored
on recall degradation against an exact, uncached baseline, so the cost of
being fast comes out as a number instead of an assumption.

## What this is not

Not a database. It owns no data and makes no durability promise — kill the
process and nothing is lost but warm memory. It's also not an approximate
nearest neighbor library; it sits above whatever index Postgres is using and
is measured against exact search, not against another approximation.

## Status

In progress. Foundations are landing now; the first build slice is the
ground truth path — the exact retrieval baseline and the measurement harness,
with no cache in it at all. Nothing measured later means anything without it.

Corpus is Project Gutenberg, with the access distribution fitted to
Gutenberg's own published download counts rather than an assumed Zipf
exponent.

## License

Apache 2.0.
