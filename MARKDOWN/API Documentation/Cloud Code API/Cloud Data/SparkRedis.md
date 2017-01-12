# SparkRedis

Provides access to the Games Redis Instance.
Rather than copy and paste the excellent documentation from the Redis site, we've opted to link to the relevant page through the documentation.
e.g.
<pre rel="highlighter" code-brush="js" contenteditable="false">var redis = Spark.getRedis();</pre>

## append
_signature_ append(string key, string value)</p>
_returns_ number</p>

See <a href="http://redis.io/commands/append">http://redis.io/commands/append</a>
## bitcount
_signature_ bitcount(string key)</p>
_returns_ number</p>

See <a href="http://redis.io/commands/bitcount">http://redis.io/commands/bitcount</a>

_signature_ bitcount(string key, number start, number end)</p>
_returns_ number</p>

See <a href="http://redis.io/commands/bitcount">http://redis.io/commands/bitcount</a>
## bitop
_signature_ bitop(string op, string destKey, string[] srcKeys)</p>
_returns_ number</p>

See <a href="http://redis.io/commands/bitop">http://redis.io/commands/bitop</a>
## decr
_signature_ decr(string key)</p>
_returns_ number</p>

See <a href="http://redis.io/commands/decr">http://redis.io/commands/decr</a>
## decrBy
_signature_ decrBy(string key, number integer)</p>
_returns_ number</p>

See <a href="http://redis.io/commands/decrBy">http://redis.io/commands/decrBy</a>
## del
_signature_ del(string[] keys)</p>
_returns_ number</p>

See <a href="http://redis.io/commands/del">http://redis.io/commands/del</a>
## exists
_signature_ exists(string key)</p>
_returns_ boolean</p>

See <a href="http://redis.io/commands/exists">http://redis.io/commands/exists</a>
## expire
_signature_ expire(string key, number seconds)</p>
_returns_ number</p>

See <a href="http://redis.io/commands/expire">http://redis.io/commands/expire</a>
## expireAt
_signature_ expireAt(string key, number unixTime)</p>
_returns_ number</p>

See <a href="http://redis.io/commands/expireAt">http://redis.io/commands/expireAt</a>
## flushdb
_signature_ flushdb()</p>
_returns_ string</p>

See <a href="http://redis.io/commands/flushdb">http://redis.io/commands/flushdb</a>
## get
_signature_ get(string key)</p>
_returns_ string</p>

See <a href="http://redis.io/commands/get">http://redis.io/commands/get</a>
## getbit
_signature_ getbit(string key, number offset)</p>
_returns_ boolean</p>

See <a href="http://redis.io/commands/getbit">http://redis.io/commands/getbit</a>
## getrange
_signature_ getrange(string key, number startOffset, number endOffset)</p>
_returns_ string</p>

See <a href="http://redis.io/commands/getrange">http://redis.io/commands/getrange</a>
## hdel
_signature_ hdel(string key, string[] fields)</p>
_returns_ number</p>

See <a href="http://redis.io/commands/hdel">http://redis.io/commands/hdel</a>
## hexists
_signature_ hexists(string key, string field)</p>
_returns_ boolean</p>

See <a href="http://redis.io/commands/hexists">http://redis.io/commands/hexists</a>
## hget
_signature_ hget(string key, string field)</p>
_returns_ string</p>

See <a href="http://redis.io/commands/hget">http://redis.io/commands/hget</a>
## hgetAll
_signature_ hgetAll(string key)</p>
_returns_ string[]</p>

See <a href="http://redis.io/commands/hgetAll">http://redis.io/commands/hgetAll</a>
## hincrBy
_signature_ hincrBy(string key, string field, number value)</p>
_returns_ number</p>

See <a href="http://redis.io/commands/hincrBy">http://redis.io/commands/hincrBy</a>
## hincrByFloat
_signature_ hincrByFloat(string key, string field, number increment)</p>
_returns_ number</p>

See <a href="http://redis.io/commands/hincrByFloat">http://redis.io/commands/hincrByFloat</a>
## hkeys
_signature_ hkeys(string key)</p>
_returns_ string[]</p>

See <a href="http://redis.io/commands/hkeys">http://redis.io/commands/hkeys</a>
## hlen
_signature_ hlen(string key)</p>
_returns_ number</p>

See <a href="http://redis.io/commands/hlen">http://redis.io/commands/hlen</a>
## hmget
_signature_ hmget(string key, string[] fields)</p>
_returns_ string[]</p>

See <a href="http://redis.io/commands/hmget">http://redis.io/commands/hmget</a>
## hmset
_signature_ hmset(string key, JSON hash)</p>
_returns_ string</p>

See <a href="http://redis.io/commands/hmset">http://redis.io/commands/hmset</a>
## hset
_signature_ hset(string key, string field, string value)</p>
_returns_ number</p>

See <a href="http://redis.io/commands/hset">http://redis.io/commands/hset</a>
## hsetnx
_signature_ hsetnx(string key, string field, string value)</p>
_returns_ number</p>

See <a href="http://redis.io/commands/hsetnx">http://redis.io/commands/hsetnx</a>
## hvals
_signature_ hvals(string key)</p>
_returns_ string[]</p>

See <a href="http://redis.io/commands/hvals">http://redis.io/commands/hvals</a>
## incr
_signature_ incr(string key)</p>
_returns_ number</p>

See <a href="http://redis.io/commands/incr">http://redis.io/commands/incr</a>
## incrBy
_signature_ incrBy(string key, number integer)</p>
_returns_ number</p>

See <a href="http://redis.io/commands/incrBy">http://redis.io/commands/incrBy</a>
## incrByFloat
_signature_ incrByFloat(string key, number increment)</p>
_returns_ number</p>

See <a href="http://redis.io/commands/incrByFloat">http://redis.io/commands/incrByFloat</a>
## keys
_signature_ keys(string pattern)</p>
_returns_ string[]</p>

See <a href="http://redis.io/commands/keys">http://redis.io/commands/keys</a>
## lindex
_signature_ lindex(string key, number index)</p>
_returns_ string</p>

See <a href="http://redis.io/commands/lindex">http://redis.io/commands/lindex</a>
## linsert
_signature_ linsert(string key, string where, string pivit, string value)</p>
_returns_ number</p>

See <a href="http://redis.io/commands/linsert">http://redis.io/commands/linsert</a>
## llen
_signature_ llen(string key)</p>
_returns_ number</p>

See <a href="http://redis.io/commands/llen">http://redis.io/commands/llen</a>
## lpop
_signature_ lpop(string key)</p>
_returns_ string</p>

See <a href="http://redis.io/commands/lpop">http://redis.io/commands/lpop</a>
## lpush
_signature_ lpush(string key, string[] strings)</p>
_returns_ number</p>

See <a href="http://redis.io/commands/lpush">http://redis.io/commands/lpush</a>
## lpushx
_signature_ lpushx(string key, string[] strings)</p>
_returns_ number</p>

See <a href="http://redis.io/commands/lpushx">http://redis.io/commands/lpushx</a>
## lrange
_signature_ lrange(string key, number start, number end)</p>
_returns_ string[]</p>

See <a href="http://redis.io/commands/lrange">http://redis.io/commands/lrange</a>
## lrem
_signature_ lrem(string key, number count, string value)</p>
_returns_ number</p>

See <a href="http://redis.io/commands/lrem">http://redis.io/commands/lrem</a>
## lset
_signature_ lset(string key, number index, string value)</p>
_returns_ string</p>

See <a href="http://redis.io/commands/lset">http://redis.io/commands/lset</a>
## ltrim
_signature_ ltrim(string key, number start, number end)</p>
_returns_ string</p>

See <a href="http://redis.io/commands/ltrim">http://redis.io/commands/ltrim</a>
## mget
_signature_ mget(string[] keys)</p>
_returns_ string[]</p>

See <a href="http://redis.io/commands/mget">http://redis.io/commands/mget</a>
## mset
_signature_ mset(string[] keysvalues)</p>
_returns_ string</p>

See <a href="http://redis.io/commands/mset">http://redis.io/commands/mset</a>
## msetnx
_signature_ msetnx(string[] keysvalues)</p>
_returns_ number</p>

See <a href="http://redis.io/commands/msetnx">http://redis.io/commands/msetnx</a>
## persist
_signature_ persist(string key)</p>
_returns_ number</p>

See <a href="http://redis.io/commands/persist">http://redis.io/commands/persist</a>
## pexpire
_signature_ pexpire(string key, number milliseconds)</p>
_returns_ number</p>

See <a href="http://redis.io/commands/pexpire">http://redis.io/commands/pexpire</a>
## pexpireAt
_signature_ pexpireAt(string key, number millisecondsTimestamp)</p>
_returns_ number</p>

See <a href="http://redis.io/commands/pexpireAt">http://redis.io/commands/pexpireAt</a>
## psetex
_signature_ psetex(string key, number milliseconds, string value)</p>
_returns_ string</p>

See <a href="http://redis.io/commands/psetex">http://redis.io/commands/psetex</a>
## pttl
_signature_ pttl(string key)</p>
_returns_ number</p>

See <a href="http://redis.io/commands/pttl">http://redis.io/commands/pttl</a>
## rename
_signature_ rename(string oldkey, string newkey)</p>
_returns_ string</p>

See <a href="http://redis.io/commands/rename">http://redis.io/commands/rename</a>
## renamenx
_signature_ renamenx(string oldkey, string newkey)</p>
_returns_ number</p>

See <a href="http://redis.io/commands/renamenx">http://redis.io/commands/renamenx</a>
## rpop
_signature_ rpop(string key)</p>
_returns_ string</p>

See <a href="http://redis.io/commands/rpop">http://redis.io/commands/rpop</a>
## rpoplpush
_signature_ rpoplpush(string srckey, string dstkey)</p>
_returns_ string</p>

See <a href="http://redis.io/commands/rpoplpush">http://redis.io/commands/rpoplpush</a>
## rpush
_signature_ rpush(string key, string[] strings)</p>
_returns_ number</p>

See <a href="http://redis.io/commands/rpush">http://redis.io/commands/rpush</a>
## rpushx
_signature_ rpushx(string key, string[] strings)</p>
_returns_ number</p>

See <a href="http://redis.io/commands/rpushx">http://redis.io/commands/rpushx</a>
## sadd
_signature_ sadd(string key, string[] members)</p>
_returns_ number</p>

See <a href="http://redis.io/commands/sadd">http://redis.io/commands/sadd</a>
## scard
_signature_ scard(string key)</p>
_returns_ number</p>

See <a href="http://redis.io/commands/scard">http://redis.io/commands/scard</a>
## sdiff
_signature_ sdiff(string[] keys)</p>
_returns_ string[]</p>

See <a href="http://redis.io/commands/sdiff">http://redis.io/commands/sdiff</a>
## sdiffstore
_signature_ sdiffstore(string dstkey, string[] keys)</p>
_returns_ number</p>

See <a href="http://redis.io/commands/sdiffstore">http://redis.io/commands/sdiffstore</a>
## set
_signature_ set(string key, string value, string nxxx, string expx, number time)</p>
_returns_ string</p>

See <a href="http://redis.io/commands/set">http://redis.io/commands/set</a>

_signature_ set(string key, string value, string nxxx, string expx, number time)</p>
_returns_ string</p>

See <a href="http://redis.io/commands/set">http://redis.io/commands/set</a>

_signature_ set(string key, string value, string nxxx)</p>
_returns_ string</p>

See <a href="http://redis.io/commands/set">http://redis.io/commands/set</a>

_signature_ set(string key, string value)</p>
_returns_ string</p>

See <a href="http://redis.io/commands/set">http://redis.io/commands/set</a>
## getSet
_signature_ getSet(string key, string value)</p>
_returns_ string</p>

See <a href="http://redis.io/commands/getSet">http://redis.io/commands/getSet</a>
## setbit
_signature_ setbit(string key, number offset, boolean value)</p>
_returns_ boolean</p>

See <a href="http://redis.io/commands/setbit">http://redis.io/commands/setbit</a>
## setex
_signature_ setex(string key, number seconds, string value)</p>
_returns_ string</p>

See <a href="http://redis.io/commands/setex">http://redis.io/commands/setex</a>
## setnx
_signature_ setnx(string key, string value)</p>
_returns_ number</p>

See <a href="http://redis.io/commands/setnx">http://redis.io/commands/setnx</a>
## setrange
_signature_ setrange(string key, number offset, string value)</p>
_returns_ number</p>

See <a href="http://redis.io/commands/setrange">http://redis.io/commands/setrange</a>
## sinter
_signature_ sinter(string[] keys)</p>
_returns_ string[]</p>

See <a href="http://redis.io/commands/sinter">http://redis.io/commands/sinter</a>
## sinterstore
_signature_ sinterstore(string dstkey, string[] keys)</p>
_returns_ number</p>

See <a href="http://redis.io/commands/sinterstore">http://redis.io/commands/sinterstore</a>
## sismember
_signature_ sismember(string key, string member)</p>
_returns_ boolean</p>

See <a href="http://redis.io/commands/sismember">http://redis.io/commands/sismember</a>
## smembers
_signature_ smembers(string key)</p>
_returns_ string[]</p>

See <a href="http://redis.io/commands/smembers">http://redis.io/commands/smembers</a>
## smove
_signature_ smove(string srckey, string dstkey, string member)</p>
_returns_ number</p>

See <a href="http://redis.io/commands/smove">http://redis.io/commands/smove</a>
## sort
_signature_ sort(string key)</p>
_returns_ string[]</p>

See <a href="http://redis.io/commands/sort">http://redis.io/commands/sort</a>

_signature_ sort(string key, string dstkey)</p>
_returns_ number</p>

See <a href="http://redis.io/commands/sort">http://redis.io/commands/sort</a>
## spop
_signature_ spop(string key)</p>
_returns_ string</p>

See <a href="http://redis.io/commands/spop">http://redis.io/commands/spop</a>
## srandmember
_signature_ srandmember(string key, number count)</p>
_returns_ string[]</p>

See <a href="http://redis.io/commands/srandmember">http://redis.io/commands/srandmember</a>

_signature_ srandmember(string key)</p>
_returns_ string</p>

See <a href="http://redis.io/commands/srandmember">http://redis.io/commands/srandmember</a>
## srem
_signature_ srem(string key, string[] members)</p>
_returns_ number</p>

See <a href="http://redis.io/commands/srem">http://redis.io/commands/srem</a>
## strlen
_signature_ strlen(string key)</p>
_returns_ number</p>

See <a href="http://redis.io/commands/strlen">http://redis.io/commands/strlen</a>
## substr
_signature_ substr(string key, number start, number end)</p>
_returns_ string</p>

See <a href="http://redis.io/commands/substr">http://redis.io/commands/substr</a>
## sunion
_signature_ sunion(string[] keys)</p>
_returns_ string[]</p>

See <a href="http://redis.io/commands/sunion">http://redis.io/commands/sunion</a>
## sunionstore
_signature_ sunionstore(string dstkey, string[] keys)</p>
_returns_ number</p>

See <a href="http://redis.io/commands/sunionstore">http://redis.io/commands/sunionstore</a>
## ttl
_signature_ ttl(string key)</p>
_returns_ number</p>

See <a href="http://redis.io/commands/ttl">http://redis.io/commands/ttl</a>
## type
_signature_ type(string key)</p>
_returns_ string</p>

See <a href="http://redis.io/commands/type">http://redis.io/commands/type</a>
## zadd
_signature_ zadd(string key, number score, string member)</p>
_returns_ number</p>

See <a href="http://redis.io/commands/zadd">http://redis.io/commands/zadd</a>
## zcard
_signature_ zcard(string key)</p>
_returns_ number</p>

See <a href="http://redis.io/commands/zcard">http://redis.io/commands/zcard</a>
## zcount
_signature_ zcount(string key, number min, number max)</p>
_returns_ number</p>

See <a href="http://redis.io/commands/zcount">http://redis.io/commands/zcount</a>

_signature_ zcount(string key, string min, string max)</p>
_returns_ number</p>

See <a href="http://redis.io/commands/zcount">http://redis.io/commands/zcount</a>
## zincrby
_signature_ zincrby(string key, number score, string member)</p>
_returns_ number</p>

See <a href="http://redis.io/commands/zincrby">http://redis.io/commands/zincrby</a>
## zinterstore
_signature_ zinterstore(string dstkey, string[] sets)</p>
_returns_ number</p>

See <a href="http://redis.io/commands/zinterstore">http://redis.io/commands/zinterstore</a>
## zrange
_signature_ zrange(string key, number start, number end)</p>
_returns_ string[]</p>

See <a href="http://redis.io/commands/zrange">http://redis.io/commands/zrange</a>
## zrangeByScore
_signature_ zrangeByScore(string key, string min, string max, number offset, number count)</p>
_returns_ string[]</p>

See <a href="http://redis.io/commands/zrangeByScore">http://redis.io/commands/zrangeByScore</a>

_signature_ zrangeByScore(string key, number min, number max, number offset, number count)</p>
_returns_ string[]</p>

See <a href="http://redis.io/commands/zrangeByScore">http://redis.io/commands/zrangeByScore</a>

_signature_ zrangeByScore(string key, number min, number max)</p>
_returns_ string[]</p>

See <a href="http://redis.io/commands/zrangeByScore">http://redis.io/commands/zrangeByScore</a>

_signature_ zrangeByScore(string key, string min, string max)</p>
_returns_ string[]</p>

See <a href="http://redis.io/commands/zrangeByScore">http://redis.io/commands/zrangeByScore</a>
## zrangeByScoreWithScores
_signature_ zrangeByScoreWithScores(string key, string min, string max)</p>
_returns_ JSON</p>

See <a href="http://redis.io/commands/zrangeByScoreWithScores">http://redis.io/commands/zrangeByScoreWithScores</a>

_signature_ zrangeByScoreWithScores(string key, string min, string max, number offset, number count)</p>
_returns_ JSON</p>

See <a href="http://redis.io/commands/zrangeByScoreWithScores">http://redis.io/commands/zrangeByScoreWithScores</a>

_signature_ zrangeByScoreWithScores(string key, number min, number max, number offset, number count)</p>
_returns_ JSON</p>

See <a href="http://redis.io/commands/zrangeByScoreWithScores">http://redis.io/commands/zrangeByScoreWithScores</a>

_signature_ zrangeByScoreWithScores(string key, number min, number max)</p>
_returns_ JSON</p>

See <a href="http://redis.io/commands/zrangeByScoreWithScores">http://redis.io/commands/zrangeByScoreWithScores</a>
## zrangeWithScores
_signature_ zrangeWithScores(string key, number start, number end)</p>
_returns_ JSON</p>

See <a href="http://redis.io/commands/zrangeWithScores">http://redis.io/commands/zrangeWithScores</a>
## zrank
_signature_ zrank(string key, string member)</p>
_returns_ number</p>

See <a href="http://redis.io/commands/zrank">http://redis.io/commands/zrank</a>
## zrem
_signature_ zrem(string key, string[] members)</p>
_returns_ number</p>

See <a href="http://redis.io/commands/zrem">http://redis.io/commands/zrem</a>
## zremrangeByRank
_signature_ zremrangeByRank(string key, number start, number end)</p>
_returns_ number</p>

See <a href="http://redis.io/commands/zremrangeByRank">http://redis.io/commands/zremrangeByRank</a>
## zremrangeByScore
_signature_ zremrangeByScore(string key, string start, string end)</p>
_returns_ number</p>

See <a href="http://redis.io/commands/zremrangeByScore">http://redis.io/commands/zremrangeByScore</a>

_signature_ zremrangeByScore(string key, number start, number end)</p>
_returns_ number</p>

See <a href="http://redis.io/commands/zremrangeByScore">http://redis.io/commands/zremrangeByScore</a>
## zrevrange
_signature_ zrevrange(string key, number start, number end)</p>
_returns_ string[]</p>

See <a href="http://redis.io/commands/zrevrange">http://redis.io/commands/zrevrange</a>
## zrevrangeByScore
_signature_ zrevrangeByScore(string key, number max, number min, number offset, number count)</p>
_returns_ string[]</p>

See <a href="http://redis.io/commands/zrevrangeByScore">http://redis.io/commands/zrevrangeByScore</a>

_signature_ zrevrangeByScore(string key, string max, string min, number offset, number count)</p>
_returns_ string[]</p>

See <a href="http://redis.io/commands/zrevrangeByScore">http://redis.io/commands/zrevrangeByScore</a>

_signature_ zrevrangeByScore(string key, string max, string min)</p>
_returns_ string[]</p>

See <a href="http://redis.io/commands/zrevrangeByScore">http://redis.io/commands/zrevrangeByScore</a>

_signature_ zrevrangeByScore(string key, number max, number min)</p>
_returns_ string[]</p>

See <a href="http://redis.io/commands/zrevrangeByScore">http://redis.io/commands/zrevrangeByScore</a>
## zrevrangeByScoreWithScores
_signature_ zrevrangeByScoreWithScores(string key, string max, string min)</p>
_returns_ JSON</p>

See <a href="http://redis.io/commands/zrevrangeByScoreWithScores">http://redis.io/commands/zrevrangeByScoreWithScores</a>

_signature_ zrevrangeByScoreWithScores(string key, number max, number min, number offset, number count)</p>
_returns_ JSON</p>

See <a href="http://redis.io/commands/zrevrangeByScoreWithScores">http://redis.io/commands/zrevrangeByScoreWithScores</a>

_signature_ zrevrangeByScoreWithScores(string key, number max, number min)</p>
_returns_ JSON</p>

See <a href="http://redis.io/commands/zrevrangeByScoreWithScores">http://redis.io/commands/zrevrangeByScoreWithScores</a>

_signature_ zrevrangeByScoreWithScores(string key, string max, string min, number offset, number count)</p>
_returns_ JSON</p>

See <a href="http://redis.io/commands/zrevrangeByScoreWithScores">http://redis.io/commands/zrevrangeByScoreWithScores</a>
## zrevrangeWithScores
_signature_ zrevrangeWithScores(string key, number start, number end)</p>
_returns_ JSON</p>

See <a href="http://redis.io/commands/zrevrangeWithScores">http://redis.io/commands/zrevrangeWithScores</a>
## zrevrank
_signature_ zrevrank(string key, string member)</p>
_returns_ number</p>

See <a href="http://redis.io/commands/zrevrank">http://redis.io/commands/zrevrank</a>
## zscore
_signature_ zscore(string key, string member)</p>
_returns_ number</p>

See <a href="http://redis.io/commands/zscore">http://redis.io/commands/zscore</a>
## zunionstore
_signature_ zunionstore(string dstkey, string[] sets)</p>
_returns_ number</p>

See <a href="http://redis.io/commands/zunionstore">http://redis.io/commands/zunionstore</a>
