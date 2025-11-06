# Spotify APK and API testing

## Prep apkeep and download Spotify APK file 

The simplest example is to download a single APK to the current directory:

```shell
apkeep -e 'ttowne43@gmail.com' --oauth-token oauth2_4/0Ab32j90GfEIW*************************************
apkeep -a com.spotify.music -d google-play -e 'ttowne43@@gmail.com' -t aas_et/AKppINbacc7vM11NAWSB************************************* .
Downloading com.spotify.music...
com.spotify.music downloaded successfully!
ls -lh com.spotify.music.apk 
-rw-rw-r-- 1 ttow ttow 70M Nov  4 11:59 com.spotify.music.apk
```

## Prep mobsf

Run docker version of mobsf 

```shell
ttow@tunnelmtn:~/Documents/ttow/mobsf$ docker compose up 
[+] Running 1/1
 ✔ Container mobsf  Created                                                                                                                      0.0s 
Attaching to mobsf
mobsf  | [INFO] 05/Nov/2025 18:12:33 - Downloading JADX from https://github.com/skylot/jadx/releases/download/v1.5.0/jadx-1.5.0.zip
mobsf  | [INFO] 05/Nov/2025 18:12:33 - Loading User config from: /home/mobsf/.MobSF/config.py
mobsf  | [INFO] 05/Nov/2025 18:12:37 - 
mobsf  |   __  __       _    ____  _____       _  _   _  _   
mobsf  |  |  \/  | ___ | |__/ ___||  ___|_   _| || | | || |  
mobsf  |  | |\/| |/ _ \| '_ \___ \| |_  \ \ / / || |_| || |_ 
mobsf  |  | |  | | (_) | |_) |__) |  _|  \ V /|__   _|__   _|
mobsf  |  |_|  |_|\___/|_.__/____/|_|     \_/    |_|(_) |_|  
mobsf  | 
mobsf  | [INFO] 05/Nov/2025 18:12:37 - Author: Ajin Abraham | opensecurity.in
mobsf  | [INFO] 05/Nov/2025 18:12:37 - Mobile Security Framework v4.4.3
[#-------------------------------------------------] 2.43%REST API Key: 094e3c59cccb9af88f16c7a7dca87197ff3db2cbdca6d19b74dc43722476410f
mobsf  | Default Credentials: mobsf/mobsf
mobsf  | [INFO] 05/Nov/2025 18:12:37 - OS Environment: Linux (debian 12 bookworm) Linux-6.14.0-33-generic-x86_64-with-glibc2.36
mobsf  | [INFO] 05/Nov/2025 18:12:37 - Python Version: 3.13.7
mobsf  | [INFO] 05/Nov/2025 18:12:37 - CPU Cores: 4, Threads: 8, RAM: 31.25 GB
mobsf  | [INFO] 05/Nov/2025 18:12:37 - MobSF Basic Environment Check
...
mobsf  | [INFO] 05/Nov/2025 18:14:06 - Loading User config from: /home/mobsf/.MobSF/config.py
mobsf  | [INFO] 05/Nov/2025 18:32:58 - 
mobsf  |   __  __       _    ____  _____       _  _   _  _   
mobsf  |  |  \/  | ___ | |__/ ___||  ___|_   _| || | | || |  
mobsf  |  | |\/| |/ _ \| '_ \___ \| |_  \ \ / / || |_| || |_ 
mobsf  |  | |  | | (_) | |_) |__) |  _|  \ V /|__   _|__   _|
mobsf  |  |_|  |_|\___/|_.__/____/|_|     \_/    |_|(_) |_|  
mobsf  | 
mobsf  | [INFO] 05/Nov/2025 18:32:58 - Author: Ajin Abraham | opensecurity.in
mobsf  | [INFO] 05/Nov/2025 18:32:58 - Mobile Security Framework v4.4.3
mobsf  | REST API Key: 094e3c59cccb9af88f16c7a7dca87197ff3db2cbdca6d19b74dc43722476410f
mobsf  | Default Credentials: mobsf/mobsf
mobsf  | [INFO] 05/Nov/2025 18:32:58 - OS Environment: Linux (debian 12 bookworm) Linux-6.14.0-33-generic-x86_64-with-glibc2.36
mobsf  | [INFO] 05/Nov/2025 18:32:58 - Python Version: 3.13.7
mobsf  | [INFO] 05/Nov/2025 18:32:58 - CPU Cores: 4, Threads: 8, RAM: 31.25 GB
mobsf  | [INFO] 05/Nov/2025 18:32:58 - MobSF Basic Environment Check
mobsf  | [INFO] 05/Nov/2025 18:32:58 - Checking for Update.
mobsf  | [INFO] 05/Nov/2025 18:32:58 - No updates available.

```

## Start Upload and SAST Scan 

```shell
curl -F 'file=@/home/ttow/temp/apkeep/com.spotify.music.apk' http://localhost:8000/api/v1/upload -H "Authorization: 094e3c****"
curl -X POST --url http://localhost:8000/api/v1/scan --data "scan_type=apk&file_name=com.spotify.music.apk&hash=846cdec965c3461a6a204c6f982f00ef" -H "Authorization: 094e3c****"
curl -s -X POST --url http://localhost:8000/api/v1/scorecard --data "hash=846cdec965c3461a6a204c6f982f00ef" -H "Authorization: 094e3c****" | jq '.app_name, .file_name, .version_name, .hash, .security_score'

"Spotify"
"com.spotify.music.apk"
"9.0.90.1229"
"846cdec965c3461a6a204c6f982f00ef"
52

```

Mobsf processing ...


```shell
mobsf  | [INFO] 05/Nov/2025 18:42:40 - MIME Type: application/octet-stream FILE: com.spotify.music.apk
mobsf  | [INFO] 05/Nov/2025 18:42:40 - Android APK uploaded
mobsf  | [INFO] 05/Nov/2025 18:47:59 - Scan Hash: 846cdec965c3461a6a204c6f982f00ef
mobsf  | [INFO] 05/Nov/2025 18:47:59 - Starting Analysis on: com.spotify.music.apk
mobsf  | [INFO] 05/Nov/2025 18:47:59 - Generating Hashes
mobsf  | [INFO] 05/Nov/2025 18:47:59 - Extracting APK
mobsf  | [INFO] 05/Nov/2025 18:48:00 - Unzipping
mobsf  | [INFO] 05/Nov/2025 18:48:00 - Parsing APK with androguard
mobsf  | [INFO] 05/Nov/2025 18:48:01 - Extracting APK features using aapt/aapt2
mobsf  | [INFO] 05/Nov/2025 18:48:01 - Getting Hardcoded Certificates/Keystores
mobsf  | [INFO] 05/Nov/2025 18:48:01 - Getting AndroidManifest.xml from APK
mobsf  | [INFO] 05/Nov/2025 18:48:01 - Converting AXML to XML with apktool
mobsf  | [INFO] 05/Nov/2025 18:48:07 - Parsing AndroidManifest.xml
mobsf  | [INFO] 05/Nov/2025 18:48:07 - Extracting Manifest Data
mobsf  | [INFO] 05/Nov/2025 18:48:07 - Manifest Analysis Started
mobsf  | [INFO] 05/Nov/2025 18:48:08 - App Link Assetlinks Check - [com.spotify.music.SpotifyMainActivity] https://spotify.test-app.link
mobsf  | [INFO] 05/Nov/2025 18:48:08 - App Link Assetlinks Check - [com.spotify.music.SpotifyMainActivity] https://spotify-alternate.test-app.link
mobsf  | [INFO] 05/Nov/2025 18:48:08 - App Link Assetlinks Check - [com.spotify.music.SpotifyMainActivity] https://spotify.app.link
mobsf  | [INFO] 05/Nov/2025 18:48:08 - App Link Assetlinks Check - [com.spotify.music.SpotifyMainActivity] https://spotify-alternate.app.link
mobsf  | [INFO] 05/Nov/2025 18:48:08 - App Link Assetlinks Check - [com.spotify.music.SpotifyMainActivity] https://spotify.link
mobsf  | [INFO] 05/Nov/2025 18:48:08 - App Link Assetlinks Check - [com.spotify.music.SpotifyMainActivity] https://www.spotify.com
mobsf  | [INFO] 05/Nov/2025 18:48:08 - App Link Assetlinks Check - [com.spotify.music.SpotifyMainActivity] https://auth-callback.spotify.com
mobsf  | [WARNING] 05/Nov/2025 18:48:09 - Invalid Host: www-testing.spotify.net
mobsf  | [INFO] 05/Nov/2025 18:48:09 - App Link Assetlinks Check - [com.spotify.payment.callback.PaymentCallbackActivity] https://www.spotify.com
mobsf  | [INFO] 05/Nov/2025 18:48:09 - Reading Network Security config from network_security_config.xml
mobsf  | [INFO] 05/Nov/2025 18:48:09 - Parsing Network Security config
mobsf  | [INFO] 05/Nov/2025 18:48:09 - Performing Static Analysis on: Spotify (com.spotify.music)
mobsf  | [INFO] 05/Nov/2025 18:48:10 - Fetching Details from Play Store: com.spotify.music
mobsf  | [INFO] 05/Nov/2025 18:48:10 - Checking for Malware Permissions
mobsf  | [INFO] 05/Nov/2025 18:48:10 - Fetching icon path
mobsf  | [INFO] 05/Nov/2025 18:48:10 - Library Binary Analysis Started
mobsf  | [INFO] 05/Nov/2025 18:48:10 - Reading Code Signing Certificate
mobsf  | [INFO] 05/Nov/2025 18:48:11 - Getting Signature Versions
mobsf  | [INFO] 05/Nov/2025 18:48:12 - Running APKiD 3.0.0
mobsf  | [INFO] 05/Nov/2025 18:48:27 - Trackers Database is up-to-date
mobsf  | [INFO] 05/Nov/2025 18:48:27 - Detecting Trackers
mobsf  | [INFO] 05/Nov/2025 18:48:38 - Decompiling APK to Java with JADX
mobsf  | [INFO] 05/Nov/2025 18:51:32 - Converting DEX to Smali
mobsf  | [INFO] 05/Nov/2025 18:51:32 - Converting classes.dex to Smali Code
mobsf  | [INFO] 05/Nov/2025 18:51:32 - Converting classes4.dex to Smali Code
mobsf  | [INFO] 05/Nov/2025 18:51:32 - Converting classes2.dex to Smali Code
mobsf  | [INFO] 05/Nov/2025 18:51:32 - Converting classes6.dex to Smali Code
mobsf  | [INFO] 05/Nov/2025 18:51:32 - Converting classes7.dex to Smali Code
mobsf  | [INFO] 05/Nov/2025 18:51:32 - Converting classes9.dex to Smali Code
mobsf  | [INFO] 05/Nov/2025 18:51:32 - Converting classes5.dex to Smali Code
mobsf  | [INFO] 05/Nov/2025 18:51:32 - Converting classes3.dex to Smali Code
mobsf  | [INFO] 05/Nov/2025 18:51:32 - Converting classes8.dex to Smali Code
mobsf  | [INFO] 05/Nov/2025 18:51:32 - Converting classes10.dex to Smali Code
mobsf  | [INFO] 05/Nov/2025 18:51:32 - Code Analysis Started on - java_source
mobsf  | [INFO] 05/Nov/2025 18:52:11 - Reading file contents for SAST
mobsf  | [INFO] 05/Nov/2025 18:52:35 - Android SBOM Analysis Completed
mobsf  | [INFO] 05/Nov/2025 18:53:26 - Android SAST Completed
mobsf  | [INFO] 05/Nov/2025 18:53:26 - Android API Analysis Started
mobsf  | [INFO] 05/Nov/2025 18:54:13 - Android API Analysis Completed
mobsf  | [INFO] 05/Nov/2025 18:54:13 - Android Permission Mapping Started
mobsf  | [INFO] 05/Nov/2025 19:18:48 - Extracting String data from APK
mobsf  | [INFO] 05/Nov/2025 19:18:49 - Extracting String data from Code
mobsf  | [INFO] 05/Nov/2025 19:18:49 - Extracting String values and entropies from Code
mobsf  | [INFO] 05/Nov/2025 19:19:02 - Starting Firebase Analysis
mobsf  | [INFO] 05/Nov/2025 19:19:02 - Looking for Firebase URL(s)
mobsf  | [INFO] 05/Nov/2025 19:19:03 - Checking for Firebase Remote Config
mobsf  | [INFO] 05/Nov/2025 19:19:06 - Maltrail Database is outdated!
mobsf  | [INFO] 05/Nov/2025 19:19:06 - Updating Maltrail Database
mobsf  | [INFO] 05/Nov/2025 19:19:06 - Saving to Database
mobsf  | [INFO] 05/Nov/2025 19:33:24 - Analysis is already Done. Fetching data from the DB...
```
## Prep android emulator for MOBSF DAST scan 

Use AndroidStudio to create emulator then prep docker network for the emulator

```shell
./start_avd.sh Pixel_3_XL 5556 /home/ttow/Downloads/open_gapps-x86-9.0-mini-20220503.zip 
Starting AVD Pixel_3_XL on port 5556
Waiting for emulator to boot...
Warning: socat is not installed. Skipping port forwarding with socat. This might be required for docker in Linux.
Installing PlayStore
Archive:  /home/ttow/Downloads/open_gapps-x86-9.0-mini-20220503.zip
signed by SignApk
 extracting: ./play/Core/backuprestore-all.tar.lz  
 extracting: ./play/Core/carriersetup-all.tar.lz  
 extracting: ./play/Core/configupdater-all.tar.lz  
 extracting: ./play/Core/datatransfertool-all.tar.lz  
 extracting: ./play/Core/defaultetc-common.tar.lz  
 extracting: ./play/Core/defaultframework-common.tar.lz  
 extracting: ./play/Core/extservicesgoogle-all.tar.lz  
 extracting: ./play/Core/extsharedgoogle-all.tar.lz  
 extracting: ./play/Core/gmscore-x86.tar.lz  
 extracting: ./play/Core/googlebackuptransport-all.tar.lz  
 extracting: ./play/Core/googlecontactssync-all.tar.lz  
 extracting: ./play/Core/googlefeedback-all.tar.lz  
 extracting: ./play/Core/googleonetimeinitializer-all.tar.lz  
 extracting: ./play/Core/googlepartnersetup-all.tar.lz  
 extracting: ./play/Core/gsfcore-all.tar.lz  
 extracting: ./play/Core/setupwizarddefault-all.tar.lz  
 extracting: ./play/Core/setupwizardtablet-all.tar.lz  
 extracting: ./play/Core/vending-x86.tar.lz  
/home/ttow/Android/Sdk/platform-tools/adb
play
Waiting for the emulator to be ready...
Press enter to continue
Installing PlayStore components
* daemon not running; starting now at tcp:5037
* daemon started successfully
restarting adbd as root
remount started
remount succeeded
Press enter to continue
remount succeeded
Press enter to continue
play/etc/: 10 files pushed, 0 skipped. 1.6 MB/s (104513 bytes in 0.064s)
play/framework/: 2 files pushed, 0 skipped. 3.5 MB/s (210982 bytes in 0.057s)
play/app/: 2 files pushed, 0 skipped. 25.4 MB/s (1640243 bytes in 0.062s)
play/priv-app/: 12 files pushed, 0 skipped. 237.3 MB/s (203418394 bytes in 0.818s)
PlayStore installed successfully

```
## MobSFy Android Runtime

MobSF Dynamic Analyzer Supports
• Genymotion Android VM version 4.1 - 11.0 (arm64, x86, and x86_64 upto API 30)
• Android Emulator AVD (non production) version 5.0 - 11.0 (arm, arm64, x86, and x86_64 upto API 30)
• Corellium Android VM (userdebug builds) version 7.1.2 - 11.0 (arm64 upto API 30)
Android version >= 9.0 recommended

```shell
[INFO] 05/Nov/2025 21:42:01 - Connecting to Android emulator-5556
[INFO] 05/Nov/2025 21:42:01 - Waiting for 2 seconds...
[INFO] 05/Nov/2025 21:42:19 - MobSFying Android instance
[INFO] 05/Nov/2025 21:42:20 - ADB Restarted
[INFO] 05/Nov/2025 21:42:20 - Waiting for 2 seconds...
[INFO] 05/Nov/2025 21:42:22 - Connecting to Android emulator-5556
[INFO] 05/Nov/2025 21:42:23 - Waiting for 2 seconds...
[INFO] 05/Nov/2025 21:42:25 - Restarting ADB Daemon as root
[INFO] 05/Nov/2025 21:42:25 - Waiting for 2 seconds...
[INFO] 05/Nov/2025 21:42:27 - Reconnecting to Android Device
[INFO] 05/Nov/2025 21:42:27 - Waiting for 2 seconds...
[INFO] 05/Nov/2025 21:42:30 - Found Android Studio Emulator
[INFO] 05/Nov/2025 21:42:30 - Remounting
[INFO] 05/Nov/2025 21:42:30 - Performing System check
[INFO] 05/Nov/2025 21:42:30 - Android API Level identified as 28
[INFO] 05/Nov/2025 21:42:31 - Android Version identified as 9.0
[INFO] 05/Nov/2025 21:42:31 - Android OS architecture identified as x86
[INFO] 05/Nov/2025 21:42:32 - Downloading binary frida-server-17.2.17-android-x86
[INFO] 05/Nov/2025 21:42:39 - Copying frida server for x86
[WARNING] 05/Nov/2025 21:42:46 - mitmproxy root CA is not generated yet.
[INFO] 05/Nov/2025 21:42:46 - MobSFying Completed!

```
