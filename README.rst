Python library for Raspberry Pi and SDD1306 connected via I2C/SPI
--------------------------------------------------------------------------------------------
- Forked from rm-hull/luma.oled <https://github.com/rm-hull/luma.oled> .
- Examples of Japanese font "misaki font" for OLED Display (1.3 inch / 128 x 64) included.
- Luma's work is highly versatile. Python 2 or 3, I2C or SPI, Raspberry Pi or Linux-based SBC.
- Read the great document at https://ssd1306.readthedocs.io/en/ 


Installation
^^^^^^^^^^^^
::

    sudo apt-get install libjpeg62-turbo-dev libjpeg-dev
    sudo -H pip3 install --upgrade luma.oled


Nice Japanese font - misaki font and installation
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
misaki font is 8 x 8 Truetype font in almost in 7 x 7 area so that it has high readability in small space.
http://littlelimit.net/misaki.htm

::

    cd luma.examples/examples
    mkdir misakifont
    cd misakifont
    wget http://littlelimit.net/arc/misaki/misaki_ttf_2019-02-03a.zip
    unzip misaki_ttf_2019-02-03a.zip


Test drive from luma.examples
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
::

    git clone https://github.com/Naohiro2g/luma.examples.git
    cd luma.examples/examples

    # misaki font
    python3 crawl-misaki.py --interface spi  # for SPI connection
    python3 crawl-misaki.py                  # for I2C connection

    # moving cube in 3D
    python3 3d_box.py --interface spi
    # space invaders!
    python3 invaders.py --interface spi
    # bouncing balls with FPS
    python3 bounce.py --interface spi
    
    # bench marking     approx. 80FPS
    python3 perfloop.py --interface spi
    # see https://github.com/rm-hull/luma.oled/wiki/Usage-&-Benchmarking#096-spi-oled---ssd1306


SPI connection to my display module (VCC and GND was reversed !)
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
`*`: exchangeable with any GPIO pins by command-line options below::

    --bcm-reset 20
    --bcm-data-command 21

Modified from [Hardware](https://github.com/Naohiro2g/luma.oled/blob/master/doc/hardware.rst)

Wiring to Rpi Pins
^^^^^^^^^^^^^^^^^^

======= ===== ===== ======= 
Left    BCM   BCM   Right
======= ===== ===== =======
Red     3.3   24    Blue
Yellow  10    GND   Brown
`---`   9     25    Green
Orange  11    8     Purple
======= ===== ===== =======



I2C connection
^^^^^^^^^^^^^^

========== ====== ============ ====================
OLED Pin   Name   Remarks      RPi Function
========== ====== ============ ====================
4 Yellow   SDA    Data         GPIO 2 (SDA)
3 Orange   SCL    Clock        GPIO 3 (SCL)
2 Red      VCC    +3.3V Power  3V3
1 Brown    GND    Ground       GND
========== ====== ============ ====================




Original README
^^^^^^^^^^^^^^^

`luma.core <https://github.com/rm-hull/luma.core>`__ **|** 
`luma.docs <https://github.com/rm-hull/luma.docs>`__ **|** 
`luma.emulator <https://github.com/rm-hull/luma.emulator>`__ **|** 
`luma.examples <https://github.com/rm-hull/luma.examples>`__ **|** 
`luma.lcd <https://github.com/rm-hull/luma.lcd>`__ **|** 
`luma.led_matrix <https://github.com/rm-hull/luma.led_matrix>`__ **|** 
luma.oled

Luma.OLED
---------
**Display drivers for SSD1306 / SSD1309 / SSD1322 / SSD1325 / SSD1327 / SSD1331 / SSD1351 / SH1106**

.. image:: https://travis-ci.org/rm-hull/luma.oled.svg?branch=master
   :target: https://travis-ci.org/rm-hull/luma.oled

.. image:: https://coveralls.io/repos/github/rm-hull/luma.oled/badge.svg?branch=master
   :target: https://coveralls.io/github/rm-hull/luma.oled?branch=master

.. image:: https://readthedocs.org/projects/luma-oled/badge/?version=latest
   :target: http://luma-oled.readthedocs.io/en/latest/?badge=latest

.. image:: https://img.shields.io/pypi/pyversions/luma.oled.svg
   :target: https://pypi.python.org/pypi/luma.oled

.. image:: https://img.shields.io/pypi/v/luma.oled.svg
   :target: https://pypi.python.org/pypi/luma.oled

.. image:: https://img.shields.io/maintenance/yes/2019.svg?maxAge=2592000

Python library interfacing OLED matrix displays with the SSD1306, SSD1309,
SSD1322, SSD1325, SSD1327, SSD1331, SSD1351 or SH1106 driver using I2C/SPI on
the Raspberry Pi and other linux-based single-board computers - it provides a
Pillow-compatible drawing canvas, and other functionality to support:

* scrolling/panning capability,
* terminal-style printing,
* state management,
* color/greyscale (where supported),
* dithering to monochrome

Documentation
-------------
Full documentation with installation instructions and examples can be found on
https://luma-oled.readthedocs.io.

A list of tested devices can be found in the
`wiki <https://github.com/rm-hull/luma.oled/wiki/Usage-&-Benchmarking>`_.

The display pictured below is a SSD1306 (128 x 64 pixels), and the board is `tiny` enough to fit
inside the RPi case.

.. image:: https://raw.githubusercontent.com/rm-hull/luma.oled/master/doc/images/mounted_display.jpg
   :alt: mounted

.. image:: https://raw.githubusercontent.com/rm-hull/luma.oled/master/doc/images/ssd1322.jpg
   :alt: ssd1322

As well as display drivers for various physical OLED devices, there are
emulators that run in real-time (with pygame) and others that can take
screenshots, or assemble animated GIFs, as per the examples below (source code
for these is available in the `luma.examples <https://github.com/rm-hull/luma.examples>`_ 
git repository:

.. image:: https://raw.githubusercontent.com/rm-hull/luma.oled/master/doc/images/clock_anim.gif?raw=true
   :alt: clock

.. image:: https://raw.githubusercontent.com/rm-hull/luma.oled/master/doc/images/invaders_anim.gif?raw=true
   :alt: invaders

.. image:: https://raw.githubusercontent.com/rm-hull/luma.oled/master/doc/images/crawl_anim.gif?raw=true
   :alt: crawl

Breaking changes
----------------
Version 2.0.0 was released on 11 January 2017: this came with a rename of the
github project from **ssd1306** to **luma.oled** to reflect the changing nature
of the codebase.

Some core functionality has been moved out to another git repository,
`luma.core <https://github.com/rm-hull/luma.core>`_: this has enabled
another project to have a facelift: **pcd8544** has now been reborn as
`luma.lcd <https://github.com/rm-hull/luma.lcd>`_: the same API can now be
used across both projects. Likewise **max7219** has been renamed to
`luma.led_matrix <https://github.com/rm-hull/luma.led_matrix>`_ so
it can also take advantage of the common API.

The consequence is that any existing code that uses the old **ssd1306** package
will need to be updated. The changes should be limited to altering import
statements only, and are described in the 
`upgrade documentation <https://luma-oled.readthedocs.io/en/latest/upgrade.html>`_.

License
-------
The MIT License (MIT)

Copyright (c) 2014-18 Richard Hull and contributors

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
