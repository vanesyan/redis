# CAUTION: WORK IN PROGRESS

[![Test Status][cirrusci-image]][cirrusci-url] [![Code Coveraege][codecov-image]][codecov-url]

High performance Redis client for Dart VM.

### Features
* Pub/Sub
* Connection pooling
* Lua scripts

### Installation
To be able to install this library on your machine make sure you have
installed `pub` Dart package manager:
```sh
$ pub get redis
```

### Basic usage
```dart
import 'package:redis/redis.dart' show Connection;

Future<void> main() async {
  final cnx = await Connection.connect(InternetAddress.loopbackIPv4);
}
```

### Connection pool usage
```dart
import 'package:redis/redis.dart' show Pool;

Future<void> main() async {
  final pool = await Pool.connect(InternetAddress.loopbackIPv4);
  
  await pool.set('key', 'value');
  
  final value = await pool.get('key'); // => 'value'
}
```

### Pub/Sub usage
```dart
import 'package:redis/redis.dart' show Subscriber;

Future<void> main() async {
  final cnx = await Connection.connect(InternetAddress.loopbackIPv4);
  final subscriber = await Subscriber.connect(InternetAddress.loopbackIPv4);
  
  await cnx.publish('');
  
  await for (final message in subscriber.messages) {
    print(message.value);
  }
}
```


[cirrusci-image]: https://api.cirrus-ci.com/github/vanesyan/redis.dart.svg?branch=master
[cirrusci-url]: https://cirrus-ci.com/github/vanesyan/redis.dart
[codecov-image]: https://codecov.io/gh/vanesyan/redis.dart/branch/master/graph/badge.svg
[codecov-url]: https://codecov.io/gh/vanesyan/redis.dart
