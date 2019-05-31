CFLAGS += -MD -MP
sources = a.c b.c

all: $(sources:.c=.o)
	gcc -o aa $^

clean:
	rm -rf aa *.o *.d

-include $(sources:.c=.d)

