## Pre-requisities
    Ubertooth-One USB (Hardware)
    Unix-based OS (tested on Ubuntu 18.04)
    Ubertooth tools (setup described below)

# Ubertooth Tools
Build Guide from GreatScottGadgets focusing on other OS setups: 
(https://github.com/greatscottgadgets/ubertooth/wiki/Build-Guide)

## Step 1: Install nescessay libraries

```sudo apt-get install cmake libusb-1.0-0-dev make gcc g++ libbluetooth-dev \pkg-config libpcap-dev python-numpy python-pyside python-qt4```

## Step 2: libbtbb

```cd /opt && wget https://github.com/greatscottgadgets/libbtbb/archive/2018-12-R1.tar.gz -O libbtbb-2018-12-R1.tar.gz && tar xf libbtbb-2018-12-R1.tar.gz && cd libbtbb-2018-12-R1 && mkdir build && cd build && cmake .. && make && sudo make install```

## Step 3: Ubertooth

```cd /opt && wget https://github.com/greatscottgadgets/ubertooth/releases/download/2018-12-R1/ubertooth-2018-12-R1.tar.xz -O ubertooth-2018-12-R1.tar.xz && tar xf ubertooth-2018-12-R1.tar.xz && cd ubertooth-2018-12-R1/host && mkdir build && cd build && cmake .. && make && sudo make install && sudo ldconfig```

## Step 4: Kismet

```cd /opt && sudo apt-get install libpcap0.8-dev libcap-dev pkg-config build-essential libnl-3-dev libncurses5-dev libpcre3-dev libpcap-dev libcap-dev && wget https://kismetwireless.net/code/kismet-2013-03-R1b.tar.xz  && tar xf kismet-2013-03-R1b.tar.xz && cd kismet-2013-03-R1b && ln -s ../ubertooth-2018-12-R1/host/kismet/plugin-ubertooth . && ./configure && make && make plugins && sudo make suidinstall && sudo make plugins-install && sed -i 's/logtypes=pcapdump,gpsxml,netxml,nettxt,alert/logtypes=pcapdump,gpsxml,netxml,nettxt,alert,pcapbtbb,pcapng/g' /usr/local/etc/kismet.conf```

## Step 5: Wireshark

```apt-get install wireshark-dev libwireshark-dev && cd /opt/libbtbb-2018-12-R1/wireshark/plugins/btbb && mkdir build && cd build && cmake -DCMAKE_INSTALL_LIBDIR=/usr/lib/x86_64-linux-gnu/wireshark/libwireshark3/plugins .. && make && sudo make install```

```cd /opt/libbtbb-2018-12-R1/wireshark/plugins/btbredr && mkdir build && cd build && cmake -DCMAKE_INSTALL_LIBDIR=/usr/lib/x86_64-linux-gnu/wireshark/libwireshark3/plugins .. && make && sudo make install```


