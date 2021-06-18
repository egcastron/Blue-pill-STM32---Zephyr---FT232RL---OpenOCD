# PROGRAMACIÓN BLUE PILL VÍA FT232RL Y OPENOCD, CON IMAGEN GENERADA EN ZEPHYR.

Luego de instalar OpenOCD, el archivo  ft232r.cfg se encuentra en la carpeta raíz openocd-code/tcl/interface/
éste se encarga de configurar el ft232rl como programador para el stm32; también se debe usar el archivo stm32f103c8_blue_pill.cfg que se encuentra en  openocd-code/tcl/board, el cual establece el tamaño de la flash y el archivo fuente de configuración del STM32: ((stm32f1x.cfg) éste se encuentra en openocd-code/tcl/target).

finalmente el archivo de configuración queda de la siguiente manera:
[ft232r.cfg](ft232r.cfg)

en la carpeta del proyecto usar:   
          
    openocd openocd -f ft232r.cfg
    
La imagen generada por Zephyr, .bin o .elf también puede ir en la carpeta del proyecto.

del FT232RL se usan los pines del jtag: TMS, TDI, TDO y TCK; vcc y gnd 


