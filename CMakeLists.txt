cmake_minimum_required(VERSION 3.12.0)
if(NOT PROOF_FULL_BUILD)
    list(APPEND CMAKE_MODULE_PATH "${CMAKE_INSTALL_PREFIX}/lib/cmake/modules")
    include(ProofInternal)
endif()

project(ProofSeed VERSION ${PROOF_VERSION} LANGUAGES CXX)

find_package(Qt5Core CONFIG REQUIRED)
if(NOT PROOF_FULL_BUILD)
    proof_init()
    find_package(proof-gtest CONFIG REQUIRED)
    enable_testing()
endif()

add_subdirectory(3rdparty/optional)

proof_add_target_sources(Seed
    src/proofseed/future.cpp
    src/proofseed/spinlock.cpp
    src/proofseed/tasks.cpp
)

proof_add_target_headers(Seed
    include/proofseed/planting.h
    include/proofseed/proofalgorithms.h
    include/proofseed/future.h
    include/proofseed/proofseed_global.h
    include/proofseed/spinlock.h
    include/proofseed/tasks.h
    include/proofseed/helpers/prooftypetraits.h
    include/proofseed/helpers/tuplemaker.h
)

proof_add_module(Seed
    QT_LIBS Core
    OTHER_LIBS optional
)

add_subdirectory(tests/proofseed)

