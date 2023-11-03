# Home Assistant Add-on: PlexRipper

## How to use

This addon starts a PlexRipper instance within HomeAssistant.
You can change the root path setting and set it to /share/PlexRipper to get access to media in ha.

For more info see [full documentation](https://plexripper.rocks) or checkout the [Git repository](https://github.com/frosit/addon-plexripper).

> Note: This addon is under development

## Configuration

* plexripper_root: The parent directory for folders like /Music, /Downloads etc.
* plexripper_publish: The parent directory where the application is exported after build/publishing

## Building

During container build, a version of PlexRipper is created under `/opt/plexripper`. If you set the `plexripper_publish` config option to that path, it would probably not build again from scratch.