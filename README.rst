==========================
QDB Django Cache Backend
==========================

A simple QDB cache backend for Django based on `django-redis-cache` v0.10.0.


Notice
------

1. `qdb-py` does not support HiredisParser, use PythonParser instead.
2. `qdb` doest not support `pipeline`.
3. `qdb` does not support `password`.


Usage
-----

1. Run ``python setup.py install`` to install,
   or place ``qdb_cache`` on your Python path.

2. Modify your Django settings to use ``qdb_cache`` :

On Django < 1.3::

    CACHE_BACKEND = 'qdb_cache.cache://<host>:<port>'

On Django >= 1.3::


    # When using TCP connections
    CACHES = {
        'default': {
            'BACKEND': 'qdb_cache.QdbCache',
            'LOCATION': '<host>:<port>',
            'OPTIONS': {
                'DB': 1,
                'PARSER_CLASS': 'qdb.connection.PythonParser'
            },
        },
    }

    # When using unix domain sockets
    # Note: ``LOCATION`` needs to be the same as the ``unixsocket`` setting
    # in your qdb.json
    CACHES = {
        'default': {
            'BACKEND': 'qdb_cache.QdbCache',
            'LOCATION': '/path/to/socket/file',
            'OPTIONS': {
                'DB': 1,
                'PARSER_CLASS': 'qdb.connection.PythonParser'
            },
        },
    }


