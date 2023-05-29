# Attemp to port ChibiOS to Artery AT32F435/7 chip

See ChibiOS/demos/STM32/RT-AT32F435-ARTERY144 for demo project for Artery AT-START-F435 board. Only blinks LEDs for now.

See openocd for OpenOCD with Artery chip support. See demos/STM32/RT-AT32F435-ARTERY144/at32f4x.cfg openocd_artery.sh and gdb.sh as example on how to flash and run.

## Current status

Test hangs... LEDs continue to blink...

```
*** ChibiOS/RT Test Suite
***
*** Compiled:     May 30 2023 - 01:39:21
*** Platform:     AT32F435/437 High Performance with DSP, FPU and MPU
*** Test Board:   Artery AT-START-F435 board
***
*** Text size:    63720 bytes
*** RO data size: 10332 bytes
*** Data size:    220 bytes
*** BSS size:     5640 bytes

============================================================================
=== Test Sequence 1 (Information)
----------------------------------------------------------------------------
--- Test Case 1.1 (Port Info)
--- Architecture:                       ARMv7E-M
--- Core Variant:                       Cortex-M4
--- Compiler:                           GCC 11.3.1 20220712
--- Port Info:                          Advanced kernel mode
--- Natural alignment:                  4
--- Stack alignment:                    8
--- Working area alignment:             8
--- Result: SUCCESS
----------------------------------------------------------------------------
--- Test Case 1.2 (Kernel Info)
--- Product:                            ChibiOS/RT
--- Stable Flag:                        0
--- Version String:                     7.1.0
--- Major Number:                       7
--- Minor Number:                       1
--- Patch Number:                       0
--- Result: SUCCESS
----------------------------------------------------------------------------
--- Test Case 1.3 (Kernel Settings)
--- CH_CFG_ST_RESOLUTION:               32
--- CH_CFG_ST_FREQUENCY:                10000
--- CH_CFG_INTERVALS_SIZE:              32
--- CH_CFG_TIME_TYPES_SIZE:             32
--- CH_CFG_ST_TIMEDELTA:                2
--- CH_CFG_TIME_QUANTUM:                0
--- CH_CFG_MEMCORE_SIZE:                0
--- CH_CFG_NO_IDLE_THREAD:              0
--- CH_CFG_OPTIMIZE_SPEED:              1
--- CH_CFG_USE_TM:                      1
--- CH_CFG_USE_REGISTRY:                1
--- CH_CFG_USE_WAITEXIT:                1
--- CH_CFG_USE_SEMAPHORES:              1
--- CH_CFG_USE_SEMAPHORES_PRIORITY:     0
--- CH_CFG_USE_MUTEXES:                 1
--- CH_CFG_USE_MUTEXES_RECURSIVE:       0
--- CH_CFG_USE_CONDVARS:                1
--- CH_CFG_USE_CONDVARS_TIMEOUT:        1
--- CH_CFG_USE_EVENTS:                  1
--- CH_CFG_USE_EVENTS_TIMEOUT:          1
--- CH_CFG_USE_MESSAGES:                1
--- CH_CFG_USE_MESSAGES_PRIORITY:       0
--- CH_CFG_USE_DYNAMIC:                 1
--- CH_DBG_STATISTICS:                  0
--- CH_DBG_SYSTEM_STATE_CHECK:          0
--- CH_DBG_ENABLE_CHECKS:               0
--- CH_DBG_ENABLE_ASSERTS:              0
--- CH_DBG_TRACE_MASK:                  255
--- CH_DBG_TRACE_BUFFER_SIZE:           128
--- CH_DBG_ENABLE_STACK_CHECK:          0
--- CH_DBG_FILL_THREADS:                0
--- CH_DBG_THREADS_PROFILING:           0
--- Result: SUCCESS
============================================================================
=== Test Sequence 2 (System layer and port interface)
----------------------------------------------------------------------------
--- Test Case 2.1 (System integrity functionality)
--- Result: SUCCESS
----------------------------------------------------------------------------
--- Test Case 2.2 (Critical zones functionality)
--- Result: SUCCESS
----------------------------------------------------------------------------
--- Test Case 2.3 (Interrupts handling functionality)
--- Result: SUCCESS
============================================================================
=== Test Sequence 3 (Time and Intervals Functionality)
----------------------------------------------------------------------------
--- Test Case 3.1 (System Tick Counter functionality)
--- Result: SUCCESS
----------------------------------------------------------------------------
--- Test Case 3.2 (Time ranges functionality)
--- Result: SUCCESS
============================================================================
=== Test Sequence 4 (Time Stamps Functionality)
----------------------------------------------------------------------------
--- Test Case 4.1 (Time Stamps functionality)
--- Result: SUCCESS
============================================================================
=== Test Sequence 5 (Threads Functionality)
----------------------------------------------------------------------------
--- Test Case 5.1 (Thread Sleep functionality)
--- Result: SUCCESS
----------------------------------------------------------------------------
--- Test Case 5.2 (Ready List functionality, threads priority order)
--- Result: SUCCESS
----------------------------------------------------------------------------
--- Test Case 5.3 (Priority change test)
--- Result: SUCCESS
----------------------------------------------------------------------------
--- Test Case 5.4 (Priority change test with Priority Inheritance)
--- Result: SUCCESS
============================================================================
=== Test Sequence 6 (Suspend/Resume)
----------------------------------------------------------------------------
--- Test Case 6.1 (Suspend and Resume functionality)
--- Result: SUCCESS
============================================================================
=== Test Sequence 7 (Counter Semaphores)
----------------------------------------------------------------------------
--- Test Case 7.1 (Semaphore primitives, no state change)
--- Result: SUCCESS
----------------------------------------------------------------------------
--- Test Case 7.2 (Semaphore enqueuing test)
--- Result: SUCCESS
----------------------------------------------------------------------------
--- Test Case 7.3 (Semaphore timeout test)
--- Result: SUCCESS
----------------------------------------------------------------------------
--- Test Case 7.4 (Testing chSemAddCounterI() functionality)
--- Result: SUCCESS
----------------------------------------------------------------------------
--- Test Case 7.5 (Testing chSemWaitSignal() functionality)
--- Result: SUCCESS
----------------------------------------------------------------------------
--- Test Case 7.6 (Testing Binary Semaphores special case)
--- Result: SUCCESS
============================================================================
=== Test Sequence 8 (Mutexes, Condition Variables and Priority Inheritance)
----------------------------------------------------------------------------
--- Test Case 8.1 (Priority enqueuing test)
--- Result: SUCCESS
----------------------------------------------------------------------------
--- Test Case 8.2 (Priority return verification)
```