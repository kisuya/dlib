# dlib python warpper install for windows with anaconda

## libjpeg version issue

dlib's libjpeg version and anaconda's libjpeg version are different.

so all function of dlib's libjpeg should be blocked.

## Unicode decoding error

In Korean environment, unicode decoding error occured.

```
UnicodeDecodeError: 'utf-8' codec can't decode byte 0xb9 in position 27: invalid start byte
```

setup.py moified :

``` python
# origin
def _log_buf(buf):
    if not buf:
        return
    if sys.stdout.encoding:
        buf = buf.decode(sys.stdout.encoding)

# modified
def _log_buf(buf):
    if not buf:
        return
    if sys.stdout.encoding:
        try:
            buf = buf.decode(sys.stdout.encoding)
        except UnicodeDecodeError :
            print("Unicode decode error")
```



## Compiling dlib Python API

Before you can run the Python example programs you must compile dlib. Type:

``` bash
python setup.py install
```

or type

``` bash
python setup.py install --yes USE_AVX_INSTRUCTIONS
```

if you have a CPU that supports AVX instructions, since this makes some things run faster.  Note that you need to have boost-python installed to compile the Python API.

## Boost python build

Set the BOOST_ROOT and BOOST_LIBRARYDIR environment variables before running cmake.

E.g.  Something like this:
```
set BOOST_ROOT=C:\\local\\boost_1_57_0
set BOOST_LIBRARYDIR=C:\\local\\boost_1_57_0\\stage\\lib
```

You will also likely need to compile boost yourself rather than using one of the precompiled 
windows binaries.  Do this by going to the folder tools\\build\\ within boost and running
bootstrap.bat.  

Then run the command:
```
b2 install
```

And then add the output bin folder to your PATH.  Usually this is the C:\\boost-build-engine\\bin
folder. 

Finally, go to the boost root and run a command like this:
```
b2 -a --with-python address-model=64 toolset=msvc runtime-link=static
```