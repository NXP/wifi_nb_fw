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


