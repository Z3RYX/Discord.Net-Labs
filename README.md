# Discord.Net Labs
[![NuGet](https://img.shields.io/nuget/vpre/Discord.Net.Labs.svg?maxAge=2592000?style=plastic)](https://www.nuget.org/packages/Discord.Net.Labs)
[![Discord](https://discord.com/api/guilds/848176216011046962/widget.png)](https://discord.gg/dvSfUTet3K)

This repo is a custom fork of Discord.Net that introduces the newest features of discord for testing and experimenting. Nothing here is guaranteed to work but you are more than welcome to submit bugs in the issues tabs

## Known issues
Labs will not work with Playwo's [InteractivityAddon](https://github.com/Playwo/Discord.InteractivityAddon). The reason is that his package depends on the base discord.net lib, you can get around this by cloning his repo and building it with discord.net labs instead of discord.net.

## How to use
Setting up labs in your project is really simple, here's how to do it:
1) Remove Discord.Net from your project
2) Add Discord.Net Labs nuget to your project
3) Enjoy!

## Branches
### Dev
The main branch we pull off of to introduce new features into, the dev branch is the same as Discord.Nets dev branch

### Interactions
This branch is for anything todo with Discord Interactions, such as [Slash commands](https://discord.com/developers/docs/interactions/slash-commands) and [Message Components](https://discord.com/developers/docs/interactions/message-components). This branch is stable enough to use but does not contain all the features of interactions. 

### SlashCommandService
This branch is on pause and does not work currently, Once everything is stable with the Interaction branch we will continue working on a slash command service for it.

### web/SlashCommandService
webmilio's spin on the SlashCommandService branch, again the state of this is unknown. 


## Message Components
So, you want to use Message components? Well you're in luck! Below is a quick overview of how to use them

#### Listening for button presses
```cs
// Subscribe to the InteractionCreated event
client.InteractionCreated += Client_InteractionCreated;

...
private async Task Client_InteractionCreated(SocketInteraction arg)
{
  // If the type of the interaction is a message component
  if(arg.Type == Discord.InteractionType.MessageComponent)
  {
    // parse the args 
    var parsedArg = (SocketMessageComponent)arg;
    // respond with the update message response type. This edits the original message if you have set AlwaysAcknowledgeInteractions to false.
    await parsedArg.RespondAsync($"Clicked {parsedArg.Data.CustomId}!", type: InteractionResponseType.UpdateMessage);
  }
}
```

#### Sending messages with buttons
Theres a new field in all `SendMessageAsync` functions that takes in a `MessageComponent`, you can use it like so:
```cs
var builder = new ComponentBuilder().WithButton("Hello!", ButtonStyle.Primary, customId: "id_1");
await Context.Channel.SendMessageAsync("Test buttons!", component: builder.Build());
```

## Slash commands
Slash command example how to's can be found [here](https://github.com/Discord-Net-Labs/Discord.Net-Labs/blob/Interactions/docs/guides/commands/application-commands.md). If you want to read some code using slash commands, you can do that [here](https://github.com/quinchs/SwissbotCore/blob/master/SwissbotCore/Handlers/AutoMod/Censor.cs)
