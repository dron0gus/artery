# Attemp to port ChibiOS to Artery AT32F435/7 chip

AT32F435/437 looks very similas to STM32F4XX chips

To keep compatibility with STM32 drivers I keep STM32_ prefix for all defines

Also I keep STM32 register naming (where possible)

STM32F435 was used as baseline for this port. I did not fix copyrights and comments yet. So don't be confused by STM copyright and other STM32 stuff inside AT32 directories.

## Demo projects:

### RT-AT32F435-ARTERY144 demo

See ChibiOS/demos/STM32/RT-AT32F435-ARTERY144

Simple application blinking LEDs and executing RT and OSLIB tests on button press.

Outputs over serial port (USART1) at 38400. On Artery AT-START-F435 this USART is connected to debuger. Debugger connected to PC creates ttyACM device and forwards all AT32 output to this tty.

### USB_CDC_IAD demo

See ChibiOS/testhal/AT32/AT32F4xx/USB_CDC_IAD

Application inplementing USB device with two ACM ports. OTG1 port is used.

Simple shell is executed on both ACM ports. Few commands are available. Including RT and OSLIB tests. Type 'help' to see some tips.

Known issues:

- USB device is not recognized when connected through **some** HUBs.

## OpenOCD with Artery support

See openocd for OpenOCD with Artery chip support.

See ChibiOsdemos/STM32/RT-AT32F435-ARTERY144/at32f4x.cfg openocd_artery.sh and gdb.sh as example on how to flash and run.

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

Sometimes test dos not hang but fails:

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
--- Result: FAILURE (#3 [] "out of time window")
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
--- Result: SUCCESS
----------------------------------------------------------------------------
--- Test Case 8.3 (Repeated locks, non recursive scenario)
--- Result: SUCCESS
----------------------------------------------------------------------------
--- Test Case 8.4 (Condition Variable signal test)
--- Result: SUCCESS
----------------------------------------------------------------------------
--- Test Case 8.5 (Condition Variable broadcast test)
--- Result: SUCCESS
----------------------------------------------------------------------------
--- Test Case 8.6 (Condition Variable priority boost test)
--- Result: SUCCESS
============================================================================
=== Test Sequence 9 (Synchronous Messages)
----------------------------------------------------------------------------
--- Test Case 9.1 (Messages Server loop)
--- Result: SUCCESS
============================================================================
=== Test Sequence 10 (Event Sources and Event Flags)
----------------------------------------------------------------------------
--- Test Case 10.1 (Events registration)
--- Result: SUCCESS
----------------------------------------------------------------------------
--- Test Case 10.2 (Event Flags dispatching)
--- Result: SUCCESS
----------------------------------------------------------------------------
--- Test Case 10.3 (Events Flags wait using chEvtWaitOne())
--- Result: SUCCESS
----------------------------------------------------------------------------
--- Test Case 10.4 (Events Flags wait using chEvtWaitAny())
--- Result: SUCCESS
----------------------------------------------------------------------------
--- Test Case 10.5 (Events Flags wait using chEvtWaitAll())
--- Result: SUCCESS
----------------------------------------------------------------------------
--- Test Case 10.6 (Events Flags wait timeouts)
--- Result: SUCCESS
----------------------------------------------------------------------------
--- Test Case 10.7 (Broadcasting using chEvtBroadcast())
--- Result: SUCCESS
============================================================================
=== Test Sequence 11 (Dynamic threads)
----------------------------------------------------------------------------
--- Test Case 11.1 (Threads creation from Memory Heap)
--- Result: SUCCESS
----------------------------------------------------------------------------
--- Test Case 11.2 (Threads creation from Memory Pool)
--- Result: SUCCESS
============================================================================
=== Test Sequence 12 (Benchmarks)
----------------------------------------------------------------------------
--- Test Case 12.1 (Messages performance #1)
--- Score : 122229 msgs/S, 244458 ctxswc/S
--- Result: SUCCESS
----------------------------------------------------------------------------
--- Test Case 12.2 (Messages performance #2)
--- Score : 111094 msgs/S, 222188 ctxswc/S
--- Result: SUCCESS
----------------------------------------------------------------------------
--- Test Case 12.3 (Messages performance #3)
--- Score : 111092 msgs/S, 222184 ctxswc/S
--- Result: SUCCESS
----------------------------------------------------------------------------
--- Test Case 12.4 (Context Switch performance)
--- Score : 621232 ctxswc/S
--- Result: SUCCESS
----------------------------------------------------------------------------
--- Test Case 12.5 (Threads performance, full cycle)
--- Score : 85089 threads/S
--- Result: SUCCESS
----------------------------------------------------------------------------
--- Test Case 12.6 (Threads performance, create/exit only)
--- Score : 116484 threads/S
--- Result: SUCCESS
----------------------------------------------------------------------------
--- Test Case 12.7 (Mass reschedule performance)
--- Score : 3241 reschedules/S, 19446 ctxswc/S
--- Result: SUCCESS
----------------------------------------------------------------------------
--- Test Case 12.8 (Round-Robin voluntary reschedule)
--- Score : 303260 ctxswc/S
--- Result: SUCCESS
----------------------------------------------------------------------------
--- Test Case 12.9 (Virtual Timers set/reset performance)
--- Score : 131204 timers/S
--- Result: SUCCESS
----------------------------------------------------------------------------
--- Test Case 12.10 (Semaphores wait/signal performance)
--- Score : 548468 wait+signal/S
--- Result: SUCCESS
----------------------------------------------------------------------------
--- Test Case 12.11 (Mutexes lock/unlock performance)
--- Score : 403280 lock+unlock/S
--- Result: SUCCESS
----------------------------------------------------------------------------
--- Test Case 12.12 (RAM Footprint)
--- OS    : 144 bytes
--- Thread: 76 bytes
--- Timer : 24 bytes
--- Semaph: 12 bytes
--- Mutex : 16 bytes
--- CondV.: 8 bytes
--- EventS: 4 bytes
--- EventL: 20 bytes
--- MailB.: 40 bytes
--- Result: SUCCESS
----------------------------------------------------------------------------

Final result: FAILURE
```
