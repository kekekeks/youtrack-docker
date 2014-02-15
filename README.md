# youtrack-docker
*Dead-simple youtrack deployment using docker*

These Dockerfiles allow you to easily build images to deploy your own [youtrack](http://www.jetbrains.com/youtrack/) instance.
It's free for up to ten users, so yeah.

## Disclaimer
(quote) Please note Docker is currently under heavy development. It should not be used in production (yet)

Besides that, as always, use these scripts with care.

Don't forget to back up your data very often, too.

## Requirements
Docker has to run. It supports many platforms like Ubuntu, Arch Linux, Mac OS X, Windows, EC2 or the Google Cloud.
[Click here](http://docs.docker.io/en/latest/installation/) to get specific infos on how to install on your platform.

You also need some RAM for youtrack, but I can't really tell how much. Maybe about 200-300MB.

## Oh nice! How do I do it?
1. Install docker. [It's not very hard.](http://docs.docker.io/en/latest/installation/)
2. Check out this repository:

  `git clone git://github.com/voidus/youtrack-docker && cd youtrack-docker`

3. Create images

  `docker build -t youtrack-data data`

  `docker build -t youtrack youtrack`

4. Create your data container

  `docker run -name youtrack-data-container youtrack-data true`

5. Run it! (Stop with CTRL-C, repeat at pleasure)

  `docker run --volumes-from youtrack-data-container -p 127.0.0.1:8080:8000 --rm youtrack`

Now open your browser and point it to `http://localhost:8080` and rejoice. :)

When deploying, take a look at the provided apache config file.

### A little explanation
The last commands parameters might have to be adjusted a little, so I'll explain them one by one.

`--volumes-from youtrack-data-container`

This makes youtrack use your data. Handle with care.

`-p 127.0.0.1:8080:8000`

This makes the port 8000 that youtrack listens at available to 127.0.0.1 on port 8080.
If you want to directly expose it, remove `127.0.0.1:`. If you want to change the port, change `8080`. Don't change
`8000`, it depends on internal stuff.

`--rm`

This removes the container generated by the command after it is finished. As all interesting data is stored in
youtrack-data-container, keeping it would just make your docker-list long.

## Miscellaneous
* I appreciate feedback of all kinds. Best thing since sliced bread? Drop me a line. Killed your dog? Let's see if I can
  find out how and maybe the next one can be spared.
* Again, don't forget to make backups.
* Assuming you trust in Docker, this should a production grade setup as far as I can tell.
  But, as always: If you're doing anything important, get someone who knows your situation do be the judge of that.
