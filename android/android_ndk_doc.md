[TOC]

# 一．Android.mk文件可设置属性如下

　　在执行**ndk-build**命令时，会在当前上下文检索Android.mk文件并根据文件中的属性声明进行编译。

    说明：
    1. 赋值符号　　　 　 :=
    2. 追加赋值符号    　+=
    3. 引用已定义的值    $()

## 1 . LOCAL_PATH := $(call my-dir)

　　该语句必须写在每个 **Android.mk** 的第一行， **LOCAL_PATH** 的值为当前 **Android.mk** 文件的目录路径。在接下来的属性设置中，对于文件的使用和检索都是基于当前目录路径来进行的。

　　其中的宏 **my-dir** 由 **Build System** 提供，返回的是最近一次include的Makefile的路径。所以在Include其它Makefile后，再调用 **$(call my-dir)** 会返回其它 **Android.mk** 所在路径。

类似的宏定义还有：

    1. all-subdir-makefiles：用例　$(call all-subdir-makefiles) ，返回一个列表，包含 my-dir 中所有子目录中的 Android.mk。
    2. this-makefile：当前 Makefile 的路径。
    3. parent-makefile：返回 include tree 中父 Makefile 路径。 也就是 include 当前 Makefile 的 Makefile Path。
    4. import-module：允许寻找并 import 其它 modules 到本 Android.mk 中来。它会从 NDK_MODULE_PATH 寻找指定的模块名。用例：
     $(call import-add-path,$(LOCAL_PATH)) //添加外部导入库目录
     $(call import-module,platform/third_party/android/prebuilt/libjpeg)//添加导入库（基于上一行添加的导入库目录）
    5. $(TARGET_ARCH_ABI)：这个宏定义表示编译时对应的目标内核平台(如arm,armeabi-v7a,x86等)

## 2 . include $(CLEAR_VARS)

　　**CLEAR_VARS** 变量由 **Build System** 提供。并指向一个指定的GNU Makefile（编译脚本），由它负责清理很多 **LOCAL_xxx**.

　　例如：**LOCAL_MODULE, LOCAL_SRC_FILES, LOCAL_STATIC_LIBRARIES** 等等。但不清理 **LOCAL_PATH**.

　　这个清理动作是必须的，因为所有的编译控制文件由同一个GNU Make解析和执行，其变量是全局的。所以清理后才能避免相互影响。

## 3 . include $(call all-subdir-makefiles)

　　返回一个列表，包含 **'my-dir'** 中所有子目录中的 **Android.mk** 文件，那么子目录当中的 **Android.mk** 文件也可以被NDK检索到，之后再依据子目录下的 **Android.mk** 文件进行编译。默认情况下只检索 **LOCAL_PATH** 下的 **Android.mk** 文件。

## 4 . LOCAL_MODULE := name

　　该属性设置了模块名称，实际生成的时候文件会以 **libname.so** 的文件名保存在 **libs** 目录下，**libs** 为默认保存目录。

　　注：文件名前面的 **“lib”** 是编译完成后自动添加的，实际使用时还是要用 **“name”**，如果文件命名时本身包含 **“lib”** 字符串，例如 **libname** ,则生成的库文件不会自动添加 **”lib“”** 前缀,也即不可能出现 **liblibname** 这种情况。实际在Java代码中，用:

**System.loadLibrary("name");**

时，一定注意不要加 **"lib"** 前缀，否则会读取库文件失败，即使命名时用了 **"lib"** 前缀。

## 5 . LOCAL_SRC_FILES := filepath or .so file

　　设置源码路径或者需要依赖的 **.so** 文件的路径。**ndk** 在编译时就会获取指定路径下的源码或者 **.so** 文件，这里如果指定的是 **.so** 文件，那么该文件会被复制到ndk编译过程中生成的 **"libs"** 目录下。如果指定的是源码，那么源码将会被打包成 **.so** 文件，并放到　**"libs"** 目录下。

## 6 . LOCAL_EXPORT_C_INCLUDES := filepath

　　该属性包含头文件路径，设置后可导出头文件给外部调用。比如在预编译第三方 **.so** 库时，需要保证该目录下有第三方 **.so** 库被外部调用的头文件。

## 7 . LOCAL_C_INCLUDES := filepath/include

　　该属性声明了当前工程下源代码（ **.c** 或者 **.cpp** 文件）的头文件路径，在编译时会根据这一组路径来查找头文件。

## 8 . LOCAL_LDLIBS := -llog -latomic -lz

　　该属性可以添加 **Android** 提供的静态库到当前库中，方便调用相应的方法。例如 **-llog** 就是 **Android** 提供的用于打印 **Log** 的工具库。

## 9 . LOCAL_SHARED_LIBRARIES := modulename

　　该属性声明了一个外部库列表，列表中的库作为依赖，用于依赖预编译的动态链接库（ **.so** 文件）。这里赋值需要用预编译的库的全名。

## 10 . LOCAL_STATIC_LIBRARIES:= modulename

　　与动态链接库的依赖相似，这里声明了要链接到本模块的静态库列表。

## 11 . LOCAL_WHOLE_STATIC_LIBRARIES:=

　　静态库全链接。 不同于LOCAL_STATIC_LIBRARIES，使用该方法链接的静态库不会被优化删减未被调用的代码或文件。

## 12 . include $(BUILD_SHARED_LIBRARY)

　　BUILD_SHARED_LIBRARY指向一个编译脚本。负责收集自从上次调用 **include $(CLEAR_VARS)** 后的所有 **LOCAL_XXX** 信息。并决定编译为什么。（预编译的源文件为库文件，可实现库文件的复用）

    BUILD_SHARED_LIBRARY：编译为动态链接库
    BUILD_STATIC_LIBRARY：编译为静态链接库
    PREBUILT_SHARED_LIBRARY：动态链接库预编译
    PREBUILT_STATIC_LIBRARY：静态链接库预编译

## 13 . LOCAL_CPPFLAGS := -fexceptions -frtti -fpermissive

　　该属性可以设置编译时的一些功能选项。适用于C++代码。这里的例子包括以下选项：

    -fexceptions：允许异常功能　
    -frtti：运行时类型识别
    -fpermissive：宽松的编译形式。

## 14 . LOCAL_CFLAGS := -frtti

　　该属性同 **LOCAL_CPPFLAGS** 类似，都是设置编译时的一些功能选项，但适用于C代码的编译。

## 15 . TARGET_ARCH :=　arm

　　声明目标CPU架构名。如果为　“arm” 则声称ARM兼容的指令。与CPU架构版本无关。

## 16 . TARGET_PLATFORM := android-15

　　目标 Android 平台的名字。

## 17 . TARGET_ARCH_ABI := armeabi

　　暂时只支持两个 value，armeabi 和 armeabi-v7a。

## 18 . TARGET_ABI :=

　　目标平台和 ABI 的组合。

## 19 . LOCAL_CPP_EXTENSION:=　.cxx .cpp .cc

　　指出C++源文件的扩展名。LOCAL_CPP_EXTENSION := .cxx .cpp .cc。用于不同的C++文件后缀。

## 20 . LOCAL_CPP_FEATURES:=　rtti exceptions

　　该变量用来指定C++代码所依赖的特殊C++特性。例如，如果要告诉编译器你的C++代码使用了RTTI（RunTime Type Information）：

    LOCAL_CPP_FEATURES := rtti

如果要指定你的C++代码使用了C++异常，则：

    LOCAL_CPP_FEATURES := exceptions

该变量可以同时指定多个特性。例如：    

    LOCAL_CPP_FEATURES := rtti features


## 21 . LOCAL_ALLOW_UNDEFINED_SYMBOLS:= false

　　缺省情况下，当生成库文件时，若遇到没有定义的引用会导致"undefined error"，若设置为true,可忽略这种错误，但并不推荐。

## 22 . LOCAL_ARM_MODE:= arm

　　缺省情况下，ARM目标代码被编译为thumb模式。每个指令16位。如果指定此变量为：arm。 则指令为32位。

## 23 . LOCAL_ARM_NEON:= false

　　设置为true时，会将浮点编译成neon指令。这会极大地加快浮点运算(前提是硬件支持)只有targeting 为 'armeabi-v7a'时才可以。   

## 24 . LOCAL_DISABLE_NO_EXECUTE:= false

　　Android NDK r4增加了对“NX bit“安全特性的支持。它是默认开启的，如果你确定自己不需要该特性，你可以将它关闭，即：

    LOCAL_DISABLE_NO_EXECUTE := true

## 25 . LOCAL_EXPORT_CFLAGS:=

　　定义这个变量用来记录C/C++编译器标志集合，并且会被添加到其他任何以LOCAL_STATIC_LIBRARIES和LOCAL_SHARED_LIBRARIES的模块的LOCAL_CFLAGS定义中         


# 二．Application.mk文件可设置属性如下

　　Application.mk其实是一个小型GNU Makefile片段

## 1 . APP_PLATFORM := android-16

　　目标Android平台的版本。

## 2 . APP_ABI := all

　　生成的动态库对应的处理器类型，如armeabi-v7a,x86,armeabi等。all表示所有处理器。

## 3 . APP_CPPFLAGS := -std=c++11

　　允许使用c++11的标准函数。

## 4 . APP_STL := gnustl_static

　　设置编译时使用的标准库,stlport_static  右边的值还可以换成下面几个：

    1.system : 使用默认最小的C++运行库，这样生成的应用体积小，内存占用小，但部分功能将无法支持。
    2.stlport_static : 使用STLport作为静态库，这项是Android开发网极力推荐的。
    3.stlport_shared : STLport 作为动态库，这个可能产生兼容性和部分低版本的Android固件，目前不推荐使用。
    4.gnustl_static  : 使用 GNU libstdc++ 作为静态库。

　　默认情况下STLPORT是不支持C++异常处理和RTTI，所以不要出现 -fexceptions 或 -frtti ，如果真的需要可以使用gnustl_static来支持标准C++的特性，但生成的文件体积会偏大，运行效率会低一些。
