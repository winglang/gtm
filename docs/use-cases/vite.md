# Vite User Story

Cristian, a full-stack developer at an e-commerce company, received a task to develop a chat widget to enable customer interaction with sales representatives. Envisioning a React app enhanced with WebSocket support for an exceptional user experience, Cristian faced a challenge: he has no prior experience with WebSockets.

Anticipating a repetitive cycle of testing and tweaking to perfect the application, Cristian remembered a previous project where he battled with unfamiliar technology. a daunting period marked by endless cycles of deployment, testing, corrections, and redeployment.

Feeling discouraged, Cristian suddenly recalls a conversation with a colleague about a fascinating workshop about creating React Vite project with WebSocket support. What stood out to him was that the whole development and testing process was all done locally without the need to deploy to the cloud!!! That could change everything for him. With new hope in his heart, Cristian took it as an opportunity not only to master a new skill but also to streamline the development process.

Cristian began exploring the tutorial to grasp the fundamental wiring of his application. This tutorial wasn't just a basic guide, it was an in-depth workshop based on the newly introduced Wing `react-vite` template. This template is specifically designed to lay the groundwork for a FE and BE integration, complete with WebSocket support.

```bash
npm i -g wing
```

You can check the CLI version like this:

```bash
wing --version
0.61.4
```

And then created a new project using the new `react-vite` template:

```bash
$ mkdir my-awsome-site
$ cd my-awsome-site
$ wing new react-vite
```

Let's check out what we now have in our project directory:

```bash
/frontend
-> /.winglibs
-> /node_modules
 -> vite react template files...
/backend
 -> main.w
/ node_modules
package.json
package-lock.json
```

With Vite powering the frontend development server and Wing providing the backend infrastructure, Cristian was able to create a seamless integration between 
the two, resulting in a highly efficient and responsive development environment.

The integration also included real-time updates via WebSockets, providing the users the perfect chat experience.

> Built-in Wing platforms such as tf-aws support certain common configuration options (such as private APIs). If you need additional customization, you can always create your own custom platforms and have complete control over how your app is deployed to the cloud.
> 

Before we deploy our app to AWS, let's first check it out in the Wing Simulator:

```bash
wing run
```

> If this is the first time you are running the Wing Simulator on your machine, you'll need to sign up with your GitHub or Google credentials so that you can later deploy your app using Wing Previews and use cloud-based development tools like webhook forwarding and app sharing.
> 

Next, let's deploy this to the cloud:
TBD

A couple of weeks later, Cristian gets an email from Revital Barletz, Head of Community at the Wing team:

Hi Cristian,

What's up? I am Revital from the Wing team ♥️. You recently signed up for Wing and I wanted to reach out and welcome you to our community (we call ourselves Wingnuts... a bit corny I know).

Wing is all about creating an irresistible developer experience for building stuff on the cloud, and I think you might be able to find some kindred spirits in our community.

So, hi! Let me know if there's anything I can help with. Feel free to reply to this email or reach me out directly in our [slack](https://t.wing.cloud/slack). I'd love to learn about your first experience with Wing and see where we can improve.

Cheers,
Revital

---

A couple of weeks later, after Cristian has already joined the Wing Slack, he gets a slack message from Eyal Keren, the chief product officer of Wing.

- From: ekeren
- Message: Hey Cristian, what's up?
- Message: I am Eyal from the Wing team.
- Message: I was wondering if you might be able to spare 15 minutes for a quick chat? We are exploring some product ideas and we are looking to get some feedback from early folks in our community.

