# Changes

This file is a manually maintained list of changes for each release. Feel free
to add your changes here when sending pull requests. Also send corrections if
you spot any mistakes.

## HEAD

* Add code `POOL_NOEXIST` in PoolCluster error #846
* Add `acquireTimeout` pool option to specify a timeout for acquiring a connection #821 #854
* Add `timeout` option to all sequences #855 #863
* Default `connectTimeout` to 10 seconds
* Fix domain binding with `conn.connect`
* Fix `PROTOCOL_PACKETS_OUT_OF_ORDER` error to be catchable #844
* Return `Query` object from `pool.query` like `conn.query` #830
* Use `EventEmitter.listenerCount` when possible for faster counting

## v2.3.2 (2014-05-29)

* Fix pool leaking connections after `conn.changeUser` #833

## v2.3.1 (2014-05-26)

* Add database errors to error constants
* Add global errors to error constants
* Throw when calling `conn.release` multiple times #824 #827
* Update known error codes

## v2.3.0 (2014-05-16)

* Accept MySQL charset (like `UTF8` or `UTF8MB4`) in `charset` option #808
* Accept pool options in connection string to `mysql.createPool` #811
* Clone connection config for new pool connections
* Default `connectTimeout` to 2 minutes
* Reject unauthorized SSL connections (use `ssl.rejectUnauthorized` to override) #816
* Return last error when PoolCluster exhausts connection retries #818
* Remove connection from pool after `conn.changeUser` is released #806
* Throw on unknown SSL profile name #817
* User newer TLS functions when available #809

## v2.2.0 (2014-04-27)

* Use indexOf instead of for loops removing conn from pool #611
* Make callback to `pool.query` optional like `conn.query` #585
* Prevent enqueuing sequences after fatal error #400
* Fix geometry parser for empty fields #742
* Accept lower-case charset option
* Throw on unknown charset option #789
* Update known charsets
* Remove console.warn from PoolCluster #744
* Fix `pool.end` to handle queued connections #797
* Fix `pool.releaseConnection` to keep connection queue flowing #797
* Fix SSL handshake error to  be catchable #800
* Add `connection.threadId` to get MySQL connection ID #602
* Ensure `pool.getConnection` retrieves good connections #434 #557 #778
* Fix pool cluster wildcard matching #627
* Pass query values through to `SqlString.format` #590

## v2.1.1 (2014-03-13)

* fix authentication w/password failure for node.js 0.10.5 #746 #752
* fix authentication w/password TypeError exception for node.js 0.10.0-0.10.4 #747
* fix specifying `values` in `conn.query({...}).on(...)` pattern #755
* fix long stack trace to include the `pool.query(...)` call #715

## v2.1.0 (2014-02-20)

* crypto.createHash fix for node.js < 11 #735
* Add `connectTimeout` option to specify a timeout for establishing a connection #726
* SSL support #481

## v2.0.1

* internal parser speed improvement #702
* domains support
* 'trace' connection option to control if long stack traces are generated #713 #710 #439

## v2.0.0 (2014-01-09)

* stream improvements:
  - node 0.8 support #692
  - Emit 'close' events from query streams #688
* encoding fix in streaming LOAD DATA LOCAL INFILE #670
* Doc improvements

## v2.0.0-rc2 (2013-12-07)

* Streaming LOAD DATA LOCAL INFILE #668
* Doc improvements

## v2.0.0-rc1 (2013-11-30)

* Transaction support
* Expose SqlString.format as mysql.format()
* Many bug fixes
* Better support for dates in local time zone
* Doc improvements

## v2.0.0-alpha9 (2013-08-27)

* Add query to pool to execute queries directly using the pool
* Pool option to set queue limit
* Pool sends 'connection' event when it opens a new connection
* Added stringifyObjects option to treat input as strings rather than objects (#501)
* Support for poolClusters
* Datetime improvements
* Bug fixes

## v2.0.0-alpha8 (2013-04-30)

* Switch to old mode for Streams 2 (Node.js v 0.10.x)
* Add stream method to Query Wraps events from the query object into a node v0.10.x Readable stream
* DECIMAL should also be treated as big number
* Removed slow unnecessary stack access
* Added charsets
* Added bigNumberStrings option for forcing BIGINT columns as strings
* Changes date parsing to return String if not a valid JS Date
* Adds support for ?? escape sequence to escape identifiers
* Changes Auth.token() to force password to be in binary, not utf8 (#378)
* Restrict debugging by packet types
* Add 'multipleStatements' option tracking to ConnectionConfig. Fixes GH-408
* Changes Pool to handle 'error' events and dispose connection
* Allows db.query({ sql: "..." }, [ val1, ... ], cb); (#390)
* Improved documentation
* Bug fixes

## v2.0.0-alpha7 (2013-02-03)

* Add connection pooling (#351)

## v2.0.0-alpha6 (2013-01-31)

* Add supportBigNumbers option (#381, #382)
* Accept prebuilt Query object in connection.query
* Bug fixes

## v2.0.0-alpha5 (2012-12-03)

* Add mysql.escapeId to escape identifiers (closes #342)
* Allow custom escaping mode (config.queryFormat)
* Convert DATE columns to configured timezone instead of UTC (#332)
* Convert LONGLONG and NEWDECIMAL to numbers (#333)
* Fix Connection.escape() (fixes #330)
* Changed Readme ambiguity about custom type cast fallback
* Change typeCast to receive Connection instead of Connection.config.timezone
* Fix drain event having useless err parameter
* Add Connection.statistics() back from v0.9
* Add Connection.ping() back from v0.9

## v2.0.0-alpha4 (2012-10-03)

* Fix some OOB errors on resume()
* Fix quick pause() / resume() usage
* Properly parse host denied / similar errors
* Add Connection.ChangeUser functionality
* Make sure changeUser errors are fatal
* Enable formatting nested arrays for bulk inserts
* Add Connection.escape functionality
* Renamed 'close' to 'end' event
* Return parsed object instead of Buffer for GEOMETRY types
* Allow nestTables inline (using a string instead of a boolean)
* Check for ZEROFILL_FLAG and format number accordingly
* Add timezone support (default: local)
* Add custom typeCast functionality
* Export mysql column types
* Add connection flags functionality (#237)
* Exports drain event when queue finishes processing (#272, #271, #306)

## v2.0.0-alpha3 (2012-06-12)

* Implement support for `LOAD DATA LOCAL INFILE` queries (#182).
* Support OLD\_PASSWORD() accounts like 0.9.x did. You should still upgrade any
  user accounts in your your MySQL user table that has short (16 byte) Password
  values. Connecting to those accounts is not secure. (#204)
* Ignore function values when escaping objects, allows to use RowDataPacket
  objects as query arguments. (Alex Gorbatchev, #213)
* Handle initial error packets from server such as `ER_HOST_NOT_PRIVILEGED`.
* Treat `utf8\_bin` as a String, not Buffer. (#214)
* Handle empty strings in first row column value. (#222)
* Honor Connection#nestTables setting for queries. (#221)
* Remove `CLIENT_INTERACTIVE` flag from config. Improves #225.
* Improve docs for connections settings.
* Implement url string support for Connection configs.

## v2.0.0-alpha2 (2012-05-31)

* Specify escaping before for NaN / Infinity (they are as unquoted constants).
* Support for unix domain socket connections (use: {socketPath: '...'}).
* Fix type casting for NULL values for Date/Number fields
* Add `fields` argument to `query()` as well as `'fields'` event. This is
  similar to what was available in 0.9.x.
* Support connecting to the sphinx searchd daemon as well as MariaDB (#199).
* Implement long stack trace support, will be removed / disabled if the node
  core ever supports it natively.
* Implement `nestTables` option for queries, allows fetching JOIN result sets
  with overlapping column names.
* Fix ? placeholder mechanism for values containing '?' characters (#205).
* Detect when `connect()` is called more than once on a connection and provide
  the user with a good error message for it (#204).
* Switch to `UTF8_GENERAL_CI` (previously `UTF8_UNICODE_CI`) as the default
  charset for all connections to avoid strange MySQL performance issues (#200),
  and also make the charset user configurable.
* Fix BLOB type casting for `TINY_BLOB`, `MEDIUM_BLOB` and `LONG_BLOB`.
* Add support for sending and receiving large (> 16 MB) packets.

## v2.0.0-alpha (2012-05-15)

This release is a rewrite. You should carefully test your application after
upgrading to avoid problems. This release features many improvements, most
importantly:

* ~5x faster than v0.9.x for parsing query results
* Support for pause() / resume() (for streaming rows)
* Support for multiple statement queries
* Support for stored procedures
* Support for transactions
* Support for binary columns (as blobs)
* Consistent & well documented error handling
* A new Connection class that has well defined semantics (unlike the old Client class).
* Convenient escaping of objects / arrays that allows for simpler query construction
* A significantly simpler code base
* Many bug fixes & other small improvements (Closed 62 out of 66 GitHub issues)

Below are a few notes on the upgrade process itself:

The first thing you will run into is that the old `Client` class is gone and
has been replaced with a less ambitious `Connection` class. So instead of
`mysql.createClient()`, you now have to:

```js
var mysql      = require('mysql');
var connection = mysql.createConnection({
  host     : 'localhost',
  user     : 'me',
  password : 'secret',
});

connection.query('SELECT 1', function(err, rows) {
  if (err) throw err;

  console.log('Query result: ', rows);
});

connection.end();
```

The new `Connection` class does not try to handle re-connects, please study the
`Server disconnects` section in the new Readme.

Other than that, the interface has stayed very similar. Here are a few things
to check out so:

* BIGINT's are now cast into strings
* Binary data is now cast to buffers
* The `'row'` event on the `Query` object is now called `'result'` and will
  also be emitted for queries that produce an OK/Error response.
* Error handling is consistently defined now, check the Readme
* Escaping has become more powerful which may break your code if you are
  currently using objects to fill query placeholders.
* Connections can now be established explicitly again, so you may wish to do so
  if you want to handle connection errors specifically.

That should be most of it, if you run into anything else, please send a patch
or open an issue to improve this document.

## v0.9.6 (2012-03-12)

* Escape array values so they produce sql arrays (Roger Castells, Colin Smith)
* docs: mention mysql transaction stop gap solution (Blake Miner)
* docs: Mention affectedRows in FAQ (Michael Baldwin)

## v0.9.5 (2011-11-26)

* Fix #142 Driver stalls upon reconnect attempt that's immediately closed
* Add travis build
* Switch to urun as a test runner
* Switch to utest for unit tests
* Remove fast-or-slow dependency for tests
* Split integration tests into individual files again

## v0.9.4 (2011-08-31)

* Expose package.json as `mysql.PACKAGE` (#104)

## v0.9.3 (2011-08-22)

* Set default `client.user` to root
* Fix #91: Client#format should not mutate params array
* Fix #94: TypeError in client.js
* Parse decimals as string (vadimg)

## v0.9.2 (2011-08-07)

* The underlaying socket connection is now managed implicitly rather than explicitly.
* Check the [upgrading guide][] for a full list of changes.

## v0.9.1 (2011-02-20)

* Fix issue #49 / `client.escape()` throwing exceptions on objects. (Nick Payne)
* Drop < v0.4.x compatibility. From now on you need node v0.4.x to use this module.

## Older releases

These releases were done before maintaining this file:

* [v0.9.0](https://github.com/felixge/node-mysql/compare/v0.8.0...v0.9.0)
  (2011-01-04)
* [v0.8.0](https://github.com/felixge/node-mysql/compare/v0.7.0...v0.8.0)
  (2010-10-30)
* [v0.7.0](https://github.com/felixge/node-mysql/compare/v0.6.0...v0.7.0)
  (2010-10-14)
* [v0.6.0](https://github.com/felixge/node-mysql/compare/v0.5.0...v0.6.0)
  (2010-09-28)
* [v0.5.0](https://github.com/felixge/node-mysql/compare/v0.4.0...v0.5.0)
  (2010-09-17)
* [v0.4.0](https://github.com/felixge/node-mysql/compare/v0.3.0...v0.4.0)
  (2010-09-02)
* [v0.3.0](https://github.com/felixge/node-mysql/compare/v0.2.0...v0.3.0)
  (2010-08-25)
* [v0.2.0](https://github.com/felixge/node-mysql/compare/v0.1.0...v0.2.0)
  (2010-08-22)
* [v0.1.0](https://github.com/felixge/node-mysql/commits/v0.1.0)
  (2010-08-22)
