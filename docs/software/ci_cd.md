# Idea #

<https://github.com/ajdurbin/test> contains a sample application that follows all of the CI/CD concepts. We build a web application using Flask, create a Docker image for it, have a test suite, use Travis-CI's GitHub integration to build the image and run tests before deploying to Docker Hub, then use Heroku's GitHub integration to deploy the application online after Travis-CI passes. Travis-CI allows us to define private environment variables in each repository's settings that can be referenced in any scripts. This is very useful for passwords.

- <https://docs.travis-ci.com/user/docker/>
- <https://docs.travis-ci.com/user/deployment/heroku/>
- <https://devcenter.heroku.com/articles/github-integration>
- <https://medium.com/bettercode/how-to-build-a-modern-ci-cd-pipeline-5faa01891a5b>
- <https://docs.travis-ci.com/user/getting-started/>
- <https://medium.com/craft-academy/deploying-heroku-and-travis-ci-69d998ad408a>
- <https://codeburst.io/ci-cd-with-github-travis-ci-and-heroku-e088a24f32ef>

# Selfhosted #
Travis-CI does not really have a local image to be used. The major open-source alternative is Jenkins, but I have yet to be able to set it up appropriately using Docker to provision the slaves. Alternatives include Drone, CircleCI, Gitlab CI/CD. Drone is packaged as a Docker image and also uses YAML files like Travis-CI. Heroku is an excellent service for running Docker web applications and has 500 hours free per month usage. It has a command-line utility that is easily installed to test applications to be deployed before committing changes and triggering a build. But this is a supervised method, so it can be useful for developing first. Heroku also uses a Procfile that we need to find out more about.

- <http://docs.drone.io/getting-started/>
- <https://devcenter.heroku.com/articles/procfile>


# Sample .travis.yml #
```
sudo: required
services:
- docker
language: python
python:
- "3.5"
install:
- pip install -r requirements.txt
script:
- python -m pytest -v
after_success:
- echo "$DOCKER_PASS" | docker login -u "$DOCKER_USER" --password-stdin
- export APP=test
- export REPO=$DOCKER_USER/$APP
- export TAG=`if [ "$TRAVIS_BRANCH" == "master" ]; then echo "latest"; else echo $TRAVIS_BRANCH ; fi`
- docker build -f Dockerfile -t $REPO:$TAG -t $REPO:travis-$TRAVIS_BUILD_NUMBER .
- docker push $REPO:$TAG
- docker push $REPO:travis-$TRAVIS_BUILD_NUMBER
```

# Tools #
* jenkins
* travis-ci
* drone-io
* bettercodehub
* heroku

# Selfhosted V2 #
Jenkins has proven to be extremely difficult to install and configure slaves properly, plus I'm not a fan of the syntax. Alternatives are Drone and Concourse. All Drone tutorials look like they use Github repositories, but documentation allows you to specify Gitea, for example. Appears to be free to selfhost, though not super clear. Documentation is okay, uses YAML for the build files, seems pretty popular. Other alternative is Concourse, which is open source and has a good tutorial on installation. Also Abstruse. Of these Drone looks to be the most popular.

Wanted features:
- trigger build on commit
- run unit tests and email on failure
- build image, push to registry (local, remote), deploy
- Bonus points for Heroku deployment too
