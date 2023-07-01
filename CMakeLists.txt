cmake_minimum_required(VERSION 3.20)

set(NAME mpfr)
set(VERSION 4.2.0)

project(cmeel-${NAME} VERSION ${VERSION})

include(FindPkgConfig)
pkg_check_modules(GMP gmp)

include(ExternalProject)
ExternalProject_Add(
  ${NAME}
  URL "https://www.mpfr.org/mpfr-current/${NAME}-${VERSION}.tar.xz"
      DOWNLOAD_EXTRACT_TIMESTAMP OFF
  BUILD_IN_SOURCE ON
  CONFIGURE_COMMAND "./configure" "--prefix=${CMAKE_INSTALL_PREFIX}"
                    "--with-gmp=${GMP_PREFIX}"
  BUILD_COMMAND "make"
  TEST_COMMAND "make" "check"
  INSTALL_COMMAND "make" "install")

# dummy file for install target
install(FILES README.md DESTINATION share/cmeel-${NAME}/)
