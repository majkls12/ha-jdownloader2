# JDownloader 2 Modern

This unofficial Home Assistant app runs JDownloader 2 using the actively
maintained [`jlesage/jdownloader-2`](https://github.com/jlesage/docker-jdownloader-2)
container. It supports `aarch64` (including Raspberry Pi 5) and `amd64`.

## First start

1. Start the app.
2. Select **Open Web UI**, or browse to `http://HOME_ASSISTANT_IP:5801`.
3. Open the **My.JDownloader** tab and sign in if remote access is wanted.
4. Under **Settings → General**, set the default download folder to:

   ```text
   /media/downloads
   ```

5. Disable **Subfolder by package name** if package folders are not wanted.

> Do not use `/output`. It is not mapped to persistent Home Assistant storage
> by this wrapper. Downloads should be stored below `/media`.

## Persistent data and backups

JDownloader configuration and state are stored in the app-specific
`addon_config` folder, mounted as `/config` inside the container. Home Assistant
includes it when this app is selected in a backup. Downloaded files below
`/media` are separate and are not part of the app backup.

## Running beside another JDownloader app

The web interface uses host port `5801`. Port `3129` is intentionally not
exposed, allowing an older JDownloader app to keep using that port. Cloud-based
MyJDownloader access still works; only direct LAN mode is unavailable.

## Updates

Container updates are deliberately installed through Home Assistant. This
repository checks upstream releases automatically and bumps the app manifest
when a newer stable `jlesage/jdownloader-2` tag appears. Home Assistant then
offers a normal update, leaving installation under the user's control.

JDownloader can still update its own core and plugins inside the persistent
configuration. `KEEP_APP_RUNNING=1` lets the container restart JDownloader
without terminating the whole Home Assistant app.

## Repairing JDownloader

The upstream container supports repairing an installation by creating a file
named `.fix_jd_install` under `/config` and restarting the app. Make a backup
before using this function. See the upstream documentation for details.

## Security

The web UI is exposed on the local network without authentication by default.
Do not forward port `5801` directly to the internet.

## Credits and disclaimer

- Container: [`jlesage/docker-jdownloader-2`](https://github.com/jlesage/docker-jdownloader-2)
  by Jocelyn Le Sage, licensed under the MIT License.
- JDownloader is developed by AppWork GmbH.
- Home Assistant is a project of the Open Home Foundation.
- This unofficial wrapper was created with OpenAI Codex for MaJkl (`@majkls12`).

The JDownloader name and logo are used only to identify the wrapped
application and remain the property of their respective owner. The logo assets
are not covered by this wrapper's MIT License.

This project is not affiliated with or endorsed by JDownloader, AppWork GmbH,
Jocelyn Le Sage, Home Assistant, or the Open Home Foundation.
