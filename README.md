# winston-ravendb

A RavenDB transport for [winston][0].

## Usage
``` js
module.exports["should return elapsed time/ticks in zero when not started"] = function(test) {
	test.expect(3);

	var stopwatch = Stopwatch.create();
	test.equal(stopwatch.isRunning, false);
	test.equal(stopwatch.elapsedMilliseconds, 0);
	test.equal(stopwatch.elapsedTicks, 0);

	test.done();
};

module.exports["should return elapsed time/ticks not in zero when started"] = function(test) {
	test.expect(3);

	var stopwatch = Stopwatch.create();

	stopwatch.start();

	sleep.sleep(2);

	stopwatch.stop();

	test.equal(stopwatch.isRunning, false);
	test.ok(stopwatch.elapsedMilliseconds > 0);
	test.ok(stopwatch.elapsedTicks > 0);

	test.done();
};

module.exports["should return elapsed time/ticks not in zero when restarted"] = function(test) {
	test.expect(3);

	var stopwatch = Stopwatch.create();

	stopwatch.restart();

	sleep.sleep(2);

	stopwatch.stop();

	test.equal(stopwatch.isRunning, false);
	test.ok(stopwatch.elapsedMilliseconds > 0);
	test.ok(stopwatch.elapsedTicks > 0);

	test.done();
};

module.exports["should return elapsed time/ticks in zero after reset"] = function(test) {
	test.expect(3);

	var stopwatch = Stopwatch.create();

	stopwatch.start();

	sleep.sleep(2);

	stopwatch.stop();
	stopwatch.reset();

	test.equal(stopwatch.isRunning, false);
	test.equal(stopwatch.elapsedMilliseconds, 0);
	test.equal(stopwatch.elapsedTicks, 0);

	test.done();
};```

###Queries

#### Filter by level

``` js
logger.query({level: "error"}, function(err, results) {
	if(err) {
		//error handling
	}
	//do something
});
```

#### Filter by dates

``` js
logger.query({from: "2013-01-01", to: 2013-12-31}, function(err, results) {
	if(err) {
		//error handling
	}
	//do something
});
```

#### Filter using lucene

``` js
logger.luceneQuery("myQuickIndex", "timestamp:[2013-01-01 TO 2013-04-02] AND level:NULL", function(err, results) {
	if(err) {
		//error handling
	}
	//do something
});
```

#### Filter using fluent api

``` js
logger.query("myCustomQuickIndex")
	.where("level")
	.is("error")
	.results(function(err, results) {
		if(err) {
			//error handling
		}
		//do something
	});
```

The RavenDB transport takes the following options:

* __level:__ Level of messages that this transport should log, defaults to 'info'.
* __entityName:__ 'Raven-Entity-Name' in RavenDB , defaults to 'Log'.
* __connectionString:__ The connection string for connecting to RavenDB.
* __database:__ The name of the database you want to log to.
* __serverUrl:__ The url where RavenDB is running (required if no connectionString supplied).
* __username:__ The username for conencting to RavenDB (required if no connectionString supplied and depending on RavenDB authentication).
* __password:__ The password for conencting to RavenDB (required if no connectionString supplied and depending on RavenDB authentication).
* __apiKey:__  The apiKey for conencting to RavenDB (required if no connectionString supplied and depending on RavenDB authentication).
* __proxyUrl:__ Proxy url if needed.

## Installation

### Installing stopwacht

``` bash
  $ npm install winston
  $ npm install winston-ravendb
```