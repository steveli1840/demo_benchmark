#OBJS=uiv.o npd.o aob.o msf.o dbf.o uaf.o
SRCS=$(wildcard *.c)
OBJS=$(patsubst %.c,%.o,$(SRCS))
TARGET = basic.a

.PHONY: all clean

all: $(TARGET)

$(TARGET): $(OBJS)
	$(AR) crv $@ $^

clean:
	rm -f $(TARGET) $(OBJS)
