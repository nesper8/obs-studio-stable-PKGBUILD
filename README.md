# obs-studio-stable-PKGBUILD
Stable obs-studio PKGBUILD for Arch Linux with ftl-sdk obs-browser and obs-vst

I have also disabled VLC plugin

Omit this flag to re-enable it
```
-DDISABLE_VLC=ON \
```

### Additional Dependancies
* Pipewire (Wayland Support)
* cef-minimal (Browser Extension)

### Additional Notes
Please do note that I'm only hosting my PKGBUILD (which is ultimately just a build script for Arch OS) and the precompiled versions of OBS using my PKGBUILD
If you encounter a major bug within OBS please contact the OBS Team
