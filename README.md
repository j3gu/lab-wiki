# lab-resource

Internal documentation for the lab. To contribute please edit files under 

```
- public
- private
```

To publish contents under `public` folder to github.io, you need to [install docker](https://xinhe-lab.github.io/lab-wiki/orientation/jupyter-setup.html#install-docker), then run from `bash` terminal:

```
docker run --rm --security-opt label:disable -v $(pwd):/srv/jekyll -u $(id -u):100 -t \
	gaow/lab-wiki sos run release.sos --no-use-docker
```
to write the changes to the repo, add & commit, and push. The updated wiki will then be displayed at https://xinhe-lab.github.io/lab-wiki

To preview changes before you push:

```
docker run --rm --security-opt label:disable -v $(pwd):/srv/jekyll -u $(id -u):100 -p 4000:4000 --name wiki-server -t \
	gaow/lab-wiki sos run release.sos --no-use-docker --serve
```
then see the changes at http://0.0.0.0:4000/lab-wiki/welcome.html. You have to stop the docker based webserver after use, via command:

```
docker stop wiki-server
```

Otherwise next time the `docker run` command above will complain that port 4000 is in use.

## Why docker?

The wiki is powered by `jupyterbook` which uses `jekyll`, a `ruby` based tool for generating static website. These tools, along with their dependencies, are not straightforward to install. Also instead of vanilla `jupyterbook` + `jekyll` some modifications are made to it (making file organization much clearer) and built into `release.sos` as a pipeline, which requires `sos` to run it (requires Python 3.6+). All these tools are built into the docker image and users will only have to run the `docker` commands above.
