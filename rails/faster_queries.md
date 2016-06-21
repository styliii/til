## Faster Queries - Hit the Database Once

Last week we had pages that were timing out because they took more than 25s to
load.  Embarassing.  When I tried running on my local computer, it took 140s to
load one page.  What was going on?  Loading thousands of records and
multiple n + 1 queries were killing the page.  The goal is to hit the database
only once.

The [bullet gem](https://github.com/flyerhzm/bullet) is a great tool to tell you
what you need to include in your queries, if you are pulling data from
associated tables.

The second thing is avoiding sub queries.  It actually pays to do `.select` on
an Enumerable, instead of another query because the records are already loaded
in memory, and you don't want to hit the database again.

Lastly, caching, which can be tricky in itself, so I try to avoid it.  Caching
something on a class level will stay that way until the server restarts.
Caching on an instance object will stay that way until the object is reloaded in
memory.  So new requests via the client will refresh the cache.

