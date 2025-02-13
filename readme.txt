For RW61x -
1. FW image names:
	Production FW, for users:
		rw61x_sb_wifi_a2.bin, for CPU1_wifi of redfinch A2 board
		rw61x_sb_ble_a2.bin, for CPU2_ble of redfinch A2 board
		rw61x_sb_ble_15d4_combo_a2.bin, for CPU2 ble_15d4 combo of redfinch A2 board

2. where to get FW image:
	In the directory:  /modules/hal/nxp/zephyr/blobs/rw61x

3. How to load FW:
	(1) For Wi-Fi and BLE sample application, CPU1 and CPU2 FW are linked together with CPU3 image, don’t need to download CPU1 and CPU2 image separately.
	(2) User needs to make sure FW bin is placed at modules/hal/nxp/zephyr/blobs/rw61x.
	(3) Default FW bin names are listed in above section 1, don’t change these names, build system depends on these names find FW bin.
	(4) Default selected FW image version is A2, A1 FW is not supported
	(5) Build system will choose to link security FW with CPU3 image based on the configuration above.
	(6) For example, the CMD to write CPU3 image containing CPU1 image to flash in J-link window:
		loadbin C:\xxx\zephyr.bin,0x08000000

For IW416 -
1. FW image names:
	Production FW, for users:
		sdIW416_wlan.bin, for wifi cpu of IW416 board
		uartIW416_bt.bin, for ble cpu of IW416 board
		sduartIW416_wlan_bt.bin, for combo cpus of IW416 board

2. where to get FW image:
	In the directory:  /modules/hal/nxp/zephyr/blobs/IW416

3. How to load FW:
	(1) For Wi-Fi only and BLE only applications use standalone firmware.
	(2) User needs to make sure FW bin is placed at modules/hal/nxp/zephyr/blobs/IW416.
	(3) Default FW bin names are listed in above section 1, don’t change these names, build system depends on these names find FW bin.
	(4) Default selected FW image version is A2.
	(5) On boot up host will load respective firmware images to CPU 1 or 2.
	(6) For example, the CMD to write Host image containing entire application image to flash in J-link window:
		loadbin C:\xxx\zephyr.bin

For NW61x -
1. FW image names:
	Production FW, for users:
		sd_nw61x.bin.se, for wifi cpu of NW61x board
		uart_nw61x.bin.se, for ble cpu of NW61x board
		sduart_nw61x.bin.se, for combo cpus of NW61x board

2. where to get FW image:
	In the directory:  /modules/hal/nxp/zephyr/blobs/nw61x

3. How to load FW:
	(1) For Wi-Fi only and BLE only applications use standalone firmware.
	(2) User needs to make sure FW bin is placed at modules/hal/nxp/zephyr/blobs/nw61x.
	(3) Default FW bin names are listed in above section 1, don’t change these names, build system depends on these names find FW bin.
	(4) Default selected FW image version is A1, A0 FW is not supported.
	(5) On boot up host will load respective firmware images to CPU 1 or 2.
	(6) For example, the CMD to write Host image containing entire application image to flash in J-link window:
		loadbin C:\xxx\zephyr.bin
4. Only secured Wi-Fi and BT controller firmware images are supported.
