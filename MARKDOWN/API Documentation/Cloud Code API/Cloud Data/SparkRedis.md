# SparkRedis

Provides access to the Games Redis Instance.

Rather than copy and paste the excellent documentation from the Redis site, we've opted to link to the relevant page through the documentation.

e.g.

<pre rel="highlighter" code-brush="js" contenteditable="false">var redis = Spark.getRedis();</pre>


## append
_signature_ append(string key, string value)</p>
_returns_ number</p>

See <a href="http://redis.io/commands/${getterMetaData.fullMethodName}">http://redis.io/commands/${getterMetaData.fullMethodName}</a>

## bitcount
_signature_ bitcount(string key)</p>
_returns_ number</p>

See <a href="http://redis.io/commands/${getterMetaData.fullMethodName}">http://redis.io/commands/${getterMetaData.fullMethodName}</a>


_signature_ bitcount(string key, number start, number end)</p>
_returns_ number</p>

See <a href="http://redis.io/commands/${getterMetaData.fullMethodName}">http://redis.io/commands/${getterMetaData.fullMethodName}</a>

## bitop
_signature_ bitop(string op, string destKey, string[] srcKeys)</p>
_returns_ number</p>

See <a href="http://redis.io/commands/${getterMetaData.fullMethodName}">http://redis.io/commands/${getterMetaData.fullMethodName}</a>

## decr
_signature_ decr(string key)</p>
_returns_ number</p>

See <a href="http://redis.io/commands/${getterMetaData.fullMethodName}">http://redis.io/commands/${getterMetaData.fullMethodName}</a>

## decrBy
_signature_ decrBy(string key, number integer)</p>
_returns_ number</p>

See <a href="http://redis.io/commands/${getterMetaData.fullMethodName}">http://redis.io/commands/${getterMetaData.fullMethodName}</a>

## del
_signature_ del(string[] keys)</p>
_returns_ number</p>

See <a href="http://redis.io/commands/${getterMetaData.fullMethodName}">http://redis.io/commands/${getterMetaData.fullMethodName}</a>

## exists
_signature_ exists(string key)</p>
_returns_ boolean</p>

See <a href="http://redis.io/commands/${getterMetaData.fullMethodName}">http://redis.io/commands/${getterMetaData.fullMethodName}</a>

## expire
_signature_ expire(string key, number seconds)</p>
_returns_ number</p>

See <a href="http://redis.io/commands/${getterMetaData.fullMethodName}">http://redis.io/commands/${getterMetaData.fullMethodName}</a>

## expireAt
_signature_ expireAt(string key, number unixTime)</p>
_returns_ number</p>

See <a href="http://redis.io/commands/${getterMetaData.fullMethodName}">http://redis.io/commands/${getterMetaData.fullMethodName}</a>

## get
_signature_ get(string key)</p>
_returns_ string</p>

See <a href="http://redis.io/commands/${getterMetaData.fullMethodName}">http://redis.io/commands/${getterMetaData.fullMethodName}</a>

## getbit
_signature_ getbit(string key, number offset)</p>
_returns_ boolean</p>

See <a href="http://redis.io/commands/${getterMetaData.fullMethodName}">http://redis.io/commands/${getterMetaData.fullMethodName}</a>

## getrange
_signature_ getrange(string key, number startOffset, number endOffset)</p>
_returns_ string</p>

See <a href="http://redis.io/commands/${getterMetaData.fullMethodName}">http://redis.io/commands/${getterMetaData.fullMethodName}</a>

## hdel
_signature_ hdel(string key, string[] fields)</p>
_returns_ number</p>

See <a href="http://redis.io/commands/${getterMetaData.fullMethodName}">http://redis.io/commands/${getterMetaData.fullMethodName}</a>

## hexists
_signature_ hexists(string key, string field)</p>
_returns_ boolean</p>

See <a href="http://redis.io/commands/${getterMetaData.fullMethodName}">http://redis.io/commands/${getterMetaData.fullMethodName}</a>

## hget
_signature_ hget(string key, string field)</p>
_returns_ string</p>

See <a href="http://redis.io/commands/${getterMetaData.fullMethodName}">http://redis.io/commands/${getterMetaData.fullMethodName}</a>

## hgetAll
_signature_ hgetAll(string key)</p>
_returns_ string[]</p>

See <a href="http://redis.io/commands/${getterMetaData.fullMethodName}">http://redis.io/commands/${getterMetaData.fullMethodName}</a>

## hincrBy
_signature_ hincrBy(string key, string field, number value)</p>
_returns_ number</p>

See <a href="http://redis.io/commands/${getterMetaData.fullMethodName}">http://redis.io/commands/${getterMetaData.fullMethodName}</a>

## hincrByFloat
_signature_ hincrByFloat(string key, string field, number increment)</p>
_returns_ number</p>

See <a href="http://redis.io/commands/${getterMetaData.fullMethodName}">http://redis.io/commands/${getterMetaData.fullMethodName}</a>

## hkeys
_signature_ hkeys(string key)</p>
_returns_ string[]</p>

See <a href="http://redis.io/commands/${getterMetaData.fullMethodName}">http://redis.io/commands/${getterMetaData.fullMethodName}</a>

## hlen
_signature_ hlen(string key)</p>
_returns_ number</p>

See <a href="http://redis.io/commands/${getterMetaData.fullMethodName}">http://redis.io/commands/${getterMetaData.fullMethodName}</a>

## hmget
_signature_ hmget(string key, string[] fields)</p>
_returns_ string[]</p>

See <a href="http://redis.io/commands/${getterMetaData.fullMethodName}">http://redis.io/commands/${getterMetaData.fullMethodName}</a>

## hmset
_signature_ hmset(string key, JSON hash)</p>
_returns_ string</p>

See <a href="http://redis.io/commands/${getterMetaData.fullMethodName}">http://redis.io/commands/${getterMetaData.fullMethodName}</a>

## hset
_signature_ hset(string key, string field, string value)</p>
_returns_ number</p>

See <a href="http://redis.io/commands/${getterMetaData.fullMethodName}">http://redis.io/commands/${getterMetaData.fullMethodName}</a>

## hsetnx
_signature_ hsetnx(string key, string field, string value)</p>
_returns_ number</p>

See <a href="http://redis.io/commands/${getterMetaData.fullMethodName}">http://redis.io/commands/${getterMetaData.fullMethodName}</a>

## hvals
_signature_ hvals(string key)</p>
_returns_ string[]</p>

See <a href="http://redis.io/commands/${getterMetaData.fullMethodName}">http://redis.io/commands/${getterMetaData.fullMethodName}</a>

## incr
_signature_ incr(string key)</p>
_returns_ number</p>

See <a href="http://redis.io/commands/${getterMetaData.fullMethodName}">http://redis.io/commands/${getterMetaData.fullMethodName}</a>

## incrBy
_signature_ incrBy(string key, number integer)</p>
_returns_ number</p>

See <a href="http://redis.io/commands/${getterMetaData.fullMethodName}">http://redis.io/commands/${getterMetaData.fullMethodName}</a>

## incrByFloat
_signature_ incrByFloat(string key, number increment)</p>
_returns_ number</p>

See <a href="http://redis.io/commands/${getterMetaData.fullMethodName}">http://redis.io/commands/${getterMetaData.fullMethodName}</a>

## keys
_signature_ keys(string pattern)</p>
_returns_ string[]</p>

See <a href="http://redis.io/commands/${getterMetaData.fullMethodName}">http://redis.io/commands/${getterMetaData.fullMethodName}</a>

## lindex
_signature_ lindex(string key, number index)</p>
_returns_ string</p>

See <a href="http://redis.io/commands/${getterMetaData.fullMethodName}">http://redis.io/commands/${getterMetaData.fullMethodName}</a>

## linsert
_signature_ linsert(string key, string where, string pivit, string value)</p>
_returns_ number</p>

See <a href="http://redis.io/commands/${getterMetaData.fullMethodName}">http://redis.io/commands/${getterMetaData.fullMethodName}</a>

## llen
_signature_ llen(string key)</p>
_returns_ number</p>

See <a href="http://redis.io/commands/${getterMetaData.fullMethodName}">http://redis.io/commands/${getterMetaData.fullMethodName}</a>

## lpop
_signature_ lpop(string key)</p>
_returns_ string</p>

See <a href="http://redis.io/commands/${getterMetaData.fullMethodName}">http://redis.io/commands/${getterMetaData.fullMethodName}</a>

## lpush
_signature_ lpush(string key, string[] strings)</p>
_returns_ number</p>

See <a href="http://redis.io/commands/${getterMetaData.fullMethodName}">http://redis.io/commands/${getterMetaData.fullMethodName}</a>

## lpushx
_signature_ lpushx(string key, string[] strings)</p>
_returns_ number</p>

See <a href="http://redis.io/commands/${getterMetaData.fullMethodName}">http://redis.io/commands/${getterMetaData.fullMethodName}</a>

## lrange
_signature_ lrange(string key, number start, number end)</p>
_returns_ string[]</p>

See <a href="http://redis.io/commands/${getterMetaData.fullMethodName}">http://redis.io/commands/${getterMetaData.fullMethodName}</a>

## lrem
_signature_ lrem(string key, number count, string value)</p>
_returns_ number</p>

See <a href="http://redis.io/commands/${getterMetaData.fullMethodName}">http://redis.io/commands/${getterMetaData.fullMethodName}</a>

## lset
_signature_ lset(string key, number index, string value)</p>
_returns_ string</p>

See <a href="http://redis.io/commands/${getterMetaData.fullMethodName}">http://redis.io/commands/${getterMetaData.fullMethodName}</a>

## ltrim
_signature_ ltrim(string key, number start, number end)</p>
_returns_ string</p>

See <a href="http://redis.io/commands/${getterMetaData.fullMethodName}">http://redis.io/commands/${getterMetaData.fullMethodName}</a>

## mget
_signature_ mget(string[] keys)</p>
_returns_ string[]</p>

See <a href="http://redis.io/commands/${getterMetaData.fullMethodName}">http://redis.io/commands/${getterMetaData.fullMethodName}</a>

## mset
_signature_ mset(string[] keysvalues)</p>
_returns_ string</p>

See <a href="http://redis.io/commands/${getterMetaData.fullMethodName}">http://redis.io/commands/${getterMetaData.fullMethodName}</a>

## msetnx
_signature_ msetnx(string[] keysvalues)</p>
_returns_ number</p>

See <a href="http://redis.io/commands/${getterMetaData.fullMethodName}">http://redis.io/commands/${getterMetaData.fullMethodName}</a>

## persist
_signature_ persist(string key)</p>
_returns_ number</p>

See <a href="http://redis.io/commands/${getterMetaData.fullMethodName}">http://redis.io/commands/${getterMetaData.fullMethodName}</a>

## pexpire
_signature_ pexpire(string key, number milliseconds)</p>
_returns_ number</p>

See <a href="http://redis.io/commands/${getterMetaData.fullMethodName}">http://redis.io/commands/${getterMetaData.fullMethodName}</a>

## pexpireAt
_signature_ pexpireAt(string key, number millisecondsTimestamp)</p>
_returns_ number</p>

See <a href="http://redis.io/commands/${getterMetaData.fullMethodName}">http://redis.io/commands/${getterMetaData.fullMethodName}</a>

## psetex
_signature_ psetex(string key, number milliseconds, string value)</p>
_returns_ string</p>

See <a href="http://redis.io/commands/${getterMetaData.fullMethodName}">http://redis.io/commands/${getterMetaData.fullMethodName}</a>

## pttl
_signature_ pttl(string key)</p>
_returns_ number</p>

See <a href="http://redis.io/commands/${getterMetaData.fullMethodName}">http://redis.io/commands/${getterMetaData.fullMethodName}</a>

## rename
_signature_ rename(string oldkey, string newkey)</p>
_returns_ string</p>

See <a href="http://redis.io/commands/${getterMetaData.fullMethodName}">http://redis.io/commands/${getterMetaData.fullMethodName}</a>

## renamenx
_signature_ renamenx(string oldkey, string newkey)</p>
_returns_ number</p>

See <a href="http://redis.io/commands/${getterMetaData.fullMethodName}">http://redis.io/commands/${getterMetaData.fullMethodName}</a>

## rpop
_signature_ rpop(string key)</p>
_returns_ string</p>

See <a href="http://redis.io/commands/${getterMetaData.fullMethodName}">http://redis.io/commands/${getterMetaData.fullMethodName}</a>

## rpoplpush
_signature_ rpoplpush(string srckey, string dstkey)</p>
_returns_ string</p>

See <a href="http://redis.io/commands/${getterMetaData.fullMethodName}">http://redis.io/commands/${getterMetaData.fullMethodName}</a>

## rpush
_signature_ rpush(string key, string[] strings)</p>
_returns_ number</p>

See <a href="http://redis.io/commands/${getterMetaData.fullMethodName}">http://redis.io/commands/${getterMetaData.fullMethodName}</a>

## rpushx
_signature_ rpushx(string key, string[] strings)</p>
_returns_ number</p>

See <a href="http://redis.io/commands/${getterMetaData.fullMethodName}">http://redis.io/commands/${getterMetaData.fullMethodName}</a>

## sadd
_signature_ sadd(string key, string[] members)</p>
_returns_ number</p>

See <a href="http://redis.io/commands/${getterMetaData.fullMethodName}">http://redis.io/commands/${getterMetaData.fullMethodName}</a>

## scard
_signature_ scard(string key)</p>
_returns_ number</p>

See <a href="http://redis.io/commands/${getterMetaData.fullMethodName}">http://redis.io/commands/${getterMetaData.fullMethodName}</a>

## sdiff
_signature_ sdiff(string[] keys)</p>
_returns_ string[]</p>

See <a href="http://redis.io/commands/${getterMetaData.fullMethodName}">http://redis.io/commands/${getterMetaData.fullMethodName}</a>

## sdiffstore
_signature_ sdiffstore(string dstkey, string[] keys)</p>
_returns_ number</p>

See <a href="http://redis.io/commands/${getterMetaData.fullMethodName}">http://redis.io/commands/${getterMetaData.fullMethodName}</a>

## set
_signature_ set(string key, string value, string nxxx, string expx, number time)</p>
_returns_ string</p>

See <a href="http://redis.io/commands/${getterMetaData.fullMethodName}">http://redis.io/commands/${getterMetaData.fullMethodName}</a>


_signature_ set(string key, string value, string nxxx)</p>
_returns_ string</p>

See <a href="http://redis.io/commands/${getterMetaData.fullMethodName}">http://redis.io/commands/${getterMetaData.fullMethodName}</a>


_signature_ set(string key, string value)</p>
_returns_ string</p>

See <a href="http://redis.io/commands/${getterMetaData.fullMethodName}">http://redis.io/commands/${getterMetaData.fullMethodName}</a>


_signature_ set(string key, string value, string nxxx, string expx, number time)</p>
_returns_ string</p>

See <a href="http://redis.io/commands/${getterMetaData.fullMethodName}">http://redis.io/commands/${getterMetaData.fullMethodName}</a>

## getSet
_signature_ getSet(string key, string value)</p>
_returns_ string</p>

See <a href="http://redis.io/commands/${getterMetaData.fullMethodName}">http://redis.io/commands/${getterMetaData.fullMethodName}</a>

## setbit
_signature_ setbit(string key, number offset, boolean value)</p>
_returns_ boolean</p>

See <a href="http://redis.io/commands/${getterMetaData.fullMethodName}">http://redis.io/commands/${getterMetaData.fullMethodName}</a>

## setex
_signature_ setex(string key, number seconds, string value)</p>
_returns_ string</p>

See <a href="http://redis.io/commands/${getterMetaData.fullMethodName}">http://redis.io/commands/${getterMetaData.fullMethodName}</a>

## setnx
_signature_ setnx(string key, string value)</p>
_returns_ number</p>

See <a href="http://redis.io/commands/${getterMetaData.fullMethodName}">http://redis.io/commands/${getterMetaData.fullMethodName}</a>

## setrange
_signature_ setrange(string key, number offset, string value)</p>
_returns_ number</p>

See <a href="http://redis.io/commands/${getterMetaData.fullMethodName}">http://redis.io/commands/${getterMetaData.fullMethodName}</a>

## sinter
_signature_ sinter(string[] keys)</p>
_returns_ string[]</p>

See <a href="http://redis.io/commands/${getterMetaData.fullMethodName}">http://redis.io/commands/${getterMetaData.fullMethodName}</a>

## sinterstore
_signature_ sinterstore(string dstkey, string[] keys)</p>
_returns_ number</p>

See <a href="http://redis.io/commands/${getterMetaData.fullMethodName}">http://redis.io/commands/${getterMetaData.fullMethodName}</a>

## sismember
_signature_ sismember(string key, string member)</p>
_returns_ boolean</p>

See <a href="http://redis.io/commands/${getterMetaData.fullMethodName}">http://redis.io/commands/${getterMetaData.fullMethodName}</a>

## smembers
_signature_ smembers(string key)</p>
_returns_ string[]</p>

See <a href="http://redis.io/commands/${getterMetaData.fullMethodName}">http://redis.io/commands/${getterMetaData.fullMethodName}</a>

## smove
_signature_ smove(string srckey, string dstkey, string member)</p>
_returns_ number</p>

See <a href="http://redis.io/commands/${getterMetaData.fullMethodName}">http://redis.io/commands/${getterMetaData.fullMethodName}</a>

## sort
_signature_ sort(string key, string dstkey)</p>
_returns_ number</p>

See <a href="http://redis.io/commands/${getterMetaData.fullMethodName}">http://redis.io/commands/${getterMetaData.fullMethodName}</a>


_signature_ sort(string key)</p>
_returns_ string[]</p>

See <a href="http://redis.io/commands/${getterMetaData.fullMethodName}">http://redis.io/commands/${getterMetaData.fullMethodName}</a>

## spop
_signature_ spop(string key)</p>
_returns_ string</p>

See <a href="http://redis.io/commands/${getterMetaData.fullMethodName}">http://redis.io/commands/${getterMetaData.fullMethodName}</a>

## srandmember
_signature_ srandmember(string key, number count)</p>
_returns_ string[]</p>

See <a href="http://redis.io/commands/${getterMetaData.fullMethodName}">http://redis.io/commands/${getterMetaData.fullMethodName}</a>


_signature_ srandmember(string key)</p>
_returns_ string</p>

See <a href="http://redis.io/commands/${getterMetaData.fullMethodName}">http://redis.io/commands/${getterMetaData.fullMethodName}</a>

## srem
_signature_ srem(string key, string[] members)</p>
_returns_ number</p>

See <a href="http://redis.io/commands/${getterMetaData.fullMethodName}">http://redis.io/commands/${getterMetaData.fullMethodName}</a>

## strlen
_signature_ strlen(string key)</p>
_returns_ number</p>

See <a href="http://redis.io/commands/${getterMetaData.fullMethodName}">http://redis.io/commands/${getterMetaData.fullMethodName}</a>

## substr
_signature_ substr(string key, number start, number end)</p>
_returns_ string</p>

See <a href="http://redis.io/commands/${getterMetaData.fullMethodName}">http://redis.io/commands/${getterMetaData.fullMethodName}</a>

## sunion
_signature_ sunion(string[] keys)</p>
_returns_ string[]</p>

See <a href="http://redis.io/commands/${getterMetaData.fullMethodName}">http://redis.io/commands/${getterMetaData.fullMethodName}</a>

## sunionstore
_signature_ sunionstore(string dstkey, string[] keys)</p>
_returns_ number</p>

See <a href="http://redis.io/commands/${getterMetaData.fullMethodName}">http://redis.io/commands/${getterMetaData.fullMethodName}</a>

## ttl
_signature_ ttl(string key)</p>
_returns_ number</p>

See <a href="http://redis.io/commands/${getterMetaData.fullMethodName}">http://redis.io/commands/${getterMetaData.fullMethodName}</a>

## type
_signature_ type(string key)</p>
_returns_ string</p>

See <a href="http://redis.io/commands/${getterMetaData.fullMethodName}">http://redis.io/commands/${getterMetaData.fullMethodName}</a>

## zadd
_signature_ zadd(string key, number score, string member)</p>
_returns_ number</p>

See <a href="http://redis.io/commands/${getterMetaData.fullMethodName}">http://redis.io/commands/${getterMetaData.fullMethodName}</a>

## zcard
_signature_ zcard(string key)</p>
_returns_ number</p>

See <a href="http://redis.io/commands/${getterMetaData.fullMethodName}">http://redis.io/commands/${getterMetaData.fullMethodName}</a>

## zcount
_signature_ zcount(string key, string min, string max)</p>
_returns_ number</p>

See <a href="http://redis.io/commands/${getterMetaData.fullMethodName}">http://redis.io/commands/${getterMetaData.fullMethodName}</a>


_signature_ zcount(string key, number min, number max)</p>
_returns_ number</p>

See <a href="http://redis.io/commands/${getterMetaData.fullMethodName}">http://redis.io/commands/${getterMetaData.fullMethodName}</a>

## zincrby
_signature_ zincrby(string key, number score, string member)</p>
_returns_ number</p>

See <a href="http://redis.io/commands/${getterMetaData.fullMethodName}">http://redis.io/commands/${getterMetaData.fullMethodName}</a>

## zinterstore
_signature_ zinterstore(string dstkey, string[] sets)</p>
_returns_ number</p>

See <a href="http://redis.io/commands/${getterMetaData.fullMethodName}">http://redis.io/commands/${getterMetaData.fullMethodName}</a>

## zrange
_signature_ zrange(string key, number start, number end)</p>
_returns_ string[]</p>

See <a href="http://redis.io/commands/${getterMetaData.fullMethodName}">http://redis.io/commands/${getterMetaData.fullMethodName}</a>

## zrangeByScore
_signature_ zrangeByScore(string key, number min, number max)</p>
_returns_ string[]</p>

See <a href="http://redis.io/commands/${getterMetaData.fullMethodName}">http://redis.io/commands/${getterMetaData.fullMethodName}</a>


_signature_ zrangeByScore(string key, string min, string max)</p>
_returns_ string[]</p>

See <a href="http://redis.io/commands/${getterMetaData.fullMethodName}">http://redis.io/commands/${getterMetaData.fullMethodName}</a>


_signature_ zrangeByScore(string key, string min, string max, number offset, number count)</p>
_returns_ string[]</p>

See <a href="http://redis.io/commands/${getterMetaData.fullMethodName}">http://redis.io/commands/${getterMetaData.fullMethodName}</a>


_signature_ zrangeByScore(string key, number min, number max, number offset, number count)</p>
_returns_ string[]</p>

See <a href="http://redis.io/commands/${getterMetaData.fullMethodName}">http://redis.io/commands/${getterMetaData.fullMethodName}</a>

## zrangeByScoreWithScores
_signature_ zrangeByScoreWithScores(string key, string min, string max)</p>
_returns_ JSON</p>

See <a href="http://redis.io/commands/${getterMetaData.fullMethodName}">http://redis.io/commands/${getterMetaData.fullMethodName}</a>


_signature_ zrangeByScoreWithScores(string key, number min, number max, number offset, number count)</p>
_returns_ JSON</p>

See <a href="http://redis.io/commands/${getterMetaData.fullMethodName}">http://redis.io/commands/${getterMetaData.fullMethodName}</a>


_signature_ zrangeByScoreWithScores(string key, number min, number max)</p>
_returns_ JSON</p>

See <a href="http://redis.io/commands/${getterMetaData.fullMethodName}">http://redis.io/commands/${getterMetaData.fullMethodName}</a>


_signature_ zrangeByScoreWithScores(string key, string min, string max, number offset, number count)</p>
_returns_ JSON</p>

See <a href="http://redis.io/commands/${getterMetaData.fullMethodName}">http://redis.io/commands/${getterMetaData.fullMethodName}</a>

## zrangeWithScores
_signature_ zrangeWithScores(string key, number start, number end)</p>
_returns_ JSON</p>

See <a href="http://redis.io/commands/${getterMetaData.fullMethodName}">http://redis.io/commands/${getterMetaData.fullMethodName}</a>

## zrank
_signature_ zrank(string key, string member)</p>
_returns_ number</p>

See <a href="http://redis.io/commands/${getterMetaData.fullMethodName}">http://redis.io/commands/${getterMetaData.fullMethodName}</a>

## zrem
_signature_ zrem(string key, string[] members)</p>
_returns_ number</p>

See <a href="http://redis.io/commands/${getterMetaData.fullMethodName}">http://redis.io/commands/${getterMetaData.fullMethodName}</a>

## zremrangeByRank
_signature_ zremrangeByRank(string key, number start, number end)</p>
_returns_ number</p>

See <a href="http://redis.io/commands/${getterMetaData.fullMethodName}">http://redis.io/commands/${getterMetaData.fullMethodName}</a>

## zremrangeByScore
_signature_ zremrangeByScore(string key, number start, number end)</p>
_returns_ number</p>

See <a href="http://redis.io/commands/${getterMetaData.fullMethodName}">http://redis.io/commands/${getterMetaData.fullMethodName}</a>


_signature_ zremrangeByScore(string key, string start, string end)</p>
_returns_ number</p>

See <a href="http://redis.io/commands/${getterMetaData.fullMethodName}">http://redis.io/commands/${getterMetaData.fullMethodName}</a>

## zrevrange
_signature_ zrevrange(string key, number start, number end)</p>
_returns_ string[]</p>

See <a href="http://redis.io/commands/${getterMetaData.fullMethodName}">http://redis.io/commands/${getterMetaData.fullMethodName}</a>

## zrevrangeByScore
_signature_ zrevrangeByScore(string key, number max, number min, number offset, number count)</p>
_returns_ string[]</p>

See <a href="http://redis.io/commands/${getterMetaData.fullMethodName}">http://redis.io/commands/${getterMetaData.fullMethodName}</a>


_signature_ zrevrangeByScore(string key, number max, number min)</p>
_returns_ string[]</p>

See <a href="http://redis.io/commands/${getterMetaData.fullMethodName}">http://redis.io/commands/${getterMetaData.fullMethodName}</a>


_signature_ zrevrangeByScore(string key, string max, string min)</p>
_returns_ string[]</p>

See <a href="http://redis.io/commands/${getterMetaData.fullMethodName}">http://redis.io/commands/${getterMetaData.fullMethodName}</a>


_signature_ zrevrangeByScore(string key, string max, string min, number offset, number count)</p>
_returns_ string[]</p>

See <a href="http://redis.io/commands/${getterMetaData.fullMethodName}">http://redis.io/commands/${getterMetaData.fullMethodName}</a>

## zrevrangeByScoreWithScores
_signature_ zrevrangeByScoreWithScores(string key, number max, number min, number offset, number count)</p>
_returns_ JSON</p>

See <a href="http://redis.io/commands/${getterMetaData.fullMethodName}">http://redis.io/commands/${getterMetaData.fullMethodName}</a>


_signature_ zrevrangeByScoreWithScores(string key, string max, string min)</p>
_returns_ JSON</p>

See <a href="http://redis.io/commands/${getterMetaData.fullMethodName}">http://redis.io/commands/${getterMetaData.fullMethodName}</a>


_signature_ zrevrangeByScoreWithScores(string key, number max, number min)</p>
_returns_ JSON</p>

See <a href="http://redis.io/commands/${getterMetaData.fullMethodName}">http://redis.io/commands/${getterMetaData.fullMethodName}</a>


_signature_ zrevrangeByScoreWithScores(string key, string max, string min, number offset, number count)</p>
_returns_ JSON</p>

See <a href="http://redis.io/commands/${getterMetaData.fullMethodName}">http://redis.io/commands/${getterMetaData.fullMethodName}</a>

## zrevrangeWithScores
_signature_ zrevrangeWithScores(string key, number start, number end)</p>
_returns_ JSON</p>

See <a href="http://redis.io/commands/${getterMetaData.fullMethodName}">http://redis.io/commands/${getterMetaData.fullMethodName}</a>

## zrevrank
_signature_ zrevrank(string key, string member)</p>
_returns_ number</p>

See <a href="http://redis.io/commands/${getterMetaData.fullMethodName}">http://redis.io/commands/${getterMetaData.fullMethodName}</a>

## zscore
_signature_ zscore(string key, string member)</p>
_returns_ number</p>

See <a href="http://redis.io/commands/${getterMetaData.fullMethodName}">http://redis.io/commands/${getterMetaData.fullMethodName}</a>

## zunionstore
_signature_ zunionstore(string dstkey, string[] sets)</p>
_returns_ number</p>

See <a href="http://redis.io/commands/${getterMetaData.fullMethodName}">http://redis.io/commands/${getterMetaData.fullMethodName}</a>

