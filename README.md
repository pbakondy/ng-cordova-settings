ng-cordova-settings
==========

Store and read settings permanently on local filesystem in Cordova/Ionic projects.

When you run your application in device ng-cordova-settings uses the local filesystem (with cordova-plugin-file) and the system logs (with console.log).

When you run your application in browser with <code>ionic serve</code> the ng-cordova-settings uses browsers localStorage and the browser console (with console.log).

## Dependencies

- [ngCordova](http://ngcordova.com/) ( required version v0.1.14-alpha )
- [cordova-plugin-file](https://github.com/apache/cordova-plugin-file)

## Installation

Add cordova plugin

```bash
$ cordova plugin add cordova-plugin-file
```

Install ng-cordova-settings manually, or with ionic:

```bash
$ ionic add ng-cordova-settings
```

Include *ng-cordova-settings.min.js* and  *ng-cordova.min.js* in your index.html file before cordova.js and after your AngularJS / Ionic file (since ngCordova depends on AngularJS).

```html
<script src="lib/ngCordova/dist/ng-cordova.min.js"></script>
<script src="lib/ng-cordova-settings/dist/ng-cordova-settings.min.js"></script>
<script src="cordova.js"></script>
```

Note: you don't have to use the complete ngCordova package. I suggest to create a [Custom Build](http://ngcordova.com/build/) with file module.


## Usage

### settings.read()

Gives back an Object with all the stores values

### settings.read(&lt;String&gt; key)

Gives back the value of the specified key.

### settings.read(&lt;Array&gt; keyList)

Gives back an Object with the values of the specified keys.

### settings.write(&lt;String&gt; key)

Removes the value of the specified key from settings.

### settings.write(&lt;String&gt; key, &lt;Mixed&gt; value)

Sets the value for the specified key. Value can be any JSON-like type: boolean, number, string, object, or array.

### settings.write(&lt;Object&gt; values)

Where values = { key1: value1, key2: value2 ... }

Sets the values for the specified keys.

### settings.keys()

Returns an array with the stored keys in settings file.

### settings.empty()

Empties settings file.

### settings.remove()

Deletes settings file.

### settings.setStorageFilename(&lt;String&gt; filename)

You can set the local filename for the settings file (default settings.txt).


### Example use

```js
angular.module('starter', ['ionic', 'ng-cordova-settings'])
  .controller('mainCtrl', ['$scope', 'settings', '$ionicPlatform', function($scope, settings, $ionicPlatform) {

  function testing1() {
    settings.write('key0', 'value0').then(
      function() {
        testing2();
      },
      function(error) {
        console.log(error);
      }
    );
  }

  function testing2() {
    settings.write({ key1: 'value1', key2: 'value2' }).then(
      function() {
        testing3();
      },
      function(error) {
        console.log(error);
      }
    );
  }

  function testing3() {
    settings.read().then(function(result) {
      console.log(result); // { key0: 'value0', key1: 'value1', key2: 'value2' }
    });
    settings.read('key1').then(function(result) {
      console.log(result); // 'value1'
    });
    settings.read(['key0', 'key1']).then(function(result) {
      console.log(result); // { key0: 'value0', key1: 'value1' }
    });
    settings.keys().then(function(result) {
      console.log(result); // [ 'key0', 'key1', 'key2' ]
    });
  }

  $ionicPlatform.ready(function() {
    testing1();
  });


}]);
```


## Author

#### Peter Bakondy

- https://github.com/pbakondy


## LICENSE

**ng-cordova-settings** is licensed under the MIT Open Source license. For more information, see the LICENSE file in this repository.
