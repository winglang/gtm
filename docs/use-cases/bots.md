# Bots User Story
> Note: This is a "meta" use case. It covers the scenario of creating bots with Wing through a Slack/OpenAI example. But the plan for this use case is to create three (3) types of bots: Slack, Discord and GitHub. For each one we will build the relevant collaterals and narratives but the technical foundation should be similar.

Amiel, a hip designer at a hip startup, is falling in love with ChatGPTs photo creation capabilities. He wants to build a Slack Bot that can create visual designs using his company's visual design style. His team will be able to use this bot to generate visuals for blogs, social posts and all that jazz.

He searches online for "How to build a slack bot with ChatGPT?" and finds a post written by the infamous Nathan Tarbert, a community engineer from the Wing team. The blog explains how to make a Slack Bot that can draw pictures using OpenAI and Wing. Imagine his surprise! This is exactly what he was looking for!

> Alternatively, Amiel is directed to the dev.to article, which leads to the blog.

> Alternatively, Amiel searches Reddit under r/slack and discovers this blog post.

> Alternatively, Amiel's colleague, Elad Cohen, mentions seeing a funny TikTok from the Wing team about the neat integration of Open AI, Slack, and Wing and suggests finding a solution in the Wing project.

---

Title: **How to build and deploy a ChatGPT Slack Bot with Wing**

This guide will walk you through building and deploying a fully working AI-powered Slack Bot with Wing and deploying it to your AWS account.

Our bot will be triggered by "@mentions" on a Slack channel and use Dall-E (OpenAI's image generation model) to produce a response. It can be used for a million different things. We are going to deploy this application on AWS in 3 minutes!

[Let us know](https://t.winglang.io/slack) what you are building with it.

If you like, you can also check out these resources:

- Watch this [demo video](https://winglang.io/videos/slack-bot)
- Sign up for an [online workshop](https://winglang.io/workshops/slack-bot)

Before we get started, a few words about Wing. Wing is a new open-source framework for building serverless applications. Wing's mission is to offer the best serverless developer experience on the planet. One of the biggest pains people have when using serverless is that they constantly have to wait for deployments, and what I love most about Wing is the Wing Simulator which allows you to develop your entire serverless application without having to deploy anything on the cloud. Let's get started and you'll see what I mean.

The Wing framework currently supports two programming languages: TypeScript and [Winglang](https://wing.cloud/winglang). This post is available in both, so pick the one you love! <links to both versions>

So without further ado, bring in the BOTS!

## Creating a new application

Let's start by installing the Wing CLI (you'll need Node.js >= 20.x installed):

```bash
npm i -g wing
```

You can check the CLI version like this:

```bash
wing --version
0.62.1
```

> As you can see, Wing is still in pre-release, so expect some hiccups and don't be shy reporting issues or get help from the awesome people hanging out on the [Wing Slack](https://t.winglang.io/slack).

Ok, now that we have the Wing CLI installed, let's create a new project using the `slack-bot` quick-start:

```bash
$ mkdir my-slack-bot
$ cd my-slack-bot
$ wing new slack-bot
```

## Exploring your new project

Some files were created from this quick-start project. You'll see 3 files `README.md`, `main.w`, and `package.json`.

Let's take a look at the `main.w` file:

```js
bring slack;
bring cloud;

const bot = new slack.App() as "slack";

bot.onEvent("app_mention", inflight (ctx, event) => {
  let mention = slack.AppMentionEvent.fromJson(event);

  let message = new slack.Message();
  message.addSection("You mentioned me, with: {mention.text}");
  ctx.thread.post(message);
});
```

The behavior should be pretty self explanatory: when our bot is @mentioned in a Slack channel, we send a response message back to slack thread.

Cool, ha?

## Configure your Slack application

Head over to the [Slack Apps Dashboard](https://api.slack.com/apps) and create a new Slack app for our bot. 

Then within the `OAuth & Permissions` section, add the following scopes to your bot token:
- `app_mentions:read`
- `chat:write`

Once the scopes are defined, install the app to your workspace and copy the `Bot User OAuth Token` and `Signing Secret` to be used in the next step.

### Subscribing to Slack events

In order for Slack to be able to send messages to your app, we will need to add a new event subscription. Navigate to the `Event Subscriptions` section and enable events.

Under `Subscribe to bot events`, add the following events:
- `app_mention`

## Configuring your application 

In order for our app to be able to work it will need:

1. Configure a Slack app and provide the following Slack credentials:
  - `SLACK_SIGNING_SECRET`
  - `SLACK_BOT_TOKEN`

These credentials will be provided through the use of `cloud.Secret` resources. We will see how to configure them below.

## Configure your secrets

The Slack tokens we obtained need to be stored for the application to use them. In order to configure them, we can simple run `wing secrets main.w --create` with the desired platform, in the case of local testing the simulator is the default platform so no additional flags are needed. Whereas for AWS we can use the `tf-aws` platform, just append the flag `-t tf-aws` to the command.

### Local secret configuration

Running the blow command will result in an interactive prompt where you can input the Slack credentials:

```bash
wing secrets main.w --create

2 secrets found in main.w

Enter the value for SLACK_SIGNING_SECRET: ********
Enter the value for SLACK_BOT_TOKEN: ********

Secrets saved to .env file
```

This results in a `.env` file being created with the secrets stored in it.

### AWS secret configuration

Just like the local configuration, the AWS configuration is done in the same way, but with the `-t tf-aws` flag:

```bash
wing secrets main.w --create -t tf-aws

2 secrets found in main.w

Enter the value for SLACK_SIGNING_SECRET: ********
Enter the value for SLACK_BOT_TOKEN: ********

Secrets saved to AWS Secrets Manager
```

This will store the secrets in AWS Secrets Manager.

## Testing your application locally

When you are ready to test the application locally, you can run the following command:

```bash
wing it
```

This will start the Wing Simulator and run your application locally. 

> Slack offers two different ways to interact with events, one is through the Events API and the other is through Slack Sockets. The Events API requires a redirect URL to be configured in the Slack app, whereas Slack Sockets bypass this requirement through the use of a WebSocket connection. In the simulator your bot will use Slack Sockets so no need to use a redirect URL just yet, but when deploying to AWS you will need to configure one, which is explained in the next section.

Once its running you can go ahead and give it a try by mentioning your bot in a Slack channel. 

> Note: Be sure to try this in a channel where the bot is in, otherwise it won't work. To add the bot to a channel you just need to add it in the channel integrations.

## Deploying your application to AWS

Once you are happy with the bot and want to deploy it to the cloud, we just need to compile to the `tf-aws` platform and deploy it using Terraform:

```bash
wing compile -t tf-aws
terraform -chdir=./target/main.tfaws init
terraform -chdir=./target/main.tfaws apply -auto-approve
```

## Configure your Slack app with the Redirect URL

In the output of the `apply` command you will see a Redirect URL that you will need to add to your Slack app configuration, in the Event subscriptions section.

To do so, head back to the Slack API Dashboard and navigate to the `Event Subscriptions` section. Add the Redirect URL to the `Request URL` field and save the changes.

## Fin

Thats it! You now have a fully functioning Slack bot deployed to AWS. You can now mention your bot in a channel and see the magic happen.