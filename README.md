# JetsonTx2
My Research on Jetson TX2
first need to boot with jetpack3.3 cuz of 4.0 doesnt give shit about tx2
https://developer.nvidia.com/embedded/jetpack
ty for jkjung
 https://jkjung-avt.github.io/opencv3-on-tx2/
$ sudo apt-get install aptitude
$ sudo apt-get install nano(maybe need it someday)
 
 download ocv.sh
$ sudo chmod -x ocv.sh
$ sudo bash ocv.sh
should change (line #41) as 'backend      : TkAgg' both of them
$ sudo vim /usr/local/cuda/include/cuda_gl_interop.h
//#if defined(__arm__) || defined(__aarch64__)
//#ifndef GL_VERSION
//#error Please include the appropriate gl headers before including cuda_gl_interop.h
//#endif
//#else
 #include <GL/gl.h>
//#endif
$ cd /usr/lib/aarch64-linux-gnu/
$ sudo ln -sf tegra/libGL.so libGL.so
$ mkdir -p ~/src
$ cd ~/src
$ wget https://github.com/opencv/opencv/archive/3.4.0.zip \
       -O opencv-3.4.0.zip
$ unzip opencv-3.4.0.zip
### Build opencv (CUDA_ARCH_BIN="6.2" for TX2, or "5.3" for TX1)
$ cd ~/src/opencv-3.4.0
$ mkdir build
$ cd build
$ cmake -D CMAKE_BUILD_TYPE=RELEASE -D CMAKE_INSTALL_PREFIX=/usr/local \
        -D WITH_CUDA=ON -D CUDA_ARCH_BIN="6.2" -D CUDA_ARCH_PTX="" \
        -D WITH_CUBLAS=ON -D ENABLE_FAST_MATH=ON -D CUDA_FAST_MATH=ON \
        -D ENABLE_NEON=ON -D WITH_LIBV4L=ON -D BUILD_TESTS=OFF \
        -D BUILD_PERF_TESTS=OFF -D BUILD_EXAMPLES=OFF \
        -D WITH_QT=ON -D WITH_OPENGL=ON ..
$ make -j4
$ sudo make install
its all for opencv version 3

