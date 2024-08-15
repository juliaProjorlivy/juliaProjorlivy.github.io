---
title: Заливаем прошивку в плату black pill   
date: 2024/8/15
categories:
  - Electronics 
tags:
  - Blackpill
  - dfu-util
---
# Заливаем прошивку в плату black pill   
Все время забываю команды для прошивки, поэтому решила написать небольшую заметку о том, как залить прошивку на плату black pill.   
Плату подключаем по USB к компьютеру. Особенностью этого контроллера является то, что необходимости в програматоре нет: все, что нужно это сама платка.    
Для прошивки:   
1. Нажимаем и удерживаем кнопку BOOT0   
2. Удерживая BOOT0, нажимаем на кнопку NRST, при этом должне погаснуть синий светодиод   
3. На компьютере выполняем команду    
   
```
sudo dfu-util -d 0483:df11 -a 0 -s 0x08000000:leave -D nuttx.bin
```
0483:df11 - usb идентификатор подключенной платы (виден, конда выполнены 1-2 пункты). Этот идентификатор можно найти следующей командой:   
```
lsusb # команда для нахождения подключенных устройств
Bus 003 Device 029: ID 0483:df11 STMicroelectronics STM Device in DFU Mode # результат

```
Вывод в терминале после этой команды должен выглядеть примерно следующим образом   
```
Clearing status
Determining device status...
DFU state(2) = dfuIDLE, status(0) = No error condition is present
DFU mode device DFU version 011a
Device returned transfer size 2048
DfuSe interface name: "Internal Flash  "
Downloading element to address = 0x08000000, size = 75984
Erase   	[=========================] 100%        75984 bytes
Erase    done.
Download	[=========================] 100%        75984 bytes
Download done.
File downloaded successfully
Submitting leave request...
Transitioning to dfuMANIFEST state
```
На этом процесс прошивки закончен.   
P.S.  Решение подсмотрела [здесь.](https://acassis.wordpress.com/2020/06/07/flashing-the-blackpill-on-linux-using-dfu-util/)   
   
