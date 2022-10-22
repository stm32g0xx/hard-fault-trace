# HardFaultTrace Example

The STM32G079RBTx project that automatically tracks and locates error codes for ARM Cortex-M series MCUs, and automatically analyzes the causes of errors. 

## How to use CmBacktrace

Run this project on your a STM32G079RBTx board, you should see the following logs:

```bash
System initialize finish. Starting..
addr:0x00 value:0x20001F98
addr:0x04 value:0x08000159

Firmware name: HardFaultTrace, hardware version: V1.0.0, software version: V0.1.0
Fault on thread defaultTask
===== Thread stack information =====
  addr: 20001058    data: 08000159
  addr: 2000105c    data: 080010cb
  addr: 20001060    data: a5a5a5a5
  addr: 20001064    data: a5a5a5a5
====================================
=================== Registers information ====================
  R0 : 0000001c  R1 : 00000003  R2 : 0000000a  R3 : 08001f69
  R12: 00000000  LR : 080014d9  PC : 08001f6a  PSR: 21000000
==============================================================
Show more call stack info by run: addr2line -e HardFaultTrace.axf -a -f 08001f6a 080014d8 08000158 080010ca
```

Use the `addr2line` command to view the function call stack details and locate the error code

```bash
$ addr2line -e HardFaultTrace.axf -a -f 08001f6a 080014d8 08000158 080010ca
0x08001f6a
fault_test_by_unalign
Core/Src/app_freertos.c:76
0x080014d8
UART_WaitOnFlagUntilTimeout
Drivers/STM32G0xx_HAL_Driver/Src/stm32g0xx_hal_uart.c:3465
0x08000158
Reset_Handler
startup_stm32g070xx.s:119
0x080010ca
StartDefaultTask
Core/Src/app_freertos.c:142
```
