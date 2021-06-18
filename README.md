## PROGRAMACIÓN BLUE PILL VÍA FT232RL Y OPENOCD, CON IMAGEN GENERADA EN ZEPHYR.

Luego de instalar OpenOCD, el archivo  ft232r.cfg se encuentra en la carpeta raíz openocd-code/tcl/interface/
éste se encarga de configurar el ft232rl como programador para el stm32; también se debe usar el archivo stm32f103c8_blue_pill.cfg que se encuentra en  openocd-code/tcl/board, el cual establece el tamaño de la flash y el archivo fuente de configuración del STM32: ((stm32f1x.cfg) éste se encuentra en openocd-code/tcl/target).

finalmente el archivo de configuración queda de la siguiente manera:
[ft232r.cfg](ft232r.cfg)

en la carpeta del proyecto usar:   
          
    openocd openocd -f ft232r.cfg
    
La imagen generada por Zephyr, .bin o .elf también puede ir en la carpeta del proyecto.



del FT232RL se usan los pines del jtag: TMS, TDI, TDO y TCK; vcc y gnd:

![alt text](https://github.com/egcastron/Blue-pill-STM32---Zephyr---FT232RL---OpenOCD/blob/master/img/ft232.jpeg?raw=true)

y estos pines van a los pines del BLUE PILL: PA15, PB3, SWIO, SWCLK:

![alt text](https://github.com/egcastron/Blue-pill-STM32---Zephyr---FT232RL---OpenOCD/blob/master/img/bluePill.jpeg?raw=true)



conectar el ft232rl al PC.
Luego poner el Blue Pill en Programming mode:

![alt text](https://github.com/egcastron/Blue-pill-STM32---Zephyr---FT232RL---OpenOCD/blob/master/img/OPmode.jpeg?raw=true)



Ahora desde una terminal en dicha carpeta correr el comando: 
          
          sudo openocd -f ft232r.cfg
          
y aparecerá: Info : Listening on port 2000 for gdb connections

Abrir otra terminal desde la carpeta del proyecto y correr: 
          
          telnet localhost 2001
          
primero hacer el reset hal antes de programar para detener algún proceso que esté corriendo:

          reset halt

para mirar los bancos de memoria con:

          flash banks 

en este caso nos arroja el valor de la memoria base: 0x08000000 (desde donde inicia la flash):

![alt text](https://github.com/egcastron/Blue-pill-STM32---Zephyr---FT232RL---OpenOCD/blob/master/img/telnet.png?raw=true)

y luego se sube la imagen: 

          flash write_image erase "zephyr.bin" 0x08000000
          reset run

después de programada, se pasa el Blue Pill de nuevo a Operating mode, y al conectarla ya tendrá el programa corriendo.






