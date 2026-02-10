# BeWhere Connector

A JavaScript connector library for integrating with the BeWhere Service API. This connector provides a simple and convenient way to interact with BeWhere's tracking and beacon management services from your Scriptr.io applications.

## Table of Contents

- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Configuration](#configuration)
- [Usage](#usage)
- [API Methods](#api-methods)
  - [Authentication](#authentication)
  - [Beacons](#beacons)
  - [Snapshots](#snapshots)
  - [Streams](#streams)
  - [Device Configuration](#device-configuration)
- [Examples](#examples)

## Prerequisites

- An active account in the BeWhere Service
- Access to Scriptr.io IDE
- Underscore module installed in Scriptr.io IDE

## Installation

1. Clone or download this repository into your Scriptr.io workspace
2. Ensure the underscore module is installed in your Scriptr.io IDE

## Configuration

Edit the configuration file at `./bewhere/config` with your BeWhere account credentials:

```javascript
//The bewhere Info 
const bewhere = {
    baseUrl: "api.bewhere.com",
    endPoint: "https://api.bewhere.com/",
    name: "BeWhere ACCOUNT NAME", // not used for now but it will help you distinguish your apps
   
    username: "<USER_NAME>",
    apiKey: "<api_token>",
    accountId: "<account_id>",
};
```

**Configuration Parameters:**
- `baseUrl`: The base URL of the BeWhere API
- `endPoint`: The full endpoint URL for API calls
- `name`: A descriptive name for your application (optional)
- `username`: Your BeWhere account username
- `apiKey`: Your BeWhere API authentication token
- `accountId`: Your BeWhere account identifier

## Usage

### Basic Setup

```javascript
var bwModule = require('./bewhere/BeWhere');

var bw = new bwModule.BeWhere();
var cnMngr = bw.getConnectorManager();
var myConnector = cnMngr.getConnector();

try {
    var result = myConnector.getTypesBeacons();
    return result;
} catch(exception) {
    return exception;
}
```

## API Methods

### Authentication

#### `getAuthTokens(data)`
Retrieve authentication tokens for a user.

```javascript
var tokens = myConnector.getAuthTokens({
    user: "username" // optional, defaults to config username
});
```

#### `authentication(auth)`
Authenticate with the BeWhere service.

```javascript
var authResult = myConnector.authentication(authObject);
```

### Beacons

#### `getTypesBeacons()`
Get all available beacon types.

```javascript
var beaconTypes = myConnector.getTypesBeacons();
```

#### `getBeacons(data)`
Get all beacons for an account.

```javascript
var beacons = myConnector.getBeacons({
    accountId: "your-account-id" // optional, defaults to config accountId
});
```

#### `getBeacon(data)`
Get details for a specific beacon.

```javascript
var beacon = myConnector.getBeacon({
    deviceId: "device-id",
    accountId: "your-account-id" // optional, defaults to config accountId
});
```

### Snapshots

#### `getSnapshots(data)`
Get all snapshots for an account.

```javascript
var snapshots = myConnector.getSnapshots({
    accountId: "your-account-id" // optional, defaults to config accountId
});
```

#### `getSnapshot(data)`
Get a specific snapshot by device ID.

```javascript
var snapshot = myConnector.getSnapshot({
    deviceId: "device-id",
    accountId: "your-account-id" // optional, defaults to config accountId
});
```

### Streams

#### `getStreamsHistory(data)`
Get stream history for an account.

```javascript
var history = myConnector.getStreamsHistory({
    accountId: "your-account-id" // optional, defaults to config accountId
});
```

### Device Configuration

#### `getDeviceConfig(data)`
Get configuration for a specific beacon device.

```javascript
var config = myConnector.getDeviceConfig({
    deviceId: "device-id",
    accountId: "your-account-id" // optional, defaults to config accountId
});
```

#### `postDeviceConfig(data)`
Update configuration for a specific beacon device.

```javascript
var result = myConnector.postDeviceConfig({
    deviceId: "device-id",
    bwPayload: { /* configuration object */ },
    accountId: "your-account-id" // optional, defaults to config accountId
});
```

## Examples

### Example 1: Get All Beacons

```javascript
var bwModule = require('./bewhere/BeWhere');

var bw = new bwModule.BeWhere();
var connector = bw.getConnectorManager().getConnector();

try {
    var beacons = connector.getBeacons();
    return beacons;
} catch(exception) {
    console.error("Error fetching beacons:", exception);
    return exception;
}
```

### Example 2: Get Specific Beacon Details

```javascript
var bwModule = require('./bewhere/BeWhere');

var bw = new bwModule.BeWhere();
var connector = bw.getConnectorManager().getConnector();

try {
    var beacon = connector.getBeacon({
        deviceId: "357591080108407"
    });
    return beacon;
} catch(exception) {
    console.error("Error fetching beacon:", exception);
    return exception;
}
```

### Example 3: Update Device Configuration

```javascript
var bwModule = require('./bewhere/BeWhere');

var bw = new bwModule.BeWhere();
var connector = bw.getConnectorManager().getConnector();

try {
    var result = connector.postDeviceConfig({
        deviceId: "357591080108407",
        bwPayload: {
            // your configuration settings here
        }
    });
    return result;
} catch(exception) {
    console.error("Error updating device config:", exception);
    return exception;
}
```

### Example 4: Custom Configuration

```javascript
var bwModule = require('./bewhere/BeWhere');

// Override default configuration
var customConfig = {
    bewhere: {
        endPoint: "https://custom-api.bewhere.com/",
        username: "custom-user",
        apiKey: "custom-token",
        accountId: "custom-account-id"
    }
};

var bw = new bwModule.BeWhere(customConfig);
var connector = bw.getConnectorManager().getConnector();

try {
    var beacons = connector.getBeacons();
    return beacons;
} catch(exception) {
    return exception;
}
```

## Error Handling

The connector uses a consistent error handling pattern. All API calls should be wrapped in try-catch blocks:

```javascript
try {
    var result = connector.someMethod();
    return result;
} catch(exception) {
    // Handle error
    console.error("API Error:", exception);
    return {
        error: true,
        details: exception
    };
}
```

## Support

For issues or questions about the BeWhere Service API, please contact BeWhere support or refer to the official BeWhere API documentation.

## License

Please refer to your BeWhere Service agreement for terms of use.
