# just_audio_handlers

## Description
A few composable implementations of @ryanheise 's [audio_service](https://github.com/ryanheise/audio_service) `AudioHandler`.
There are:
1. The base handler, which works with [just_audio](https://pub.dev/packages/just_audio)
2. A handler which can persist the current position, either to memory or HiveDb (or you can define your own persistance layer. For example, if youre app has many audio files, persisting current position (even to memory) allows you to support seeking even on other audio files which aren't currently playing, and play will start at the right place
3. A download handler, which works with a downloader class (supplied is an implementation which works with flutter_downloader), and will play from offline file if it's there.

In addition, there are some conveniance things.
1. A `DownloadButton` widget
2. Various streams, which combine media item and playback state, optionaly the persisted position also

## State
### 🚧 In production app, written for my use case, use with caution 🚧
Originally, this was written to work with the `playFromUri` family of methods.
Now, I use `playFromMediaId` etc, which relies on `getMedia` by ID.
It might still be usable without implementing `getMedia`, but I haven't tested that, and probably won't get around to it unless I need it.
A PR to fix that (if broken) would be welcome.

## TODO
Todo

## History
This is roughly my 7th major rewrite of audio handling.
1. My first run used one of the older audio_player(s)
2. Switched to an older version of audio_service with that audio player
3. Switched to an older version of just_audio (pretty much version 0.0.1)
4. The whole thing was a mess, so rewrote it
5. It was still a mess, so I rewrote it again, this time as its own plugin, [just_audio_service](https://github.com/yringler/just_audio_service)
6. That was pretty good for a while, then I tried updating it to null safety, and it just wasn't working. A problem it had is that it worked very hard to handle bugs which had already been fixed in audio_service and just_audio
7. This! It is massivley simplified over previous versions, because of the incredible work @ryanheise and all of the collaborators have put in to just_audio and audio_service, notably having one isolate, which massively simplifies a bunch of thorny problems, and the new composition API (which addmittedly was inspired by my own work in just_audio_service - a nice positive feedback loop).
