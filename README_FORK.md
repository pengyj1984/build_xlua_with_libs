同步原项目
=====

## build注意事项
生成windows相关库的时候，注意检查下 vs 的工具路径，可能需要修改。

## 从原项目合并
从主页 clone 到本地之后，可以通过 git remote -v 查看远程分支。默认应该只有自己的分支。
输入指令 git remote add upstream https://github.com/chexiongsheng/build_xlua_with_libs 建立与原项目的关联。
此时再输入指令 git remote -v 查看应该会多出两条记录。
通过指令 git pull upstream master 即可实现同步原项目的代码，再 push 到自己的项目即可。


## 同步xLua
xLua 原项目 https://github.com/Tencent/xLua
将 xLua 项目中的内容同步到 LibsTestProj 下面对应的地方

## 同步 lua-protobuf
lua-protobuf 原项目 https://github.com/starwing/lua-protobuf.git