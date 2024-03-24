# Bots User Story
> Note: This is a "meta" use case. It covers the scenario of creating bots with Wing through a Slack/OpenAI example. But the plan for this use case is to create three (3) types of bots: Slack, Discord and GitHub. For each one we will build the relevant collaterals and narratives but the technical foundation should be similar.

Amiel, a hip designer at a hip startup, is falling in love with ChatGPTs photo creation capabilities. He wants to build a Slack Bot that can create visual designs using his company's visual design style. His team will be able to use this bot to generate visuals for blogs, social posts and all that jazz.

He searches online for "How to build a slack bot with ChatGPT?" and finds a post written by the infamous Nathan Tarbert, a community engineer from the Wing team. The blog explains how to make a Slack Bot that can draw pictures using OpenAI and Wing. Imagine his surprise! This is exactly what he was looking for!

> Alternatively, Amiel is directed to the dev.to article, which leads to the blog.

> Alternatively, Amiel searches Reddit under r/slack and discovers this blog post.

> Alternatively, Amiel's colleague, Elad Cohen, mentions seeing a funny TikTok from the Wing team about the neat integration of Open AI, Slack, and Wing and suggests finding a solution in the Wing project.

---

Title: **How to build and deploy a ChatGPT Slack Bot with Wing**

This guide will walk you through building and deploying a fully working Slack Bot on Wing Cloud integrated with OpenAI's API.

Our bot will be triggered by "@mentions" on a Slack channel and use ChatGPT to produce a response. It can be used for a million different things. We are going to deploy this application on AWS in 3 minutes!

[Let us know](https://t.winglang.io/slack) what you are building it with it.

If you like, you can also check out these resources:

- Watch this [demo video](https://wing.cloud/videos/slack-bot)
- Sign up for an [online workshop](https://wing.cloud/workshops/slack-bot)

Before we get started, a few words about Wing. Wing is a new open-source framework for building serverless applications. Wing's mission is to offer the best serverless developer experience on the planet. One of the biggest pains people have when using serverless is that they constantly have to wait for deployments, and what I love most about Wing is the Wing Simulator which allows you to develop your entire serverless application without having to deploy anything on the cloud. Let's get started and you'll see what I mean.

The Wing framework currently supports two programming languages: TypeScript and [Winglang](https://wing.cloud/winglang). For the purposes of this post, This post is available in both, so pick the one you love!

So without further ado, brin in the BOTS!

## Creating a new application

Let's start by installing the Wing CLI (you'll need Node.js >= 10.x installed):

```bash
npm i -g wingcli
```

You can check the CLI version like this:

```bash
wing --version
0.62.1
```

> As you can see, Wing is still in pre-release, so expect some hiccups and don't be shy reporting issues or get help from the awesome people hanging out on the Wing slack.

Ok, now that we have the Wing CLI installed, let's create a new project using the `ai-slack-bot` quick-start:

```bash
$ mkdir my-slack-bot
$ cd my-slack-bot
$ wing new ai-slack-bot
```

## Exploring your new project

Some files were created from this quick-start project. You'll see 3 files `README.md`, `main.w` and `package.json`.

Let's take a look at the `main.w` file:

```js
bring slack;
bring openai;
bring cloud;

const bot = new slack.App() as "slack";

const ai = new openai.OpenAi() as "openai";

bot.onEvent("app_mention", inflight (ctx, event) => {
  let mention = slack.AppMentionEvent.fromJson(event);

  let images = ai.generateImage(
    model: "dall-e-3",
    prompt: mention.text,
    size: "1024x1024"
  );

  let message = new slack.Message();
  message.addImage(images.at(0), alt: message);
  ctx.thread.post(message);
});
```

The behavior should be pretty self explanatory: when our bot is @mentioned in a Slack channel, we send a request to OpenAI to generate the image and we post back the result in a thread.

Cool, ha?

## Configure your Slack application

Head over to the Slack API Dashboard and create a new Slack app for out bot. 

Then within the `OAuth & Permissions` section, add the following scopes to your bot token:
- `app_mentions:read`
- `chat:write`

Once the scopes are defined, install the app to your workspace and copy the `Bot User OAuth Token` and `Signing Secret` to be used in the next step.

### Subscribing to Slack events

In order for Slack to be able to send messages to your app, we will need to add a new event subscription. Navigate to the `Event Subscriptions` section and enable events.

Under `Subscribe to bot events`, add the following events:
- `app_mention`

## Configure your OpenAI API key

(TODO: add instructions on how to get an OpenAI API key. Which can be done in the blog)

## Configuring your application 

In order for our app to be able to work it will need:

1. Configure a Slack app and provide the following Slack credentials:
  - `SLACK_SIGNING_SECRET`
  - `SLACK_BOT_TOKEN`
2. Configure an OpenAI API key and provide the following OpenAI credentials:
  - `OPEN_AI_API_KEY`

These credentials can be provided either through environment variables or through the `wing.toml` file. In a production environment, it is recommended to use environment variables.

## Testing your application locally

When you are ready to test the application locally, you can run the following command:

```bash
wing it
```

This will start the Wing Simulator and run your application locally. In the simulator your bot will use Slack Sockets so no need to use a redirect URL just yet.

Once its running you can go ahead and give it a try by mentioning your bot in a Slack channel. 

> Note: Be sure to try this in a channel where the bot is in, otherwise it won't work. To add the bot to a channel you just need to add it in the channel integrations.

## Deploying your application to AWS

Once you are happy with the bot and want to deploy it to the cloud, we just need to compile to the `tf-aws` target and deploy it using Terraform:

```bash
wing compile -t tf-aws
terraform -chdir=./target/main.tfaws init
terraform -chdir=./target/main.tfaws apply -auto-approve
```

In the output of the `apply` command you will see a Redirect URL that you will need to add to your Slack app configuration, in the Event subscriptions section.

And that's it! You now have a fully working Slack bot that can generate images using OpenAI's API.