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
curl -X POST --url http://archer:8000/api/v1/scan --data "scan_type=apk&file_name=com.spotify.music.apk&hash=846cdec965c3461a6a204c6f982f00ef" -H "Authorization: 094e3c****"
curl -X POST --url http://localhost:8000/api/v1/scan --data "scan_type=apk&file_name=com.spotify.music.apk&hash=846cdec965c3461a6a204c6f982f00ef" -H "Authorization: 094e3c****"
curl -s -X POST --url http://localhost:8000/api/v1/scorecard --data "hash=846cdec965c3461a6a204c6f982f00ef" -H "Authorization: 094e3c****" | jq '.app_name, .file_name, .version_name, .hash, .security_score'

"Spotify"
"com.spotify.music.apk"
"9.0.90.1229"
"846cdec965c3461a6a204c6f982f00ef"
52

```
