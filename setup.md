# Setup Git Kata Environment

Before starting Git Kata hands-on exercises a fully functional Git environment is needed. This document contains how to prepare an isolated and clean git environment every time.

## Prerequisite

Before starting the docker should be installed in the computer. If it didn't install, the following link should be visited.

[Install Docker Engine](https://docs.docker.com/engine/install/)

## Build from Scratch

The docker image is so simple and lightweight for the Git Kata. It can be built locally.

```dockerfile
FROM alpine:latest

RUN apk fix && \
    apk update && \
    apk upgrade && \
    apk add git less

WORKDIR /kata
```

For basic scenarios, `git` and `less` is enough. However, for more complex scenarios, the following Dockerfile can be used.

```dockerfile
FROM alpine:latest

RUN apk fix && \
    apk update && \
    apk upgrade && \
    apk add git less git-lfs gpg openssh patch && \
    git lfs install

WORKDIR /kata
```

During the build operation, the docker needs to connect to the internet to download the required packages. Due to this the build command should contain the `--network host` parameter.

```bash
docker build --network host --tag <tag-name>
```

## Ready Docker Images

If the system has some limitations or don't want to deal with building an image, the following image is in your service.

[tatoglu/git-kata](https://hub.docker.com/r/tatoglu/git-kata)

That has some tags to identify the installed packages.

### Basic Package Image

The `basic` tag image contains only `git` and `less` packages. It is handy for many of the kata scenarios.

```bash
docker pull tatoglu/git-kata:basic
```

### Full Package Image

The `full` tag image contains all the packages mentioned below. It can be used for some edge and remote repository kata scenarios. The `latest` tag also refers to this image.

- git
- less
- git-lfs
- gpg
- openssh
- patch

```bash
docker pull tatoglu/git-kata:full
```

## Before Staring

Using a docker image is an optional step. However, if this is wanted to skip, don't forget that the environment should be arranged like the first time of the git before and after running every kata scenario.

In addition, please check the below disclaimer, if wanted to use the current git installation without the docker image. 

The Git Kata project is provided as-is and does not come with any warranties or guarantees of any kind. By using the Git Kata project, you acknowledge and agree to the following:

1. The Git Kata project is for educational and training purposes only. It is not intended to be used in production environments or for critical systems.
2. The Git Kata project may contain bugs, errors, or inconsistencies. While we strive to provide accurate and reliable information, we cannot guarantee the correctness or completeness of the content.
3. The Git Kata project may involve executing Git commands that can modify your local repositories and Git configuration. It is your responsibility to ensure that you have backups and take necessary precautions before running any Git commands.
4. The Git Kata project may reference third-party tools, libraries, or services. We do not endorse or provide support for these third-party components, and their usage is subject to their respective licenses and terms.
5. The Git Kata project may include links to external resources or websites. We are not responsible for the content, availability, or privacy practices of these external resources.
6. The Git Kata project is not affiliated with or endorsed by Git, GitHub, GitLab, or any other version control system or service mentioned.
7. We disclaim any liability for any loss, damage, or inconvenience caused by the usage of the Git Kata project or any reliance on its content.

Please use the Git Kata project responsibly, exercise caution, and ensure that you understand the implications of the actions you take. If you encounter any issues or have concerns, please reach out to us and we will do our best to address them.

## Starting

Before starting every kata scenario, the following command must be run to prepare the required git environment. The required git environment tag is written on the scenario documents.

```bash
docker run -it tatoglu/git-kata:basic /bin/sh
```

The image was built locally you should run the following command. Don't forget the change the `<tag-name>`.

```bash
docker run -it <tag-name> /bin/sh
```

Some scenarios need to connect to the Internet. In this case, the following command should be worked.

```bash
docker run -it --network host tatoglu/git-kata:basic /bin/sh
```

## After Staring

With the docker images, the non-configured environment will be ready. But before running the kata scenarios some config should be set. To learn this please check the [Git Configuration](config.md) scenario document.
