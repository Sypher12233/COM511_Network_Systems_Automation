[Personal Learning Record](../../personal_journal/personal_journal.md) | [Session Notes](../sessions/README.md) 

# Session 5

## Topics covered
*What topics were covered in this session*
* Why containers: faster to start and lighter than full VMs
* Images vs containers: an image is the template, a container is a running copy of it
* Docker Desktop
* Running a container and mapping a port to the host
* Dockerfile and building an image with `docker build`

## Personal Notes and research following this session
*Which class sessions and personal research refers to technology in this proposal. Link to examples.*
* Docker Desktop Learning center walkthroughs: "How do I run a container?" and TODO (name of the other walkthrough)
* Docker sample app: [welcome-to-docker](https://github.com/docker/welcome-to-docker)
* Session notes: [Installing and using Docker Desktop](../../../sessions/session5/docs/InstalingAndUsingDockerDesktop.md)

## Exercises and results
*What exercises did you complete. What results. Screen shots and notes*
### Installing Docker Desktop
* Installed Docker Desktop on my MacBook
* Used the built-in terminal in Docker Desktop for the commands

### Walkthrough 1: running my first container
* Followed the Docker Desktop walkthrough to run the `welcome-to-docker` container
* Container's port 80 mapped to port 8088 on my laptop
* Result: container showed up in the Containers list

![Docker Desktop containers list](../images/w5-docker-desktop.png)

### Walkthrough 2: building my own image
* Cloned the sample app with `git clone` and moved into the `welcome-to-docker` folder
* The repo already has a Dockerfile. It starts from `node:18-alpine` and creates an `/app` folder
* Built the image with `docker build -t img .`
* Ran a container from my image on port 8089 (TODO: confirm the run command)
* Result: opened `http://localhost:8089` and got the "You ran your first container" page

![Container running in the browser](../images/w5-first-container.png)



## Summary of learning
*What did you learn through these exercises*

[Personal Learning Record](../../personal_journal/personal_journal.md) | [Session Notes](../sessions/README.md) 

## Summary of learning
*What did you learn through these exercises*
* TODO: 3–4 bullets in your own words (prompts below)