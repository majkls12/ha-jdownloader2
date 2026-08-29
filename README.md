# JDownloader 2 Modern for Home Assistant

[![Check upstream image](https://github.com/majkls12/ha-jdownloader2/actions/workflows/update-upstream.yml/badge.svg)](https://github.com/majkls12/ha-jdownloader2/actions/workflows/update-upstream.yml)

An unofficial Home Assistant app that runs JDownloader 2 using the actively
maintained [`jlesage/jdownloader-2`](https://github.com/jlesage/docker-jdownloader-2)
container image.

The wrapper provides:

- `aarch64` support for Raspberry Pi 5 and `amd64` support;
- persistent JDownloader configuration through Home Assistant `addon_config`;
- read/write access to Home Assistant `/media`;
- a browser-based desktop on port 5801;
- upstream version monitoring through GitHub Actions;
- normal Home Assistant update notifications with user-controlled installation.

## Installation

1. In Home Assistant, open **Settings → Apps → App store** (called
   **Add-ons** in older versions).
2. Open the three-dot menu and select **Repositories**.
3. Add:

   ```text
   https://github.com/majkls12/ha-jdownloader2
   ```

4. Install **JDownloader 2 Modern**.
5. Start it and open `http://HOME_ASSISTANT_IP:5801`.
6. Set the JDownloader download directory to `/media/downloads`.

See [the app documentation](jdownloader2_modern/DOCS.md) for details.

## Automated upstream tracking

The scheduled workflow checks Docker Hub once per day for a newer stable
`jlesage/jdownloader-2` tag. When one is found, it updates the Home Assistant
manifest and changelog and commits the change. Home Assistant can then display
the update normally. Installing updates remains a user decision unless the user
explicitly enables automatic updates in Home Assistant.

## Credits

- Container image: [`jlesage/docker-jdownloader-2`](https://github.com/jlesage/docker-jdownloader-2), MIT licensed.
- JDownloader: AppWork GmbH.
- Wrapper: created with OpenAI Codex for MaJkl (`@majkls12`).

The JDownloader name and logo are used only to identify the wrapped
application and remain the property of their respective owner. The logo assets
are not covered by this repository's MIT License.

This is an unofficial community project and is not affiliated with or endorsed
by the upstream projects.

## License

The wrapper files in this repository are released under the MIT License. The
container image and JDownloader retain their own respective licenses.
