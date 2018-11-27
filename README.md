# fimber 

Extensible logging for Flutter.

Based on famous Android logging library - [Timber](https://github.com/JakeWharton/timber), this is library for simplify logging for Flutter.
Using similar (as far as Dart lang allows) method API with same concepts for tree and planting logging tree.

## Getting Started

To start add using it:
### Add `fimber` to `pubspec.yaml` 
```yaml
dependencies:
  fimber: ^0.1.3
  ```
- remember about import in file you plan to use Fimber
```dart
import 'package:fimber/fimber.dart';

```

### Initialize logging tree on start of your application
```dart

void main() {
  Fimber.addTree(DebugTree());
  // app code here ...
}
 
```

### Start using it with static methods:

```dart
import 'fimber.dart';


void main() {
  var parameter = 343.0;
  // use directly
  Fimber.i("Test message $argument");
  Fimber.i("Extra error message", ex: Exception("Test thorwable"));
  
  // other log levels
  Fimber.d("DEBUG");
  Fimber.v("VERBOSE");
  Fimber.w("WARN");
  
}

```

This will log the value and grab a TAG from stacktrace - that is little costly and if more logs will be done per second.

### Create tagged version of Fimber 

And use its instance inside class, you can create logger for a dart file or for a class.

```dart
var logger = FimberLog("MY_TAG");

void main() {
  
  logger.d("Test message");
}

// or inside a class
class SomeBloc {
  var logger = FimberLog("SomeBloc");
  String fetchMessage() {
    logger.d("About to fetch some data.");
    //...
    var data = "load something";

    logger.d("Retrived data (len = ${data.length}");
    return data;
  }
}
```

### Use block function and pass method that uses logger.

Use this function to log multiple messages with same tag, allows optional return value.
Due to nature of auto-tag generation from stacktrace this block only does it once and create local FimberLog instance to pass into the anonymous method.

```dart
    var someMessage = "Test message from inside of block";
    var output = Fimber.block((log) {
      log.d("Started block");
      var i = 0;
      for (i = 0; i < 10; i++) {
        log.d("$someMessage, value: $i");
      }
      log.i("End of block");
      return i;
    });
```

## TODO - road map

- un-plant single tree
- allow line format configuration from dart code 
- Add Crashlytics plugin (maybe other remote logger tools) with [flutter_crashlytics](https://pub.dartlang.org/packages/flutter_crashlytics)

## Licence

```

   Copyright 2018 Mateusz Perlak

   Licensed under the Apache License, Version 2.0 (the "License");
   you may not use this file except in compliance with the License.
   You may obtain a copy of the License at

       http://www.apache.org/licenses/LICENSE-2.0

   Unless required by applicable law or agreed to in writing, software
   distributed under the License is distributed on an "AS IS" BASIS,
   WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
   See the License for the specific language governing permissions and
   limitations under the License.
```