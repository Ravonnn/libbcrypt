cmake_minimum_required(VERSION 3.28)

project(bcrypt)

enable_language(ASM)

# just doing cmake . will build a shared or static lib and honor existing environment setting
# to force build static, cmake . -DBUILD_SHARED_LIBS=Off
# to force build shared, cmake . -DBUILD_SHARED_LIBS=On

if (NOT BUILD_SHARED_LIBS)
	message ("Building a static library")
else ()
	message ("Building a shared library")
endif ()


set( CMAKE_ASM_FLAGS "${CXXFLAGS} -x assembler-with-cpp")

add_library(bcrypt STATIC
		src/crypt_blowfish.c
		src/crypt_gensalt.c
		src/wrapper.c
		src/bcrypt.c
		src/x86.S
)

target_include_directories(bcrypt PUBLIC ${CMAKE_SOURCE_DIR}/include)
