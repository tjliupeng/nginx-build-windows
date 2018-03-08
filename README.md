# nginx build on Windows

## Environment and Tools

- Microsoft Visual Studio 2015
- MinGW (which including Msys)
- Perl, such as ActivePerl to build Openssl
- ThirdParty libraries source: PCRE, zlib and Openssl
- Version: nginx 1.13.9; PCRE 8.40; Openssl 1.1.0g; zlib 1.2.11

You can download the library source code tar.gz and extract them to the objs/lib folder. This repository includes them already.

Note: The version in the Openssl folder name should be removed because in the file auto\lib\openssl\makefile.msvc the folder name is without version information.

## Build Steps

1. Open the "Developer Command Prompt for VS2015". Run "C:\Program Files (x86)\Microsoft Visual Studio 14.0\VC\bin\vcvars32.bat".
2. Run "C:\MinGW\msys\1.0\msys.bat" to open the MINGW32 environment.
3. Enter the repository folder. Run the command
```
auto/configure \
--with-cc=cl \
--builddir=objs \
--prefix= \
--conf-path=conf/nginx.conf \
--pid-path=logs/nginx.pid \
--http-log-path=logs/access.log \
--error-log-path=logs/error.log \
--sbin-path=nginx.exe \
--http-client-body-temp-path=temp/client_body_temp \
--http-proxy-temp-path=temp/proxy_temp \
--http-fastcgi-temp-path=temp/fastcgi_temp \
--with-cc-opt=-DFD_SETSIZE=1024 \
--with-pcre=objs/lib/pcre-8.40 \
--with-zlib=objs/lib/zlib-1.2.11 \
--with-openssl=objs/lib/openssl \
--with-openssl-opt=no-asm \
--with-select_module  \
--with-http_ssl_module \
```
4. Run "nmake -f objs/Makefile".
5. The nginx.exe should be generated in objs folder.