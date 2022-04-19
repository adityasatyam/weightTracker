# weightTracker
This is a fitness app

Basic App config and APK generation

1.Changing React native App name:
    appname/android/app/src/main/res/values/strings.xml:

    <resources>
        <string name="app_name">Weight Tracker</string>
    </resources>


2.Changing RN app icon:
    a.Download png image from : https://www.flaticon.com/
    b. Open : https://easyappicon.com/ : Upload png and Generate
    c. Replace respective images from : weightTracker/android/app/src/main/res/

3.Creating build:
    a. Run inside project : 
         keytool -genkeypair -v -storetype PKCS12 -keystore my-upload-key.keystore -alias my-key-alias -keyalg RSA -keysize 2048 -validity 10000
    b. Copy my-upload-key.keystore to android/app
    c. Go to: android/gradle.properties and Paste: 
        MYAPP_UPLOAD_STORE_FILE=my-upload-key.keystore
        MYAPP_UPLOAD_KEY_ALIAS=my-key-alias
        MYAPP_UPLOAD_STORE_PASSWORD=*****
        MYAPP_UPLOAD_KEY_PASSWORD=*****
    d.Modify android/app/build.gradle:
        ...
            android {
                ...
                defaultConfig { ... }
                signingConfigs {
                    release {
                        if (project.hasProperty('MYAPP_UPLOAD_STORE_FILE')) {
                            storeFile file(MYAPP_UPLOAD_STORE_FILE)
                            storePassword MYAPP_UPLOAD_STORE_PASSWORD
                            keyAlias MYAPP_UPLOAD_KEY_ALIAS
                            keyPassword MYAPP_UPLOAD_KEY_PASSWORD
                        }
                    }
                }
                buildTypes {
                    release {
                        ...
                        signingConfig signingConfigs.release
                    }
                }
            }
        ...
    e.Generate APK : 
        cd android
        ./gradlew assembleRelease
    f.weightTracker/android/app/build/outputs/apk/release/ 

