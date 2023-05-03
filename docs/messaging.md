# Winglang Messaging Guide

> Just some guidance on how to work with this doc: It's basically a playbook that summarizes the
> essence of how we want to present Wing to the world. It includes various messages in different
> formats aimed at engaging "intellectually curious" backend developers, which we identified as our
> initial target audience. The idea is to have multiple options from which we can mix and match the
> right message in the right format across different channels (e.g., website, social media and press
> releases). But first, we need to make sure that all the messages are accurately conveying the most
> important themes. So please review and feel free to comment and suggest any edits. 

## Background

The cloud has evolved to become a ubiquitous platform for running almost every type of application. It allows developers to deliver value by leveraging services and infrastructure, which take care of many of the challenges of building and running software. However, the cloud is a highly dynamic and complex environment, and writing applications often requires understanding low-level details of disparate cloud services. 

Cloud complexity is largely driven by the way applications are built and managed. Currently
available programming languages are designed to tell a single machine what to do. This stands in
contrast to the nature of the cloud, which is basically a single big distributed computer. 

To bridge this gap, backend developers must use custom configuration and code to stitch together
machines and services into a cohesive application. They must use different programming languages,
platforms and tools, and spend significant time and effort on non-functional requirements. The
result is frequent context switching, and increased cognitive load that harms the developer
experience, which in turn impacts productivity and code quality.

The concept of DevOps was formed to address this challenge, aiming to free developers to focus on
writing functional code. However, DevOps teams have become a major bottleneck for innovation and
fast delivery. They are increasingly required to facilitate application deployment for developers
instead of focusing on critical matters such as proactively managing performance, availability and
security. As digital transformation continues to accelerate, these problems exacerbate, resulting in
inefficiencies and friction points:

* Slow "inner-loop" iteration cycles
* Tool fatigue
* Release of "half-baked code"
* Inability to run and test code locally 
* Internal platforms are growing "tax" 
* Cloud provider lock-in 
* Manual and error-prone security/observability processes
* DevOps resources become scarce and expensive

To realize the full benefits of cloud-driven innovation, complexity should be handled at the
compiler level. This calls for a new breed of programming languages that treat the cloud in a
holistic and cohesive manner, abstracting the complexity of the underlying parts, and empowering
developers with self-service capabilities to minimize the reliance on DevOps so they can focus on
writing functional code.

## Company messaging

Monada aims to democratize the cloud with software solutions that enable developers to deliver
better code faster and more securely, with the autonomy to build, run, debug, and test complete
cloud applications within their local environments. Monada was founded by ex-Microsoft, ex-Amazon
with a track record of building successful open-source cloud development tools such as the AWS CDK.

## Primary product messaging

Winglang is a new open-source programming language designed for the cloud. It enables backend
developers to build distributed systems that leverage cloud services as first-class citizens.

Winglang is a statically-typed language that compiles to JavaScript and Terraform. By providing a
built-in local simulator, and an observability & debugging console, Winglang reduces cognitive load
and context switching, enabling developers to stay in their creative flow. 

Wing supports backend developers with self-service capabilities to minimize dependency on DevOps,
improve code quality and security, accelerate delivery, and easily move code between clouds and
platforms.

Wing is open sourced by Monada, founded by ex-Microsoft, ex-Amazon with a track record of building
successful open-source cloud development tools such as the AWS CDK. 

## Tagline

A cloud-oriented programming language

Winglang combines cloud resources and application code into a unified programming model, enabling
developers to build distributed systems that leverage cloud services as first-class citizens 

/

Winglang enables developers to build distributed systems that leverage cloud services as first-class
citizens, combining cloud resources and application code into a unified programming model.

[a cloud without glue, no boilerplate code]

[Wing treats the entire cloud as a single, distributed computer, enabling developers to write higher level code while delegating…]

## Key takeaways (how do we want the end user to feel)

* I can finally focus on what interests me the most - writing functional code, and finding creative
  solutions to complex problems instead of spending time on non-functional requirements
* I can be more productive and independent at my job, and create better code, faster, while keep
  working with my existing tools and platforms
* I will be able to collaborate with fellow backend developers on creating innovative new features
  that will improve my day-to-day workflows

## 25 words

Wing combines infrastructure and runtime code in one language, enabling backend developers to stay
in their creative flow, and to deliver better software, faster and more securely. 

## 50 words

Wing is a cloud-oriented programming language that combines infrastructure and runtime code, with
built-in local simulator and observability & debugging console. Wing enables backend developers to
stay in their creative flow, minimize dependency on DevOps, improve code quality and security,
accelerate delivery, and easily move code between clouds and platforms. 

## 100 words

Wing redefines the cloud development experience with a single language that combines infrastructure
and runtime code. Designed with the goal of enabling backend developers to stay in their creative
flow, Wing features a local simulator and an observability & debugging console that allow for
instant feedback and shortened iteration cycles. Using Wing, developers can create complete cloud
applications while moving most of the complexity from DevOps to the Wing compiler, and minimizing
friction. Instead of manually having to wire up everything, the Wing compiler looks at the code and
automatically produces all the configuration and glue under the hood, freeing developers to focus on
writing functional code.

## Differentiating product messages/USPs

### Stick to your coding style (Simple adoption) 

> #dev experience #freedom of choice

* Winglang is easy to learn, inspired by modern object-oriented programming languages
* Familiar and intuitive syntax, which allows developers to easily use Winglang for a wide range of
use cases
* Integrates into existing codebases - write runtime code in other languages and reference it with
Winglang
* Equipped with a variety of compiler plugins and libraries that enable developers to easily extent
and customize Wingland to work with their existing environment 
* [business benefit] Winglang enables developers to focus on the value they are creating for their
users, rather than the mechanics of the platform

### Bring back your creative flow/Bridging the gap between imagination and creation (Creativity)
> #dev experience 

* No boilerplate code, no glue logic. Winglang abstracts away the underlying complexity of
the cloud, enabling developers to unleash their creativity and focus on writing great code 
* Winglang eliminates mundane, repetitive work, taking care of scaling, load balancing, security
policies, and other infrastructure-related concerns
* Winglang features baked-in best practices that minimize the need for cumbersome, error-prone
manual cloud infrastructure configuration processes, enabling developers to focus on improving code
quality, reliability and security

### The whole cloud at your command/The cloud is the computer (Cohesive programming)
> #dev experience #productivity 

* Winglang treats the entire cloud as a single, distributed computer, enabling developers to write
higher level code while automatically creating all the required infrastructure configurations and
cloud mechanics based on intent
* Use any cloud service and compile to multiple clouds and provisioning engines with full control
over the details 
* Winglang Inflights are distributed computing primitives that represent cloud resources, and can be
executed on compute platforms such as containers, CI/CD pipelines or FaaS 
* Automatic generation of IAM policies and other cloud mechanics 
* [business benefit] Top-class cloud development experience that minimizes cognitive load, friction
and boilerplate

### Batteries included 
> #dev experience #productivity 

* Winglang is shipped with a library and ecosystem of cloud-independent resources, and a simulator
to run, debug and test complete cloud applications within local environments 
* Import and export CDK constructs to and from 
* Winglang Integrates into existing codebases - write runtime code in other languages and reference
it with 
* Winglang Fine tune infrastructure with escape hatches into underlying layers 
* Built-in support for common cloud services, such as AWS Lambda and SNS 
* Natively use any cloud resource in the Terraform ecosystem Interoperable with the JavaScript
ecosystem 
* Native JSON and schema validation support
* [business benefit] Write and deliver better code faster while reducing the cost of cloud
development environments

### Stay in the flow with minimal context switching and instant feedback (Instant local simulation)
> #dev experience #productivity 

* Take full advantage of deploying to the cloud while retaining the speed and simplicity of building
and testing an all-encompassing monolith 
* The Winglang simulator is a set of APIs that can be used to test Winglang applications without
having to deploy the application to a cloud provider
* Visualize, interact, and debug locally with the Winglang Console
* Unit test entire cloud architectures without mocking the cloud around them
* [business benefit] Iterate much faster with instant feedback on code changes 

### Win back independence
> #dev experience #freedom of choice

* Wing provides developers with self-service capabilities and first-class support for cloud
infrastructure resources to minimize dependency on DevOps 
* Apply policy and customization through compiler plugins
* Reduce friction by separating Dev and Ops concerns
* Fine tune infrastructure with escape hatches into underlying layers
* Winglang frees developers from having to deal with non-functional concerns so they can shift their
attention back to actually creating applications
* [business benefit] Improve code quality and security, accelerate delivery, and easily move code
between clouds and platforms

### Breaking free from cloud lock-in (Code portability)
> #freedom of choice #productivity

* Wing lets developers work at a higher level of abstraction to make applications
cloud-portable and avoid vendor lock-in 
* Write code that is portable across cloud providers, as well as can run in a local simulator for
testing and development
* Write code that defines complete architectures without having to know in
advance how these resources will be implemented

### Open-source driven innovation 
> #freedom of choice #dev experience 

* Join our open-source community to share knowledge, contribute and collaborate with fellow backend
engineers in creating the first cloud-oriented programming language
* We aim to inspire trust and foster collaboration by making the Winglang open-source community a
highly transparent and welcoming environment for developers

### Embracing cloud diversity 
> #freedom of choice #dev experience
* Use any service, compile to multiple clouds and provisioning engines with full control over the
details
* Use our plugins and libraries to customize the compilation output of your Winglang applications,
such as infrastructure definitions
* Native JSON and schema validation support

### Write better and safer code 
> #productivity #dev experience 

* Winglang is immutable by default, encouraging developers to write more functional and robust code
