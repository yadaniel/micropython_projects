git clone https://github.com/micropython/micropython.git
cd micropython/ports/stm32
make -j4 submodules
BOARD=NUCLEO_L432KC make -j4


