<img src="http://i.imgur.com/M9TvvSy.png" alt="clive-mascot" width=64px />

## ☝️ That's Clive

He's a very simple bot that monitors Twitch chat for clips and auto-posts them to Discord.

_**Like this!**_  
<img src="https://i.imgur.com/N1CFDLD.png" title="Rich Discord Example" />

## 🤖 Instructions

### Docker

```
docker create \
  --name=clive \
  -e DISCORD_WEBHOOK_URL= \
  -e TWITCH_CHANNELS=twitch \
  -e TWITCH_CLIENT_ID= \
  -e RESTRICT_CHANNELS=true \
  -e MODS_ONLY=false \
  -e SUBS_ONLY=false \
  -e BROADCASTER_ONLY=false \
  -e RICH_EMBED=true \
  -e URL_AVATAR=http://i.imgur.com/9s3TBNv.png \
  -e BOT_USERNAME=Clive \
  -v </path/to/appdata/db>:/db \
  --restart always \
  axothic/clive
```

### Docker-compose

```
version: "3"
services:
  clive:
    image: axothic/clive
    container_name: clive
    environment:
      - DISCORD_WEBHOOK_URL=
      - TWITCH_CHANNELS=twitch
      - TWITCH_CLIENT_ID=
      - RESTRICT_CHANNELS=true
      - MODS_ONLY=false
      - SUBS_ONLY=false
      - BROADCASTER_ONLY=false
      - RICH_EMBED=true
      - URL_AVATAR=http://i.imgur.com/9s3TBNv.png
      - BOT_USERNAME=Clive
    volumes:
      - </path/to/appdata/db>:/db #optional (consistent database)
    restart: always
```

### 🚩 Environment Flags

`ENVIRONMENT_NAME` (required or optional to be set) \[default production setting]

- **`DISCORD_WEBHOOK_URL` (required)**
  - Set this to your Discord webhook for the channel you want Clive to post in! [Discord webhook URL](http://i.imgur.com/sEUCxct.png)
- **`TWITCH_CHANNELS` (required)**
  - Set the channels you want Clive to monitor for clips. These are also used for `RESTRICT_CHANNELS` If you wanted to watch for clips in `Monstercat`'s chat, you would use `"monstercat"`. If you wanted to monitor multiple channels, you would use `"monstercat mrchowderclam updownleftdie"`.
- `TWITCH_CLIENT_ID` (optional, suggested) \[null]
  - Needed for Twitch API functionality. This allows Clive to get more data about the clip for its messages! More info: [Twitch Dev Getting Started](https://dev.twitch.tv/get-started)
- `RESTRICT_CHANNELS` (optional) \[true]
  - **REQUIRES**: `TWITCH_CLIENT_ID` to be set. If true, only shares clips that are listed in `TWITCH_CHANNELS`.
- `MODS_ONLY` (optional) \[false]
  - If true, only allows mods to post clips.
- `SUBS_ONLY` (optional) \[false]
  - If true, only allows subscribers to post clips.
- `BROADCASTER_ONLY` (optional) \[false]
  - If true, only allows the broadcaster to post clips. **NOTE**: broadcaster is **not** considered a mod by default on Twitch.
- `RICH_EMBED` (optional) \[true]

  - **REQUIRES**: `TWICH_CLIENT_ID` to be set. If true will post two messages to Discord the first being the video and the second being a rich embed box that contains more information about the clip. Two separate messages are necessary because Discord doesn't allow setting `video` element inside of the rich embed object.

`MODS_ONLY`, `SUBS_ONLY`, and `BROADCASTER_ONLY` can be combined. Example: turning all `BROADCASTER_ONLY` and `SUBS_ONLY` will only share clips posted by those two groups. All three set to `false` on means anyone can post a clip link. Be careful if you are not using a `TWITCH_CLIENT_ID` AND `RESTRICT_CHANNELS` or else ANY clips will be shared to your Discord.

## 📋 Todo

- ~~Option to only send clips of a certain channel or channels.~~
- ~~Option to only send clips posted by broadcaster, mods, or subs.~~
- ~~Set the `DISCORD_WEBHOOK_URL` to pull from an evar or something.~~
- ~~Track previously posted twitch clips~~
- ~~Use Discord Rich Embed messages~~
- Having a UI or hosting this somewhere would be nice.
- Make clive an actual Discord bot, but that would require actual work lol.
- ~~MFW the Readme is bigger than the app LUL~~

## 👯 Contributing

1.  Create your own feature branch (using `git checkout -b ...` or whatever you want to use).
2.  Write some nice code. Commit it! Push it!
3.  Use Github's excellent pull request feature to submit a PR.
4.  Someone will review your PR and merge to master!
5.  Yay.
