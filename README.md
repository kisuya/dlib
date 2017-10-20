# dlib python warpper install for windows with anaconda

## libjpeg version issue

dlib's libjpeg version and anaconda's libjpeg version are different.

so all function of dlib's libjpeg will be blocked.

## Compiling dlib Python API

Before you can run the Python example programs you must compile dlib. Type:

```bash
python setup.py install
```

or type

```bash
python setup.py install --yes USE_AVX_INSTRUCTIONS
```

if you have a CPU that supports AVX instructions, since this makes some things run faster.  Note that you need to have boost-python installed to compile the Python API.

