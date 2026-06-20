cmake_minimum_required(VERSION 3.16)
project(GoldenRatioFHE VERSION 1.0.0 LANGUAGES CXX)
set(CMAKE_CXX_STANDARD 17)

find_package(OpenSSL REQUIRED)
find_package(PkgConfig REQUIRED)
pkg_check_modules(OQS liboqs)

include_directories(${CMAKE_SOURCE_DIR}/include)

# Φ-Fractal Engine
add_executable(phi_fractal engines/phi-fractal/fractal_engine.cpp)
target_link_libraries(phi_fractal OpenSSL::SSL OpenSSL::Crypto)

# Φ-FHE V.10 (SEAL + OpenFHE + Liquid PQC + Fractal)
add_executable(fhe_v10 engines/fhe_v10.cpp)
target_link_libraries(fhe_v10 OpenSSL::SSL OpenSSL::Crypto ${OQS_LIBRARIES} dl)

# SpiralDB
add_executable(spiral_db gateway/spiral-db/spiral_db.cpp)
target_link_libraries(spiral_db OpenSSL::SSL OpenSSL::Crypto)
