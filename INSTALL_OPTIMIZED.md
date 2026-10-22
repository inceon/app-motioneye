# motionEye Optimized for Home Assistant

This fork builds motionEye from `inceon/motioneye`, pinned to commit
`40b6708ac9cb10443d9a8fa4847fbd63b588be05`. It includes movie-player cleanup,
nonblocking and atomic previews, thumbnail timeouts, background MP4 faststart,
and content-based cache invalidation for the player script. Version
`0.45.0-optimized.2` also adds FPS-based snapshot scheduling, hidden-tab pauses,
correct FPS reporting, touch sliders, and responsive settings and dialogs.

## Publish and install

1. Push `feature/local-setup` in `inceon/motioneye`. The pinned source archive
   must be accessible to the HA builder.
2. Commit and push this app repository to its `main` branch.
3. In Home Assistant open **Settings → Apps → Install app → menu → Repositories**
   and add `https://github.com/inceon/app-motioneye`.
4. Select **Check for updates** if necessary, then install **motionEye Optimized**
   from the Inceon repository. There is no `image` key in its config: Supervisor
   builds the image on your HA machine. The first installation can take a while.

The ordinary motionEye source repository is not an app-store repository;
add this app repository instead. Official release images and the upstream
Edge update do not contain these custom changes.

## Move your configuration

1. Create a Home Assistant backup of your running motionEye app. Separately
   ensure important recordings are backed up; shared media is not necessarily
   included in an app-only backup.
2. In the existing motionEye UI export **General Settings → Configuration → Backup**.
3. Stop the existing app. Both apps use host networking and the same internal
   backend port, so do not run them simultaneously.
4. Configure the new app with the same app options, start it, and import your
   motionEye configuration using **General Settings → Configuration → Restore**.
5. Check each camera's storage path. The app maps `/share` and `/media`; keep
   existing recordings at their current paths and verify the new app can read
   and write those paths.
6. Verify live video, the movie list, playback, switching recordings, and a new
   recording through **Open Web UI** before enabling the new app's watchdog or
   starting it automatically at boot. Keep the old app stopped for rollback.

Home Assistant stores app-private `/data` separately for each repository/app ID.
Installing this app does not automatically import the old app's configuration.
To roll back, stop the optimized app and start the original app.

## Existing video files

Faststart is applied to newly completed MP4 recordings without re-encoding.
Existing archive recordings are not automatically converted. Choose H.264 for
new recordings if the camera/source supports it; faststart does not change
HEVC into H.264. The four converted demo recordings on the development computer
are separate from recordings in Home Assistant.

## Local testing instead of publishing

Copy the `motioneye` directory into Home Assistant's local-apps directory using
Terminal & SSH or Samba, refresh the app store, then install the local app.
Keep `image` absent from `config.yaml` so Supervisor builds this Dockerfile.
