badg.us
=======

badg.us is a badge service based on [django-badger][] and [playdoh][].

[playdoh]: https://github.com/mozilla/playdoh
[django-badger]: https://github.com/mozilla/django-badger

Bugs and Ideas
--------------
Feel free to file them [as issues on the badges.mozilla.org project][issues]!

[issues]: https://github.com/mozilla/badges.mozilla.org/issues

Development
-----------

Here's how I get it running on my MacBook:

    git clone 
    git submodule update --init --recursive
    # some submodules could be out of dates. please, update submodules if there are error while installing.
    # git submodule foreach 'git fetch origin; git checkout $(git rev-parse --abbrev-ref HEAD); git reset --hard origin/$(git rev-parse --abbrev-ref HEAD); git submodule update --recursive; git clean -dfx'
    virtualenv --no-site-packages venv
    . ./venv/bin/activate
    pip install -r requirements/compiled.txt
    pip install -r requirements/dev.txt
    # Set up a mysql database
    # Edit badgus/settings/local-dist.py and rename the flie to local.py
    # change db credentials and add HMAC_KEYS
    ./manage.py syncdb
    ./manage.py migrate
    ./manage.py compress_assets
    ./manage.py runserver 0.0.0.0:8000

Under Ubuntu 12.10 (64 bit), all the above worked after first installing some
packages and rejiggering some files:

    sudo apt-get install build-essential python-dev python-pip \
        python-virtualenv mysql-server libmysqlclient-dev libxml2-dev \
        libxslt-dev memcached libjpeg8 libjpeg62-dev libfreetype6 \
        libfreetype6-dev

    sudo ln -s /usr/lib/x86_64-linux-gnu/libjpeg.so /usr/lib
    sudo ln -s /usr/lib/x86_64-linux-gnu/libfreetype.so /usr/lib
    sudo ln -s /usr/lib/x86_64-linux-gnu/libz.so /usr/lib

License
-------
This software is licensed under the [New BSD License][BSD]. For more
information, read the file ``LICENSE``.

[BSD]: http://creativecommons.org/licenses/BSD/
