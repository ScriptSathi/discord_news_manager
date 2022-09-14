# [Deep search gatherer](https://github.com/ScriptSathi/Deep_Search_Gatherer)

## Prerequisite

- Docker Compose version v2.6.0 or higher

## <a name="introduction">Introduction</a>

This project is a full featured RSS **discord bot** using 2 services over a docker compose. It is used to track RSS feeds / youtube channels / twitter accounts / subreddit or common websites and post it over discord channels
-  The [discord information gatherer bot](https://github.com/ScriptSathi/discord_information_gatherer) who track RSS feeds, youtube channel, twitter accounts and subreddit and publish it on discord 
- The [scrape2RSS](https://github.com/ScriptSathi/scrape2RSS/) who generate an RSS feed based on a simple url

## <a name="features">Features</a> 

example url that can be tracked (you can put this in your config file to try it)
- A Twitter account `@MyTwitterAccount`
- A Subreddit `r/MySubreddit`
- A very common RSS feed url `https://www.cert.ssi.gouv.fr/alerte/feed/`
- A youtube channel `https://www.youtube.com/c/LiveOverflow`
- A static webpage `https://www.synacktiv.com/publications`

## <a name="disclaimer">Disclaimer</a>

This project need docker to be installed and this **is not** intended as an introduction to docker.

 If you are unfamiliar with Docker, check out the [Introduction to Docker](https://training.docker.com/introduction-to-docker) webinar, or consult your favorite search engine.

## <a name="prepare">Prepare the project</a>

Before starting the project you need to pull git submodules and build the docker images.
```
bash init.sh
```

## <a name="start">Start the project</a>

After you added your configuration file in `config_file` (view next section for this part), just run the below command
```
docker compose -d up
```

## <a name="config-file">Create the config file</a>

The configuration file is compatible with either `json` and `yaml` (or `yml`) format.
View the documentation [here](https://github.com/ScriptSathi/discord_information_gatherer) for json usage.
<br/>
**Put your configuration file in the `config_file/` directory**

## <a name="bot-cmds">Bot Commands</a>

To interact with the bot, simply tag the bot at the beggining of the message(`@Information Gatherer` by default)

| Commands | Explanations 
|----|----|
| `add` | No Aliases <br/> __Parameters__: <br/>- just give the desired url after specifying the "add" command <br/> - `channel`: the channel ID where you want to post news on (you need to enable dev mode in your discord settings) <br/> - `name`: (optional) Chose a name for the registered feed|
| `delete` |  Aliases: `del` / `dl` <br/> Take the name of the feed to delete as parameter|
| `help` | Aliases: `-h` / `` (no params) <br/> Display the help menu |
| `list` | List all the registered feeds in your server |

### Examples
####  Add Youtube channel or an RSS feed
```bash
@Information Gatherer add https://www.youtube.com/c/LiveOverflow channel 1009496824605843607
```
```bash
@Information Gatherer add https://www.youtube.com/c/LiveOverflow channel 1009496824605843607 name LiveOverflow
```
####  Add Twitter
```bash
@Information Gatherer add @LiveOverflow channel 1009496824605843607
```
####  Add Reddit
```bash
@Information Gatherer add r/netsec channel 1009496824605843607
```
####  Delete a feed
```bash
@Information Gatherer del LiveOverflow
```
####  List feeds
```bash
@Information Gatherer ls
```

## <a name="min-config">Minimal configuration needed</a> 
```
token: <TOKEN>
```

## <a name="allow-parameters">Configuration parameters</a> 

| Parameters | Explanation | Default value |
|----|----| ----|
| `token` | Your bot token, it's **mandatory** variable. | "" |
| `refresh-time` | Time between refreshes of a feed, in second | 900 |
| `published_since_default` | Maximum age of news before it's discarded, in second. Used only when `published_since` of a feed is not set. <br/>If `published_since_default` or `published_since` are equal to `0`, only posts published after the initialization of this bot will be sent (usefull in case you use [Scrape2RSS feature](https://github.com/ScriptSathi/scrape2RSS)) | 0 |
| `gameplayed` | Change the game displayed in bot profile | "Eating some RSS feeds" |
| `twitter` |<li>`enabled` (default: False) - Enable the feature<li>`bearer_token` (default: "") Needed to auth the Twitter API | [] |
| `reddit` |<li>`enabled` (default: False) - Enable the feature<li>`client_id` (default: "") Needed to auth the Reddit API<li>client_secret (default: "") Needed to auth the Reddit API<li>`password` (default: "") Needed to auth the Reddit account for accessing reddit data<li>`username` (default: "") Needed to auth the Reddit account for accessing reddit data | [] |


## [Scrape2RSS feature](https://github.com/ScriptSathi/scrape2RSS)

If you want to follow a website that doesn't have an RSS feed, submit the URL of the page in the `url` parameter like a normal feed.
To be used, you need to set the [full bot project](https://github.com/ScriptSathi/Deep_Search_Gatherer)

## <a name="youtube-feature">Youtube Feature</a> 

To follow a youtube channel just put the youtube url in the `url` field.

Format tested: 
- `https://www.youtube.com/c/<Channel-Name>`
- `https://www.youtube.com/user/<Channel-Name>`