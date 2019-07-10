# Android CI [![Android CI on Docker Hub](https://img.shields.io/docker/automated/code0987/android-ci.svg)](https://store.docker.com/community/images/code0987/android-ci)

An image for building Android apps with support for multiple SDK Build Tools. This Docker image contains the Android SDK and most common packages necessary for building Android apps in a CI tool. 

Based on [javiersantos/android-ci](https://github.com/javiersantos/android-ci).

## Sample usages

### GitLab
*.gitlab-ci.yml*

```yml
image: code0987/android-ci:latest

before_script:
    - export GRADLE_USER_HOME=`pwd`/.gradle
    - chmod +x ./gradlew

cache:
  key: "$CI_COMMIT_REF_NAME"
  paths:
     - .gradle/

stages:
  - build

build:
  stage: build
  script:
     - ./gradlew assembleDebug
  artifacts:
    paths:
      - app/build/outputs/apk/
```
