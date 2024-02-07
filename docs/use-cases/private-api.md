# Private API Gateway User Story

Sandy is a developer in Billie, a tech company building robots that help clean up restrooms in public places. Sandy is tasked by her CEO, Sandy, to create a service that can be used to get the last update sent to a Billie robot. Billies upload their status to an S3 Bucket every once in a while under a key `updates/billie-[id].json` (where `id` is the unique identifier of the robot).

This service needs to be accessed by some internal systems deployed inside the company's private VPC, so Sandy is looking for a way to implement this using an AWS Lambda function and an API Gateway with private endpoint.

She searches Google for "private API gateway" and browsed some of the AWS documentation. All of them look pretty hairy and scary. "So much configuration is required for such a simple request", she thinks.

Suddenly she notices a **[dev.to](http://dev.to/)** link that reads *"Private API Gateway on AWS for humans"*. She clicks through and a beautiful blog post with an appealing playful graphics pops up. The blog is written by Nathan Tarbert, a community engineer from the Wing team.

Alternatively: Sandy posted a message in an AWS discord channel she hangs out in and someone pointed her how to the [dev.to](http://dev.to/) article.

Alternatively: Sandy searched Reddit under /r/aws and found this blog post.

Alternatively: Sandy's colleague, Sandy, mentioned he saw a funny TikTok from the Wing team about the pains of VPC configuration and suggested to look up a solution in the Wing project.

---

Title: **Private API Gateway on AWS for humans**

Recently, I heard from a few folks on [Wing Slack](https://t.wing.cloud/slack) that Wing really helped them create API services that are running inside a VPC with a private API Gateway. They talked about spending days trying to figure out the relationships between VPC endpoints, security groups, AWS Lambda and API Gateway, and how with Wing this was dead simple.

I thought it might be useful for others in our community, so I'd like to share some instructions and demonstrate how to use a new [Wing Quickstart](https://wing.cloud/quickstarts) I created to make it easy for folks to build API services running inside a VPC.

If you like, you can also check out these resources:

- Watch this [demo video](https://wing.cloud/videos/private-api-aws)
- Sign up for an [online workshop](https://wing.cloud/workshops/private-api-aws)

Before we get started, a few words about Wing. Wing is a new open-source framework for building serverless applications. Wing's mission is to offer the best serverless developer experience on the planet. One of the biggest pains people have when using serverless is that they constantly have to wait for deployments, and what I love most about Wing is the Wing Simulator which allows you to develop your entire serverless application without having to deploy anything on the cloud. Let's get started and you'll see what I mean.

Wing currently supports two programming languages: TypeScript and [Winglang](https://wing.cloud/winglang). For the purposes of this post, I'll use Winglang, but if you pass `-l=typescript` when you create your project, you'll get a TypeScript project.

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

Ok, now that we have the Wing CLI installed, let's create a new project using the `aws-private-api` quickstart:

```bash
$ mkdir my-api
$ cd my-api
$ wing new private-api-aws
```

> As mentioned above, you can use the --language=typescript option to create a TypeScript version of this project.
> 

---

> Meanwhile, at the Wing office in Tel-Aviv, a Slack bing ♬ note is heard from all laptops which interrupts a heated office conversation about where to conduct the next Wing offsite. Ainvoner looks at his phone and sees that a Slack message was posted to the #mona-analytics channel. The message reads 🚀 A new "private-api-aws" project was just created! The total number of "private-api-aws" projects created so far is 2,340. He shares this news with the team and everyone start jumping up and down with pure joy.
> 

---

Let's check out what we now have in our project directory:

```bash
main.w
wing.toml
package.json
```

If we look at the `main.w` file, we'll see:

```js
bring cloud;

let api = new cloud.Api();
api.get("/", inflight () => {
  return {
    status: 200,
    body: "hello, from within the VPC!"
  };
});
```

You'll notice, there's nothing in this Wing code that implies that the API needs to be inside the VPC. This is because in Wing, this type of configuration happens at that *platform level* and not at the *application level*.

Your platform configuration happens inside `wing.toml`:

```toml
[tf-aws]
vpc = "new"
vpc_apigateway = true
vpc_lambda = true
```

This `wing.toml` file sets configuration options for the `tf-aws` platform. The quickstart configures the platform to create a new VPC for this app and put Amazon API Gateways and AWS Lambda functions inside that VPC.

> Built-in Wing platforms such as tf-aws support certain common configuration options (such as private APIs). If you need additional customization, you can always create your own custom platforms and have complete control over how your app is deployed to the cloud.
> 

Before we deploy our app to AWS, let's first check it out in the Wing Simulator:

```bash
wing run
```

> If this is the first time you are running the Wing Simulator on your machine, you'll need to sign up with your GitHub credentials so that you can later on setup your app for Wing Previews and use cloud-based development tools like webhook forwarding and app sharing.
> 

Once the Wing Simulator is running, you'll be able to see your API endpoint, invoke it and see the response.

Next, let's deploy this to the cloud:

```
wing deploy -t tf-aws
```

This command will compile and deploy your Wing application to the AWS account configured in your environment. You'll notice that it will create a new VPC for you with all the desired setup.

But what if I wanted to deploy my app into an existing VPC? It's very common for a VPC to be shared across multiple applications. This can be done by editing your `wing.toml` file like this:

```toml
[tf-aws]
vpc = "existing"
vpc_id = "vpc-288494x"
vpc_private_subnets = [ "subnet-a112", "subnet-a2x1" ]
vpc_apigateway = true
vpc_lambda = true
```

That's it, by setting `vpc` to `existing` and by adding the relevant private subnets Wing won't create a new VPC but rather add the application resources to an existing VPC in your account.

---

Sandy couldn't hold her excitement! This is exactly what she was looking for. She went ahead and created her project and wrote this code:

```js
bring cloud;
bring aws;

let bucket = () => {
  if app.target == "sim" {
		let bucket = new cloud.Bucket();
		// populate the bucket with data when running in the simulator
		bucket.addObject("updates/billie-001", "status=ok");
		return bucket;
  } else {
    return aws.Bucket.fromBucketName("billie-status-bucket");
  }
}();

let api = new cloud.Api();

api.get("/status/:billieid", inflight (req) => {
  let id = req.params.get("billieid");
  try {
		let body = bucket.get("updates/billie-{id}");
		return {
		  status: 200,
		  body: body
		};
  } catch {
		return { 
			status: 404 
		};
  }
});
```

She had to look up the `aws.Bucket.fromBucketName()` static method in order to figure out how to reference an existing AWS S3 bucket from Wing, but the docs were super easy and helpful on that topic.

The cool thing was that when she ran this in the Wing Simulator, it displayed this "external bucket" as if it was part of the application (only with dotted lines in the Wing Console), and she could actually add some data to it for testing.

---

A couple of weeks later, Sandy gets an email from Revital Barletz, Head of Community at the Wing team:

- To: sandyh@billie.bot
- From: revitalb@wing.cloud
- Title: Welcome Wingnut

Hi Sandy,

What's up? I am Revital from the Wing team ♥️. You recently signed up for Wing and I wanted to reach out and welcome you to our community (we call ourselves Wingnuts... a bit corny I know).

Wing is all about creating an irresistible developer experience for building stuff on the cloud, and I think you might be able to find some kindred spirits in our community.

So, hi! Let me know if there's anything I can help with. Feel free to reply to this email or reach me out directly in our [slack](https://t.wing.cloud/slack). I'd love to learn about your first experience with Wing and see where we can improve.

Cheers,
Revital

---

A couple of weeks later, after Sandy has already joined the Wing Slack, she gets a slack message from Eyal Keren, the chief product officer of Wing.

- From: ekeren
- Message: Hey Sandy, what's up?
- Message: I am Eyal from the Wing team.
- Message: I was wondering if you might be able to spare 15 minutes for a quick chat? We are exploring some product ideas and we are looking to get some feedback from early folks in our community.
