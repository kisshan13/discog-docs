---
sidebar_position: 1
id: g1
slug: creating-a-bot
---

# Creating a bot

If you haven't already installed the packages then you can do just by this command. And yes remember to initialize a new go project before starting.

```
go get github.com/kisshan13/discog
```

## Creating a new bot

```go
import (
	discog "github.com/kisshan13/discog"
)

func main() {
	bot, err := discog.NewBot("<token>", nil)
}
```

Here to create a new bot we can use `discog.NewBot` function which creates a new bot instance.

It takes two parameters:

- `token` : Discord bot token which you can get one for your bot from Discord Developer Portal
- `manager` : It's a command manager which `discog` provides which is responsible for the intraction handling of the bot.

**⚠️ You need to have command manager then only you can run your bot**

## Running the bot

```go
bot.Run(func(session *discordgo.Session, err error) {
		if err != nil {
			panic(err)
		}
		log.Println("Bot is running")
	})
```


### Full Code

```go
import (
	log
	"github.com/bwmarrin/discordgo"
	discog "github.com/kisshan13/discog"
)

func main() {
	bot, err := discog.NewBot("<token>", nil)

	bot.Run(func(session *discordgo.Session, err error) {
		if err != nil {
			panic(err)
		}
		log.Println("Bot is running")
	})
}
```

[See a working example](https://github.com/kisshan13/discog-examples)