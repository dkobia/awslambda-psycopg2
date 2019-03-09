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

Copy the `psycopg2` folder in the `build` folder into your AWS Lambda zip package.

### Compile with different versions of libraries

*Library needs to be compiled in amazon linux environment.
Most likely you don't have the environment.*

**Solution? Docker!**

1. Install Docker.
1. Download the
  [PostgreSQL source code](https://ftp.postgresql.org/pub/source) (.tar.gz),
  rename to **postgresql.tar.gz** and put it into `sources` folder.
1. Download the
  [psycopg2 source code](http://initd.org/psycopg/tarballs) (.tar.gz),
  rename to **psycopg2.tar.gz** and put it into `sources` folder.
1. build image: `make build`
1. run image: `make run`
1. delete image if you don't need it anymore: `make clean`

custom compiled psycopg2 library is now in `build` folder.

### Compile with SSL support

- Change step 4 above to: `make build SSL=1`