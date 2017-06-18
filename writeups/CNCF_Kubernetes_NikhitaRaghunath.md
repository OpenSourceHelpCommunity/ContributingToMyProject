# How to contribute to Kubernetes

Kubernetes is a huge project and one the [fastest growing projects](http://redmonk.com/fryan/2016/11/08/kubernetes-from-evolution-to-an-established-ecosystem/) of all time. At first, the codebase might feel intimidating and scary but please don't give up because you will end up learning a LOT and be introduced to an amazing community!

Note: Kubernetes is written in Go so if you are not familiar with it, it is recommended you go through the [Go tour](https://tour.golang.org/welcome/1).

## Table of Contents

1. [What is Kubernetes](#what-is-kubernetes)
2. [What does the name mean](#what-does-the-name-mean)
3. [How to learn about Kubernetes](#how-to-learn-about-kubernetes)
4. [Installing Kubernetes locally](#installing-kubernetes-locally)
    1. [Dependencies](#dependencies)
        1. [Go](#go)
        2. [etcd](#etcd)
    2. [Workflow](#workflow)
5. [Diving into the codebase](#diving-into-the-codebase)
    1. [Understanding the API](#understanding-the-api)
    2. [Sign the CLA](#sign-the-cla)
    3. [Finding an issue to work on](#finding-an-issue-to-work-on)
6. [Communication](#communication)
7. [Miscellaneous](#miscellaneous)
8. [Conclusion](#conclusion)

## What is Kubernetes

[Kubernetes](https://github.com/kubernetes/kubernetes) is an open-source system for automating deployment, scaling, and management of containerized applications. It groups containers that make up an application into logical units for easy management and discovery. Kubernetes builds upon a decade and a half of experience at Google running production workloads at scale using a system called [Borg](https://research.google.com/pubs/pub43438.html), combined with best-of-breed ideas and practices from the community.

Basically what this means is that real production apps span multiple containers. Those containers must be deployed across multiple server hosts. Kubernetes gives you the orchestration and management capabilities required to deploy containers, at scale, for these workloads. Kubernetes orchestration allows you to build application services that span multiple containers, schedule those containers across a cluster, scale those containers, and manage the health of those containers over time.

Kubernetes also needs to integrate with networking, storage, security, telemetry and other services to provide a comprehensive container infrastructure.

## What does the name mean

When people hear of Kubernetes, the first question they ask is - why is it called Kubernetes and how is it pronounced?!

Kubernetes, pronounced as _“koo-burr-NET-eez”_, is Greek for "helmsman" or "pilot". Get it? Helping you navigate the murky waters of cloud computing and containerized applications? :D

Its development and design are heavily influenced by Google's Borg system and many of the top contributors to the project previously worked on Borg. The original codename for Kubernetes within Google was Project Seven, a reference to a Star Trek character that is a 'friendlier' Borg. The seven spokes on the wheel of the Kubernetes logo is a nod to that codename.

Since Kubernetes is a long name, it is usually abbreviated to _k8s_ (K – eight characters – S) or just _kube_.

There is also an inside joke about the pronounciation of `kubectl`, the command line interface for running commands against Kubernetes clusters. Noone knows the correct pronounciation - take your pick from the following!

1. kube-control
2. kube-C-T-L
3. kube-cuddle
4. the recent [kube-ek-til](https://twitter.com/thockin/status/873403604035555328)


## How to learn about Kubernetes

There are multiple resources available from where you can learn about Kubernetes. However, my personal recommendation would be to go through the following resources first. Once you feel comfortable with these, you can explore more further.

1. Go through the [interactive tutorials](https://kubernetes.io/docs/tutorials/kubernetes-basics/) first. Execute all commands by yourself and try to understand what is happening. If you don't understand on the first go, that is totally okay. The important part is that you get familiar with `kubectl` so that when you learn more about Kubernetes, it doesn't look completely new to you.

2. Go through some blog posts [[1](https://blog.giantswarm.io/understanding-basic-kubernetes-concepts-i-introduction-to-pods-labels-replicas/)][[2](https://www.digitalocean.com/community/tutorials/an-introduction-to-kubernetes)] to understand the key concepts of k8s like pods, nodes, services, etc.

3. I'd strongly recommend going through the Udacity course [Scalable Microservices with Kubernetes](https://www.udacity.com/course/scalable-microservices-with-kubernetes--ud615) by Kelsey Hightower and Carter Morgan. They are excellent teachers and explain about Docker and Kubernetes in a very easy way.

## Installing Kubernetes locally

It is recommended that you install Kubernetes on Linux or Mac.

### Dependencies

#### Go
Kubernetes is written in Go. If you don't have a Go development environment, please [set one up](https://golang.org/doc/install). Make sure you install Go version 1.8.1 for Kubernetes to work properly. This YouTube [tutorial](https://www.youtube.com/watch?v=5qI8z_lB5Lw) is pretty handy to understand about `GOPATH`.

Ensure your `GOPATH` and `PATH` have been configured in accordance with the Go environment instructions.

Dependency management for Go is done using `godep`. Once you have configured your Go environment, run the following:

```bash
$ go get -u github.com/tools/godep
```

Make sure it is installed correctly:

```bash
$ godep version
```

#### etcd

Kubernetes maintains state in [etcd](https://coreos.com/etcd/docs/latest), a distributed key store.

You can install it locally _after_ installing installing Kubernetes too! There is a script in the k8s repo which does this for you. So once have completed installing Kubernetes as shown below, do the following:

```bash
$ hack/install-etcd.sh
$ echo export PATH="\$PATH:$(pwd)/third_party/etcd" >> ~/.profile
```

### Workflow

Fork the [repo](https://github.com/kubernetes/kubernetes) first and then follow these commands. Theey show the workflow you'll need to follow to install kubernetes locally.

```bash
$ working_dir=$GOPATH/src/k8s.io
$ user={your github profile name}

# clone the repo
$ mkdir -p $working_dir
$ cd $working_dir
$ git clone https://github.com/$user/kubernetes.git

# add upstream
$ cd $working_dir/kubernetes
$ git remote add upstream https://github.com/kubernetes/kubernetes.git

# Never push to upstream master
git remote set-url --push upstream no_push
```

While working on some code, to keep your branch in sync, you need to rebase to HEAD.

```bash
# While on your feature branch
$ git fetch upstream
$ git rebase upstream/master
```

To start a cluster locally:

```bash
$ hack/local-cluster-up.sh -O
```

To build and test:

```bash
# to build
$ make

# to build and start a cluster
$ hack/local-cluster-up.sh
```

Writing tests is important! There are different types of tests: unit tests, integration tests and e2e tests. You can find instructions on how to run them [here](https://github.com/kubernetes/community/blob/master/contributors/devel/testing.md). 

To install and set up the `kubectl` binary, please read the instructions [here](https://kubernetes.io/docs/tasks/tools/install-kubectl/). For a much more detailed overview, please refer this [repository](https://github.com/kubernetes/community/tree/master/contributors/devel).

## Diving into the codebase

### Understanding the API
Before you start exploring issues and find things to work on, you need to understand how the kubernetes API is structured. This [document](https://github.com/kubernetes/community/blob/master/contributors/devel/api-conventions.md) explains the design of the API. Also go through the [architecture](https://github.com/kubernetes/community/blob/master/contributors/design-proposals/architecture.md) to understand how different components are connected together. It is crucial that you understand this before moving further. If you have any queries, feel free to ask on Slack.

Documentation is great but you will also learn a lot by going through issue comments. This is where most of the discussion happens and you can pick up important points about how a piece of code works.

### Sign the CLA
Kubernetes is a Cloud Native Computing Foundation (CNCF) product. To contribute code, you need to sign a Contributors License Agreement (CLA). Instructions to sign the CLA electronically can be found [here](https://github.com/kubernetes/kubernetes/wiki/CLA-FAQ).

### Finding an issue to work on

1. Kubernetes is a **huge** project and has more than 4,300 issues open at any given point of time. There are issue labels like [`for-new-contributors`](https://github.com/kubernetes/kubernetes/issues?q=is%3Aopen+is%3Aissue+label%3Afor-new-contributors) which can help you to find potential issues you can work on. 

2. Personally, I would recommend you to go through the issues mentioned in the kubectl roadmap - especially the issues under _[improve error messages](https://github.com/kubernetes/community/wiki/Roadmap:-kubectl#improve-help--error-messages--output)_. If you don't understand how to solve an issue, that's okay, move on to the next one. But make sure that you at least _try_ to search for the code associated with the issue. At this point, it is NOT important for you to solve issues but to understand how the code is structured and understand the code. Once you see the code and feel comfortable with it, you can easily move ahead with solving issues.

3. If you find an issue you would like to work on, comment on the issue that you would like to work on it. Please note that only org members can be "assigned" to issues. So even though you won't be assigned to an issue, consider yourself assigned and start working on it. If you have some queries and don't get a response within 1-2 days (probable since most devs are super busy), ping the OP of the issue on slack.

4. Kubernetes has several teams working on a specific component. These teams are called Special Interest Groups or _SIGs_. Example: SIG Auth, SIG AWS, SIG API Machinery. This [document](https://github.com/kubernetes/community/blob/master/sig-list.md) lists all the SIGs along with links to their mailing lists, slack channel and meetings. If you prefer to work on a particular component, I would suggest you to join the SIGs relevant to your interest and go through their meeting notes to understand what the team is working on now. If you would like to know the project/team better, you could also join the meeting. It is not necessary to contribute during the meetings, you can lurk around too. Tell them that you would love to contribute. The community is very friendly so you'll mostly find someone who would love to help and mentor you! :)

## Communication

There are multiple methods of communication - the most receptive one is slack.

* Slack:
    - Please visit this [site](http://slack.k8s.io/) to get an invite.
    - There are multiple channels catering to different needs. For general development questions, ask in #kubernetes-dev.
    - For SIG specific questions, ask in the SIG channel. Example: #sig-api-machinery.

* Mailing lists:
    - The general mailing list where all the important announcements are made is [kubernetes-dev](https://groups.google.com/forum/#!forum/kubernetes-dev).
    - Each SIG has its main mailing list where SIG related announcements are made.
    - Each SIG also has other mailing lists like "kubernetes-sig-api-machinery-api-reviews". So when someone mentions `@kubernetes/sig-api-machinery-api-reviews` in a PR, the PR comments are sent to the mailing list. This is done to notify the concerned members about a PR or code change.

* Twitter: official Kubernetes [handle](https://twitter.com/kubernetesio?lang=en) for cool announcements.

* [Kubeweekly](http://kube.news/): It aggregates all interesting weekly news about Kubernetes in the form of a newsletter.

## Miscellaneous

There are few other points about kubernetes you should know!

1. Each file in the codebase has a copyright header. There are many cases when the dev who modifies the code ends up changing the year in the copyright header too. It is a not a grave error but don't do that - the year denotes the year when the file was _created_, not _modified_.

2. While opening a PR, please go through the issues and search if your PR closes an issue. If it does, mention it in your PR description as `fixes #XXXX`. Note that each PR needs to have an issue associated with it to be merged unless, of course, it is trivial.

3. There are many scripts available under the `hack` directory that make your life easier (like `local-cluster-up.sh` you just used). Most of them are huge makefiles - you don't need to worry about the code but only learn to use them. For example, if you update any imports in any file, you need to update the `BUILD` files by running the following command. Don't worry too much about these commands, you'll learn as you contribute but you should be aware of them.

    ```
    $ ./hack/update-bazel.sh
    ```

4. When you submit a PR, make sure you follow the PR template. You will notice a RELEASE NOTE section in template. This is used to write a release note if the PR you submitted introduces a **significant** change. 99% of the time, it is not needed. So you need to write it as:


    ```release-note
    NONE
    ```

5. Since you are not a member of the k8s org, you will need an org member to comment `@k8s-bot ok to test` so that the CI starts testing your changes. It could so happen that your code encounters a **flaky test** - this means that it is not the fault of your code that the test failed. In this case, you need to re-run the test using a command like `@k8s-bot pull-kubernetes-e2e-gce-etcd3 test this`. Don't be intimidated about this, the bot will tell you which command to run! In any case, there is a [list](https://github.com/kubernetes/test-infra/blob/master/commands.md) of commands you can use with the bot. There is a whole `test-infra` [repo](https://github.com/kubernetes/test-infra) which takes care of the testing! ;)

6. Once your code doesn't flake anymore, it will be tested again by the submit queue before merging. You can view the submit queue [here](https://submit-queue.k8s.io/#/prs). Finally, your code will be merged! \o/

7. The Kubernetes repo undergoes a code freeze just before a release. There is a proper release schedule followed which dictates when the code freeze will start. [This](https://github.com/kubernetes/features/blob/master/release-1.7/release-1.7.md) is the schedule for the 1.7 release. Note that most of the devs would be **really** busy a week or two before the code freeze so don't be disheartened if you don't receive a quick response then.

## Conclusion

The Kubernetes codebase is huge and it is one of the fastest moving projects in the world. It is _easy_ to get intimidated by it but please remember that the struggle that you face while starting out will be **worth it**. You will be exposed to good coding practices, interesting discussions, healthy code review and most importantly, you will be a part of a wonderful community!

If you have specific questions, want to share your experience/problems you are facing during contributing or just want to say hi - feel free to DM me (@nikhita) on the k8s slack. :)