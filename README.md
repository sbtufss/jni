jni 生成的so文件在jni/app/build/intermediates/cmake/debug/obj这个目录下面，而我们开发jni主要的步骤就是两步
第一步：首先创建工程的时候让他支持c++,他会自动生成一个jni demo
第二步：了解jni/app/CMakeLists.txt文件，他是配置jni的，其中
add_library( # Sets the name of the library.
             other-lib          //so的文件名

             # Sets the library as a shared library.
             SHARED

             # Provides a relative path to your source file(s).
             src/main/cpp/other-lib.c
             src/main/cpp/my-lib.c)
就是酱other.c和my-lib.c编译到other-lib里面,可以添加多个library(分开写)，也可以将多个c文件写到一起，然后这个是编译，接下来这个是将java关联起来的
target_link_libraries( # Specifies the target library.
                       other-lib    //关联的so文件

                       # Links the target library to the log library
                       # included in the NDK.
                       ${log-lib} )
有多少个so文件就在这里写上多少个，就像上面的，我们值add一个library，那我们只关联一个library

然后我们引入so文件
static {
        System.loadLibrary("other-lib");//other-lib就是so文件名
    }
声明方法
public native String sayHelloFromJNI();然后在按快捷键alt+回车键酒会自动的在other-lib.c里面自动的生成方法,前提下必须创建好other-lib.c文件
文件目录在jni/app/src/main/cpp/other-lib.c
