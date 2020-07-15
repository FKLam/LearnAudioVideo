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
