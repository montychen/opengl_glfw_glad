CMAKE_MINIMUM_REQUIRED(VERSION 2.8) # cmake最低版本要求

PROJECT(study_opengl)    # 工程名 CppTemplate

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++17") # 添加c++17标准支持

SET(CMAKE_C_COMPILER "/usr/bin/gcc") # 默认c编译器
SET(CMAKE_CXX_COMPILER "/usr/bin/g++") # 默认c++编译器

SET(CMAKE_BUILD_TYPE "Debug")  # Debug模式 选项: Release Debug MinSizeRel RelWithDebInfo

SET(CMAKE_CXX_FLAGS_DEBUG "$ENV{CXXFLAGS} -O0 -Wall -g2 -ggdb")  # debug模式下 gdb相关选项
SET(CMAKE_CXX_FLAGS_RELEASE "$ENV{CXXFLAGS} -O3 -Wall") # release模式下 gdb相关选项

# set(CMAKE_VERBOSE_MAKEFILE ON) # 开启调试 出现问题时开启

# enable_testing() # 打开测试

add_definitions(-DDEBUG) # 相当于代码中 #define DEBUG

# add_subdirectory(test) # 添加test子目录

SET(EXECUTABLE_OUTPUT_PATH "${PROJECT_SOURCE_DIR}/bin") # 可执行文件输出目录
INCLUDE_DIRECTORIES("${PROJECT_SOURCE_DIR}/include") # 头文件包含目录

INCLUDE_DIRECTORIES("/usr/local/include")   # 用brew 安装软件，头文件都放在这个目录。
LINK_LIBRARIES("/usr/local/lib/libglfw.dylib")  # 用brew安安装软件，库文件都放在这里
LINK_LIBRARIES("/usr/local/lib/libsoil2-debug.a")    # 下一步生成的 SOIL2 库文件。





# 这段代码可以区分操作系统
MESSAGE("Identifying the OS...")
if(WIN32)
  MESSAGE("This is Windows.")
elseif(APPLE)
  MESSAGE("This is MacOS.")
elseif(UNIX)
  MESSAGE("This is Linux.")
endif()
# 这段代码可以区分操作系统

AUX_SOURCE_DIRECTORY(src DIR_SRCS) # 添加源代码文件夹, 自动扫描所有文件

add_executable(dj_opengl# 输出的可执行文件名
   ${DIR_SRCS}
)
# 也可以这么写
# add_executable(chess  # 输出名为chess的可执行文件
#    ./src/main.cpp
#    ./src/utils.cpp
# )
