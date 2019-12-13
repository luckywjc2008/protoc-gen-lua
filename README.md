# protoc-gen-lua
forked from https://github.com/topameng/protoc-gen-lua
protoc-gen-lua

**默认放在C盘目录C:\protoc-gen-lua-master\protoc-gen-lua-master， 生成lua放在 protoc-gen-lua\example\Lua\Protol 目录

修改说明：

替换了protoc-gen-lua\protobuf下的编译lua源码

支持嵌套类（必需在使用类之前声明）
支持int64, uint64 
解包的协议对象支持 tostring 操作 

操作说明
将protoc-gen-lua\protobuf里的lua源码放到工程目录
通过protoc-gen-lua\example\make_proto.bat生成*proto.lua

编译环境: 
Python2.7.8
https://www.python.org/downloads/release/python-278/
protobuf-2.5.0目录是编译好的protobuf2.5.0

注意:
嵌套的proto 必须在当前 proto 之前声明
安装python后, 需要在protobuf2.5 的python 目录下执行命令 Python setup.py install 
**
Google's Protocol Buffers project, ported to Lua

"Protocol Buffers" is a binary serialization format and technology, released to the open source community by Google in 2008.

There are various implementations of Protocol Buffers and this is for Lua.

Install

Install python runtime and the protobuf 2.3 for python.

checkout the code.

Compile the C code:

$cd protobuf && make

Make a link to protoc-gen-lua in your $PATH:

$cd /usr/local/bin && sudo ln -s /path/to/protoc-gen-lua/plugin/protoc-gen-lua

Then you can compile the .proto like this:

protoc --lua_out=./ foo.proto

Quick Example

You write a .proto file like this:

person.proto :

  message Person {
    required int32 id = 1;
    required string name = 2;
    optional string email = 3;
  }
Then you compile it.

Then, make sure that protobuf/ in package.cpath and package.path, you use that code like this:

require "person_pb"

-- Serialize Example
local msg = person_pb.Person()
msg.id = 100
msg.name = "foo"
msg.email = "bar"
local pb_data = msg:SerializeToString()

-- Parse Example
local msg = person_pb.Person()
msg:ParseFromString(pb_data)
print(msg.id, msg.name, msg.email)
The API of this library is similar the protobuf library for python. For a more complete example, read the python documentation.
