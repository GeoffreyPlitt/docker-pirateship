This folder is where you put your configs for each service.

These configs get symlinked/shared into the Vagrant VM and
then into the Docker containers so that any changes turn
into modifications here that you can commit in Git.

In this way, forking this repo and then committing your
config changes offers a nice way to make this suite of
tools work for you, but still be able to merge in upstream
changes from the original repo.
