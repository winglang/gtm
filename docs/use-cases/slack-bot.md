# Slack Bot User Story

Amiel, who works as a designer at a hip startup, really likes the pictures made by OpenAI. He wants to show his team how cool they are. He looks online and finds a beautiful blog post written by Nathan Tarbert, a community engineer from the Wing team, explaining how to make a Slack bot that can draw pictures using OpenAI and Wing in just five minutes!

Alternatively, Amiel is directed to the [dev.to](http://dev.to/) article, which leads to the blog.

Alternatively, Amiel searches Reddit under TBD and discovers this blog post.

Alternatively, Amiel's colleague, Elad Cohen, mentions seeing a funny TikTok from the Wing team about the neat integration of Open AI, Slack, and Wing and suggests finding a solution in the Wing project.

---

Title: **How to Build a Slack Bot, with Open AI, Using Wing in less than 5 minutes**

I thought it might be useful for others in our community, so I'd like to share some instructions and demonstrate how to use a new [Wing Quickstart](https://wing.cloud/quickstarts) I created to make it easy for folks to build a Slack bot app integrated with Open AI.

If you like, you can also check out these resources:

- Watch this [demo video](https://wing.cloud/videos/slack-bot)
- Sign up for an [online workshop](https://wing.cloud/workshops/slack-bot)

Before we get started, a few words about Wing. Wing is a new open-source framework for building serverless applications. Wing's mission is to offer the best serverless developer experience on the planet. One of the biggest pains people have when using serverless is that they constantly have to wait for deployments, and what I love most about Wing is the Wing Simulator which allows you to develop your entire serverless application without having to deploy anything on the cloud. Let's get started and you'll see what I mean.

Wing currently supports two programming languages: TypeScript and [Winglang](https://wing.cloud/winglang). For the purposes of this post, I'll use Winglang, but if you pass `-l=typescript` when you create your project, you'll get a TypeScript project.

Let's start by installing the Wing CLI (you'll need Node.js >= 10.x installed):

```bash 
npm i -g wingcli
```

You can check the CLI version like this:

```bash
wing --version
0.33.40
```

> As you can see, Wing is still in pre-release, so expect some hiccups and don't be shy reporting issues or get help from the awesome people hanging out on the Wing slack.
> 

Ok, now that we have the Wing CLI installed, let's create a new project using the s`slack-bot-with-open-ai` quickstart:

```bash
$ mkdir my-api
$ cd my-api
$ wing new slack-bot-with-open-ai
```

> As mentioned above, you can use the --language=typescript option to create a TypeScript version of this project.
> 

---

> Meanwhile, at the Wing office in Tel-Aviv, a Slack bing ♬ note is heard from all laptops which interrupts a heated office conversation about where to conduct the next Wing offsite. Ainvoner looks at his phone and sees that a Slack message was posted to the #mona-analytics channel. The message reads 🚀 A new "slack-bot-with-open-ai” project was just created! The total number of `slack-bot-with-open-ai` projects created so far is 2,340. He shares this news with the team and everyone start jumping up and down with pure joy.
> 

---

Let's check out what we now have in our project directory:

```bash
main.w
wing.toml
package.json
```

If we look at the `main.w` file, you will find:

- A Slack app and an Open App are created

```js
bring slack;
bring openai;

const ai = new openai.OpenAi ({ … });
const app = new slack.SlackApp({ … });
```

- The implementation of the `/generateImage [text]` command. Whenever a user types this command in one of their slack channel, an image related to the provided text will be generated upon request.
- The Slack bot listens for the **`/**generateImage` command using the **`app.command`** method.
- When the command is invoked, it extracts the text provided with the command.
- Note: This is a simplified example. You'll need to set up your Slack app, handle authentication, and implement the actual image generation logic and all of that using Winglang 🙂.

```js
app.command('/generateImage', inflight (command) => {
  // Acknowledge the command request   
	command.ack();
	// Extract the text from the command
	let text = command.body.text;
	// Generate the image based on the provided text
	let generatedImage = ai.generateImage(text);
	// Post the generated image to the Slack channel
	app.client.chat.postMessage({
	  channel: command.body.channel_id,
	  blocks: [
	  {
		  type: 'image',
		  image_url: generatedImage.url,
		  alt_text: 'Generated Image'
	  }
	 ]
	});
});
```

        
Alternatively, the user can also use the command `@generateImage  [text]` and that will end with the same result.

```js
app.message('mention', inflight (mention) => {
	// Check if the message contains the @generateImage mention
	if mention.message.text.includes('@generateImage') {
	  // Extract the text after the @generateImage mention
	  let text = mention.message.text.replace('@generateImage', '').trim();
	
	  // Post the generated image to the Slack channel
	  await say({
	    blocks: [
	    {
	      type: 'image',
	      image_url: generatedImage.url,
	      alt_text: 'Generated Image
	    }
	    ]
	  });
	}
});

```

Your platform configuration happens inside `wing.toml`:

Slack configuration/secrets

Open AI configuration/secrets

This `wing.toml` file sets configuration options for the wing app. Your configuration will be available at runtime on AWS and when running locally. 

Let's first check it out in the Wing Simulator:

`wing run`

> If this is the first time you are running the Wing Simulator on your machine, you'll need to sign up with your GitHub credentials so that you can later on setup your app for Wing Previews and use cloud-based development tools like webhook forwarding and app sharing.
> 

Next, let's deploy this to the cloud:

TBD - Wing.Cloud or AWS?

---

Amiel couldn't hold his excitement! This is exactly what he was looking for. He went ahead and created his project and wrote this code:

```js
bring cloud;
bring aws;
```

TBD

---

A couple of weeks later, Amiel gets an email from Revital Barletz, Head of Community at the Wing team:

To: [amiel@designer.bot](mailto:sandyh@billie.bot)

From: [revitalb@wing.cloud](mailto:revitalb@wing.cloud)

Title: Welcome Wingnut

Hi Amiel,

What's up? I am Revital from the Wing team ♥️. You recently signed up for Wing and I wanted to reach out and welcome you to our community (we call ourselves Wingnuts... a bit corny I know).

Wing is all about creating an irresistible developer experience for building stuff on the cloud, and I think you might be able to find some kindred spirits in our community.

So, hi! Let me know if there's anything I can help with. Feel free to reply to this email or reach me out directly in our [slack](https://t.wing.cloud/slack). I'd love to learn about your first experience with Wing and see where we can improve.

Cheers,

Revital

---

A couple of weeks later, after Amiel has already joined the Wing Slack, he gets a slack message from Eyal Keren, the chief product officer of Wing.

From: ekeren

Message: Hey Amiel, what's up?

Message: I am Eyal from the Wing team.

Message: I was wondering if you might be able to spare 15 minutes for a quick chat? We are exploring some product ideas and we are looking to get some feedback from early folks in our community.
