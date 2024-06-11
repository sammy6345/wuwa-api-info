# Wuthering Waves API's

## Gacha
https://aki-gm-resources-oversea.aki-game.net/aki/gacha/index.html#/record?
#### Variables
| Variable Name | Variable Type    | Possible Values                                                                                                                                                                                                  | Required | Additional info                                                                                                                              |
| ------------- | ---------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | -------------------------------------------------------------------------------------------------------------------------------------------- |
| svr_id        | alpha-num string | - `10cd7254d57e58ae560b15d51e34b4c8` (SEA)<br>- `591d6af3a3090d8ea00d8f86cf6d7501`<br>- `6eb2a235b30d05efd77bedb5cf60999e` (EU)<br>- `86d52186155b148b5c138ceb41be9650`<br>- `76402e5b20be2c39f095a152090afddc` (CN?) | yes      | Server ID, likely fixed based on server selected, 32 characters                                                                              |
| player_id     | int              | `123456789`                                                                                                                                                                                                      | yes      | It's your player ID                                                                                                                          |
| lang          | string           | - `zh-Hans`<br>- `zh-Hant`<br>- `en`<br>- `ja`<br>- `ko`<br>- `fr`<br>- `de`<br>- `es`                                                                                                                           | yes      | Language used in reply info                                                                                                                  |
| gacha_id      | int              |                                                                                                                                                                                                                  |          |                                                                                                                                              |
| gacha_type    | int              |                                                                                                                                                                                                                  | yes/no   | initial banner to load. Not required if viewing the web page through a browser, but will select the banner "NaN" with no results if left out |
| svr_area      | string           | - `global`                                                                                                                                                                                                       | no?      | presumably ether cn or global. (SEA used in personal testing, had global assigned to the variable)                                           |
| record_id     | string           |                                                                                                                                                                                                                  | yes      | 32 characters long, unknown use,                                                                                                             |
| resources_id  | string           |                                                                                                                                                                                                                  | no       | 32 characters long, unknown use                                                                                                              |

## Announcements

### Index
https://aki-gm-resources-oversea.aki-game.net/aki/announcement/index.html? `%VARIABLES_GO_HERE%` /#/

#### Variables
| Variable Name | Variable Type | Possible Values                                                                                                                                                                                                          | Required | Additional Info                                                                                                                       |
| ------------- | ------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | -------- | ------------------------------------------------------------------------------------------------------------------------------------- |
| sdk_version   | string        |                                                                                                                                                                                                                          | no       | game sdk version check?                                                                                                               |
| server_id     | string        | - `10cd7254d57e58ae560b15d51e34b4c8` (SEA)<br>- `591d6af3a3090d8ea00d8f86cf6d7501`<br>- `6eb2a235b30d05efd77bedb5cf60999e` (EU)<br>- `86d52186155b148b5c138ceb41be9650`<br>- `76402e5b20be2c39f095a152090afddc` (CN?) | yes      | same as svr_id above                                                                                                                  |
| lang          | string        |                                                                                                                                                                                                                          | yes      | Language used in reply info                                                                                                           |
| did           |               |                                                                                                                                                                                                                          | no       |                                                                                                                                       |
| role_id       | int           | `123456789`                                                                                                                                                                                                              | yes      | same as player_id from gacha url, it is the same as your player ID ingame                                                             |
| svr_area      | string        | - `global`                                                                                                                                                                                                               | no       |                                                                                                                                       |
| user_id       | int           | `123456789`                                                                                                                                                                                                              | no       | Not your player ID.                                                                                                                   |
| extend        |               | `extend`                                                                                                                                                                                                                 | no       | ¯\\_(ツ)_/¯                                                                                                                            |
| game_id       |               |                                                                                                                                                                                                                          | no       |                                                                                                                                       |
| channel       | int           | - `160`                                                                                                                                                                                                                  | yes      |                                                                                                                                       |
| platform      |               | - `Android`<br>- `PC`                                                                                                                                                                                                    | yes      | presumably they can have platform-specific announcements, which will only go to a single platform if only it is affected by something |
| channel_op    | ?             |                                                                                                                                                                                                                          | yes      | blank variable works, just have it in the url...                                                                                      |
| pkg_id        |               |                                                                                                                                                                                                                          | no       |                                                                                                                                       |

### JSON entry
https://aki-gm-resources-back.aki-game.net/gamenotice/G153/ `%SERVER_ID%` /entrypoint.json
(https://aki-gm-resources-back.aki-game.net/gamenotice/G153/10cd7254d57e58ae560b15d51e34b4c8/entrypoint.json)

%SERVER_ID% is in place of the Server ID for the respective server in the url to fetch. Returns JSON with the format 
```json
{
	"h5AppUrl":[
		"https://aki-gm-resources-oversea.aki-game.net/aki/announcement/index.html"
	],
	"contentUrl":[
		"https://aki-gm-resources-back.aki-game.net/gamenotice/G153/%SERVER_ID%/notice.json"
	]
}
```

### Game Announcement List (JSON)

https://aki-gm-resources-back.aki-game.net/gamenotice/G153/ `%SERVER_ID%` /notice.json
(https://aki-gm-resources-back.aki-game.net/gamenotice/G153/10cd7254d57e58ae560b15d51e34b4c8/notice.json)

#### Format

```json
"game":[ // Game and Community announcements
	{
		"contentPrefix":[ //
			"url here"
		],
		"red":1, //int
		"permanent":0, //int
		"id":"id string",
		"startTimeMs":1717322580000, //Date() compatable int.
		"endTimeMs":1717322580000, //same as above
		"platform": [1,2,3], //PC, Android, iOS? unknown which is which.
		"channel": [], //it appears to be empty by default.
		"whiteList": [],
		"tabTitle":{
			"language code":"string",
		},
		"tabBanner":{
			"language code":["url to banner image"],
		}
	},
	...
],
"activity":[ // Banners and ingame events
	{
		// Same format as above
	}
]
```


### Game Announcement content
The notices listed in the server's `notice.json` can all have their listing retrieved too.
Url: https://aki-gm-resources-back.aki-game.net/gamenotice/content/G153/ `%SERVER_ID%` / `%NOTICE_ID%` / `%LANG`.json
https://aki-gm-resources-back.aki-game.net/gamenotice/content/G153/591d6af3a3090d8ea00d8f86cf6d7501/10183/en.json
#### Format

```json
{
	"noticeId": "id string",
	"textContent": "Notice content (as html w/ inline styling)",
	"textTitle": "Notice title",
	"banner": "url for the image at the top of the banner"
}
```




## Launcher...

https://aki-config-cf.aki-game.net/JcTQ9ER793yUAUBMJbzOuHtSXgPrsTPd/index.json

https://cdn-aws-hw-mc.aki-game.net/prod/client/JcTQ9ER793yUAUBMJbzOuHtSXgPrsTPd/Windows/KeyList_1.0.0.json

Encoded json file

https://cdn-aws-hw-mc.aki-game.net/prod/client/JcTQ9ER793yUAUBMJbzOuHtSXgPrsTPd/Windows/config.json