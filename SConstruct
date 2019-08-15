#!/search/odin/oyc/anaconda3/bin/python

import os

env = Environment()

root_path = os.getcwd()

env.Append(CPPPATH = [root_path,
        '/search/odin/zhangjun/tools/brpc/include',
	'/search/odin/zhangjun/tools/protobuf-3.7.1/include',
        ])
env.Append(LIBPATH = [
	'/search/odin/zhangjun/tools/brpc/lib',
	'/search/odin/zhangjun/tools/protobuf-3.7.1/lib',
	])

env.Append(LIBS = ['brpc'])
env.Append(LIBS = ['protobuf'])
#env.Append(LIBS = ['tcmalloc_and_profiler'])

env.Append(RPATH = [
	'/search/odin/zhangjun/tools/brpc/lib',
	'/search/odin/zhangjun/tools/protobuf-3.7.1/lib',
	])

#env.Append(CCFLAGS = ['-Wall', '-O2', '-std=c++11', '-g'])
#env.Append(CCFLAGS = ['-O2', '-std=c++11', '-g', '-DUSE_RTTI=1'])
env.Append(CCFLAGS = ['-O2', '-std=c++11', '-g', '-Wl,-Bstatic', '-DGFLAGS_NS=gflags'])
# -DBRPC_WITH_GLOG=0 
# -DNDEBUG -O2 -D__const__= -pipe -W -Wall -Wno-unused-parameter -fPIC -fno-omit-frame-pointer
#env.Append(LINKLAGS = ['-static'])


# https://github.com/SCons/scons/wiki/ProtocBuilder
protoc = Builder(action="protoc --cpp_out=. $SOURCE")
env2 = Environment(
        ENV = {'PATH': os.environ['PATH']},
        BUILDERS={'Protoc':protoc})
env2.Protoc("data.pb.cc data.pb.h".split(), "data.proto")

env.Program(
    target = "server",
    source = [
        "main.cc",
        "data.pb.cc",
        "engine.cc",
        "service.cc",
        "engine_manager.cc",
        "channel.cc",
    ],
)


#env.Program(
#    target = "client",
#    source = [
#        "client.cpp",
#        "echo.pb.cc",
#    ],
#)
