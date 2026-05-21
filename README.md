# Mattermost Voice Plugin — Metaviz fork

> **This is a patched fork** of [streamer45/mattermost-plugin-voice](https://github.com/streamer45/mattermost-plugin-voice) used internally at Metaviz.
>
> Changes vs. upstream `v0.3.0`:
>
> - The post emitted on `/voice` carries `file_ids: [<id>]` in addition to the original `type: "custom_voice"` and `props.fileId`. Without `file_ids`, voice messages were invisible on Mattermost mobile (mobile clients don't load plugin webapp bundles and therefore never render `custom_voice` posts).
> - The inline player UI was rewritten to match Mattermost mobile's voice-message look — circular play button, draggable scrubber with floating thumb, duration text, and a download icon. Touch-enabled.
> - A `:has()` CSS rule hides the duplicate file-attachment card that Mattermost auto-renders alongside the custom `PostType` (we need `file_ids` for mobile but on web our `PostType` already renders the audio inline).
>
> Result: identical voice-message UX on web and mobile, no duplicate UI on web.

---

This plugin adds support for basic **voice messaging** in Mattermost.

![](https://i.imgur.com/hPZ3GhG.gif)

## Demo

A demo server running the latest version of this plugin is located [here](https://mm.krad.stream/testing/channels/town-square).  
You can login using the following details:

```
Username: demo
Password: password
```

## Usage

To start sending a voice message you can either use the ```/voice``` slash command or the existing file attachment functionality as shown in the picture above.

## Limitations

This plugin only works on web client and desktop app. Mobile native apps are **not** [supported](https://developers.mattermost.com/extend/plugins/mobile/).

## Installation

1. Download the latest version from the [release page](https://github.com/streamer45/mattermost-plugin-voice/releases).
2. Upload the file through **System Console > Plugins > Plugin Management**, or manually upload it to the Mattermost server under plugin directory. See [documentation](https://docs.mattermost.com/administration/plugins.html#set-up-guide) for more details.

## Development

Use ```make dist``` to build this plugin.

Use `make deploy` to deploy the plugin to your local server.

Before running `make deploy` you need to set a few environment variables:

```
export MM_SERVICESETTINGS_SITEURL=http://localhost:8065
export MM_ADMIN_USERNAME=admin
export MM_ADMIN_PASSWORD=password
```

For more details on how to develop a plugin refer to the official [documentation](https://developers.mattermost.com/extend/plugins/).

## License

[mattermost-plugin-voice](https://github.com/streamer45/mattermost-plugin-voice) is licensed under [MIT](LICENSE)  
[mp3rec-wasm](https://github.com/streamer45/mp3rec-wasm) is licensed under [MIT](LICENSE)  
[LAME](http://lame.sourceforge.net/) is licensed under [LGPL](vendor/lame/COPYING)  
