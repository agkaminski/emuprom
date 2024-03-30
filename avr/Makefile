ISP ?= usbasp
#ISP ?= avrisp2

all: emuprom.c
	avr-gcc -DF_CPU=8000000UL -O2 -mmcu=atmega8 -Wall emuprom.c uart/uart.c -o bin/emuprom
	avr-objcopy -Oihex bin/emuprom bin/emuprom.hex
	size -A -d bin/emuprom

fuse:
	avrdude -c${ISP} -pm8 -U lfuse:w:0xe4:m -U hfuse:w:0xd9:m

install:
	avrdude -c${ISP} -pm8 -U flash:w:bin/emuprom.hex:i

clean:
	rm -f bin/*
