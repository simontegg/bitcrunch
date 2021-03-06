
# bitcrunch

Redis analytics for node.js.

**Note:** *not ready for production use.*

## Bitmaps

Hashes and maps input values to an internal linear identifier via [redis-identity](https://github.com/gjohnson/redis-identity). You can then ask the bitmap various questions ranging some simple membership to more complex bitwise operations.

Inspired by: [fast-easy-realtime-metrics-using-redis-bitmaps](http://blog.getspool.com/2011/11/29/fast-easy-realtime-metrics-using-redis-bitmaps/)

*Basic logic*

```js
var bitcrunch = require('bitcrunch');

var won = bitcrunch('won');
var lost = bitcrunch('lost');

// winners

won
.add('a+foobar@email.com')
.add('b+foobar@email.com')
.add('c+foobar@email.com');

// losers

lost
.add('c+foobar@email.com')
.add('d+foobar@email.com');


// won AND lost

won
.and(lost)
.count(function(err, total){
  console.log('%s won and lost', total);
});

// won OR lost

won
.or(lost)
.count(function(err, total){
  console.log('%s won or lost', total);
});
```

*Membership*

```js
var bitcrunch = require('bitcrunch');

var likes = bitcrunch('likes')
.add('js')
.add('lua')
.add('redis');

likes.includes('js', function(err, result){
  console.log('result = %s', result);
});
```

## todo

  - command-queue / promises for chaining (that works).
  - complex logic (and/or/and), kinda requires the promises.
  - do we really need to hash values?.
  - NOT.
  - XOR.

## attribution

  - [fast-easy-realtime-metrics-using-redis-bitmaps](http://blog.getspool.com/2011/11/29/fast-easy-realtime-metrics-using-redis-bitmaps/)
  - [bitmapist](http://amix.dk/blog/post/19714#bitmapist-Powerful-realtime-analytics-with-Redis-2-6s-bitmaps-and)
  - [crashlytics-on-redis-analytics](http://www.slideshare.net/crashlytics/crashlytics-on-

## License

MIT