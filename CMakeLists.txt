cmake_minimum_required (VERSION 2.6)
project (ble_emulator)

include_directories(
					bluez-5.41 
					bluez-5.41/lib
					/usr/include/glib-2.0
					/usr/lib/x86_64-linux-gnu/glib-2.0/include
					)

file(GLOB SOURCES "src/main.c"
				"src/gap.c"
				"src/gatt.c"
				"src/efivars.c"
				"src/attach.c"
				"src/log.c")


					 

add_definitions(-DHAVE_CONFIG_H)

link_directories(bluez-5.41/lib)



add_executable(ble_emulator ${SOURCES} 
							#"bluez-5.41/src/shared/.libs/io-glib.o"
							"bluez-5.41/src/shared/.libs/hci.o"
							"bluez-5.41/src/shared/.libs/gap.o"
							"bluez-5.41/src/shared/.libs/queue.o"
							"bluez-5.41/src/shared/.libs/mainloop.o"
							"bluez-5.41/src/shared/.libs/gatt-helpers.o"
							"bluez-5.41/src/shared/.libs/io-mainloop.o"
							"bluez-5.41/src/shared/.libs/hci-crypto.o"
							"bluez-5.41/src/shared/.libs/ecc.o"
							#"bluez-5.41/src/shared/.libs/timeout-glib.o"
							"bluez-5.41/src/shared/.libs/crypto.o"
							"bluez-5.41/src/shared/.libs/pcap.o"
							"bluez-5.41/src/shared/.libs/att.o"
							"bluez-5.41/src/shared/.libs/gatt-client.o"
							"bluez-5.41/src/shared/.libs/uhid.o"
							#"bluez-5.41/src/shared/.libs/tester.o"
							"bluez-5.41/src/shared/.libs/gatt-server.o"
							"bluez-5.41/src/shared/.libs/hfp.o"
							"bluez-5.41/src/shared/.libs/gatt-db.o"
							"bluez-5.41/src/shared/.libs/mgmt.o"
							"bluez-5.41/src/shared/.libs/ad.o"
							"bluez-5.41/src/shared/.libs/btsnoop.o"
							"bluez-5.41/src/shared/.libs/ringbuf.o"
							"bluez-5.41/src/shared/.libs/util.o"
							"bluez-5.41/src/shared/.libs/timeout-mainloop.o")

target_link_libraries(ble_emulator bluetooth-internal )

