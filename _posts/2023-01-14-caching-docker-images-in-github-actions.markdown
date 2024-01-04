---
title:  "Caching Docker images in Github Actions"
date:   2023-01-14 00:00:00 +1000
tags: Docker Github
comments: true
classes: wide
---

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

In simple words, the `build-push-action` lets you use a powered-up version of Docker inside Github Actions. This is a game changer because Github Actions runners work remotely and are ephemeral. They have a fundamental limitation in networking and file access - its not as easy to use Docker on Github Actions as it would on your local computer. The `build-push-action` plugin helps solve this issue.

<!---
- Introduction
    - Github actions
        """
        Github Actions is my go-to platform for building and pushing Docker images as part of a CI/CD pipeline. The benefits of using Github Actions are:
            1. My Dockerfile and any related code are *right there*. All I need is a simple [Checkout Action](https://github.com/actions/checkout) and voila, my code is there for the workflow to access.
            2. Since you are running CI/CD on the same platform as where your code is, triggering your workflow feels very natural. The CI/CD pipeline is tightly integrated with your Git workflow. No need to setup cross-service access.
            3. I'm used to it.
        """
    - Building docker images
        """
        The world is your oyster when using Github Actions. You can do a plethora of different tasks, like `make`ing your executable, running unit tests or even deploying your app to the cloud. In particular, I find myself building and pushing Docker images A LOT on Github Actions. That is because the [build-push-action](https://github.com/docker/build-push-action) plugin makes things super easy. 
        """
    - Won't it be nice if you could do that in Github Actions, too?
        """
        Now wont it be nice if we could cache Docker steps on Github Actions, too? I have been looking for a way to do this for a while now, but it seemed too good to be true. Until I found 

        """
- Caching images with buildx
    - What is buildx? 
        """
        In simple words, the *build-push-action* lets you use a powered-up version of Docker inside Github Actions. This is powerful because Github Actions runners work remotely and are ephemeral. They have a fundamental limitation in networking and file-access - its not as easy to use Docker on Github Actions as it would on your local computer. The build-push-action plugin helps solve this issue.

        """
    - How it works
        """

        """
- How to use
    - Building the image
    - .github actions language
    - Example repo
- Conclusion
-->
