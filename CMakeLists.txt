cmake_minimum_required(VERSION 3.12)
project(oks VERSION 0.0.0)

find_package(daq-cmake REQUIRED)

daq_setup_environment()

find_package(Boost COMPONENTS thread date_time regex program_options REQUIRED)
find_package(config REQUIRED)
find_package(ers REQUIRED)
find_package(logging REQUIRED)
find_package(system REQUIRED)

# JCF, Oct-18-2022: stripped out functionality which requires authentication packages daq_tokens and pam
daq_add_library( *.cpp LINK_LIBRARIES ers::ers Boost::thread Boost::date_time Boost::regex stdc++fs system::system logging::logging config::config)

daq_add_application(oks_dump oks_dump.cxx LINK_LIBRARIES oks)
daq_add_application(oks_git_repository oks_git_repository.cxx LINK_LIBRARIES oks)
daq_add_application(oks_clone_repository oks_clone_repository.cxx LINK_LIBRARIES oks Boost::program_options)
daq_add_application(oks_validate_repository oks_validate_repository.cxx LINK_LIBRARIES oks Boost::program_options)

daq_install()
