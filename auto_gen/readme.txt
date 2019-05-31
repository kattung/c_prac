Reference:
http://www.microhowto.info/howto/automatically_generate_makefile_dependencies.html
https://www.gnu.org/software/make/manual/html_node/Automatic-Prerequisites.html#Automatic-Prerequisites


To generate dependency files:

1. Add directive:
   -include $(SRC:%.c = %.d)

2. for GNU GCC:
   Method 1: Add rule
     add rule that compile c code with cflags '-M'
     to generate dependency file
     and then use 'sed' to add *.d to dependency files
     ---- example ------------
     %.d: %.c
            set -e; rm -f $@; \
            $(CC) -M $(CPPFLAGS) $< > $@.$$$$; \
            sed 's,\($*\)\.o[ :]*,\1.o $@ : ,g' < $@.$$$$ > $@; \
            rm -f $@.$$$$
     -------------------------

   Method 2: Add CFLAGS
     -MD:    gcc cflags, generat dependency rule and save to *.d
             including system headers.
     -MMD:   like -MD, but not include system headers
     -MP:    create rules for generating each dependency.
             suppresses error when header deleted/renamed.
     example: CFLAGS += -MD -MP

3. for ARM compiler:
   * armcc:
     CFLAGS += --md --depend_dir=<dir_path>

   * armasm:
     ASFLAGS += --md
