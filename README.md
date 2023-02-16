# Getting Started

## CircleCI Config Example

```
version: 2.1

jobs:
  swiftlint:
    docker:
        - image: ghcr.io/ciaranmul/swiftlintdocker:latest
    steps:
        - checkout
        - run: swiftlint lint --reporter html | tee swiftlint.result.html
        - store_artifacts:
            path: swiftlint.result.html
```

## Running Locally

```
docker run -v `pwd`:`pwd` -w `pwd` ghcr.io/ciaranmul/swiftlintdocker swiftlint lint
```

# About The Image

## Base Docker Image

The docker image is based on the official CircleCI base container image. This image is itself based on Ubuntu.

## Swift

Swift is not packaged with the CircleCI Base image by default so must be installed separaretly. Since the CircleCI Base image is based on Ubuntu, the Ubuntu build of Swift, as provided by Apple, is used. Dependencies for installing Swift are installed from apt.

## SwiftLint

SwiftLint is cloned and then built and installed based on how it is done in the official SwiftLint Dockerfile.

# This approach V.S. forking the SwiftLint repo and using its existing Dockerfile

By taking the approach of maintaining a separate Dockerfile that describes our SwiftLint requirements, instead of forking the whole SwiftLint project, we should have less upkeep to do. Rather than have to keep our fork up to date with changes to the SwiftLint project, we can simply update the tag for the swiftlint version and occasionally update the dependencies.

