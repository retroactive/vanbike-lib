# VanBike-Library
Access VanMoof Bikes without App.

## Features
* Retrieve Parameters (Battery, Distance, Settings, ...)
* Retrieve Firmware/Hardware/Software/Model/Serial Number
* Start Bike-Module
* Unlock Bike
* Set Region Settings
* Set Lightning Settings
* Set Power Level
* Set Units
* Show Firmware
* Reset Distance
* Pair Remote
* ...

## Compatibility
* Electrified S (2016) - possible
* Electrified X (2016) - possible
* Electrified S (2017) - tested
* Electrified X (2017) - possible
* Electrified S2 - untested
* Electrified X2 - untested
* Electrified S3 - untested
* Electrified X3 - untested

## Usage
### Install
```shell script
# Yarn
yarn add poket-jony/vanbike-lib

# NPM
npm i poket-jony/vanbike-lib
```

### Build Distribution
```shell script
# Development
yarn dev

# Production
yarn prod
```

### ES6
```javascript
import { VanBikeService, ModuleStateEntity, LockStateEntity } from 'vanbike-lib';
const vanBikeService = new VanBikeService('ENCRYPTION-KEY');
```

### Browser
```html
<script type="text/javascript" src="/dist/vanbike-lib.js"></script>
```
```javascript
const vanBikeService = new VanBikeLib.VanBikeService('ENCRYPTION-KEY');
const ModuleStateEntity = VanBikeLib.ModuleStateEntity;
const LockStateEntity = VanBikeLib.LockStateEntity;
```

## Example
For more examples see `example` folder.
```javascript
// Event listener
vanBikeService.notify((parameters) => {
    console.log(parameters);
});

// Connect
await vanBikeService.connect();

// Authenticate
await vanBikeService.authenticate();

// Turn on
const moduleState = new ModuleStateEntity();
moduleState.setState(moduleState.STATE_ON);
await vanBikeService.setModuleState(moduleState);

// Unlock
const lockState = new LockStateEntity();
lockState.setState(lockState.STATE_UNLOCKED);
await vanBikeService.setLockState(lockState);

// Disconnect
vanBikeService.disconnect();
```

## Documentation
#### VanBikeService
* `constructor(encryptionKey : string) : void`
* `getBluetoothService() : BluetoothService`
* `connect() : Promise`
* `disconnect() : void`
* `isConnected() : bool`
* `notify(callback : function) : void`
* `authenticate() : Promise`
* `setModuleState(ModuleStateEntity moduleState) : Promise`
* `setLockState(LockStateEntity lockState) : Promise`
* `setLightningState(LightningStateEntity lightningState) : Promise`
* `setPowerLevelState(PowerStateEntity powerState, RegionStateEntity regionState) : Promise`
* `setUnitState(UnitStateEntity unitState) : Promise`
* `showFirmware() : Promise`
* `resetDistance() : Promise`
* `pairRemote() : Promise`

## Notice
### CORS Policy
The `WebService` calls the VanMoof API directly.
This is probably not possible in Browsers because of [CORS-Policy](https://developer.mozilla.org/docs/Web/HTTP/CORS).
Use a workaround with the Chrome-Plugin: [Allow CORS: Access-Control-Allow-Origin](https://chrome.google.com/webstore/detail/allow-cors-access-control/lhobafahddgcelffkeicbaginigeejlf).
Or use this service from NodeJS. 

## License
MIT