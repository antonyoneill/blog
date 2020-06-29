# Remarkable Syncthing

In order to replace the remarkable cloud sync with an arguably more secure/trusted cloud sync I am using Syncthing.

## Installation

Following the notes from Evidlo:

0. [Install entware on remarkable](https://github.com/antonyoneill/remarkable_entware)
0. [Install and configure Syncthing](https://github.com/antonyoneill/remarkable_syncthing)

## Folder Configuration

I recommend symlinking some of the directories within the root filesystem so that while syncthing the configuration folder it's not possible to fill the drive. (Doing so may lock you out)

Recommended links:

```bash
mv /usr/share/remarkable /home/remarkable-resources
ln -s /home/remarkable-resources /usr/share/remarkable
```

Recommended Folder Sync in Syncthing

* `/home/root/.local/share/remarkable/xochitl` - `remarkable-notepads`
* `/home/root/.config/remarkable/xochitl` - `remarkable-config`
* `/home/remarkable-resources` - `remarkable-resources`

## Post Remarkable Update

When the remarkable tablet is updated, customised files are often replaced.

You'll want to carefully override the files in `/home/remarkable-resources` with the new files from ReMarkable. Then relink the `remarkable-resources` folder as above.

Next up, you'll also need to re-activate the entware installation using the script in the [remarkable_entware repo](https://github.com/antonyoneill/remarkable_entware)
