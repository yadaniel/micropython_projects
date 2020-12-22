# basic build
git clone https://github.com/micropython/micropython.git  
cd micropython/ports/stm32  
make -j4 submodules  
BOARD=NUCLEO_L432KC make -j4  
  
# enable other modules  
cd micropython/ports/stm32/boards/NUCLEO_L432KC  
change 0 to 1 to build stm module  
    #define MICROPY_PY_STM              (0)  
    #define MICROPY_PY_STM              (1)  

# build mpy-cross, required to freeze scripts into build
cd mpy-cross  
make -j4  
  
# add custom script for frozen build (deprecated)  
cd micropython/ports/stm32  
mkdir script  
touch custom.py  
vim custom.py # edit  
make BOARD=NUCLEO_L432KC FROZEN_MPY_DIR=scripts  
  
# add custom script for frozen build  
cd micropython/ports/stm32  
mkdir script  
touch custom.py  
vim custom.py # edit  
cd micropython/ports/stm32/boards  
vim manifest.py # add the line below  
freeze("$(MPY_DIR)/ports/stm32/scripts", "custom.py")  
make -j4 BOARD=NUCLEO_L432KC FROZEN_MANIFEST=boards/manifest.py  



