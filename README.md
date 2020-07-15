# LearnAudioVideo
记录学习音视频
## 1.MP3编码引擎LAME
SourceForge：https://sourceforge.net/projects/lame/files/lame
### build_armv7.sh脚本
```
./configure \
--disable-shared \
--disable-frontend \
--host=arm-apple-darwin \
--prefix="./thin/armv7" \
CC="xcrun -sdk iphoneos clang -arch armv7" \
CFLAGS="-arch armv7 -fembed-bitcode -miphoneos-version-min=7.0" \ LDFLAGS="-arch armv7 -fembed-bitcode -miphoneos-version-min=7.0" make clean
make -j8 make install
```
### build_arm64.sh脚本
```
./configure \
--disable-shared \
--disable-frontend \
--host=arm-apple-darwin \
--prefix="./thin/arm64" \
CC="xcrun -sdk iphoneos clang -arch arm64" \
CFLAGS="-arch arm64 -fembed-bitcode -miphoneos-version-min=7.0" \ LDFLAGS="-arch arm64 -fembed-bitcode -miphoneos-version-min=7.0" make clean
make -j8 make install
```
### 合并静态库命令lipo
```
lipo -create ./arm64/lib/libmp3lame.a ./armv7/lib/libmp3lame.a -output libmp3lame.a
```
## 2.FDK_AAC编码、解码AAC格式音频文件的开源库
SourceForge：https://sourceforge.net/p/opencore-amr/fdk-aac/ci/v0.1.4/tree/
### build_armv7.sh脚本
```
./configure \
--enable-static \
--disable-shared \
--host=arm-apple-darwin \ --prefix="$FDK_ROOT_DIR/thin/armv7"
CC="xcrun -sdk iphoneos clang" \ AS="gas-preprocessor.pl $CC"
CFLAGS="-arch armv7 -mios-simulator-version-min=7.0" \ LDFLAGS="-arch armv7 -mios-simulator-version-min=7.0" make clean
make -j8 make install
```
### FDK_AAC的配置选项中要去比LAME多配置一项AS参数，并且需要安装gas-preprocesssor
https://github.com/applexiaohao/gas-preprocessor
下载gas-preprocessor.pl，然后复制到/usr/local/bin/目录下，修改/usr/local/bin/gas-preprocessor.pl的文件权限为可执行权限
```
chmod 777 /usr/local/bin/gas-preprocessor.pl
```
## 3.X264是一个开源的H.264/MPEG-4 AVC视频编码函数库
http://www.videolan.org/developers/x264.html
git clone git://git.videolan.org/x264.git
### build_armv7.sh脚本
```
#!/bin/sh
export AS="gas-preprocessor.pl -arch arm -- xcrun -sdk iphoneos clang" export CC="xcrun -sdk iphoneos clang"
./configure \
--enable-static \
--enable-pic \
--disable-shared \
--host=arm-apple-darwin \
--extra-cflags="-arch armv7 -mios-version-min=7.0" \ --extra-asflags="-arch armv7 -mios-version-min=7.0" \ --extra-ldflags="-arch armv7 -mios-version-min=7.0" \ --prefix="./thin/armv7"
make clean
make -j8
make install
```
