#Notes:
#1. eRPC must have been compiled with DTRANSPORT=dpdk; use `make dpdk`
LIBS = -lerpc -lpthread -lnuma -ldl

error:
	@echo "Please choose one of the following targets: dpdk, clean"
	@exit 2
# DPDK flags come from pkg-config. If DPDK is installed in a non-standard
# prefix, set PKG_CONFIG_PATH to its lib/pkgconfig directory.
DPDK_CFLAGS = $(shell pkg-config --cflags libdpdk)
DPDK_LIBS = $(shell pkg-config --libs libdpdk)
dpdk:
	g++ -g -std=c++11 -o server server.cc \
		-Wno-deprecated-declarations \
		-DERPC_DPDK=true -march=native $(DPDK_CFLAGS) \
		-I ../src -I ../third_party/asio/include \
		-L ../build $(LIBS) \
		-Wl,--whole-archive $(DPDK_LIBS) -Wl,--no-whole-archive \
		-lnuma -ldl

	g++ -g -std=c++11 -o client client.cc \
		-Wno-deprecated-declarations \
		-DERPC_DPDK=true -march=native $(DPDK_CFLAGS) \
		-I ../src -I ../third_party/asio/include \
		-L ../build $(LIBS) \
		-Wl,--whole-archive $(DPDK_LIBS) -Wl,--no-whole-archive \
		-lnuma -ldl
clean:
	rm server client

