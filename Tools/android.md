<!--
 * This file is part of RS Cheat Sheets.
 *
 * RS Cheat Sheets is free software: you can redistribute it and/or modify
 * it under the terms of the GNU General Public License as published by
 * the Free Software Foundation, either version 3 of the License, or
 * (at your option) any later version.
 *
 * RS Cheat Sheets is distributed in the hope that it will be useful,
 * but WITHOUT ANY WARRANTY; without even the implied warranty of
 * MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
 * GNU General Public License for more details.
 *
 * You should have received a copy of the GNU General Public License
 * along with RS Cheat Sheets. If not, see <https://www.gnu.org/licenses/>.
 */
-->

[Home](../README.md)

# Android

## Table Of Contents
<!-- TOC -->

- [Android](#android)
	- [Table Of Contents](#table-of-contents)
	- [Links](#links)
	- [Packages](#packages)
	- [Manifest](#manifest)
		- [@s](#s)
	- [Permissions](#permissions)
		- [Most Common Permissions](#most-common-permissions)
	- [Gradle](#gradle)
	- [APK files](#apk-files)
	- [Location](#location)
	- [Location to Address](#location-to-address)
	- [Rest](#rest)
	- [Login Screen](#login-screen)
		- [Google signing](#google-signing)
	- [Questions](#questions)
	- [Data Extraction Rules](#data-extraction-rules)
	- [Backup Rules](#backup-rules)
	- [Themes](#themes)
	- [Intents](#intents)

<!-- /TOC -->

## [Links](#table-of-contents)
- https://developer.android.com/
- https://developers.google.com/android

## [Packages](#table-of-contents)

## [Manifest](#table-of-contents)
AndroidManifest.xml file provides info about the app to the Android Operating system.

Such info can include
- App's package name
- Version
- All components for the app(activities, services, broadcast receivers)
- Where the main activity(entry point) for the app is.
- Permissions required for the app
- App icon
- App's compatibility settings
  - Which is used to make sure the app is compatible with the device and android version of the device.
- etc.

Example of AndroidManifest.xml:
```xml
<?xml version="1.0" encoding="utf-8"?> <!-- XML Prolog -->
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"> <!-- XML Namespaces -->

    <!-- Permissions -->
    <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
    <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />

    <application
        android:allowBackup="true" // Weather the apps data will be backup. This includes settings, app specific files like images and documents, etc
        android:dataExtractionRules="@xml/data_extraction_rules" // A XML file used to define rules for data extraction during backup and restore operations.
        android:fullBackupContent="@xml/backup_rules" // An XML file used to contain the rules for which files and folders should be included or excluded during a full backup
        android:icon="@mipmap/ic_launcher" // App icon
        android:label="@string/app_name" // Apps name on device
        android:roundIcon="@mipmap/ic_launcher_round" // Round app icon
        android:supportsRtl="true" // Do the apps layouts support right to left languages. This will mirror and adjust the UI elements that use text.
        android:theme="@style/Theme.Android_location_tutorial" // Sets the theme of the app
        tools:targetApi="31"> // Sets the API(Android version) the app us built for
        <activity // Only one activity can be interacting with the user at once
            android:name=".MainActivity" // Defines where the activity is stored. The "." means that activity is in the same project as the manifest file
            android:exported="true"> // Can other apps launch this activity/app
            <intent-filter> // Settings for how the activity responds to different intents.
                <action android:name="android.intent.action.MAIN" /> // Sets this activity to be the main entry point of the app.

                <category android:name="android.intent.category.LAUNCHER" /> // This activity is meant to be the launch activity that is used when the launch icon is pressed.
            </intent-filter>
        </activity>
    </application>

</manifest>
```

### [@s](#table-of-contents)
The @s in the AndroidManifest.xml refer to a specific type of resource and Android knows where to look based on that type. Each @ type is referring to a specific XML vocabulary.

| Type name | Description                                     | Default File/Folder path                    |
|-----------|-------------------------------------------------|---------------------------------------------|
| @string   | String resource such as the name of your app.   | res/values/strings.xml                      |
| @style    | Style resource such as a theme.                 | res/values/styles.xml  or res/values/themes |
| @drawable | Image assets used throughout the app.           | res/drawable/                               |
| @mipmap   | Static app launcher icons.                      | res/mipmap/                                 |
| @layout   | Layout resource such as a page for your app.    | res/layout/                                 |
| @color    | Color resource such as a defined primary color. | res/values/colors.xml                       |
| @dimen    | Dimensional resource such as a text size.       | res/values/                                 |

The different files in the mipmap folder refers to different screen densities(number of pixels in a given area).

| dpi(dots per inch) Name | Screen Density                                 |
|-------------------------|------------------------------------------------|
| mdpi                    | 160dpi                                         |
| hdpi                    | 1.5x mdpi(240dpi)                              |
| xhdpi                   | 2x mdpi(320dpi)                                |
| xxhdpi                  | 3x mdpi(480dpi)                                |
| xxxhdpi                 | 4x mdpi(640dpi)                                |
| anydpi-v26              | Vector drawable that is resolution independent |

The version of the app icon that is used depends on the device's screen density and the Android version it's running. If it is running version 26 or greater the anydpi-v26 is used.

## [Permissions](#table-of-contents)
### [Most Common Permissions](#table-of-contents)

## [Gradle](#table-of-contents)
The gradle is a tool to automate the building process for android.

It is used to:
- Compile source code
- Managing dependencies
- Managing plugins
- Generating APK files

## [APK files](#table-of-contents)
Android 
## [Location](#table-of-contents)

## [Location to Address](#table-of-contents)

content providers - Abstract the way for how data is stored and retrieved from your app to other apps.
  - Content providers work through URIs
  - FLAG_GRANT_READ_URI_PERMISSION
Android permissions

## [Rest](#table-of-contents)
Communicating using HTTP requests

## [Login Screen](#table-of-contents)
### [Google signing](#table-of-contents)

## [Questions](#table-of-contents)
  - Build vs run app
  - Sync gradle. What is teh gradle
  - SDK Manager. What are SDKs?
  - Device Manager

## [Data Extraction Rules](#table-of-contents)
Rules for data extraction during backup and restore operations
Which data should be extracted from your app during the backup process, and how it should be handled when restoring the app's data.

## [Backup Rules](#table-of-contents)
<full-backup-content>
    <exclude domain="no-backup" />
    <exclude domain="cache" />
    <include domain="file" path="databases/" />
    <!-- Additional rules as needed -->
</full-backup-content>

## [Themes](#table-of-contents)
How do you work with themes?

## [Intents](#table-of-contents)
Intents are used for sending data from one app to another.