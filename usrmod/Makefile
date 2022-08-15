CFLAGS			?= -O2 -Wall 
CFLAGS			+= -I../include
XTABLES_SO_DIR		?= $(shell pkg-config xtables --variable xtlibdir)
CC			= mips-linux-gnu-gcc
LD                      = mips-linux-gnu-ld
MUSL_DIR		= /root/musl-install

.PHONY: all install uninstall clean

all: libxt_RANDMAP.so

install: libxt_RANDMAP.so
	install -Dm644 libxt_RANDMAP.so "${XTABLES_SO_DIR}/libxt_RANDMAP.so"

uninstall:
	rm -f "${XTABLES_SO_DIR}/libxt_RANDMAP.so"

clean:
	rm -f *.o *.so

libxt_RANDMAP.so: libxt_RANDMAP.o
	$(LD) -shared -fPIC -nostdlib -o $@ $^ $(MUSL_DIR)/lib/libc.a /usr/lib/gcc-cross/mips-linux-gnu/10/libgcc.a;

libxt_RANDMAP.o: libxt_RANDMAP.c
	$(CC) ${CFLAGS} -D_INIT=libxt_RANDMAP_init -fPIC -nostdlib -I$(MUSL_DIR)/include -I/root/iptables-include -c -o $@ $<;
