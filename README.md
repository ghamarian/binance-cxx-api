## Binance C++ API

Library for accessing Binance Bincoin Exchange using web sockets and JSON.

This version is derived from https://github.com/binance-exchange/binacpp with slight fixes:

 * Corrected enless recursion in `BinaCPP::to_string`
 * Commented out flags no longer supported by modern versions of web sockets
 * CMake build system

### Prerequisites

```
sudo apt-get install libjsoncpp-dev libcurl4-nss-dev libwebsockets-dev
```

### Building

```
git clone https://github.com/dmikushin/binance-cxx-api.git
cd binance-cxx-api
mkdir build
cd build/
cmake ..
./example
```
