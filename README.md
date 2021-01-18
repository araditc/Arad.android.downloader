# Arad.android.downloader

A power full resumable download library for Android

![](https://i.ibb.co/NZmn09T/cloud-computing.png)

Download
--------

```groovy
repositories {
    maven { url 'https://jitpack.io' }
}

dependencies {
	        implementation 'com.github.araditc:Arad.android.resumableUploader:Tag'
}
```

How do I use Arad Arad downloader?
-------------------

### Overview of PRDownloader library
* PRDownloader can be used to download any type of files like image, video, pdf, apk and etc.
* This file downloader library supports pause and resume while downloading a file.
* Supports large file download.
* This downloader library has a simple interface to make download request.
* We can check if the status of downloading with the given download Id.
* PRDownloader gives callbacks for everything like onProgress, onCancel, onStart, onError and etc while downloading a file.
* Supports proper request canceling.
* Many requests can be made in parallel.
* All types of customization are possible.

## Using PRDownloader Library in your Android application

Add this in your build.gradle
```groovy
implementation 'com.mindorks.android:prdownloader:0.6.0'
```
Do not forget to add internet permission in manifest if already not present
```xml
<uses-permission android:name="android.permission.INTERNET" />
```
Then initialize it in onCreate() Method of application class :
```java
PRDownloader.initialize(getApplicationContext());
```
Initializing it with some customization
```java
// Enabling database for resume support even after the application is killed:
PRDownloaderConfig config = PRDownloaderConfig.newBuilder()
                .setDatabaseEnabled(true)
                .build();
PRDownloader.initialize(getApplicationContext(), config);

// Setting timeout globally for the download network requests:
PRDownloaderConfig config = PRDownloaderConfig.newBuilder()
                .setReadTimeout(30_000)
                .setConnectTimeout(30_000)
                .build();
PRDownloader.initialize(getApplicationContext(), config); 
```

### Make a download request
```java
int downloadId = PRDownloader.download(url, dirPath, fileName)
                        .build()
                        .setOnStartOrResumeListener(new OnStartOrResumeListener() {
                            @Override
                            public void onStartOrResume() {
                               
                            }
                        })
                        .setOnPauseListener(new OnPauseListener() {
                            @Override
                            public void onPause() {
                               
                            }
                        })
                        .setOnCancelListener(new OnCancelListener() {
                            @Override
                            public void onCancel() {
                                
                            }
                        })
                        .setOnProgressListener(new OnProgressListener() {
                            @Override
                            public void onProgress(Progress progress) {
                               
                            }
                        })
                        .start(new OnDownloadListener() {
                            @Override
                            public void onDownloadComplete() {
                               
                            }

                            @Override
                            public void onError(Error error) {
                               
                            }
                        });            
```

### Pause a download request
```java
PRDownloader.pause(downloadId);
```

### Resume a download request
```java
PRDownloader.resume(downloadId);
```

### Cancel a download request
```java
// Cancel with the download id
PRDownloader.cancel(downloadId);
// The tag can be set to any request and then can be used to cancel the request
PRDownloader.cancel(TAG);
// Cancel all the requests
PRDownloader.cancelAll();
```

### Status of a download request
```java
Status status = PRDownloader.getStatus(downloadId);
```

### Clean up resumed files if database enabled
```java
// Method to clean up temporary resumed files which is older than the given day
PRDownloader.cleanUp(days);
```

License
--------

  
  Copyright 2020 Arad-Itc.
 
  Licensed under the Arad License, Version 2.0 (the "License");
  you may not use this file except in compliance with the License.
  You may obtain a copy of the License at
 
  https://arad-itc.com/
 
  Unless required by applicable law or agreed to in writing, software
  distributed under the License is distributed on an "AS IS" BASIS,
  WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
  See the License for the specific language governing permissions and
  limitations under the License.

