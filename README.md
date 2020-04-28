gr-hpsdr
========

gnuradio 3.8 modules for OpenHPSDR Hermes / Metis and Red Pitaya using the OpenHpsdr protocol.   July 2017

* hermesNB  sources decimated downconverted 48K-to-384K receiver complex stream(s), and sinks one 48k sample rate transmit complex stream.
* hermesWB  sources raw ADC samples as a vector of floats, with vlen=16384. Each individual vector contains time contiguous samples. However there are large time gaps between between vectors. This is how HPSDR produces raw samples, it is due to Ethernet interface rate limitations between HPSDR and the host computer.

The modules are compatible with version 3.8.x of gnuradio and Hermes firmware version 1.8 through 3.2 (known as OpenHPSDR
protocol 1). It is not compatible with the new OpenHPSDR protocol 2.

Updated to increase the maximum number of receivers to 7.  Hermes only supports 4 receivers due to limited FPGA capacity. Red Pitaya with the OpenHPSDR protocol supports 6 receivers.  Note that beyond 4 receivers and 384k sample rate exceeds 100 Mb/s Ethernet interface capacity.

If no Alex module is present (just Hermes/Metis) then the Alex control fields will have no effect, and the Verbose mode will produce nonsense for Fwd and Rev power measurements, but valid Hermes FPGA revision string.

It is sometimes necessary to delete all files inside the build subdirectory before re-running cmake.

To build:
---------

    mkdir build 
    cd build 
    cmake ..
    make 
    sudo make install 
    sudo ldconfig 

Note: the build configuration writes files to locations prefixed with  /usr/local  which is appropriate for gnuradio that has been installed and built from source. If gnuradio was installed from a binary (for example using apt-get) it may expect Out-Of-Tree modules to be installed in a different location. If so the cmake command may need to be modified to change the desired installation path:

    cmake .. -DCMAKE_INSTALL_PREFIX=/the-prefix-to-utilize


Release Tags:
-------------

* v1.0 - An older version provided for backwards compatibility (for gnuradio 3.7.2 to 3.7.9, and Ubuntu 14.04).
* v1.1 - Supports 1 or 2 receivers, gnuradio 3.7.10 and later, and Ubuntu 16.04. The buffer handling in this version is more efficient than v1.2 and later, but that may not be important in your application.
* v1.2 - Supports 1 to 7 receivers. Your actual hardware likely supports fewer than 7 receivers. Hermes supports 4, Red Pitaya 6. More than 4 receivers / 384k requires the use of gigabit Ethernet.


