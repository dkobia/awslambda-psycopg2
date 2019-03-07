psycopg2 Python Library for AWS Lambda
======================================

This is a custom compiled psycopg2 C library for Python. Due to AWS Lambda
missing the required PostgreSQL libraries in the AMI image, we needed to
compile psycopg2 with the PostgreSQL `libpq.so` library statically linked
libpq library instead of the default dynamic link.

### This library is compiled with:

- psycopg2 2.7.7
- postgresql 10.7
- Python 3.7

### How to use

Copy the `psycopg2` directory into your AWS Lambda zip package.

### Instructions on compiling this package from scratch

Here was the process that was used to build this package. You will need to
perform these steps if you want to build a different version of the psycopg2
library.

1. Download the
  [PostgreSQL source code](https://ftp.postgresql.org/pub/source) (.tar.gz) and extract into a directory.
2. Download the
  [psycopg2 source code](http://initd.org/psycopg/tarballs) (.tar.gz) and extract into a directory.
3. Go into the PostgreSQL source directory and execute the following commands:
  - `./configure --prefix {path_to_postgresql_source} --without-readline --without-zlib`
  - `make`
  - `make install`
4. Go into the psycopg2 source directory and edit the `setup.cfg` file with the following:
  - `pg_config={path_to_postgresql_source/bin/pg_config}`
  - `static_libpq=1`
5. Execute `python setup.py build` in the psycopg2 source directory.

After the above steps have been completed you will then have a build directory
and the custom compiled psycopg2 library will be contained within it. Copy this
directory into your AWS Lambda package and you will now be able to access
PostgreSQL from within AWS Lambda using the psycopg2 library!

#### Compiling with ssl support

To compile with ssl support steps 3 and 4 above become.

3. Go into the PostgreSQL source directory and execute the following commands:
  - `./configure --prefix {path_to_postgresql_source} --without-readline --without-zlib --with-openssl`
  - `make`
  - `make install`
4. Go into the psycopg2 source directory and edit the `setup.cfg` file with the following:
  - `pg_config={path_to_postgresql_source/bin/pg_config}`
  - `static_libpq=1`
  - `libraries=ssl crypto`

All other steps are identical.
