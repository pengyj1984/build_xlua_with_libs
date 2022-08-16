同步原项目
=====

## build注意事项
生成windows相关库的时候，注意检查下 vs 的工具路径，可能需要修改。

## 从原项目合并
从主页 clone 到本地之后，可以通过 git remote -v 查看远程分支。默认应该只有自己的分支。
输入指令 git remote add upstream https://github.com/chexiongsheng/build_xlua_with_libs 建立与原项目的关联。
此时再输入指令 git remote -v 查看应该会多出两条记录。
通过指令 git pull upstream master 即可实现同步原项目的代码，再 push 到自己的项目即可。

## 同步 LuaJIT
LuaJIT 原项目 https://github.com/LuaJIT/LuaJIT
目前用的是 luajit-2.1.0b3
luajit-2.1 中是2022.05.20从github上拉下来的，但是用这个生成的 windows 版本 dll 有问题，会导致unity闪退
更换luajit库的方法:
1. 修改需要运行的脚本中的目录，比如运行 make_win64_luajit_vs2017.bat, 修改第四行 cd %~dp0\luajit-2.1.0b3\src 改成 cd %~dp0\luajit-2.1\src
2. 同样是上面那个脚本，第五行，call msvcbuild_mt.bat static 改成 call msvcbuild.bat static
3. 修改 build/CMakeLists.txt，大概42行左右， set(LUAJIT_SRC_PATH luajit-2.1.0b3/src) 改成 set(LUAJIT_SRC_PATH luajit-2.1/src)

如果是 android版本，不需要改上面的 1，2两步，但是 CMakeLists.txt 要改。另外修改对应脚本内容
比如执行 make_android_luajit_arm64.sh
修改其中第六行 SRCDIR=$DIR/luajit-2.1.0b3 改成 SRCDIR=$DIR/luajit-2.1

修改完运行即可。不过在windows上，用最新的luajit会报错，还是用luajit-2.1.0b3比较稳定。
但是在 android 上需要用最新的 luajit2.1才行，不然lua-protobuf 会报错.


## 同步xLua
xLua 原项目 https://github.com/Tencent/xLua
将 xLua 项目中的内容同步到 LibsTestProj 下面对应的地方

## 同步 lua-protobuf
lua-protobuf 原项目 https://github.com/starwing/lua-protobuf.git

## 在Ubuntu22.04上生成 Android
1. 需要手动安装 libncurses5，因为22.04默认的是 libncurses6. --- sudo apt install libncurses5
2. 生成 luajit 版本时使用脚本 make_android_luajit_arm64.sh。需要安装 gcc 的 multilib 库。 sudo apt install gcc-multilib