---
title:  "Caching Docker images in Github Actions"
date:   2023-01-14 00:00:00 +1000
tags: Docker Github
comments: true
classes: wide
header: 
  teaser: https://rolzy-blog-assets.s3.ap-southeast-2.amazonaws.com/teaser-images/gha-docker-cache.png
---

![Docker and GHA](https://rolzy-blog-assets.s3.ap-southeast-2.amazonaws.com/splash-images/gha-docker-cache-1280.png)

Github Actions is my go-to platform for building a CI/CD pipeline. 

IMO, the benefits of using Github Actions are:

1. My codebase is literally *right there*. All I need is a simple [Checkout Action](https://github.com/actions/checkout) and voila, all my code is there for the workflow to access.
2. Since you are running CI/CD on the same platform as where your code is, triggering your workflow feels very natural. The CI/CD pipeline is tightly integrated with your Git workflow. No need to setup cross-service access.
3. I'm used to using Github and Github Actions.

The world is your oyster when using Github Actions. You can perform a plethora of different tasks, like `make`-ing your executable, running unit tests or even deploying your app to the cloud. In particular, I find myself building and pushing Docker images A LOT on Github Actions. 

A big challenge when using Docker, especially in the field of machine learning, is that Docker images gets real big real quick. A GPU supported Docker container with Nvidia CUDA can easily get close to 10GB. It takes a looooooooooooooong time to build images of this size. This is not so much of a problem when building in a local computer, because Docker natively [cache steps that you've already run before](https://docs.docker.com/build/cache/). 

Now wont it be nice if we could cache Docker steps on Github Actions, too? I have been looking for a way to do this for a while now, and I finally found a way with [build-push-action](https://github.com/docker/build-push-action).

## The "build-push-action" action
From the repo: 
> GitHub Action to build and push Docker images with Buildx with full support of the features provided by Moby BuildKit builder toolkit. This includes multi-platform build, secrets, remote cache, etc. and different builder deployment/namespacing options.

In simple words, the `build-push-action` lets you use a powered-up version of Docker inside Github Actions. This is powerful because Github Actions runners have a fundamental limitation in networking and file-access. They work remotely and are ephemeral. Its not as easy to use Docker on Github Actions as it would on your local computer. 

Take caching for example. Caching your intermediate Docker build results requires you to have persistent storage. However, CI/CD build environments like Github Actions have no persistence between runs. This is where the `build-push-action` plugin comes into play.
e
The plugin takes care of your caching needs by storing the intermediate build results in a separate permanent storage. There are a few storage options available. You can embed them into your image, store it as a different image in the registry, or even upload it to a Cloud storage solution. For the full list of available storage options, check out [here](https://docs.docker.com/build/cache/backends/#backends). 

## How to use
I have created an example repo here: [https://github.com/rolzy/gha-docker-cache-example](https://github.com/rolzy/gha-docker-cache-example).
The code snippets in this section are from the code repository, so you can refer to that as well.

Using the `build-push-action` plugin is very simple. First, we configure the Buildx instance using the [setup-buildx-action](https://github.com/docker/setup-buildx-action):
```
- name: Set up Docker Buildx
  uses: docker/setup-buildx-action@v3
```

Then, we can go ahead and build the Docker image. Note that we set the `context` argument to be the name of the directory which contains the `Dockerfile`. 
```
- name: Build the image
  uses: docker/build-push-action@v5
  with:
    context: docker/
    cache-from: type=gha
    cache-to: type=gha,mode=max
```
The `cache-from` and `cache-to` arguments enable caching and specify where the Docker cache will be stored. In our example we are using the Github Actions cache exporter (`gha`) backend. Remember, there are other cache backends also available. You can check them out [here](https://docs.docker.com/build/ci/github-actions/cache/). `gha` is the recommended storage backend for Github Actions. Just note that there is a 10GB size limit for the cache stored within a repo.

And that is it! In my repo, you will see one pull request which has two workflow runs. The first run took 3 and a half minutes to build a docker image. The second one only took 30 seconds because it used the cache from the previous run. 
