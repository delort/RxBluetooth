RxBluetooth
===========

[![Build Status](https://travis-ci.org/IvBaranov/RxBluetooth.svg)](https://travis-ci.org/IvBaranov/RxBluetooth)

Android reactive bluetooth library.

Usage
-----

1. Declare permissions:
   ```xml
   <uses-permission android:name="android.permission.BLUETOOTH" />
   <uses-permission android:name="android.permission.BLUETOOTH_ADMIN" />
   ```

2. Create `RxBluetooth` instance.

3. Check if bluetooth is currently enabled and ready for use:
   ```java
   if  (!rxBluetooth.isBluetoothAvailable()) {
      // to enable blutooth via startActivityForResult()
      rxBluetooth.enableBluetooth(this, REQUEST_ENABLE_BT);
   }
   ```

4. Have fun.
5. Make sure you are unsubscribing and stopping discovery `OnDestroy()`:

   ```java
   if (rxBluetooth != null) {
         rxBluetooth.cancelDiscovery();
       }
   unsubscribe(rxBluetoothSubscription);
   ```

##### Observing devices
```java
rxBluetooth.observeDevices(this)
        .observeOn(AndroidSchedulers.mainThread())
        .subscribeOn(Schedulers.io())
        .subscribe(new Action1<BluetoothDevice>() {
          @Override public void call(BluetoothDevice bluetoothDevice) {
            //
          }
        });
```

##### Observing discovery state

To observe just `ACTION_DISCOVERY_STARTED`:

```java
 rxBluetooth.observeDiscovery(this)
     .observeOn(AndroidSchedulers.mainThread())
     .subscribeOn(Schedulers.io())
     .filter(Action.isEqualTo(BluetoothAdapter.ACTION_DISCOVERY_STARTED))
     .subscribe(new Action1<String>() {
       @Override public void call(String action) {
         //
       }
     });
```

To observe both `ACTION_DISCOVERY_STARTED` and `ACTION_DISCOVERY_FINISHED`:

```java
 rxBluetooth.observeDiscovery(this)
     .observeOn(AndroidSchedulers.mainThread())
     .subscribeOn(Schedulers.io())
     .filter(Action.isEqualTo(BluetoothAdapter.ACTION_DISCOVERY_STARTED, BluetoothAdapter.ACTION_DISCOVERY_FINISHED))
     .subscribe(new Action1<String>() {
       @Override public void call(String action) {
         //
       }
     });
```

Download
--------
```groovy
compile 'com.github.ivbaranov:rxbluetooth:0.0.2'
```

Developed By
------------
Ivan Baranov

License
-------

```
Copyright 2015 Ivan Baranov

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
