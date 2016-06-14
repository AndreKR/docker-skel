# Docker App Skeleton

Unfortunately Docker has many shortcomings:
* No way to examine a container that won't start
* Has no record of whether `-it` or `-i` must be used for `docker run` (Usually `-it` for interactive apps and `-i` for apps that work with stdin/stdout)
* By default creates a new container for each run and keeps it around
* Doesn't really complain when ports or volumes are not bound
* Generates tons of transient images during development and there's no easy way to clean them up

That is why for new apps I use this skeleton, which provides:
* A build script that creates just one tagged image and re-builds it over and over
* A run script to keep record of the necessary run options (it also mounts a volume from a directory next to the run script)
* A Dockerfile based on Ubuntu where an SSH daemon can be enabled
* A config file to be dropped into /etc/supervisor/conf.d
