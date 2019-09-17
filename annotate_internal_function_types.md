# Annotating internal function argument and return types PHP-DEV

Lack of type information for internal functions in Reflection is a
long-standing issue. In PHP 8 we finally have all the necessary technical
groundwork done to support argument and return type annotations on internal
functions at scale.

## How to do it

The only thing left is to actually add those type annotations ... to many
hundreds of functions. This is something everyone can help with, as it does
not need expertise in C.

Nikic opened a sample PR to show the process:
https://github.com/php/php-src/pull/4499

Here, we take some existing arginfo structures in basic_functions.c and
convert them into stubs in basic_functions.stub.php. We can take the
argument names from the existing arginfo. To figure out the types, we need
to look at the implementation (the php.net documentation tends to lie about
details).

For example, the first function, set_time_limit is defined in
https://github.com/php/php-src/blob/172c71980df0fe4c9d62c3365f0a2cdb139e3e86/main/main.c#L1501.
We see that it accepts an "l" parameter, which is an int. We see that it
uses RETVAL_TRUE and RETVAL_FALSE, which means the return value is a bool.

Once this is done, we need to auto-generate new arginfo data. If you have a
development setup, this is done automatically when running "make".
Otherwise, it's possible to manually run "php scripts/dev/gen_stub.php
ext/standard/basic_functions.stub.php".


## To do
ext/dba
ext/dom
ext/ffi
ext/hash
ext/imap
ext/intl
ext/libxml
ext/mbstring
ext/mysqli
ext/mysqlnd
ext/oci8
ext/odbc
ext/opcache
ext/pcntl
ext/pdo
ext/pdo_*
ext/pgsql
ext/phar
ext/pspell
ext/reflection
ext/snmp
ext/soap
ext/sockets
ext/sodium
ext/spl
ext/tidy
ext/xml
ext/xmlreader
ext/xmlrpc
ext/xmlwriter
ext/xsl


## Incomplete:
ext/standard


## Pending PRs
ext/exif
ext/fileinfo
ext/ldap
ext/session
ext/simplexml


## Complete

ext/bcmath
ext/bz2
ext/calendar
ext/com_dotnet
ext/ctype
ext/curl
ext/date
ext/enchant
ext/filter
ext/ftp
ext/gd
ext/gettext
ext/gmp
ext/iconv
ext/json
ext/openssl
ext/pcre
ext/posix
ext/readline
ext/shmop
ext/sqlite3
ext/sysvmsg
ext/sysvsem
ext/sysvshm
ext/tokenizer
ext/zip
ext/zlib
