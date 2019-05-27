# stm32f746g-disco Board Support

##### Build
```
make stm32f746g_disco_defconfig
make
```

##### To flash u-boot and SPL:
* openocd -f board/stm32f7discovery.cfg \\\
    -c "program output/images/u-boot-spl.bin 0x08000000" \\\
    -c "program output/images/u-boot.bin 0x08008000" \\\
    -c "reset run" -c shutdown

##### Run U-Boot and SPL under GDB
```
$ cd output/build/uboot-v2018.03-rc3
$ arm-none-eabi-gdb

(gdb) target remote | openocd -f board/stm32f7discovery.cfg -c "gdb_port pipe ;  log_output openocd.log"
(gdb) monitor program spl/u-boot-spl.dtb 0x08004000
(gdb) load u-boot
(gdb) load spl/u-boot-spl
(gdb) add-symbol-file u-boot
(gdb) monitor reset halt
(gdb) 
```
   add --tui to gdb command line to use the _Text User Interface_.
