# Vite User Story

Cristian, a frontend engineer at a thriving e-commerce platform, found himself facing a critical challenge in his development process. 
As his team worked on enhancing the platform's product page with dynamic features, Cristian noticed that the build times using their existing tool were 
slowing down significantly. 
With each code change requiring a lengthy rebuild process, it became difficult for him to iterate fast and maintain productivity.

Determined to overcome this obstacle, Cristian was on a mission to find a solution that could streamline their development workflow without compromising
on functionality. After thorough research, he discovered a beautiful tutorial about *React, Vite & WebSockets* with an appealing playful graphics pops up.
A lightning-fast build tool that promised near-instantaneous hot module replacement (HMR) and quick rebuild times during development. 
Intrigued by its potential, Cristian decided to integrate Vite into their project as well as leveraging Wing's backend capabilities to complement 
the frontend work done with React and Vite.

Following a detailed guide provided by Wing, Cristian embarked on integrating the three technologies – React, Vite, and Wing – into their project. 
He started with installing Wing CLI:

```bash
npm i -g wingcli
```

You can check the CLI version like this:

```bash
wing --version
0.33.40
```

And then created a new project using the `react-vite-websockets` quickstart:

```bash
$ mkdir my-awsome-site
$ cd my-api
$ wing new react-vite-websockets
```

Let's check out what we now have in our project directory:

```bash
main.w
wing.toml
package.json
```
TBD - Add description on each file.

With Vite powering the frontend development server and Wing providing the backend infrastructure, Cristian was able to create a seamless integration between 
the two, resulting in a highly efficient and responsive development environment.

The integration also included real-time updates via WebSockets, allowing users to experience immediate changes to the product page without the need for 
page refresh.

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

