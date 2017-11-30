# groupme-bot
A package that allows "bots" to listen for, and reply to, GroupMe messages. Should be required by another express program and added as a route.

## Bots
Bots provide the mechanism to parse and reply to posted messages. Bots should extend the prototype provided by /bots/bot.js. Bots have the following properties:

  * **name:** A unique identifier for the bot. This is the path a POST request must follow to reach this bot, so it must be a valid URL path.
  * **id:** The GroupMe bot ID to use when posting
  * **consult:** A function that takes a GroupMe message to be processed. Must be overridden by subclasses.
  * **post, postDelayed, and postTime:** Posts a message on this bot's behalf, optionally after some delay or at a specific time. Should be called by the bot's `consult` function. Takes the message to be posted. These are some common properties of the message object:
    * **text:** The text to display in the posted message

A Bot constructor should take the bot's ID as its only argument.

A bot will emit a `message` event when a message is posted.

## Bot Router
The botRouter function allows for the creation of an express.js Router that may run several bots simultaneously.

the botRunner function is given a BotGroup, and returns a Router object. For any bot in thr BotGroup, POST requests through the router to the path `/[bot.name]` will be directed to the bot.

## Debugging
Verbose logging can be enabled by setting the environment variable `BOT_VERBOSE` to any non-empty string.

With verbose logging enabled, information such as received / sent messages are displayed to `stdout`.