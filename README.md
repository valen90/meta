# Meta
[![Language](https://img.shields.io/badge/Swift-3-brightgreen.svg)](http://swift.org)
[![Build Status](https://travis-ci.org/nodes-vapor/meta.svg?branch=master)](https://travis-ci.org/nodes-vapor/meta)
[![codecov](https://codecov.io/gh/nodes-vapor/meta/branch/master/graph/badge.svg)](https://codecov.io/gh/nodes-vapor/meta)
[![GitHub license](https://img.shields.io/badge/license-MIT-blue.svg)](https://raw.githubusercontent.com/nodes-vapor/meta/master/LICENSE)


This package enforces clients to send a specific header in all requests. 

### [PLATFORM];[ENVIROMENT];[APP_VERSION];[DEVICE_OS];[DEVICE]

This header can look like this android;production;1.2.3;4.4;Samsung S7
 - platform
 - environment
 - app version
 - device os
 - device

For web platform only platform and enviroment is required, since rest can be found in User-Agent

Why not just use User-Agent
 - User-Agent is missing some of these details
 - User-Agent can be hard to extend / override
 - Default User-Agent in iOS & Android can be their client (OkHttp, Alamo Fire etc)

#Installation

#### Config
Update your `Package.swift` file.
```swift
.Package(url: "https://github.com/nodes-vapor/meta", majorVersion: 0)
```

Create config meta.json

```
{
    "header": "N-Meta",
    "platforms": [
        "web",
        "android",
        "ios",
        "windows"
    ],
    "environments": [
        "local",
        "development",
        "staging",
        "production"
    ],
    "exceptPaths": [
        "/js/*",
        "/css/*",
        "/images/*",
        "/favicons/*"
    ],
    "requiredEnvironments": [
        "local",
        "development",
        "staging",
        "production"
    ]
}
```

### main.swift
```
import Meta
```
Add middleware direcetly to your api groups
```swift
drop.group(MetaMiddleware(drop: drop)) { metaRoutes in
     //Routes
}
```
or add middleware global (will be loaded for all requests)
```swift
try drop.middleware.append(MetaMiddleware(drop: drop))
```
