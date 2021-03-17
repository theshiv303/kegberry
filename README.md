# Kegberry: Complete Beer Tap Monitoring and Display for Raspberry Pi

You've got a Raspberry Pi and you love beer on tap.  Now what? *Make it a
Kegberry*.

## What can it do?

* **Keg Volume Monitor.** Want to know what's left?  With a little extra
  hardware, your Kegberry becomes a powerful and battle-tested keg monitor.
* **Digital Tap List.**  Give your taps an internet presence.  Kegberry's
  server lets everyone know what's on tap.
* **Notification System.** Want to be alerted when the keg is running low,
  or when someone has started pouring?  No problem; Kegberry does it all.
* **Account System.** Give your friends and family access to your data, and
  enable privacy modes to keep others out.

... and much more.


## What does it cost?

**It's free!** You provide the Raspberry Pi and optional HDMI display,
we give you the software for free.


## Get Started

For a quick start, run our simple install script by pasting the following
command into your Raspbian system:


```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/theshiv303/kegberry/master/install.sh)"
```

The installer will guide you through the next steps.

## Issues

**Fix ghost pours**

After docker image pull:

```
sudo docker run -it [kegbot pycore container id] bash
vi kegbot/pycore/common_defs.py
pour setting... 30
exit
sudo docker commit [container id] kegbot/pycore-1:latest (or w/e)
sudo docker stop [container id]
edit docker-compose.yml to reflect new name (eg: kegbot/pycore-1:latest)
*it might not be required but i also added the command for pycore to docker-compose.yml to ensure it starts correctly:
command: python bin/kegbot_core.py
````

**Fix core_user already exists during setup**

```
sudo docker exec -it [kegbot server container id] bash
export DJANGO_SETTINGS_MODULE=pykeg.settings
django-admin migrate --fake-initial
```
Attempted to do this in views.py via management.call_command(..., fake_initial=True) but no dice.

**COMPOSE_HTTP_TIMEOUT**

```
export COMPOSE_HTTP_TIMEOUT=500
or
sudo COMPOSE_HTTP_TIMEOUT=500 docker-compose up -d
sudo COMPOSE_HTTP_TIMEOUT=500 docker-compose down
```

## Help & Next Steps

Have questions, need help, or want to show off your build? Visit the
[Kegbot Project Forum](https://forum.kegbot.org).


## Open Source: Powered by Kegbot

Kegberry is brought to you by the same team that
invented [Kegbot](https://kegbot.org/), the original intelligent Kegerator.

Under the hood, Kegberry is built around
[Kegbot Server](https://github.com/Kegbot/kegbot-server), a mature, heavily
tested keg monitoring and management server.


## License and Copyright

All code is offered under the **MIT** license, unless otherwise noted.  Please
see `LICENSE.txt` for the full license.
