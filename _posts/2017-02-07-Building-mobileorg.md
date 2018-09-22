---
layout: post
title: Building MobileOrg
tags: [android, avd, debian, emacs, emulator, linux, mobileorg]
---

    ported from my old blog

So today i tried to build [MobileOrg](https://github.com/matburt/mobileorg-android) in android studio, couldent even get the emulator to start. Complains:
> Cannot launch AVD in emulator.
Output:
libGL error: unable to load driver: i965_dri.so  
libGL error: driver pointer missing  
libGL error: failed to load driver: i965  
libGL error: unable to load driver: i965_dri.so  
libGL error: driver pointer missing  
libGL error: failed to load driver: i965  
libGL error: unable to load driver: swrast_dri.so  
libGL error: failed to load driver: swrast  
X Error of failed request:  GLXBadContext  
Major opcode of failed request:  155 (GLX)  
Minor opcode of failed request:  6 (X_GLXIsDirect)  
Serial number of failed request:  55  
Current serial number in output stream:  54  
libGL error: unable to load driver: i965_dri.so  
libGL error: driver pointer missing  
libGL error: failed to load driver: i965  
libGL error: unable to load driver: i965_dri.so  
libGL error: driver pointer missing  
libGL error: failed to load driver: i965  
libGL error: unable to load driver: swrast_dri.so  
libGL error: failed to load driver: swrast  
X Error of failed request:  GLXBadContext  
Major opcode of failed request:  155 (GLX)  
Minor opcode of failed r  
  
Turns out theres a problem that android supplied stdc++ not being compatible with the rest of the system.
This fixed it for me: (Debian stretch linux)

Backup:
> android_sdk_dir="~/<em>your_location</em>"  
<del>mv ${android_sdk_dir}/tools/lib64/libstdc++/libstdc++.so.6 ${android_sdk_dir}/tools/lib64/libstdc++/libstdc++.so.6.bak</del>  
mv ${android_sdk_dir}/emulator/lib/libstdc++/libstdc++.so.6 ${android_sdk_dir}/tools/lib64/libstdc++/libstdc++.so.6.bak

Link system to Android:
> ln -s /usr/lib/x86_64-linux-gnu/libstdc++.so.6 ${android_sdk_dir}/tools/lib64/libstdc++/libstdc++.so.6  
<ins>use ln -s /usr/lib/libstdc++ in arch</ins>

(obviously substituting your own ${android_sdk_dir})  
now the emulator boots but wont close...
credit for this solution goes to [stackoverflow.com](http://stackoverflow.com/questions/36189393/android-studio-avd-error-launching") and [code.google.com](https://code.google.com/p/android/issues/detail?id=197254#c23)  

FYI -  Mobileorg is an android app that can sync and edit org files made in emacs (my current choice of text editor). I plan to work on mobileorg, theres an entry in a todo list in an org file somewhere....
