# usb-i2c-adapters

Ubuntu version: Ubuntu 22.04.4 LTS

Kernel version: 6.8.0-52-generic

## Chip: Silicon Labs CP2112

Board: Search Amazon for this description:
"WWZMDiB CP2112 Adapter Micro USB to SMBus I2C Communication with Wires"

![cp2112 board front](cp2112-board-photo.jpg)
![cp2112 board back](cp2112-board-back.jpg)

Pull ups: 4.7K on SDA and SCL on the board

Voltage: 3.3 V, but board also supports 1.8V: Move 0-ohm jumper from R2 to
R1.

Driver: it's built into Linux

SCL frequency: 100 KHz only (driver doesn't seem to support changing it)

Performance:

Write: 1379 BPS with 29 byte packets

Read: 4433 BPS

Waveforms:

Five byte write:

![cp2112-write.png](cp2112-write.png)

Zoomed in, you can see the 100 MHz:

![cp2112-write-zoomed.png](cp2112-write-zoomed.png)

Note the large gap between bytes:

![cp2112-write-byte-gap.png](cp2112-write-byte-gap.png)

Five byte read:

![cp2112-read.png](cp2112-read.png)

Note repeated start:

![cp2112-repeated.png](cp2112-repeated.png)



dmesg on insertion:

~~~
[794148.928023] usb 3-7: New USB device found, idVendor=10c4, idProduct=ea90, bcdDevice= 0.00
[794148.928044] usb 3-7: New USB device strings: Mfr=1, Product=2, SerialNumber=3
[794148.928050] usb 3-7: Product: CP2112 HID USB-to-SMBus Bridge
[794148.928054] usb 3-7: Manufacturer: Silicon Laboratories
[794148.928057] usb 3-7: SerialNumber: 0057463B
[794148.932925] cp2112 0003:10C4:EA90.0019: hidraw0: USB HID v1.01 Device [Silicon Laboratories CP2112 HID USB-to-SMBus Bridge] on usb-0000:00:14.0-7/input0
[794148.984858] cp2112 0003:10C4:EA90.0019: Part Number: 0x0C Device Version: 0x02
~~~

i2cdetect -l:

~~~
i2c-16	unknown   	CP2112 SMBus Bridge on hidraw0  	N/A
~~~

lsmod:

~~~
hid_cp2112             40960  0
~~~

## Silicon Labs CP2112







		Write BPS	Size		Read BPS
		---------			--------

cp2112				40		4433
		X		30
		1379		29
		1262		24
		1331		20
		1229		16
		1139		8
		796		4



ft260				40		4426
		X		29
		1398		28		4196
		1410		24		3559
		1426		20
		1427		16		3014
		1328		8
		1323		4		1323


ch341						15725
Missing PUPs?
