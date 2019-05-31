
sources = a.c b.c

all: $(sources:.c=.o)
	gcc -o aa $^

clean:
	rm -rf aa *.o *.d

%.d: %.c
	set -e; rm -f $@; \
	$(CC) -M $(CPPFLAGS) $< > $@.$$$$; \
	sed 's,\($*\)\.o[ :]*,\1.o $@ : ,g' < $@.$$$$ > $@; \
	rm -f $@.$$$$

-include $(sources:.c=.d)

