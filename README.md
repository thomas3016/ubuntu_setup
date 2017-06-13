### apt-get install
```
sudo apt-get install ros-indigo-desktop-full ros-indigo-nmea-msgs ros-indigo-nmea-navsat-driver ros-indigo-sound-play ros-indigo-jsk-visualization
sudo apt-get install libnlopt-dev freeglut3-dev qtbase5-dev libqt5opengl5-dev libssh2-1-dev libarmadillo-dev libpcap-dev gksu libgl1-mesa-dev
```
### ROS Indigo
```
sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu trusty main" > /etc/apt/sources.list.d/ros-latest.list'

wget http://packages.ros.org/ros.key -O - | sudo apt-key add -

sudo apt-get update

sudo rosdep init
rosdep update
echo "source /opt/ros/indigo/setup.bash" >> ~/.bashrc
source ~/.bashrc
sudo apt-get install python-rosinstall

sudo apt-get install ros-indigo-desktop-full ros-indigo-nmea-msgs ros-indigo-nmea-navsat-driver ros-indigo-sound-play ros-indigo-jsk-visualization
sudo apt-get install libnlopt-dev freeglut3-dev qtbase5-dev libqt5opengl5-dev libssh2-1-dev libarmadillo-dev libpcap-dev gksu
```

### Cuda 7.5
```
http://developer.nvidia.com/cuda-downloads から CUDA をダウンロード
(以下、cuda-repo-ubuntu1404_7.5を想定)
sudo dpkg -i cuda-repo-ubuntu1404_7.5
sudo apt-get update
sudo apt-get install cuda-7.5

tar xvzf cudnn-7.5-linux-x64-v5.1-ga.tgz
sudo cp cuda/include/cudnn.h /usr/local/cuda/include
sudo cp cuda/lib64/libcudnn* /usr/local/cuda/lib64
sudo chmod a+r /usr/local/cuda/include/cudnn.h /usr/local/cuda/lib64/libcudnn

# sudo apt-get install nvidia-367 or sudo apt-get install nvidia-361
nvcc -V
nvidia-smi
```

### OpenCV 2
```
sudo apt-get install libgflags-dev libgoogle-glog-dev liblmdb-dev
sudo apt-get -y install libopencv-dev build-essential cmake git libgtk2.0-dev pkg-config python-dev python-numpy libdc1394-22 libdc1394-22-dev libjpeg-dev libpng12-dev libtiff4-dev libjasper-dev libavcodec-dev libavformat-dev libswscale-dev libxine-dev libgstreamer0.10-dev libgstreamer-plugins-base0.10-dev libv4l-dev libtbb-dev libqt4-dev libfaac-dev libmp3lame-dev libopencore-amrnb-dev libopencore-amrwb-dev libtheora-dev libvorbis-dev libxvidcore-dev x264 v4l-utils unzip

wget https://github.com/opencv/opencv/archive/2.4.13.2.zip
unzip 2.4.13.2.zip
cd opencv-2.4.13.2/
mkdir build && cd build/

cmake -D CMAKE_BUILD_TYPE=RELEASE -D CMAKE_INSTALL_PREFIX=$INSTALL_DIR -D WITH_TBB=ON -D BUILD_NEW_PYTHON_SUPPORT=ON -D WITH_V4L=ON -D INSTALL_C_EXAMPLES=ON -D INSTALL_PYTHON_EXAMPLES=ON -D BUILD_EXAMPLES=ON -D WITH_OPENGL=ON -D WITH_VTK=ON -DBUILD_TIFF=OFF -DCUDA_GENERATION=Auto ..

make -j8
sudo make install
sudo ldconfig

# probably needed
sudo cp -r opencv-2.4.13.2/include/opencv2 /usr/local/include

# probably needed
sudo apt-get -y install build-essential cmake git libgtk2.0-dev pkg-config python-dev python-numpy libdc1394-22 libdc1394-22-dev libjpeg-dev libpng12-dev libtiff5-dev libjasper-dev libavcodec-dev libavformat-dev libswscale-dev libxine2-dev libgstreamer0.10-dev libgstreamer-plugins-base0.10-dev libv4l-dev libtbb-dev libqt4-dev libfaac-dev libmp3lame-dev libopencore-amrnb-dev libopencore-amrwb-dev libtheora-dev libvorbis-dev libxvidcore-dev x264 v4l-utils unzip
```

### QT
```
wget http://download.qt.io/official_releases/qt/5.7/5.7.0/qt-opensource-linux-x64-5.7.0.run
chmod +x qt-opensource-linux-x64-5.7.0.run
./qt-opensource-linux-x64-5.7.0.run
sudo apt-get install mesa-common-dev
```

### .bashrc
```
source /opt/ros/indigo/setup.bash
export PATH=/home/katou01/anaconda2/bin:$PATH
export PATH="/usr/local/cuda-7.5/bin:$PATH"
export PATH="/usr/local/cuda-7.5:$PATH"
export LD_LIBRARY_PATH="/usr/local/cuda-7.5/lib64:$LD_LIBRARY_PATH"

export CAFFE_ROOT="/home/katou01/caffe"
export PYTHONPATH="/home/katou01/caffe/python:$PYTHONPATH"
 #added by Anaconda2 4.2.0 installer
export PATH="/home/katou01/anaconda2/bin:$PATH"

export C_INCLUDE_PATH="/home/katou01/anaconda2/include/:$C_INCLUDE_PATH"
export CPLUS_INCLUDE_PATH="/home/katou01/anaconda2/include/:$CPLUS_INCLUDE_PATH"
export CPLUS_INCLUDE_PATH="/home/katou01/anaconda2/include/python2.7/:$CPLUS_INCLUDE_PATH"

export LD_LIBRARY_PATH="/lib/x86_64-linux-gnu:$LD_LIBRARY_PATH"
export CPLUS_INCLUDE_PATH=/usr/include/python2.7
```

### caffe
```
sudo apt-get install libatlas-base-dev libprotobuf-dev libleveldb-dev libsnappy-dev libopencv-dev libhdf5-serial-dev protobuf-compiler

git clone https://github.com/BVLC/caffe.git
cd caffe
cp Makefile.config.example Makefile.config

# edit file Makefile.config

Use cudnn
#anaconda
python layer

vi include/caffe/layers/python_layer.hpp
#self_.attr("phase") = static_cast<int>(this->phase_);

make all -j8
make test -j8
make runtest -j8

sudo apt-get install python-dev python-pip python-numpy python-skimage gfortran
sudo pip install -r ~/caffe/python/requirements.txt

make pycaffe
```

### Autoware
```
cd $HOME
git clone https://github.com/CPFL/Autoware.git
cd ~/Autoware/ros/src
catkin_init_workspace
cd ../
./catkin_make_release
```

### Python3 virtualenv
```
sudo pip3 install virtualenv
sudo pip3 install virtualenvwrapper


export WORKON_HOME=$HOME/.virtualenvs
export PROJECT_HOME=$HOME/Devel
source /usr/local/bin/virtualenvwrapper.sh
source ./.bashrc


virtualenvwrapperで新しい環境を作る

mkvirtualenv [名前] --python /usr/bin/python3


virtualenvwrapperで環境に入る

workon [名前]


virtualenvwrapperで環境を削除

rmvirtualenvwrapper [名前]


virtualenvwrapperで環境から出る

deactivate
```

### OpenCV3 on virtual env python3
```
http://www.pyimagesearch.com/2015/07/20/install-opencv-3-0-and-python-3-4-on-ubuntu/

cmake -D CMAKE_BUILD_TYPE=RELEASE -D CMAKE_INSTALL_PREFIX=/home/katou01/.virtualenvs/py3/local  -D INSTALL_PYTHON_EXAMPLES=OFF -D PYTHON_EXECUTABLE=$(which python3) -D BUILD_opencv_python3=ON -D BUILD_opencv_python2=ON BUILD_EXAMPLES=OFF -D WITH_FFMPEG=OFF -D  BUILD_opencv_java=OFF WITH_CUDA=ON  ..

cmake -D CMAKE_BUILD_TYPE=RELEASE -D CMAKE_INSTALL_PREFIX=/home/katou01/.virtualenvs/py3/local  -DPYTHON_INCLUDE_DIRS=/home/katou01/.virtualenvs/py3/include/python3.4m -DPYTHON3_LIBRARY=/home/katou01/.virtualenvs/py3/lib/python3.4/config-3.4m-x86_64-linux-gnu/libpython3.4m.so -D PYTHON3_NUMPY_INCLUDE_DIRS=/home/katou01/.virtualenvs/py3/lib/python3.4/site-packages/numpy/core/include -DPYTHON3_PACKAGES_PATH=/home/katou01/.virtualenvs/py3/lib/python3.4/site-packages ..
```

### ubuntu16
```
sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'
sudo apt-key adv --keyserver hkp://ha.pool.sks-keyservers.net:80 --recv-key 421C365BD9FF1F717815A3895523BAEEB01FA116
sudo apt update
sudo apt install ros-kinetic-desktop-full
sudo rosdep init
rosdep update
echo "source /opt/ros/kinetic/setup.bash" >> .bashrc
source .bashrc

sudo apt install python-rosintall
sudo apt-get install ros-kinetic-desktop-full ros-kinetic-nmea-msgs ros-kinetic-nmea-navsat-driver ros-kinetic-sound-play ros-kinetic-jsk-visualization ros-kinetic-grid-map ros-kinetic-gps-common
sudo apt-get install ros-kinetic-controller-manager ros-kinetic-ros-control ros-kinetic-ros-controllers ros-kinetic-gazebo-ros-control ros-kinetic-joystick-drivers
sudo apt-get install libnlopt-dev freeglut3-dev qtbase5-dev libqt5opengl5-dev libssh2-1-dev libarmadillo-dev libpcap-dev gksu libgl1-mesa-dev libglew-dev python-wxgtk3.0

```
