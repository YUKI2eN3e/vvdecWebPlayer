# VVdeC Web Player

This project only contains the JavaScript and HTML code to build a minimal WebAssembly based VVC
Player for the web using the [VVdeC](https://github.com/fraunhoferhhi/vvdec) library. It can play
raw VVC bitstreams or MP4 files. There is no audio support, since this sample code is primarily
focused on the feasibility of decoding VVC in the browser.

The compiled VVdeC WebAssembly binary and emscripten support code are not included in this
repository, but need to be built separately and copied into the `bin/` folder.

## Usage

### Build WebAssembly

You need to build the VVdeC WebAssembly binary first. [Emscripten SDK](https://emscripten.org/) and
[CMake](http://www.cmake.org/) should be installed at this point and included in the search PATH.

Clone the VVdeC repository from https://github.com/fraunhoferhhi/vvdec. Within the vvdec directory
run:

    emcmake cmake -B build/wasm
    cmake --build build/wasm

Copy the resulting files `vvdecapp.wasm`, `vvdecapp.worker.js`, and `vvdecapp.js` from
`bin/release-static` to the `bin/` folder in this repository.

### Deploy to Webserver

Edit the `bitstreams.json` file to include the VVC files you want to play and place them below this
directory. The files can either be raw bitstreams or packaged as MP4-files.

For testing purposes a tiny script to run a Python webserver is included. Just run
`wasm_test-server.py` using Python 3 from the current directory. This starts a very simple webserver
listening on localhost port 8000. Open https://localhost:8000/ in your webrowser.

You can also deploy the player to any standard webserver. The following HTTP headers need to be set
for WebAssembly to work:

    Cross-Origin-Embedder-Policy: require-corp
    Cross-Origin-Opener-Policy: same-origin

Also, the site must be accessed using HTTPS, if not running on localhost.

## Limitations

* The player currently does not have support for playing audio.
* Performance depends on the browser and platform. At the time of writing Chrome and Edge work best.
* Safari currently does not provide multithreading support for WebAssembly (Oct. 2021).
* (UHD decoding works in principle using VVdeC > 1.3.0, but is probably too slow for practical
  purposes.)

## License

Please see [LICENSE](./LICENSE) file for the terms of use of the contents of this repository.

For more information, please contact: vvc@hhi.fraunhofer.de

**Copyright (c) 2021 Fraunhofer-Gesellschaft zur Förderung der angewandten Forschung e.V.**

**All rights reserved.**
