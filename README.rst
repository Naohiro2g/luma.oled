Read the great document at https://ssd1306.readthedocs.io/en/latest/

Installation
^^^^^^^^^^^^
::

    sudo apt-get install libjpeg62-turbo-dev libjpeg-dev
    sudo -H pip3 install --upgrade luma.oled


8x8 Japanese font - misaki font
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

http://littlelimit.net/misaki.htm

Font installation
^^^^^^^^^^^^^^^^^
::

    cd luma.examples/examples
    mkdir misakifont
    cd misakifont
    wget http://littlelimit.net/arc/misaki/misaki_ttf_2019-02-03a.zip
    unzip misaki_ttf_2019-02-03a.zip


Test drive
^^^^^^^^^^
::

    git clone https://github.com/Naohiro2g/luma.examples.git
    cd luma.examples/examples
    
    # misaki font
    python3 crawl-misaki.py --interface spi
    # moving cube in 3D
    python3 3d_box.py --interface spi
    # space invaders!
    python3 invaders.py --interface spi
    # bouncing balls with FPS
    python3 bounce.py --interface spi
    
    # bench marking     approx. 80FPS
    python3 perfloop.py --interface spi
    # see https://github.com/rm-hull/luma.oled/wiki/Usage-&-Benchmarking#096-spi-oled---ssd1306


SPI connection of my display module (VCC and GND was reversed !)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

========== ====== ============ ====================
OLED Pin   Name   Remarks      RPi Function
========== ====== ============ ====================
1 Brown    GND    Ground       GND
2 Red      VCC    +3.3V Power  3V3
3 Orange   D0     Clock        GPIO 11 (SCLK)
4 Yellow   D1     MOSI         GPIO 10 (MOSI)
5 Green    RST    Reset        GPIO 25 (*)
6 Blue     DC     Data/Command GPIO 24 (*)
7 Purple   CS     Chip Select  GPIO 8 (CE0)
========== ====== ============ ====================

*: exchangeable
Modified from [Hardware](https://github.com/Naohiro2g/luma.oled/blob/master/doc/hardware.rst)

Wiring to Rpi Pins
^^^^^^^^^^^^^^^^^^

======= ===== ===== ======= 
Left    BCM   BCM   Right
======= ===== ===== =======
Red     3.3   24    Blue
Yellow  10    GND   Brown
----    9     25    Green
Orange  11    8     Purple
======= ===== ===== =======


Original README
^^^^^^^^^^^^^^^
