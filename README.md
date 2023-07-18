
# Installing nextpnr

```sh
cd nextpnr

cmake . -DARCH=gowin -DGOWIN_BBA_EXECUTABLE=`which gowin_bba` -DPYTHON_INCLUDE_DIR=$(python3 -c "from distutils.sysconfig import get_python_inc; print(get_python_inc())")  \
-DPYTHON_LIBRARY=$(python3 -c "import distutils.sysconfig as sysconfig;import os;  print(os.path.join(sysconfig.get_config_var('LIBDIR'), [f for f in os.listdir(sysconfig.get_config_var('LIBDIR')) if f.endswith('.dylib') or f.endswith('.a')][0]))")

make
sudo make install
```
