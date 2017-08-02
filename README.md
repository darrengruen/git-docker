# GIT in a docker container

This was set up primarily for deploys. Instead of having to provision a server with git, we can simply run it inside a container.

## Usage

This can be used quite easily by running the following
`docker run -v "$(pwd):/repo" -v /etc/localtime:/etc/localtime --name git_"$(date +%s)" gruen/git`

Be sure you are in the same directory as the `.git` directory _(see gotchas below)_

## GOTCHAS
It can still be used on any project, the main caveat being you'll need to be in the top level of the git repository to run it.

For example, say you have the following directory structure:
```
app
|
 -.git
|
 -build
|
 -src
 |
  --components
```

Running the container in `app/` running the following works fine
`docker run -it --rm -v /app:/repo --name git_"$(date +%s)" gruen/git`

But running the following will fail
`docker run -it --rm -v /app/components --name git_"$(date +%s)" gruen/git`

This is because it doesn't have access to the `.git` directory

Not a big issue if you know about it, but still an issue
