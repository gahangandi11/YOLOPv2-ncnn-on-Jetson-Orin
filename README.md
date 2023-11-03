# YOLOPv2-ncnn-on-Jetson-Orin
First you have to install ncnn on your jetson device using the following commands
```
git clone https://github.com/Tencent/ncnn.git
cd ncnn
git submodule update --init
mkdir -p build
cd build
cmake -DCMAKE_BUILD_TYPE=Release -DCMAKE_TOOLCHAIN_FILE=../toolchains/jetson.toolchain.cmake -DNCNN_VULKAN=ON -DNCNN_BUILD_EXAMPLES=ON ..
make -j$(nproc)
make install
```
After you have installed ncnn, use the following commands to build the ncnn model on your jetson device

```
git clone https://github.com/gahangandi11/YOLOPv2-ncnn-on-Jetson-Orin.git
cd YOLOPv2-ncnn-on-Jetson-Orin
mkdir build
cd build 
cmake ..
make 
./yolopv2_ncnn ../imgs/veh3.jpg
```
