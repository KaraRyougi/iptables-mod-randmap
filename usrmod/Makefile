CFLAGS			?= -O2 -Wall 
CFLAGS			+= -I../include
CFLAGS			+= -I../iptables/include
XTABLES_SO_DIR	?= $(shell pkg-config xtables --variable xtlibdir)

CC				= mips-linux-musl-gcc
ARCH			= mips
LDLIBS			= -static -shared

.PHONY: all install uninstall clean

all: libxt_RANDMAP.so

install: libxt_RANDMAP.so
	install -Dm644 libxt_RANDMAP.so "${XTABLES_SO_DIR}/libxt_RANDMAP.so"

uninstall:
	rm -f "${XTABLES_SO_DIR}/libxt_RANDMAP.so"

clean:
	rm -f *.o *.so

libxt_RANDMAP.so: libxt_RANDMAP.o
	$(CC) $(LDLIBS) -fPIC -o $@ $^;

libxt_RANDMAP.o: libxt_RANDMAP.c
	$(CC) ${CFLAGS} ${LDLIBS} -D_INIT=libxt_RANDMAP_init -fPIC -c -o $@ $<;