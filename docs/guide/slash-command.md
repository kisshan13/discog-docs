---
sidebar_position: 1
id: g3
slug: slash-command
---

# Slash Commands

## Creating a slash command

To cretae a slash command you can use `discog.NewSlashCommand` function.

Example :

```go
command := discog.NewSlashCommand(discordgo.ApplicationCommand{
		Name:        "hello",
		Description: "Replies with a Hii message",
	})
```

This will create a slash command.

You can refer to [offical discord go](https://pkg.go.dev/github.com/bwmarrin/discordgo) package for more information about creating ApplicationCommand

## Adding handler to command

For now we just define the command details but we don't have the logic to handle the command. We can handle command using `SetHandler` function.

```go
    command := discog.NewSlashCommand(discordgo.ApplicationCommand{
		Name:        "hello",
		Description: "Replies with a Hii message",
	})

	command.SetHandler(func(ctx *discog.Ctx) {

		ctx.SetContent("Hii")
		err := ctx.Send()
		if err != nil {
			println(err.Error())
		}
	})
```

On using this command bot will respond like this :

![Bot info](./img/bot-res.webp)

Now the handler function will take a patameter `ctx` which contains the methods and information about the interaction.

Few things which you used from the `discog.Ctx` :

- Session `*discordgo.Session`
- Interaction `*discordgo.InteractionCreate`

And also you can see the [API reference](https://pkg.go.dev/github.com/kisshan13/discog) for more information.

## Adding Slash command to group

To add the command to our group we can use `AddCommand` function.

```go title="main.go"
command := discog.NewSlashCommand(discordgo.ApplicationCommand{
	Name:        "hello",
	Description: "Replies with a Hii message",
})

command.SetHandler(func(ctx *discog.Ctx) {
	ctx.SetContent("Hii")
	err := ctx.Send()
	if err != nil {
		println(err.Error())
	}
})

group := discog.NewCommandGroup("Simple", "Public Commands for the Bot", "")
group.AddCommand(command)

```

## Full Code

```go title="main.go"
import (
	log
	"github.com/bwmarrin/discordgo"
	discog "github.com/kisshan13/discog"
)

func main() {

	command := discog.NewSlashCommand(discordgo.ApplicationCommand{
		Name:        "hello",
		Description: "Replies with a Hii message",
	})

	command.SetHandler(func(ctx *discog.Ctx) {
		ctx.SetContent("Hii")
		err := ctx.Send()
		if err != nil {
			println(err.Error())
		}
	})

	group := discog.NewCommandGroup("Simple", "Public Commands for the Bot", "")
	group.AddCommand(command)

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
Now this will register a command named hello to your bot. And It'll reply with a `Hii` message to that interaction.