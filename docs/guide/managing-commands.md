---
id: g2
sidebar_position: 1
slug: managing-commands
---

# Managing Commands

Discog have two main components to manage commands.

- Command Manager : This is the manager which must have all the commands which you want your bot to have.
- Command Group : You can group your commands into category for that purpose a `CommandGroup` .

## Command Manager

Discog has it's own way to register commands to Discord API. You can use `CommandManager` to auto register & unregister commands from your bot.

Here's how you can create one command manager for your bot.

```go
manager := discog.NewCommandManager()
```

This will create a command manager for your bot. But currently you don't have any commands which your user can interact with your bot.

Discog also provides a great way to manage like-commands i.e let's say you want to have moderation commands the you can create a command group like `moderationGroup`, which you can add to your command manager using `AddGroup` function.

Example :

```go
manager := discog.NewCommandManager()
manager.AddGroup(moderationGroup)
```

## Command Group

Creating a command group :

```go
group := discog.NewCommandGroup("Simple", "Public Commands for the Bot", "")
```

Now this will create a command group. It will take 3 parameters :

- `name`: The name of the command group.
- `description`: Description for the command group.
- `guildId`: Guild ID for the command to register. **Empty for all Server**.

**Why command group?**

You can use command group to frame `help` command and providing commands specific to server.

Still you don't have any command so now in the next section we'll see how we can add **Slash Commands** to our command manager.

## Full Code

```go
import (
	log
	"github.com/bwmarrin/discordgo"
	discog "github.com/kisshan13/discog"
)

func main() {
	group := discog.NewCommandGroup("Simple", "Public Commands for the Bot", "")

	manager := discog.NewCommandManager()
	manager.AddGroup(group)

	bot, err := discog.NewBot("<token>", manager)

	bot.Run(func(session *discordgo.Session, err error) {
		if err != nil {
			panic(err)
		}
		log.Println("Bot is running")
	})
}
```

[See a working example](https://github.com/kisshan13/discog-examples)
