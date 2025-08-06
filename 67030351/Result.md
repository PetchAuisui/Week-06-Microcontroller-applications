## ผลการทดลอง
### การวิเคราะห์ Build Output (ใน Docker Container)
#### 1. ดูขนาด binary
```c
idf.py size
#สร้าง size.txt
idf.py size > size.txt

```
##### Result
```cExecuting action: size
Running ninja in directory /project/lab6_1_basic_build/build
Executing "ninja all"...
[1/9] Performing build step for 'bootloader'
[1/1] cd /project/lab6_1_basic_build/build/bootloader/esp-idf/esptool_py && /opt/esp/python_env/idf6.0_py3.12_env/bin/python /opt/esp/idf/components/partition_table/check_sizes.py --offset 0x8000 bootloader 0x1000 /project/lab6_1_basic_build/build/bootloader/bootloader.bin
Bootloader binary size 0x66a0 bytes. 0x960 bytes (8%) free.
[2/9] Building C object esp-idf/main/CMakeFiles/__idf_main.dir/lab6_1_basic_build.c.obj
[3/9] No install step for 'bootloader'
[4/9] Completed 'bootloader'
[5/9] Linking C static library esp-idf/main/libmain.a
[6/9] Generating esp-idf/esp_system/ld/sections.ld
[7/9] Linking CXX executable lab1_basic_build.elf
[8/9] Generating binary image from built executable
esptool.py v4.9.0
Creating esp32 image...
Merged 2 ELF sections
Successfully created esp32 image.
Generated /project/lab6_1_basic_build/build/lab1_basic_build.bin
[9/9] cd /project/lab6_1_basic_build/build/esp-idf/esptool_py && /opt/esp/python_env/idf6.0_py3.12_env/bin/python /opt/esp/idf/components/partition_table/check_sizes.py --offset 0x8000 partition --type app /project/lab6_1_basic_build/build/partition_table/partition-table.bin /project/lab6_1_basic_build/build/lab1_basic_build.bin
lab1_basic_build.bin binary size 0x279c0 bytes. Smallest app partition is 0x100000 bytes. 0xd8640 bytes (85%) free.
Running ninja in directory /project/lab6_1_basic_build/build
Executing "ninja size"...
[0/1] cd /project/lab6_1_basic_build/build && /opt/esp/tools/cmake/3.30.2/bin/cmake -D "IDF_SIZE_TOOL=/opt/esp/python_env/idf6.0_py3.12_env/bin/python;-m;esp_idf_size" -D MAP_FILE=/project/lab6_1_basic_build/build/lab1_basic_build.map -D OUTPUT_JSON= -P /opt/esp/idf/tools/cmake/run_size_tool.cmake
                             Memory Type Usage Summary                              
┏━━━━━━━━━━━━━━━━━━━━━━━┳━━━━━━━━━━━━━━┳━━━━━━━━━━┳━━━━━━━━━━━━━━━━┳━━━━━━━━━━━━━━━┓
┃ Memory Type/Section   ┃ Used [bytes] ┃ Used [%] ┃ Remain [bytes] ┃ Total [bytes] ┃
┡━━━━━━━━━━━━━━━━━━━━━━━╇━━━━━━━━━━━━━━╇━━━━━━━━━━╇━━━━━━━━━━━━━━━━╇━━━━━━━━━━━━━━━┩
│ Flash Code            │        61198 │          │                │               │
│    .text              │        61198 │          │                │               │
│ IRAM                  │        53175 │    40.57 │          77897 │        131072 │
│    .text              │        52147 │    39.79 │                │               │
│    .vectors           │         1028 │     0.78 │                │               │
│ Flash Data            │        38020 │          │                │               │
│    .rodata            │        37764 │          │                │               │
│    .appdesc           │          256 │          │                │               │
│ DRAM                  │        11944 │     6.61 │         168792 │        180736 │
│    .data              │         9696 │     5.36 │                │               │
│    .bss               │         2248 │     1.24 │                │               │
│ RTC FAST              │           36 │     0.44 │           8156 │          8192 │
│    .force_fast        │           36 │     0.44 │                │               │
│ RTC SLOW              │           24 │     0.29 │           8168 │          8192 │
│    .rtc_slow_reserved │           24 │     0.29 │                │               │
└───────────────────────┴──────────────┴──────────┴────────────────┴───────────────┘

```
`Total image size: 162125 bytes (.bin may be padded larger)`

[size.txt](size.txt)


#### 2.ดูรายละเอียดขนาดตาม component
```c
idf.py size-components 
#สร้าง size-components.txt
idf.py size-components > size-components.txt
```
##### Result
```c
Executing action: size-components
Running ninja in directory /project/lab6_1_basic_build/build
Executing "ninja all"...
[1/4] cd /project/lab6_1_basic_build/build/esp-idf/esptool_py && /opt/esp/python_env/idf6.0_py3.12_env/bin/python /opt/esp/idf/components/partition_table/check_sizes.py --offset 0x8000 partition --type app /project/lab6_1_basic_build/build/partition_table/partition-table.bin /project/lab6_1_basic_build/build/lab1_basic_build.bin
lab1_basic_build.bin binary size 0x279c0 bytes. Smallest app partition is 0x100000 bytes. 0xd8640 bytes (85%) free.
[2/4] Performing build step for 'bootloader'
[1/1] cd /project/lab6_1_basic_build/build/bootloader/esp-idf/esptool_py && /opt/esp/python_env/idf6.0_py3.12_env/bin/python /opt/esp/idf/components/partition_table/check_sizes.py --offset 0x8000 bootloader 0x1000 /project/lab6_1_basic_build/build/bootloader/bootloader.bin
Bootloader binary size 0x66a0 bytes. 0x960 bytes (8%) free.
[3/4] No install step for 'bootloader'
[4/4] Completed 'bootloader'
Running ninja in directory /project/lab6_1_basic_build/build
Executing "ninja size-components"...
[0/1] cd /project/lab6_1_basic_build/build && /opt/esp/tools/cmake/3.30.2/bin/cmake -D "IDF_SIZE_TOOL=/opt/esp/python_env/idf6.0_py3.12_env/bin/python;-m;esp_idf_size" -D IDF_SIZE_MODE=--archives -D MAP_FILE=/project/lab6_1_basic_build/build/lab1_basic_build.map -D OUTPUT_JSON= -P /opt/esp/idf/tools/cmake/run_size_tool.cmake
                                                                                  Per-archive contributions to ELF file                                                                                  
┏━━━━━━━━━━━━━━━━━━━━━━━━━┳━━━━━━━━━━━━┳━━━━━━┳━━━━━━┳━━━━━━━┳━━━━━━━┳━━━━━━━┳━━━━━━━━━━┳━━━━━━━━━━━━┳━━━━━━━┳━━━━━━━━━━━━┳━━━━━━━━━┳━━━━━━━━━━┳━━━━━━━━━━┳━━━━━━━━━━━━━┳━━━━━━━━━━┳━━━━━━━━━━━━━━━━━━━━┓
┃ Archive File            ┃ Total Size ┃ DRAM ┃ .bss ┃ .data ┃  IRAM ┃ .text ┃ .vectors ┃ Flash Code ┃ .text ┃ Flash Data ┃ .rodata ┃ .appdesc ┃ RTC FAST ┃ .force_fast ┃ RTC SLOW ┃ .rtc_slow_reserved ┃
┡━━━━━━━━━━━━━━━━━━━━━━━━━╇━━━━━━━━━━━━╇━━━━━━╇━━━━━━╇━━━━━━━╇━━━━━━━╇━━━━━━━╇━━━━━━━━━━╇━━━━━━━━━━━━╇━━━━━━━╇━━━━━━━━━━━━╇━━━━━━━━━╇━━━━━━━━━━╇━━━━━━━━━━╇━━━━━━━━━━━━━╇━━━━━━━━━━╇━━━━━━━━━━━━━━━━━━━━┩
│ libesp_app_format.a     │      26474 │   10 │   10 │     0 │     0 │     0 │        0 │        417 │   417 │      26047 │   25791 │      256 │        0 │           0 │        0 │                  0 │
│ libc.a                  │      23792 │  572 │  312 │   260 │     0 │     0 │        0 │      21560 │ 21560 │       1660 │    1660 │        0 │        0 │           0 │        0 │                  0 │
│ libfreertos.a           │      18052 │ 3847 │  741 │  3106 │ 12882 │ 12882 │        0 │        367 │   367 │        956 │     956 │        0 │        0 │           0 │        0 │                  0 │
│ libesp_hw_support.a     │      13719 │  382 │   76 │   306 │  6019 │  6019 │        0 │       6356 │  6356 │        902 │     902 │        0 │       36 │          36 │       24 │                 24 │
│ libesp_system.a         │      12611 │  742 │  309 │   433 │  3570 │  3570 │        0 │       7661 │  7661 │        638 │     638 │        0 │        0 │           0 │        0 │                  0 │
│ libheap.a               │      12037 │   12 │    8 │     4 │  7340 │  7340 │        0 │       3095 │  3095 │       1590 │    1590 │        0 │        0 │           0 │        0 │                  0 │
│ libhal.a                │      10656 │ 2621 │    8 │  2613 │  5893 │  5893 │        0 │       2044 │  2044 │         98 │      98 │        0 │        0 │           0 │        0 │                  0 │
│ libspi_flash.a          │       9845 │ 1140 │   24 │  1116 │  7194 │  7194 │        0 │       1082 │  1082 │        429 │     429 │        0 │        0 │           0 │        0 │                  0 │
│ libesp_driver_uart.a    │       7752 │  336 │   32 │   304 │     0 │     0 │        0 │       6815 │  6815 │        601 │     601 │        0 │        0 │           0 │        0 │                  0 │
│ libvfs.a                │       4294 │  236 │   44 │   192 │     0 │     0 │        0 │       3915 │  3915 │        143 │     143 │        0 │        0 │           0 │        0 │                  0 │
│ libesp_mm.a             │       4109 │  164 │  128 │    36 │  1062 │  1062 │        0 │       2669 │  2669 │        214 │     214 │        0 │        0 │           0 │        0 │                  0 │
│ libxtensa.a             │       3413 │ 1044 │    0 │  1044 │  2216 │  1789 │      427 │        117 │   117 │         36 │      36 │        0 │        0 │           0 │        0 │                  0 │
│ libnewlib.a             │       3144 │  360 │  200 │   160 │  1473 │  1473 │        0 │       1202 │  1202 │        109 │     109 │        0 │        0 │           0 │        0 │                  0 │
│ libbootloader_support.a │       2189 │    0 │    0 │     0 │  2055 │  2055 │        0 │         94 │    94 │         40 │      40 │        0 │        0 │           0 │        0 │                  0 │
│ libesp_common.a         │       1841 │    0 │    0 │     0 │     0 │     0 │        0 │         51 │    51 │       1790 │    1790 │        0 │        0 │           0 │        0 │                  0 │
│ libsoc.a                │       1521 │   40 │    0 │    40 │    37 │    37 │        0 │          0 │     0 │       1444 │    1444 │        0 │        0 │           0 │        0 │                  0 │
│ liblog.a                │       1258 │  284 │  276 │     8 │   329 │   329 │        0 │        621 │   621 │         24 │      24 │        0 │        0 │           0 │        0 │                  0 │
│ libesp_ringbuf.a        │       1150 │    0 │    0 │     0 │  1053 │  1053 │        0 │          0 │     0 │         97 │      97 │        0 │        0 │           0 │        0 │                  0 │
│ libesp_partition.a      │       1035 │    8 │    8 │     0 │     0 │     0 │        0 │        990 │   990 │         37 │      37 │        0 │        0 │           0 │        0 │                  0 │
│ libesp_rom.a            │        801 │    0 │    0 │     0 │   245 │   245 │        0 │          0 │     0 │        556 │     556 │        0 │        0 │           0 │        0 │                  0 │
│ libesp_vfs_console.a    │        677 │   16 │   16 │     0 │     0 │     0 │        0 │        481 │   481 │        180 │     180 │        0 │        0 │           0 │        0 │                  0 │
│ libesp_timer.a          │        536 │    8 │    8 │     0 │   145 │   145 │        0 │        375 │   375 │          8 │       8 │        0 │        0 │           0 │        0 │                  0 │
│ libxt_hal.a             │        475 │    0 │    0 │     0 │   443 │   443 │        0 │          0 │     0 │         32 │      32 │        0 │        0 │           0 │        0 │                  0 │
│ libefuse.a              │        319 │    0 │    0 │     0 │     0 │     0 │        0 │        263 │   263 │         56 │      56 │        0 │        0 │           0 │        0 │                  0 │
│ libapp_update.a         │        183 │    4 │    4 │     0 │     0 │     0 │        0 │        149 │   149 │         30 │      30 │        0 │        0 │           0 │        0 │                  0 │
│ libmain.a               │        126 │    0 │    0 │     0 │     0 │     0 │        0 │        126 │   126 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
│ libpthread.a            │         25 │    0 │    0 │     0 │     0 │     0 │        0 │         25 │    25 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
│ libesp_security.a       │         20 │    0 │    0 │     0 │     0 │     0 │        0 │         12 │    12 │          8 │       8 │        0 │        0 │           0 │        0 │                  0 │
│ libcxx.a                │         10 │    0 │    0 │     0 │     0 │     0 │        0 │         10 │    10 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
│ libnvs_sec_provider.a   │          5 │    0 │    0 │     0 │     0 │     0 │        0 │          5 │     5 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
│ libesp_phy.a            │          5 │    0 │    0 │     0 │     0 │     0 │        0 │          5 │     5 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
└─────────────────────────┴────────────┴──────┴──────┴───────┴───────┴───────┴──────────┴────────────┴───────┴────────────┴─────────┴──────────┴──────────┴─────────────┴──────────┴────────────────────┘
```
[size-components.txt](size-components.txt)

### 3.ดูรายละเอียดขนาดตาม source file
```c
idf.py size-files
#สร้าง size-files.txt
idf.py size-files > size-files.txt
```
#### Result
```c
Executing action: size-files
Running ninja in directory /project/lab6_1_basic_build/build
Executing "ninja all"...
[1/4] cd /project/lab6_1_basic_build/build/esp-idf/esptool_py && /opt/esp/python_env/idf6.0_py3.12_env/bin/python /opt/esp/idf/components/partition_table/check_sizes.py --offset 0x8000 partition --type app /project/lab6_1_basic_build/build/partition_table/partition-table.bin /project/lab6_1_basic_build/build/lab1_basic_build.bin
lab1_basic_build.bin binary size 0x279c0 bytes. Smallest app partition is 0x100000 bytes. 0xd8640 bytes (85%) free.
[2/4] Performing build step for 'bootloader'
[1/1] cd /project/lab6_1_basic_build/build/bootloader/esp-idf/esptool_py && /opt/esp/python_env/idf6.0_py3.12_env/bin/python /opt/esp/idf/components/partition_table/check_sizes.py --offset 0x8000 bootloader 0x1000 /project/lab6_1_basic_build/build/bootloader/bootloader.bin
Bootloader binary size 0x66a0 bytes. 0x960 bytes (8%) free.
[3/4] No install step for 'bootloader'
[4/4] Completed 'bootloader'
Running ninja in directory /project/lab6_1_basic_build/build
Executing "ninja size-files"...
[0/1] cd /project/lab6_1_basic_build/build && /opt/esp/tools/cmake/3.30.2/bin/cmake -D "IDF_SIZE_TOOL=/opt/esp/python_env/idf6.0_py3.12_env/bin/python;-m;esp_idf_size" -D IDF_SIZE_MODE=--files -D MAP_FILE=/project/lab6_1_basic_build/build/lab1_basic_build.map -D OUTPUT_JSON= -P /opt/esp/idf/tools/cmake/run_size_tool.cmake
                                                                                         Per-file contributions to ELF file                                                                                         
┏━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┳━━━━━━━━━━━━┳━━━━━━┳━━━━━━┳━━━━━━━┳━━━━━━┳━━━━━━━┳━━━━━━━━━━┳━━━━━━━━━━━━┳━━━━━━━┳━━━━━━━━━━━━┳━━━━━━━━━┳━━━━━━━━━━┳━━━━━━━━━━┳━━━━━━━━━━━━━┳━━━━━━━━━━┳━━━━━━━━━━━━━━━━━━━━┓
┃ Object File                         ┃ Total Size ┃ DRAM ┃ .bss ┃ .data ┃ IRAM ┃ .text ┃ .vectors ┃ Flash Code ┃ .text ┃ Flash Data ┃ .rodata ┃ .appdesc ┃ RTC FAST ┃ .force_fast ┃ RTC SLOW ┃ .rtc_slow_reserved ┃
┡━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━╇━━━━━━━━━━━━╇━━━━━━╇━━━━━━╇━━━━━━━╇━━━━━━╇━━━━━━━╇━━━━━━━━━━╇━━━━━━━━━━━━╇━━━━━━━╇━━━━━━━━━━━━╇━━━━━━━━━╇━━━━━━━━━━╇━━━━━━━━━━╇━━━━━━━━━━━━━╇━━━━━━━━━━╇━━━━━━━━━━━━━━━━━━━━┩
│ esp_app_desc.c.obj                  │      26474 │   10 │   10 │     0 │    0 │     0 │        0 │        417 │   417 │      26047 │   25791 │      256 │        0 │           0 │        0 │                  0 │
│ libc_a-vfprintf.o                   │      13396 │    0 │    0 │     0 │    0 │     0 │        0 │      12824 │ 12824 │        572 │     572 │        0 │        0 │           0 │        0 │                  0 │
│ tasks.c.obj                         │       9565 │  718 │  696 │    22 │ 8300 │  8300 │        0 │          0 │     0 │        547 │     547 │        0 │        0 │           0 │        0 │                  0 │
│ tlsf.c.obj                          │       6833 │    0 │    0 │     0 │ 5358 │  5358 │        0 │       1199 │  1199 │        276 │     276 │        0 │        0 │           0 │        0 │                  0 │
│ uart_vfs.c.obj                      │       4966 │  148 │   20 │   128 │    0 │     0 │        0 │       4469 │  4469 │        349 │     349 │        0 │        0 │           0 │        0 │                  0 │
│ port.c.obj                          │       4322 │ 3124 │   40 │  3084 │ 1124 │  1124 │        0 │          0 │     0 │         74 │      74 │        0 │        0 │           0 │        0 │                  0 │
│ wdt_hal_iram.c.obj                  │       3867 │ 2341 │    0 │  2341 │ 1526 │  1526 │        0 │          0 │     0 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
│ esp_mmu_map.c.obj                   │       3720 │  132 │  128 │     4 │  777 │   777 │        0 │       2669 │  2669 │        142 │     142 │        0 │        0 │           0 │        0 │                  0 │
│ libc_a-dtoa.o                       │       3626 │    0 │    0 │     0 │    0 │     0 │        0 │       3626 │  3626 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
│ vfs.c.obj                           │       3416 │  232 │   40 │   192 │    0 │     0 │        0 │       3169 │  3169 │         15 │      15 │        0 │        0 │           0 │        0 │                  0 │
│ spi_flash_chip_generic.c.obj        │       3241 │  250 │    0 │   250 │ 2991 │  2991 │        0 │          0 │     0 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
│ rtc_clk.c.obj                       │       2857 │   78 │    4 │    74 │ 2779 │  2779 │        0 │          0 │     0 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
│ uart.c.obj                          │       2786 │  188 │   12 │   176 │    0 │     0 │        0 │       2346 │  2346 │        252 │     252 │        0 │        0 │           0 │        0 │                  0 │
│ intr_alloc.c.obj                    │       2628 │   30 │   22 │     8 │  583 │   583 │        0 │       1910 │  1910 │        105 │     105 │        0 │        0 │           0 │        0 │                  0 │
│ queue.c.obj                         │       2467 │    0 │    0 │     0 │ 2194 │  2194 │        0 │          0 │     0 │        273 │     273 │        0 │        0 │           0 │        0 │                  0 │
│ libc_a-mprec.o                      │       2260 │    0 │    0 │     0 │    0 │     0 │        0 │       2008 │  2008 │        252 │     252 │        0 │        0 │           0 │        0 │                  0 │
│ spi_flash_hal_iram.c.obj            │       2101 │    0 │    0 │     0 │ 2101 │  2101 │        0 │          0 │     0 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
│ task_wdt.c.obj                      │       2034 │   38 │    5 │    33 │    0 │     0 │        0 │       1881 │  1881 │        115 │     115 │        0 │        0 │           0 │        0 │                  0 │
│ esp_err_to_name.c.obj               │       1841 │    0 │    0 │     0 │    0 │     0 │        0 │         51 │    51 │       1790 │    1790 │        0 │        0 │           0 │        0 │                  0 │
│ xtensa_vectors.S.obj                │       1801 │   20 │    0 │    20 │ 1745 │  1318 │      427 │          0 │     0 │         36 │      36 │        0 │        0 │           0 │        0 │                  0 │
│ mmu_hal.c.obj                       │       1607 │  206 │    0 │   206 │ 1401 │  1401 │        0 │          0 │     0 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
│ periph_ctrl.c.obj                   │       1597 │   42 │   34 │     8 │  107 │   107 │        0 │       1427 │  1427 │         21 │      21 │        0 │        0 │           0 │        0 │                  0 │
│ cpu_start.c.obj                     │       1450 │    5 │    5 │     0 │  658 │   658 │        0 │        779 │   779 │          8 │       8 │        0 │        0 │           0 │        0 │                  0 │
│ rtc_time.c.obj                      │       1237 │    0 │    0 │     0 │ 1200 │  1200 │        0 │          0 │     0 │         37 │      37 │        0 │        0 │           0 │        0 │                  0 │
│ esp_flash_api.c.obj                 │       1172 │   30 │    0 │    30 │  946 │   946 │        0 │         16 │    16 │        180 │     180 │        0 │        0 │           0 │        0 │                  0 │
│ rtc_io_periph.c.obj                 │       1168 │    0 │    0 │     0 │    0 │     0 │        0 │          0 │     0 │       1168 │    1168 │        0 │        0 │           0 │        0 │                  0 │
│ ringbuf.c.obj                       │       1150 │    0 │    0 │     0 │ 1053 │  1053 │        0 │          0 │     0 │         97 │      97 │        0 │        0 │           0 │        0 │                  0 │
│ heap_caps_base.c.obj                │       1115 │    0 │    0 │     0 │ 1053 │  1053 │        0 │          0 │     0 │         62 │      62 │        0 │        0 │           0 │        0 │                  0 │
│ spi_flash_chip_winbond.c.obj        │       1092 │  140 │    0 │   140 │  952 │   952 │        0 │          0 │     0 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
│ panic_arch.c.obj                    │       1091 │    0 │    0 │     0 │    0 │     0 │        0 │        803 │   803 │        288 │     288 │        0 │        0 │           0 │        0 │                  0 │
│ bootloader_flash.c.obj              │       1084 │    0 │    0 │     0 │ 1044 │  1044 │        0 │          0 │     0 │         40 │      40 │        0 │        0 │           0 │        0 │                  0 │
│ rtc_init.c.obj                      │       1083 │    0 │    0 │     0 │    0 │     0 │        0 │       1083 │  1083 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
│ xtensa_intr_asm.S.obj               │       1075 │ 1024 │    0 │  1024 │   51 │    51 │        0 │          0 │     0 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
│ bootloader_flash_config_esp32.c.obj │       1057 │    0 │    0 │     0 │  971 │   971 │        0 │         86 │    86 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
│ esp_ipc.c.obj                       │       1038 │  402 │   66 │   336 │  267 │   267 │        0 │        343 │   343 │         26 │      26 │        0 │        0 │           0 │        0 │                  0 │
│ locks.c.obj                         │       1019 │  176 │  168 │     8 │  613 │   613 │        0 │        137 │   137 │         93 │      93 │        0 │        0 │           0 │        0 │                  0 │
│ memory_layout.c.obj                 │       1016 │    0 │    0 │     0 │    0 │     0 │        0 │          0 │     0 │       1016 │    1016 │        0 │        0 │           0 │        0 │                  0 │
│ cache_utils.c.obj                   │        980 │   18 │   14 │     4 │  734 │   734 │        0 │         81 │    81 │        147 │     147 │        0 │        0 │           0 │        0 │                  0 │
│ panic.c.obj                         │        968 │   25 │    5 │    20 │   30 │    30 │        0 │        897 │   897 │         16 │      16 │        0 │        0 │           0 │        0 │                  0 │
│ heap_caps_init.c.obj                │        961 │    4 │    4 │     0 │    0 │     0 │        0 │        900 │   900 │         57 │      57 │        0 │        0 │           0 │        0 │                  0 │
│ partition.c.obj                     │        889 │    8 │    8 │     0 │    0 │     0 │        0 │        844 │   844 │         37 │      37 │        0 │        0 │           0 │        0 │                  0 │
│ nullfs.c.obj                        │        878 │    4 │    4 │     0 │    0 │     0 │        0 │        746 │   746 │        128 │     128 │        0 │        0 │           0 │        0 │                  0 │
│ multi_heap.c.obj                    │        792 │    0 │    0 │     0 │  515 │   515 │        0 │        228 │   228 │         49 │      49 │        0 │        0 │           0 │        0 │                  0 │
│ clk.c.obj                           │        778 │    0 │    0 │     0 │    0 │     0 │        0 │        765 │   765 │         13 │      13 │        0 │        0 │           0 │        0 │                  0 │
│ log_binary_heap.c.obj               │        760 │  260 │  260 │     0 │    0 │     0 │        0 │        476 │   476 │         24 │      24 │        0 │        0 │           0 │        0 │                  0 │
│ heap_caps.c.obj                     │        744 │    8 │    4 │     4 │  414 │   414 │        0 │        219 │   219 │        103 │     103 │        0 │        0 │           0 │        0 │                  0 │
│ libc_a-fseeko.o                     │        718 │    0 │    0 │     0 │    0 │     0 │        0 │        718 │   718 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
│ libc_a-fvwrite.o                    │        703 │    0 │    0 │     0 │    0 │     0 │        0 │        703 │   703 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
│ esp_rom_gpio.c.obj                  │        686 │    0 │    0 │     0 │  130 │   130 │        0 │          0 │     0 │        556 │     556 │        0 │        0 │           0 │        0 │                  0 │
│ clk_tree_hal.c.obj                  │        679 │    0 │    0 │     0 │    0 │     0 │        0 │        621 │   621 │         58 │      58 │        0 │        0 │           0 │        0 │                  0 │
│ vfs_console.c.obj                   │        677 │   16 │   16 │     0 │    0 │     0 │        0 │        481 │   481 │        180 │     180 │        0 │        0 │           0 │        0 │                  0 │
│ portasm.S.obj                       │        638 │    0 │    0 │     0 │  638 │   638 │        0 │          0 │     0 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
│ esp_cpu_intr.c.obj                  │        611 │    0 │    0 │     0 │    0 │     0 │        0 │         77 │    77 │        534 │     534 │        0 │        0 │           0 │        0 │                  0 │
│ time.c.obj                          │        585 │   20 │   20 │     0 │    0 │     0 │        0 │        565 │   565 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
│ memory_layout_utils.c.obj           │        576 │    0 │    0 │     0 │    0 │     0 │        0 │        549 │   549 │         27 │      27 │        0 │        0 │           0 │        0 │                  0 │
│ system_internal.c.obj               │        533 │    0 │    0 │     0 │  517 │   517 │        0 │          0 │     0 │         16 │      16 │        0 │        0 │           0 │        0 │                  0 │
│ panic_handler.c.obj                 │        521 │    8 │    8 │     0 │   63 │    63 │        0 │        450 │   450 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
│ esp_ipc_isr.c.obj                   │        518 │   44 │   32 │    12 │  409 │   409 │        0 │         35 │    35 │         30 │      30 │        0 │        0 │           0 │        0 │                  0 │
│ esp_clk_tree_common.c.obj           │        511 │    8 │    8 │     0 │    0 │     0 │        0 │        440 │   440 │         63 │      63 │        0 │        0 │           0 │        0 │                  0 │
│ cache_hal_esp32.c.obj               │        499 │   38 │    8 │    30 │  461 │   461 │        0 │          0 │     0 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
│ debug_helpers.c.obj                 │        498 │    0 │    0 │     0 │  498 │   498 │        0 │          0 │     0 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
│ memspi_host_driver.c.obj            │        488 │   95 │    0 │    95 │  393 │   393 │        0 │          0 │     0 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
│ spi_flash_hal.c.obj                 │        484 │    0 │    0 │     0 │    0 │     0 │        0 │        484 │   484 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
│ libc_a-svfiprintf.o                 │        472 │    0 │    0 │     0 │    0 │     0 │        0 │          0 │     0 │        472 │     472 │        0 │        0 │           0 │        0 │                  0 │
│ spi_flash_os_func_app.c.obj         │        469 │   56 │    0 │    56 │  336 │   336 │        0 │         52 │    52 │         25 │      25 │        0 │        0 │           0 │        0 │                  0 │
│ rtc_module.c.obj                    │        459 │   28 │    4 │    24 │  188 │   188 │        0 │        243 │   243 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
│ freertos_hooks.c.obj                │        457 │  136 │  128 │     8 │   43 │    43 │        0 │        278 │   278 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
│ crosscore_int.c.obj                 │        440 │   16 │    8 │     8 │  248 │   248 │        0 │        130 │   130 │         46 │      46 │        0 │        0 │           0 │        0 │                  0 │
│ esp_clk_tree.c.obj                  │        432 │    0 │    0 │     0 │    0 │     0 │        0 │        403 │   403 │         29 │      29 │        0 │        0 │           0 │        0 │                  0 │
│ spi_flash_chip_gd.c.obj             │        430 │  127 │    0 │   127 │  303 │   303 │        0 │          0 │     0 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
│ esp_flash_spi_init.c.obj            │        423 │   84 │    4 │    80 │    0 │     0 │        0 │        301 │   301 │         38 │      38 │        0 │        0 │           0 │        0 │                  0 │
│ newlib_init.c.obj                   │        402 │  144 │    0 │   144 │    0 │     0 │        0 │        258 │   258 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
│ app_startup.c.obj                   │        400 │    1 │    1 │     0 │    0 │     0 │        0 │        367 │   367 │         32 │      32 │        0 │        0 │           0 │        0 │                  0 │
│ xtensa_context.S.obj                │        394 │    0 │    0 │     0 │  394 │   394 │        0 │          0 │     0 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
│ flash_mmap.c.obj                    │        394 │    0 │    0 │     0 │  122 │   122 │        0 │        255 │   255 │         17 │      17 │        0 │        0 │           0 │        0 │                  0 │
│ esp_clk.c.obj                       │        372 │    9 │    0 │     9 │  339 │   339 │        0 │          0 │     0 │          0 │       0 │        0 │        0 │           0 │       24 │                 24 │
│ libc_a-locale.o                     │        368 │    4 │    0 │     4 │    0 │     0 │        0 │          0 │     0 │        364 │     364 │        0 │        0 │           0 │        0 │                  0 │
│ esp_timer_impl_lac.c.obj            │        357 │    0 │    0 │     0 │  114 │   114 │        0 │        243 │   243 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
│ uart_hal_iram.c.obj                 │        356 │    0 │    0 │     0 │    0 │     0 │        0 │        316 │   316 │         40 │      40 │        0 │        0 │           0 │        0 │                  0 │
│ assert.c.obj                        │        352 │    0 │    0 │     0 │  352 │   352 │        0 │          0 │     0 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
│ uart_hal.c.obj                      │        351 │    0 │    0 │     0 │    0 │     0 │        0 │        351 │   351 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
│ brownout.c.obj                      │        350 │   51 │    4 │    47 │  215 │   215 │        0 │         79 │    79 │          5 │       5 │        0 │        0 │           0 │        0 │                  0 │
│ cpu.c.obj                           │        350 │    0 │    0 │     0 │  284 │   284 │        0 │         36 │    36 │         30 │      30 │        0 │        0 │           0 │        0 │                  0 │
│ startup.c.obj                       │        348 │   11 │   11 │     0 │   42 │    42 │        0 │        287 │   287 │          8 │       8 │        0 │        0 │           0 │        0 │                  0 │
│ sleep_modes.c.obj                   │        344 │  120 │    0 │   120 │    0 │     0 │        0 │        162 │   162 │         26 │      26 │        0 │       36 │          36 │        0 │                  0 │
│ int_wdt.c.obj                       │        335 │    9 │    9 │     0 │  104 │   104 │        0 │        222 │   222 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
│ task_wdt_impl_timergroup.c.obj      │        335 │   12 │   12 │     0 │   31 │    31 │        0 │        292 │   292 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
│ libc_a-findfp.o                     │        324 │  324 │  312 │    12 │    0 │     0 │        0 │          0 │     0 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
│ windowspill_asm.o                   │        311 │    0 │    0 │     0 │  311 │   311 │        0 │          0 │     0 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
│ esp_efuse_startup.c.obj             │        302 │    0 │    0 │     0 │    0 │     0 │        0 │        246 │   246 │         56 │      56 │        0 │        0 │           0 │        0 │                  0 │
│ startup_funcs.c.obj                 │        280 │    0 │    0 │     0 │    0 │     0 │        0 │        208 │   208 │         72 │      72 │        0 │        0 │           0 │        0 │                  0 │
│ list.c.obj                          │        279 │    0 │    0 │     0 │  279 │   279 │        0 │          0 │     0 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
│ libc_a-refill.o                     │        277 │    0 │    0 │     0 │    0 │     0 │        0 │        277 │   277 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
│ spi_flash_encrypt_hal_iram.c.obj    │        276 │   36 │    0 │    36 │  240 │   240 │        0 │          0 │     0 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
│ interrupts.c.obj                    │        276 │    0 │    0 │     0 │    0 │     0 │        0 │          0 │     0 │        276 │     276 │        0 │        0 │           0 │        0 │                  0 │
│ sleep_gpio.c.obj                    │        255 │    0 │    0 │     0 │    0 │     0 │        0 │        227 │   227 │         28 │      28 │        0 │        0 │           0 │        0 │                  0 │
│ libc_a-makebuf.o                    │        246 │    0 │    0 │     0 │    0 │     0 │        0 │        246 │   246 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
│ libc_a-impure.o                     │        244 │  244 │    0 │   244 │    0 │     0 │        0 │          0 │     0 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
│ esp_time_impl.c.obj                 │        242 │   12 │   12 │     0 │  122 │   122 │        0 │        108 │   108 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
│ spi_flash_chip_issi.c.obj           │        240 │  129 │    0 │   129 │  111 │   111 │        0 │          0 │     0 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
│ flash_ops.c.obj                     │        238 │   12 │    4 │     8 │   33 │    33 │        0 │        171 │   171 │         22 │      22 │        0 │        0 │           0 │        0 │                  0 │
│ spi_flash_chip_mxic.c.obj           │        238 │  129 │    0 │   129 │  109 │   109 │        0 │          0 │     0 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
│ spi_flash_chip_drivers.c.obj        │        234 │   28 │    0 │    28 │    0 │     0 │        0 │        206 │   206 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
│ libc_a-fopen.o                      │        231 │    0 │    0 │     0 │    0 │     0 │        0 │        231 │   231 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
│ libc_a-reent.o                      │        220 │    0 │    0 │     0 │    0 │     0 │        0 │        220 │   220 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
│ brownout_hal.c.obj                  │        196 │    0 │    0 │     0 │    0 │     0 │        0 │        196 │   196 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
│ regi2c_ctrl.c.obj                   │        188 │    8 │    0 │     8 │  180 │   180 │        0 │          0 │     0 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
│ heap_idf.c.obj                      │        185 │    0 │    0 │     0 │  185 │   185 │        0 │          0 │     0 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
│ esp_ota_ops.c.obj                   │        183 │    4 │    4 │     0 │    0 │     0 │        0 │        149 │   149 │         30 │      30 │        0 │        0 │           0 │        0 │                  0 │
│ libc_a-wsetup.o                     │        168 │    0 │    0 │     0 │    0 │     0 │        0 │        168 │   168 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
│ efuse_hal.c.obj                     │        164 │    0 │    0 │     0 │  164 │   164 │        0 │          0 │     0 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
│ highint_hdl.S.obj                   │        161 │    0 │    0 │     0 │  161 │   161 │        0 │          0 │     0 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
│ chip_info.c.obj                     │        158 │    0 │    0 │     0 │    0 │     0 │        0 │        158 │   158 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
│ abort.c.obj                         │        156 │    0 │    0 │     0 │  156 │   156 │        0 │          0 │     0 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
│ cache_err_int.c.obj                 │        146 │    0 │    0 │     0 │    0 │     0 │        0 │        146 │   146 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
│ partition_target.c.obj              │        146 │    0 │    0 │     0 │    0 │     0 │        0 │        146 │   146 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
│ xtensa_intr.c.obj                   │        143 │    0 │    0 │     0 │   26 │    26 │        0 │        117 │   117 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
│ system_time.c.obj                   │        141 │    8 │    8 │     0 │   31 │    31 │        0 │        102 │   102 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
│ esp_memory_utils.c.obj              │        139 │    0 │    0 │     0 │  139 │   139 │        0 │          0 │     0 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
│ esp_err.c.obj                       │        137 │    0 │    0 │     0 │  137 │   137 │        0 │          0 │     0 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
│ esp_system_chip.c.obj               │        132 │    0 │    0 │     0 │  107 │   107 │        0 │         25 │    25 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
│ heap.c.obj                          │        131 │    0 │    0 │     0 │  131 │   131 │        0 │          0 │     0 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
│ log_lock.c.obj                      │        130 │    4 │    4 │     0 │  126 │   126 │        0 │          0 │     0 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
│ spi_flash_os_func_noos.c.obj        │        130 │   40 │    0 │    40 │   90 │    90 │        0 │          0 │     0 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
│ libc_a-flags.o                      │        129 │    0 │    0 │     0 │    0 │     0 │        0 │        129 │   129 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
│ lab6_1_basic_build.c.obj            │        126 │    0 │    0 │     0 │    0 │     0 │        0 │        126 │   126 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
│ esp_ipc_isr_handler.S.obj           │        123 │   16 │    0 │    16 │  107 │   107 │        0 │          0 │     0 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
│ heap_align_hw.c.obj                 │        118 │    0 │    0 │     0 │  118 │   118 │        0 │          0 │     0 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
│ port_common.c.obj                   │        110 │    0 │    0 │     0 │   80 │    80 │        0 │          0 │     0 │         30 │      30 │        0 │        0 │           0 │        0 │                  0 │
│ log_timestamp.c.obj                 │        108 │    4 │    4 │     0 │  104 │   104 │        0 │          0 │     0 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
│ stdatomic.c.obj                     │        107 │    8 │    0 │     8 │   99 │    99 │        0 │          0 │     0 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
│ esp_system.c.obj                    │        106 │   20 │   20 │     0 │    0 │     0 │        0 │         86 │    86 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
│ esp_cache_msync.c.obj               │        102 │   24 │    0 │    24 │   78 │    78 │        0 │          0 │     0 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
│ libm_a-s_frexp.o                    │         99 │    0 │    0 │     0 │    0 │     0 │        0 │         99 │    99 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
│ esp_rom_uart.c.obj                  │         96 │    0 │    0 │     0 │   96 │    96 │        0 │          0 │     0 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
│ tag_log_level.c.obj                 │         86 │    0 │    0 │     0 │   17 │    17 │        0 │         69 │    69 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
│ flash_brownout_hook.c.obj           │         76 │    2 │    2 │     0 │   74 │    74 │        0 │          0 │     0 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
│ mpu_hal.c.obj                       │         76 │    0 │    0 │     0 │    0 │     0 │        0 │         76 │    76 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
│ esp_ipc_isr_port.c.obj              │         74 │    0 │    0 │     0 │   40 │    40 │        0 │         34 │    34 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
│ ext_mem_layout.c.obj                │         72 │    0 │    0 │     0 │    0 │     0 │        0 │          0 │     0 │         72 │      72 │        0 │        0 │           0 │        0 │                  0 │
│ cpu_region_protect.c.obj            │         71 │    0 │    0 │     0 │    0 │     0 │        0 │         51 │    51 │         20 │      20 │        0 │        0 │           0 │        0 │                  0 │
│ log.c.obj                           │         68 │    0 │    0 │     0 │   68 │    68 │        0 │          0 │     0 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
│ init.c.obj                          │         68 │    0 │    0 │     0 │    0 │     0 │        0 │         44 │    12 │         24 │       8 │        0 │        0 │           0 │        0 │                  0 │
│ cache_esp32.c.obj                   │         67 │    8 │    0 │     8 │   59 │    59 │        0 │          0 │     0 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
│ panic_handler_asm.S.obj             │         64 │    0 │    0 │     0 │   64 │    64 │        0 │          0 │     0 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
│ state_asm--restore_extra_nw.o       │         62 │    0 │    0 │     0 │   62 │    62 │        0 │          0 │     0 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
│ state_asm--save_extra_nw.o          │         62 │    0 │    0 │     0 │   62 │    62 │        0 │          0 │     0 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
│ libc_a-fwalk.o                      │         57 │    0 │    0 │     0 │    0 │     0 │        0 │         57 │    57 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
│ log_linked_list.c.obj               │         55 │    4 │    4 │     0 │    0 │     0 │        0 │         51 │    51 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
│ port_systick.c.obj                  │         50 │    0 │    0 │     0 │   50 │    50 │        0 │          0 │     0 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
│ libc_a-printf.o                     │         50 │    0 │    0 │     0 │    0 │     0 │        0 │         50 │    50 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
│ reent_init.c.obj                    │         45 │    0 │    0 │     0 │    0 │     0 │        0 │         45 │    45 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
│ gpio_periph.c.obj                   │         40 │   40 │    0 │    40 │    0 │     0 │        0 │          0 │     0 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
│ esp_timer_init.c.obj                │         38 │    0 │    0 │     0 │    0 │     0 │        0 │         30 │    30 │          8 │       8 │        0 │        0 │           0 │        0 │                  0 │
│ dport_access.c.obj                  │         37 │    0 │    0 │     0 │   37 │    37 │        0 │          0 │     0 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
│ xtensa_init.c.obj                   │         36 │    4 │    4 │     0 │   32 │    32 │        0 │          0 │     0 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
│ esp_gpio_reserve.c.obj              │         36 │    8 │    0 │     8 │    0 │     0 │        0 │         28 │    28 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
│ libc_a-vprintf.o                    │         36 │    0 │    0 │     0 │    0 │     0 │        0 │         36 │    36 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
│ libc_a-sprint_r.o                   │         34 │    0 │    0 │     0 │    0 │     0 │        0 │         34 │    34 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
│ sar_periph_ctrl.c.obj               │         32 │    0 │    0 │     0 │    0 │     0 │        0 │         32 │    32 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
│ libc_a-mbtowc_r.o                   │         32 │    0 │    0 │     0 │    0 │     0 │        0 │         32 │    32 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
│ interrupts--intlevel.o              │         32 │    0 │    0 │     0 │    0 │     0 │        0 │          0 │     0 │         32 │      32 │        0 │        0 │           0 │        0 │                  0 │
│ bootloader_efuse.c.obj              │         30 │    0 │    0 │     0 │   30 │    30 │        0 │          0 │     0 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
│ esp_cache_utils.c.obj               │         30 │    0 │    0 │     0 │   30 │    30 │        0 │          0 │     0 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
│ log_level.c.obj                     │         29 │    4 │    0 │     4 │    0 │     0 │        0 │         25 │    25 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
│ debug_helpers_asm.S.obj             │         29 │    0 │    0 │     0 │   29 │    29 │        0 │          0 │     0 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
│ syscalls.c.obj                      │         25 │    0 │    0 │     0 │    0 │     0 │        0 │         25 │    25 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
│ libc_a-sysfcntl.o                   │         25 │    0 │    0 │     0 │    0 │     0 │        0 │         25 │    25 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
│ libc_a-sysgettod.o                  │         24 │    0 │    0 │     0 │    0 │     0 │        0 │         24 │    24 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
│ reent_syscalls.c.obj                │         22 │    0 │    0 │     0 │    0 │     0 │        0 │         22 │    22 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
│ libc_a-fseek.o                      │         21 │    0 │    0 │     0 │    0 │     0 │        0 │         21 │    21 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
│ esp_rom_sys.c.obj                   │         19 │    0 │    0 │     0 │   19 │    19 │        0 │          0 │     0 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
│ libc_a-localeconv.o                 │         19 │    0 │    0 │     0 │    0 │     0 │        0 │         19 │    19 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
│ util.c.obj                          │         18 │    4 │    4 │     0 │   14 │    14 │        0 │          0 │     0 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
│ libc_a-errno.o                      │         13 │    0 │    0 │     0 │    0 │     0 │        0 │         13 │    13 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
│ esp_ipc_isr_routines.S.obj          │         10 │    0 │    0 │     0 │   10 │    10 │        0 │          0 │     0 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
│ flash_encrypt.c.obj                 │         10 │    0 │    0 │     0 │   10 │    10 │        0 │          0 │     0 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
│ esp_efuse_api.c.obj                 │         10 │    0 │    0 │     0 │    0 │     0 │        0 │         10 │    10 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
│ pthread.c.obj                       │         10 │    0 │    0 │     0 │    0 │     0 │        0 │         10 │     5 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
│ int_asm--set_intclear.o             │          8 │    0 │    0 │     0 │    8 │     8 │        0 │          0 │     0 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
│ bootloader_mem.c.obj                │          8 │    0 │    0 │     0 │    0 │     0 │        0 │          8 │     8 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
│ esp_efuse_utility.c.obj             │          7 │    0 │    0 │     0 │    0 │     0 │        0 │          7 │     7 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
│ ubsan.c.obj                         │          5 │    0 │    0 │     0 │    5 │     5 │        0 │          0 │     0 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
│ clk_utils.c.obj                     │          5 │    0 │    0 │     0 │    5 │     5 │        0 │          0 │     0 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
│ getentropy.c.obj                    │          5 │    0 │    0 │     0 │    0 │     0 │        0 │          5 │     5 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
│ pthread_cond_var.c.obj              │          5 │    0 │    0 │     0 │    0 │     0 │        0 │          5 │     5 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
│ pthread_local_storage.c.obj         │          5 │    0 │    0 │     0 │    0 │     0 │        0 │          5 │     5 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
│ pthread_rwlock.c.obj                │          5 │    0 │    0 │     0 │    0 │     0 │        0 │          5 │     5 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
│ pthread_semaphore.c.obj             │          5 │    0 │    0 │     0 │    0 │     0 │        0 │          5 │     5 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
│ cxx_guards.cpp.obj                  │          5 │    0 │    0 │     0 │    0 │     0 │        0 │          5 │     5 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
│ cxx_init.cpp.obj                    │          5 │    0 │    0 │     0 │    0 │     0 │        0 │          5 │     5 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
│ nvs_sec_provider.c.obj              │          5 │    0 │    0 │     0 │    0 │     0 │        0 │          5 │     5 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
│ phy_override.c.obj                  │          5 │    0 │    0 │     0 │    0 │     0 │        0 │          5 │     5 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
│ log_write.c.obj                     │          4 │    4 │    0 │     4 │    0 │     0 │        0 │          0 │     0 │          0 │       0 │        0 │        0 │           0 │        0 │                  0 │
│ spi_bus_lock.c.obj                  │          4 │    0 │    0 │     0 │    0 │     0 │        0 │          0 │     0 │          4 │       4 │        0 │        0 │           0 │        0 │                  0 │
└─────────────────────────────────────┴────────────┴──────┴──────┴───────┴──────┴───────┴──────────┴────────────┴───────┴────────────┴─────────┴──────────┴──────────┴─────────────┴──────────┴────────────────────┘
```
[size-files.txt](size-files.txt)

### การ Flash และทดสอบ (ต้องออกจาก Docker หรือใช้ QEMU)
```c
idf.py qemu 
```
#### Result
<img width="1224" height="903" alt="image" src="https://github.com/user-attachments/assets/c77a0bd1-a631-4d84-94ed-054a46a0aef0" />

```c
root@9353b4f3ecf3:/project/lab6_1_basic_build# idf.py qemu
Adding "qemu"'s dependency "all" to list of commands with default set of options.
Executing action: all (aliases: build)
Running ninja in directory /project/lab6_1_basic_build/build
Executing "ninja all"...
[1/4] cd /project/lab6_1_basic_build/build/esp-idf/esptool_py &...able.bin /project/lab6_1_basic_build/build/lab1_basic_build.bin 
lab1_basic_build.bin binary size 0x279c0 bytes. Smallest app partition is 0x100000 bytes. 0xd8640 bytes (85%) free.
[1/1] cd /project/lab6_1_basic_build/build/bootloader/esp-idf/e...000 /project/lab6_1_basic_build/build/bootloader/bootloader.bin 
Bootloader binary size 0x66a0 bytes. 0x960 bytes (8%) free.
[4/4] Completed 'bootloader'Executing action: qemu
Generating flash image: /project/lab6_1_basic_build/build/qemu_flash.bin
esptool.py --chip=esp32 merge_bin --output=/project/lab6_1_basic_build/build/qemu_flash.bin --fill-flash-size=2MB --flash_mode dio --flash_freq 40m --flash_size 2MB 0x1000 bootloader/bootloader.bin 0x10000 lab1_basic_build.bin 0x8000 partition_table/partition-table.bin
esptool.py v4.9.0
SHA digest in image updated
Wrote 0x200000 bytes to file /project/lab6_1_basic_build/build/qemu_flash.bin, ready to flash to offset 0x0
Generating efuse image: /project/lab6_1_basic_build/build/qemu_efuse.bin
Running qemu (fg): qemu-system-xtensa -M esp32 -m 4M -drive file=/project/lab6_1_basic_build/build/qemu_flash.bin,if=mtd,format=raw -drive file=/project/lab6_1_basic_build/build/qemu_efuse.bin,if=none,format=raw,id=efuse -global driver=nvram.esp32.efuse,property=drive,value=efuse -global driver=timer.esp32.timg,property=wdt_disable,value=true -nic user,model=open_eth -nographic -serial mon:stdio
Adding SPI flash device
ets Jul 29 2019 12:21:46

rst:0x1 (POWERON_RESET),boot:0x12 (SPI_FAST_FLASH_BOOT)
configsip: 0, SPIWP:0xee
clk_drv:0x00,q_drv:0x00,d_drv:0x00,cs0_drv:0x00,hd_drv:0x00,wp_drv:0x00
mode:DIO, clock div:2
load:0x3fff0030,len:6372
load:0x40078000,len:15928
load:0x40080400,len:3880
entry 0x40080638
I (1154) boot: ESP-IDF v6.0-dev-1002-gbfe5caf58f 2nd stage bootloader
I (1157) boot: compile time Aug  6 2025 02:55:00
I (1158) boot: Multicore bootloader
I (1652) boot: chip revision: v3.0
I (1656) boot.esp32: SPI Speed      : 40MHz
I (1657) boot.esp32: SPI Mode       : DIO
I (1657) boot.esp32: SPI Flash Size : 2MB
I (1727) boot: Enabling RNG early entropy source...
I (1791) boot: Partition Table:
I (1792) boot: ## Label            Usage          Type ST Offset   Length
I (1793) boot:  0 nvs              WiFi data        01 02 00009000 00006000
I (1794) boot:  1 phy_init         RF data          01 01 0000f000 00001000
I (1795) boot:  2 factory          factory app      00 00 00010000 00100000
I (1867) boot: End of partition table
I (2376) esp_image: segment 0: paddr=00010020 vaddr=3f400020 size=09484h ( 38020) map
I (2667) esp_image: segment 1: paddr=000194ac vaddr=3ff80000 size=00024h (    36) load
I (2891) esp_image: segment 2: paddr=000194d8 vaddr=3ffb0000 size=025e0h (  9696) load
I (3128) esp_image: segment 3: paddr=0001bac0 vaddr=40080000 size=04558h ( 17752) load
I (3355) esp_image: segment 4: paddr=00020020 vaddr=400d0020 size=0ef10h ( 61200) map
I (3611) esp_image: segment 5: paddr=0002ef38 vaddr=40084558 size=08a60h ( 35424) load
I (4301) boot: Loaded app from partition at offset 0x10000
I (4301) boot: Disabling RNG early entropy source...
I (4379) cpu_start: Multicore app
I (8222) cpu_start: Pro cpu start user code
I (8224) cpu_start: cpu freq: 160000000 Hz
I (8225) app_init: Application information:
I (8226) app_init: Project name:     lab1_basic_build
I (8228) app_init: App version:      1
I (8229) app_init: Compile time:     Aug  6 2025 02:54:16
I (8231) app_init: ELF file SHA256:  202810b28...
I (8233) app_init: ESP-IDF:          v6.0-dev-1002-gbfe5caf58f
I (8233) efuse_init: Min chip rev:     v0.0
I (8233) efuse_init: Max chip rev:     v3.99
I (8234) efuse_init: Chip rev:         v3.0
I (8236) heap_init: Initializing. RAM available for dynamic allocation:
I (8237) heap_init: At 3FFAE6E0 len 00001920 (6 KiB): DRAM
I (8238) heap_init: At 3FFB2EA8 len 0002D158 (180 KiB): DRAM
I (8238) heap_init: At 3FFE0440 len 00003AE0 (14 KiB): D/IRAM
I (8238) heap_init: At 3FFE4350 len 0001BCB0 (111 KiB): D/IRAM
I (8239) heap_init: At 4008CFB8 len 00013048 (76 KiB): IRAM
I (8302) spi_flash: detected chip: winbond
I (8307) spi_flash: flash io: dio
I (8328) main_task: Started on CPU0
I (8328) main_task: Calling app_main()
I (8328) LAB6_1: Lab 6.1: Basic ESP32 Project Structure
I (8338) LAB6_1: ESP-IDF Version: v6.0-dev-1002-gbfe5caf58f
I (8338) LAB6_1: Free heap size: 304636 bytes
I (8338) LAB6_1: Build system test - Counter: 0
I (10338) LAB6_1: Build system test - Counter: 1
I (12338) LAB6_1: Build system test - Counter: 2
I (14338) LAB6_1: Build system test - Counter: 3
I (16338) LAB6_1: Build system test - Counter: 4
I (18338) LAB6_1: Build system test - Counter: 5
I (20338) LAB6_1: Build system test - Counter: 6
I (22338) LAB6_1: Build system test - Counter: 7
I (24338) LAB6_1: Build system test - Counter: 8
I (26338) LAB6_1: Build system test - Counter: 9
I (28338) LAB6_1: Build system test - Counter: 10
I (30338) LAB6_1: Build system test - Counter: 11
I (32338) LAB6_1: Build system test - Counter: 12
I (34338) LAB6_1: Build system test - Counter: 13
I (36338) LAB6_1: Build system test - Counter: 14
I (38338) LAB6_1: Build system test - Counter: 15
I (40338) LAB6_1: Build system test - Counter: 16
I (42338) LAB6_1: Build system test - Counter: 17
I (44338) LAB6_1: Build system test - Counter: 18
I (46338) LAB6_1: Build system test - Counter: 19
I (48338) LAB6_1: Build system test - Counter: 20
I (50338) LAB6_1: Build system test - Counter: 21
I (52338) LAB6_1: Build system test - Counter: 22
I (54338) LAB6_1: Build system test - Counter: 23
I (56338) LAB6_1: Build system test - Counter: 24
I (58338) LAB6_1: Build system test - Counter: 25
I (60338) LAB6_1: Build system test - Counter: 26
I (62338) LAB6_1: Build system test - Counter: 27
I (64338) LAB6_1: Build system test - Counter: 28
I (66338) LAB6_1: Build system test - Counter: 29
I (68338) LAB6_1: Build system test - Counter: 30
I (70338) LAB6_1: Build system test - Counter: 31
I (72338) LAB6_1: Build system test - Counter: 32
I (74338) LAB6_1: Build system test - Counter: 33
I (76338) LAB6_1: Build system test - Counter: 34
I (78338) LAB6_1: Build system test - Counter: 35
I (80338) LAB6_1: Build system test - Counter: 36
I (82338) LAB6_1: Build system test - Counter: 37
I (84338) LAB6_1: Build system test - Counter: 38
I (86338) LAB6_1: Build system test - Counter: 39
I (88338) LAB6_1: Build system test - Counter: 40

```
## การทดลองเพิ่มเติม
1. เพิ่ม Build Information (ใน Docker Container)
แก้ไข main/lab6_1_basic_build.c:

```
# เข้า container (ถ้ายังไม่ได้เข้า)
docker-compose exec esp32-dev bash
source $IDF_PATH/export.sh
cd lab6_1_basic_build
```
# แก้ไขไฟล์
```c
#include <stdio.h>
#include "freertos/FreeRTOS.h"
#include "freertos/task.h"
#include "esp_system.h"
#include "esp_log.h"

static const char *TAG = "LAB1";

void print_build_info(void)
{
    ESP_LOGI(TAG, "=== Build Information ===");
    ESP_LOGI(TAG, "Project Name: lab6_1_basic_build");
    ESP_LOGI(TAG, "ESP-IDF Version: %s", esp_get_idf_version());
    ESP_LOGI(TAG, "Compile Date: %s", __DATE__);
    ESP_LOGI(TAG, "Compile Time: %s", __TIME__);
    ESP_LOGI(TAG, "Chip Model: %s", CONFIG_IDF_TARGET);
    ESP_LOGI(TAG, "Free Heap: %d bytes", esp_get_free_heap_size());
}

void app_main(void)
{
    print_build_info();
    
    int counter = 0;
    
    while (1) {
        ESP_LOGI(TAG, "Running... Counter: %d", counter++);
        
        // แสดงสถานะ memory ทุกๆ 10 ครั้ง
        if (counter % 10 == 0) {
            ESP_LOGI(TAG, "Current free heap: %d bytes", esp_get_free_heap_size());
        }
        
        vTaskDelay(pdMS_TO_TICKS(1000));
    }
}
```
### บันทึกผลการ simulate ในโฟลเดอร์ส่งงาน
<img width="1215" height="905" alt="image" src="https://github.com/user-attachments/assets/91acfb14-4173-4a95-906c-c602443eaafb" />

```c
I (1252) boot: ESP-IDF v6.0-dev-1002-gbfe5caf58f 2nd stage bootloader
I (1256) boot: compile time Aug  6 2025 02:55:00
I (1257) boot: Multicore bootloader
I (1836) boot: chip revision: v3.0
I (1842) boot.esp32: SPI Speed      : 40MHz
I (1844) boot.esp32: SPI Mode       : DIO
I (1846) boot.esp32: SPI Flash Size : 2MB
I (1924) boot: Enabling RNG early entropy source...
I (2025) boot: Partition Table:
I (2026) boot: ## Label            Usage          Type ST Offset   Length
I (2026) boot:  0 nvs              WiFi data        01 02 00009000 00006000
I (2028) boot:  1 phy_init         RF data          01 01 0000f000 00001000
I (2029) boot:  2 factory          factory app      00 00 00010000 00100000
I (2135) boot: End of partition table
I (2770) esp_image: segment 0: paddr=00010020 vaddr=3f400020 size=09534h ( 38196) map
I (3088) esp_image: segment 1: paddr=0001955c vaddr=3ff80000 size=00024h (    36) load
I (3428) esp_image: segment 2: paddr=00019588 vaddr=3ffb0000 size=025e0h (  9696) load
I (3706) esp_image: segment 3: paddr=0001bb70 vaddr=40080000 size=044a8h ( 17576) load
I (3990) esp_image: segment 4: paddr=00020020 vaddr=400d0020 size=0efb8h ( 61368) map
I (4274) esp_image: segment 5: paddr=0002efe0 vaddr=400844a8 size=08b10h ( 35600) load
I (5331) boot: Loaded app from partition at offset 0x10000
I (5332) boot: Disabling RNG early entropy source...
I (5433) cpu_start: Multicore app
I (10287) cpu_start: Pro cpu start user code
I (10290) cpu_start: cpu freq: 160000000 Hz
I (10291) app_init: Application information:
I (10291) app_init: Project name:     lab1_basic_build
I (10292) app_init: App version:      1
I (10294) app_init: Compile time:     Aug  6 2025 02:54:16
I (10295) app_init: ELF file SHA256:  86f8f58bd...
I (10296) app_init: ESP-IDF:          v6.0-dev-1002-gbfe5caf58f
I (10296) efuse_init: Min chip rev:     v0.0
I (10297) efuse_init: Max chip rev:     v3.99
I (10298) efuse_init: Chip rev:         v3.0
I (10300) heap_init: Initializing. RAM available for dynamic allocation:
I (10302) heap_init: At 3FFAE6E0 len 00001920 (6 KiB): DRAM
I (10303) heap_init: At 3FFB2EA8 len 0002D158 (180 KiB): DRAM
I (10303) heap_init: At 3FFE0440 len 00003AE0 (14 KiB): D/IRAM
I (10304) heap_init: At 3FFE4350 len 0001BCB0 (111 KiB): D/IRAM
I (10304) heap_init: At 4008CFB8 len 00013048 (76 KiB): IRAM
I (10388) spi_flash: detected chip: winbond
I (10406) spi_flash: flash io: dio
I (10436) main_task: Started on CPU0
I (10456) main_task: Calling app_main()
I (10466) LAB1: === Build Information ===
I (10466) LAB1: Project Name: lab6_1_basic_build
I (10466) LAB1: ESP-IDF Version: v6.0-dev-1002-gbfe5caf58f
I (10466) LAB1: Compile Date: Aug  6 2025
I (10466) LAB1: Compile Time: 03:40:23
I (10466) LAB1: Chip Model: esp32
I (10466) LAB1: Free Heap: 304636 bytes
I (10466) LAB1: Running... Counter: 0
I (11466) LAB1: Running... Counter: 1
I (12466) LAB1: Running... Counter: 2
I (13466) LAB1: Running... Counter: 3
I (14466) LAB1: Running... Counter: 4
I (15466) LAB1: Running... Counter: 5
I (16466) LAB1: Running... Counter: 6
I (17466) LAB1: Running... Counter: 7
```

## คำถามทบทวน
1. Docker vs Native Setup: อธิบายข้อดีของการใช้ Docker เปรียบเทียบกับการติดตั้ง ESP-IDF บน host system
  - **Ans:**  
    - Docker: ติดตั้งง่าย, ย้ายเครื่องสะดวก, แยกจากระบบหลัก,สภาพแวดล้อมเหมือนกันทุกเครื่อ
    - Native: เข้าถึง hardware โดยตรง, เร็วกว่าเล็กน้อย, เหมาะกับ dev ที่ชำนาญ
2. Build Process: อธิบายขั้นตอนการ build ของ ESP-IDF ใน Docker container ตั้งแต่ source code จนได้ binary
  - **Ans:**
      - เข้า container: `docker-compose exec esp32-dev bash`
      - ตั้งค่า environment: `source $IDF_PATH/export.sh`
      - สร้างโปรเจกต์
      - Build:
        - `idf.py set-target esp32` – ตั้งเป้าหมาย MCU
        - `idf.py build` – compile + link → ได้ .elf + .bin
      - ตรวจสอบขนาด:` idf.py size`, `idf.py size-components`, `idf.py size-files`
3. CMake Files: บทบาทของไฟล์ CMakeLists.txt แต่ละไฟล์คืออะไร และทำงานอย่างไรใน Docker environment?
  - **Ans:**
      - Top-level CMakeLists.txt
        - ระบุชื่อโปรเจกต์
        - include ระบบ build ของ ESP-IDF

      - main/CMakeLists.txt
        - ลงทะเบียน component
        - ระบุ source file และ include dir
      - ทำงานใน Docker: idf.py เรียก cmake โดยใช้ไฟล์เหล่านี้สร้าง build system
4. Git Ignore: ไฟล์ .gitignore มีความสำคัญอย่างไรสำหรับ ESP32 project development?
  - **Ans:**
    - กันไม่ให้ไฟล์ชั่วคราว, ไฟล์ใหญ่ หรือข้อมูลลับ (เช่น build/, *.bin, *.key) ถูก push ขึ้น Git
    - ช่วยให้โปรเจกต์สะอาด และทำงานร่วมกับทีมได้ดี
5. Container Persistence: ข้อมูลใดบ้างที่จะหายไปเมื่อ restart container และข้อมูลใดที่จะอยู่ต่อ?
  - **Ans:**
    - ข้อมูลที่หาย: ไฟล์ใน container (เช่น build/ ถ้าไม่ mount)
    - ข้อมูลที่อยู่ต่อ: ไฟล์ที่ mount จาก host (source code, .gitignore, CMakeLists.txt) <br>
    * หมายเหตุ: Docker ใช้ volume mapping เช่น .:/project เพื่อให้ไฟล์อยู่ต่อได้
6. Development Workflow: เปรียบเทียบ workflow การพัฒนาระหว่างการใช้ Docker กับการทำงานบน native system
  - **Ans:**

    | หัวข้อ          | Docker             | Native                 |
    | --------------- | ------------------ | ---------------------- |
    | Setup           | เร็ว, ใช้งานง่าย   | ต้องติดตั้งหลายขั้นตอน |
    | ความเสถียร      | สภาพแวดล้อมคงที่   | อาจพังเพราะอัพเดต OS   |
    | Access hardware | ต้อง map USB       | เข้าถึงได้ทันที        |
    | การย้ายเครื่อง  | ง่าย แค่ย้าย image | ต้อง setup ใหม่        |

# Lab 6.2: Add Source Files to Project
## ทดสอบ Build และ Run (ครั้งที่ 1)
### Result
```c
rst:0x1 (POWERON_RESET),boot:0x12 (SPI_FAST_FLASH_BOOT)
configsip: 0, SPIWP:0xee
clk_drv:0x00,q_drv:0x00,d_drv:0x00,cs0_drv:0x00,hd_drv:0x00,wp_drv:0x00
mode:DIO, clock div:2
load:0x3fff0030,len:6372
load:0x40078000,len:15928
load:0x40080400,len:3880
entry 0x40080638
I (1180) boot: ESP-IDF v6.0-dev-1002-gbfe5caf58f 2nd stage bootloader
I (1183) boot: compile time Aug  6 2025 09:30:58
I (1184) boot: Multicore bootloader
I (1841) boot: chip revision: v3.0
I (1845) boot.esp32: SPI Speed      : 40MHz
I (1846) boot.esp32: SPI Mode       : DIO
I (1847) boot.esp32: SPI Flash Size : 2MB
I (1926) boot: Enabling RNG early entropy source...
I (2009) boot: Partition Table:
I (2010) boot: ## Label            Usage          Type ST Offset   Length
I (2011) boot:  0 nvs              WiFi data        01 02 00009000 00006000
I (2012) boot:  1 phy_init         RF data          01 01 0000f000 00001000
I (2013) boot:  2 factory          factory app      00 00 00010000 00100000
I (2088) boot: End of partition table
I (2703) esp_image: segment 0: paddr=00010020 vaddr=3f400020 size=09634h ( 38452) map
I (3010) esp_image: segment 1: paddr=0001965c vaddr=3ff80000 size=00024h (    36) load
I (3303) esp_image: segment 2: paddr=00019688 vaddr=3ffb0000 size=025e0h (  9696) load
I (3583) esp_image: segment 3: paddr=0001bc70 vaddr=40080000 size=043a8h ( 17320) load
I (3878) esp_image: segment 4: paddr=00020020 vaddr=400d0020 size=0f0ach ( 61612) map
I (4197) esp_image: segment 5: paddr=0002f0d4 vaddr=400843a8 size=08c58h ( 35928) load
I (5051) boot: Loaded app from partition at offset 0x10000
I (5052) boot: Disabling RNG early entropy source...
I (5140) cpu_start: Multicore app
I (9734) cpu_start: Pro cpu start user code
I (9736) cpu_start: cpu freq: 160000000 Hz
I (9737) app_init: Application information:
I (9737) app_init: Project name:     lab6_2_multiple_files
I (9738) app_init: App version:      1
I (9739) app_init: Compile time:     Aug  6 2025 09:32:23
I (9739) app_init: ELF file SHA256:  16fc844d9...
I (9740) app_init: ESP-IDF:          v6.0-dev-1002-gbfe5caf58f
I (9741) efuse_init: Min chip rev:     v0.0
I (9741) efuse_init: Max chip rev:     v3.99
I (9742) efuse_init: Chip rev:         v3.0
I (9744) heap_init: Initializing. RAM available for dynamic allocation:
I (9746) heap_init: At 3FFAE6E0 len 00001920 (6 KiB): DRAM
I (9748) heap_init: At 3FFB2EA8 len 0002D158 (180 KiB): DRAM
I (9749) heap_init: At 3FFE0440 len 00003AE0 (14 KiB): D/IRAM
I (9750) heap_init: At 3FFE4350 len 0001BCB0 (111 KiB): D/IRAM
I (9752) heap_init: At 4008D000 len 00013000 (76 KiB): IRAM
I (9821) spi_flash: detected chip: winbond
I (9831) spi_flash: flash io: dio
I (9847) main_task: Started on CPU0
I (9857) main_task: Calling app_main()
I (9857) MAIN: 🚀 Lab 6.2: Multiple Source Files Demo
I (9857) MAIN: 📍 Main function from file: ./main/lab6_2_multiple_files.c, line: 13
I (9857) MAIN: ESP-IDF Version: v6.0-dev-1002-gbfe5caf58f
I (9867) SENSOR: 🔧 Sensor initialized from file: ./main/sensor.c, line: 12
I (9867) SENSOR: 📡 Sensor module ready for operation
I (9867) MAIN: === Loop 0 ===
I (9867) SENSOR: 📊 Reading sensor data from file: ./main/sensor.c, line: 18
I (9867) SENSOR: 🌡️  Temperature: 30.5°C
I (9877) SENSOR: 💧 Humidity: 93.6%
I (11877) MAIN: === Loop 1 ===
I (11877) SENSOR: 📊 Reading sensor data from file: ./main/sensor.c, line: 18
I (11877) SENSOR: 🌡️  Temperature: 33.9°C
I (11877) SENSOR: 💧 Humidity: 96.5%
I (13877) MAIN: === Loop 2 ===
I (13877) SENSOR: 📊 Reading sensor data from file: ./main/sensor.c, line: 18
I (13877) SENSOR: 🌡️  Temperature: 32.6°C
I (13877) SENSOR: 💧 Humidity: 82.5%
I (13877) SENSOR: ✅ Sensor status check from file: ./main/sensor.c, line: 30
I (13877) SENSOR: 📈 All sensors operating normally
I (15877) MAIN: === Loop 3 ===
I (15877) SENSOR: 📊 Reading sensor data from file: ./main/sensor.c, line: 18
I (15877) SENSOR: 🌡️  Temperature: 26.7°C
I (15877) SENSOR: 💧 Humidity: 93.4%
I (17877) MAIN: === Loop 4 ===
I (17877) SENSOR: 📊 Reading sensor data from file: ./main/sensor.c, line: 18
I (17877) SENSOR: 🌡️  Temperature: 25.5°C
I (17877) SENSOR: 💧 Humidity: 66.4%
I (19877) MAIN: === Loop 5 ===
I (19877) SENSOR: 📊 Reading sensor data from file: ./main/sensor.c, line: 18
I (19877) SENSOR: 🌡️  Temperature: 26.6°C
I (19877) SENSOR: 💧 Humidity: 73.3%
I (19877) SENSOR: ✅ Sensor status check from file: ./main/sensor.c, line: 30
I (19877) SENSOR: 📈 All sensors operating normally
```
## ทดสอบ Build และ Run (ครั้งที่ 2)
### Result
```c
rst:0x1 (POWERON_RESET),boot:0x12 (SPI_FAST_FLASH_BOOT)
configsip: 0, SPIWP:0xee
clk_drv:0x00,q_drv:0x00,d_drv:0x00,cs0_drv:0x00,hd_drv:0x00,wp_drv:0x00
mode:DIO, clock div:2
load:0x3fff0030,len:6372
load:0x40078000,len:15928
load:0x40080400,len:3880
entry 0x40080638
I (1184) boot: ESP-IDF v6.0-dev-1002-gbfe5caf58f 2nd stage bootloader
I (1186) boot: compile time Aug  6 2025 09:30:58
I (1186) boot: Multicore bootloader
I (1910) boot: chip revision: v3.0
I (1914) boot.esp32: SPI Speed      : 40MHz
I (1916) boot.esp32: SPI Mode       : DIO
I (1921) boot.esp32: SPI Flash Size : 2MB
I (2054) boot: Enabling RNG early entropy source...
I (2152) boot: Partition Table:
I (2153) boot: ## Label            Usage          Type ST Offset   Length
I (2154) boot:  0 nvs              WiFi data        01 02 00009000 00006000
I (2156) boot:  1 phy_init         RF data          01 01 0000f000 00001000
I (2157) boot:  2 factory          factory app      00 00 00010000 00100000
I (2249) boot: End of partition table
I (2921) esp_image: segment 0: paddr=00010020 vaddr=3f400020 size=09824h ( 38948) map
I (3338) esp_image: segment 1: paddr=0001984c vaddr=3ff80000 size=00024h (    36) load
I (3679) esp_image: segment 2: paddr=00019878 vaddr=3ffb0000 size=025e0h (  9696) load
I (4001) esp_image: segment 3: paddr=0001be60 vaddr=40080000 size=041b8h ( 16824) load
I (4325) esp_image: segment 4: paddr=00020020 vaddr=400d0020 size=0f230h ( 62000) map
I (4639) esp_image: segment 5: paddr=0002f258 vaddr=400841b8 size=08e48h ( 36424) load
I (5910) boot: Loaded app from partition at offset 0x10000
I (5911) boot: Disabling RNG early entropy source...
I (6013) cpu_start: Multicore app
I (11483) cpu_start: Pro cpu start user code
I (11487) cpu_start: cpu freq: 160000000 Hz
I (11488) app_init: Application information:
I (11488) app_init: Project name:     lab6_2_multiple_files
I (11489) app_init: App version:      1
I (11490) app_init: Compile time:     Aug  6 2025 09:32:23
I (11490) app_init: ELF file SHA256:  17eccce31...
I (11491) app_init: ESP-IDF:          v6.0-dev-1002-gbfe5caf58f
I (11492) efuse_init: Min chip rev:     v0.0
I (11492) efuse_init: Max chip rev:     v3.99
I (11493) efuse_init: Chip rev:         v3.0
I (11495) heap_init: Initializing. RAM available for dynamic allocation:
I (11497) heap_init: At 3FFAE6E0 len 00001920 (6 KiB): DRAM
I (11498) heap_init: At 3FFB2EA8 len 0002D158 (180 KiB): DRAM
I (11499) heap_init: At 3FFE0440 len 00003AE0 (14 KiB): D/IRAM
I (11500) heap_init: At 3FFE4350 len 0001BCB0 (111 KiB): D/IRAM
I (11502) heap_init: At 4008D000 len 00013000 (76 KiB): IRAM
I (11570) spi_flash: detected chip: winbond
I (11588) spi_flash: flash io: dio
I (11604) main_task: Started on CPU0
I (11614) main_task: Calling app_main()
I (11614) MAIN: 🚀 Lab 6.2: Multiple Source Files Demo
I (11614) MAIN: 📍 Main function from file: ./main/lab6_2_multiple_files.c, line: 14
I (11614) MAIN: ESP-IDF Version: v6.0-dev-1002-gbfe5caf58f
I (11624) SENSOR: 🔧 Sensor initialized from file: ./main/sensor.c, line: 12
I (11624) SENSOR: 📡 Sensor module ready for operation
I (11624) DISPLAY: 🖥️  Display initialized from file: ./main/display.c, line: 9
I (11624) DISPLAY: 💡 Display module ready
I (11634) DISPLAY: 📢 Displaying from file: ./main/display.c, line: 15
I (11634) DISPLAY: 📺 Message: System Starting...
I (11634) MAIN: === Loop 0 ===
I (11634) DISPLAY: 🧹 Screen cleared from file: ./main/display.c, line: 28
I (11634) DISPLAY: ✨ Display ready for new content
I (11634) SENSOR: 📊 Reading sensor data from file: ./main/sensor.c, line: 18
I (11634) SENSOR: 🌡️  Temperature: 26.4°C
I (11644) SENSOR: 💧 Humidity: 68.4%
I (11644) DISPLAY: 📊 Data display from file: ./main/display.c, line: 21
I (11654) DISPLAY: 📈 Value 1: 26.50
I (11654) DISPLAY: 📉 Value 2: 61.00
I (13654) MAIN: === Loop 1 ===
I (13654) DISPLAY: 🧹 Screen cleared from file: ./main/display.c, line: 28
I (13654) DISPLAY: ✨ Display ready for new content
I (13654) SENSOR: 📊 Reading sensor data from file: ./main/sensor.c, line: 18
I (13654) SENSOR: 🌡️  Temperature: 34.4°C
I (13654) SENSOR: 💧 Humidity: 83.1%
I (13654) DISPLAY: 📊 Data display from file: ./main/display.c, line: 21
I (13654) DISPLAY: 📈 Value 1: 27.50
I (13654) DISPLAY: 📉 Value 2: 62.00
I (15654) MAIN: === Loop 2 ===
I (15654) DISPLAY: 🧹 Screen cleared from file: ./main/display.c, line: 28
I (15654) DISPLAY: ✨ Display ready for new content
I (15654) SENSOR: 📊 Reading sensor data from file: ./main/sensor.c, line: 18
I (15654) SENSOR: 🌡️  Temperature: 32.5°C
I (15654) SENSOR: 💧 Humidity: 82.8%
I (15654) DISPLAY: 📊 Data display from file: ./main/display.c, line: 21
I (15654) DISPLAY: 📈 Value 1: 28.50
I (15654) DISPLAY: 📉 Value 2: 63.00
I (15654) SENSOR: ✅ Sensor status check from file: ./main/sensor.c, line: 30
I (15664) SENSOR: 📈 All sensors operating normally
I (15664) DISPLAY: 📢 Displaying from file: ./main/display.c, line: 15
I (15664) DISPLAY: 📺 Message: Status Check Complete
```
##  แบบฝึกหัดเพิ่มเติม: เพิ่มไฟล์ LED.c
### - `idf.py size`
```c
Executing action: size
Running ninja in directory /project/lab6_2_multiple_files/build
Executing "ninja all"...
[1/4] cd /project/lab6_2_multiple_files/build/esp-idf/esptool_py && /opt/esp/python_env/idf6.0...ition_table/partition-table.bin /project/lab6_2_multiple_files/build/lab6_2_multiple_files.bin 
lab6_2_multiple_files.bin binary size 0x28480 bytes. Smallest app partition is 0x100000 bytes. 0xd7b80 bytes (84%) free.
[1/1] cd /project/lab6_2_multiple_files/build/bootloader/esp-idf/esptool_py && /opt/esp/python...offset 0x8000 bootloader 0x1000 /project/lab6_2_multiple_files/build/bootloader/bootloader.bin 
Bootloader binary size 0x66a0 bytes. 0x960 bytes (8%) free.
[4/4] Completed 'bootloader'Running ninja in directory /project/lab6_2_multiple_files/build
Executing "ninja size"...
[0/1] cd /project/lab6_2_multiple_files/build && /opt/esp/tools/cmake/3.30.2/bin/cmake -D "IDF_SIZE_TOOL=/opt/esp/python_env/idf6.0_py3.12_env/bin/python;-m;esp_idf_size" -D MAP_FILE=/project/lab6_2_multiple_files/build/lab6_2_multiple_files.map -D OUTPUT_JSON= -P /opt/esp/idf/tools/cmake/run_size_tool.cmake
                             Memory Type Usage Summary                              
┏━━━━━━━━━━━━━━━━━━━━━━━┳━━━━━━━━━━━━━━┳━━━━━━━━━━┳━━━━━━━━━━━━━━━━┳━━━━━━━━━━━━━━━┓
┃ Memory Type/Section   ┃ Used [bytes] ┃ Used [%] ┃ Remain [bytes] ┃ Total [bytes] ┃
┡━━━━━━━━━━━━━━━━━━━━━━━╇━━━━━━━━━━━━━━╇━━━━━━━━━━╇━━━━━━━━━━━━━━━━╇━━━━━━━━━━━━━━━┩
│ Flash Code            │        62434 │          │                │               │
│    .text              │        62434 │          │                │               │
│ IRAM                  │        53247 │    40.62 │          77825 │        131072 │
│    .text              │        52219 │    39.84 │                │               │
│    .vectors           │         1028 │     0.78 │                │               │
│ Flash Data            │        39460 │          │                │               │
│    .rodata            │        39204 │          │                │               │
│    .appdesc           │          256 │          │                │               │
│ DRAM                  │        11952 │     6.61 │         168784 │        180736 │
│    .data              │         9696 │     5.36 │                │               │
│    .bss               │         2256 │     1.25 │                │               │
│ RTC FAST              │           36 │     0.44 │           8156 │          8192 │
│    .force_fast        │           36 │     0.44 │                │               │
│ RTC SLOW              │           24 │     0.29 │           8168 │          8192 │
│    .rtc_slow_reserved │           24 │     0.29 │                │               │
└───────────────────────┴──────────────┴──────────┴────────────────┴───────────────┘
Total image size: 164873 bytes (.bin may be padded larger)
Note: The reported total sizes may be smaller than those in the technical reference manual due to reserved memory and application configuration. The total flash size available for the application is not included by default, as it cannot be reliably determined due to the presence of other data like the bootloader, partition table, and application partition size.
```
### `idf.py qemu`
```c
rst:0x1 (POWERON_RESET),boot:0x12 (SPI_FAST_FLASH_BOOT)
configsip: 0, SPIWP:0xee
clk_drv:0x00,q_drv:0x00,d_drv:0x00,cs0_drv:0x00,hd_drv:0x00,wp_drv:0x00
mode:DIO, clock div:2
load:0x3fff0030,len:6372
load:0x40078000,len:15928
load:0x40080400,len:3880
entry 0x40080638
I (1176) boot: ESP-IDF v6.0-dev-1002-gbfe5caf58f 2nd stage bootloader
I (1179) boot: compile time Aug  6 2025 09:30:58
I (1180) boot: Multicore bootloader
I (1888) boot: chip revision: v3.0
I (1892) boot.esp32: SPI Speed      : 40MHz
I (1893) boot.esp32: SPI Mode       : DIO
I (1894) boot.esp32: SPI Flash Size : 2MB
I (1990) boot: Enabling RNG early entropy source...
I (2089) boot: Partition Table:
I (2090) boot: ## Label            Usage          Type ST Offset   Length
I (2091) boot:  0 nvs              WiFi data        01 02 00009000 00006000
I (2092) boot:  1 phy_init         RF data          01 01 0000f000 00001000
I (2093) boot:  2 factory          factory app      00 00 00010000 00100000
I (2173) boot: End of partition table
I (2816) esp_image: segment 0: paddr=00010020 vaddr=3f400020 size=09a24h ( 39460) map
I (3163) esp_image: segment 1: paddr=00019a4c vaddr=3ff80000 size=00024h (    36) load
I (3522) esp_image: segment 2: paddr=00019a78 vaddr=3ffb0000 size=025e0h (  9696) load
I (3883) esp_image: segment 3: paddr=0001c060 vaddr=40080000 size=03fb8h ( 16312) load
I (4252) esp_image: segment 4: paddr=00020020 vaddr=400d0020 size=0f3e4h ( 62436) map
I (4653) esp_image: segment 5: paddr=0002f40c vaddr=40083fb8 size=09048h ( 36936) load
I (5749) boot: Loaded app from partition at offset 0x10000
I (5751) boot: Disabling RNG early entropy source...
I (5840) cpu_start: Multicore app
I (11140) cpu_start: Pro cpu start user code
I (11142) cpu_start: cpu freq: 160000000 Hz
I (11143) app_init: Application information:
I (11144) app_init: Project name:     lab6_2_multiple_files
I (11144) app_init: Project name:     lab6_2_multiple_files
I (11145) app_init: App version:      1
I (11145) app_init: App version:      1
I (11145) app_init: Compile time:     Aug  6 2025 09:32:23
I (11145) app_init: Compile time:     Aug  6 2025 09:32:23
I (11146) app_init: ELF file SHA256:  cad5a9d73...
I (11147) app_init: ESP-IDF:          v6.0-dev-1002-gbfe5caf58f
I (11148) efuse_init: Min chip rev:     v0.0
I (11149) efuse_init: Max chip rev:     v3.99
I (11149) efuse_init: Chip rev:         v3.0
I (11152) heap_init: Initializing. RAM available for dynamic allocation:
I (11155) heap_init: At 3FFAE6E0 len 00001920 (6 KiB): DRAM
I (11158) heap_init: At 3FFB2EB0 len 0002D150 (180 KiB): DRAM
I (11159) heap_init: At 3FFE0440 len 00003AE0 (14 KiB): D/IRAM
I (11160) heap_init: At 3FFE4350 len 0001BCB0 (111 KiB): D/IRAM
I (11161) heap_init: At 4008D000 len 00013000 (76 KiB): IRAM
I (11247) spi_flash: detected chip: winbond
I (11268) spi_flash: flash io: dio
I (11146) app_init: ELF file SHA256:  cad5a9d73...
I (11147) app_init: ESP-IDF:          v6.0-dev-1002-gbfe5caf58f
I (11148) efuse_init: Min chip rev:     v0.0
I (11149) efuse_init: Max chip rev:     v3.99
I (11149) efuse_init: Chip rev:         v3.0
I (11152) heap_init: Initializing. RAM available for dynamic allocation:
I (11155) heap_init: At 3FFAE6E0 len 00001920 (6 KiB): DRAM
I (11158) heap_init: At 3FFB2EB0 len 0002D150 (180 KiB): DRAM
I (11159) heap_init: At 3FFE0440 len 00003AE0 (14 KiB): D/IRAM
I (11160) heap_init: At 3FFE4350 len 0001BCB0 (111 KiB): D/IRAM
I (11161) heap_init: At 4008D000 len 00013000 (76 KiB): IRAM
I (11247) spi_flash: detected chip: winbond
I (11268) spi_flash: flash io: dio
I (11298) main_task: Started on CPU0
I (11308) main_task: Calling app_main()
I (11148) efuse_init: Min chip rev:     v0.0
I (11149) efuse_init: Max chip rev:     v3.99
I (11149) efuse_init: Chip rev:         v3.0
I (11152) heap_init: Initializing. RAM available for dynamic allocation:
I (11155) heap_init: At 3FFAE6E0 len 00001920 (6 KiB): DRAM
I (11158) heap_init: At 3FFB2EB0 len 0002D150 (180 KiB): DRAM
I (11159) heap_init: At 3FFE0440 len 00003AE0 (14 KiB): D/IRAM
I (11160) heap_init: At 3FFE4350 len 0001BCB0 (111 KiB): D/IRAM
I (11161) heap_init: At 4008D000 len 00013000 (76 KiB): IRAM
I (11247) spi_flash: detected chip: winbond
I (11268) spi_flash: flash io: dio
I (11298) main_task: Started on CPU0
I (11308) main_task: Calling app_main()
I (11149) efuse_init: Chip rev:         v3.0
I (11152) heap_init: Initializing. RAM available for dynamic allocation:
I (11155) heap_init: At 3FFAE6E0 len 00001920 (6 KiB): DRAM
I (11158) heap_init: At 3FFB2EB0 len 0002D150 (180 KiB): DRAM
I (11159) heap_init: At 3FFE0440 len 00003AE0 (14 KiB): D/IRAM
I (11160) heap_init: At 3FFE4350 len 0001BCB0 (111 KiB): D/IRAM
I (11161) heap_init: At 4008D000 len 00013000 (76 KiB): IRAM
I (11247) spi_flash: detected chip: winbond
I (11268) spi_flash: flash io: dio
I (11298) main_task: Started on CPU0
I (11308) main_task: Calling app_main()
I (11158) heap_init: At 3FFB2EB0 len 0002D150 (180 KiB): DRAM
I (11159) heap_init: At 3FFE0440 len 00003AE0 (14 KiB): D/IRAM
I (11160) heap_init: At 3FFE4350 len 0001BCB0 (111 KiB): D/IRAM
I (11161) heap_init: At 4008D000 len 00013000 (76 KiB): IRAM
I (11247) spi_flash: detected chip: winbond
I (11268) spi_flash: flash io: dio
I (11298) main_task: Started on CPU0
I (11308) main_task: Calling app_main()
I (11160) heap_init: At 3FFE4350 len 0001BCB0 (111 KiB): D/IRAM
I (11161) heap_init: At 4008D000 len 00013000 (76 KiB): IRAM
I (11247) spi_flash: detected chip: winbond
I (11268) spi_flash: flash io: dio
I (11298) main_task: Started on CPU0
I (11308) main_task: Calling app_main()
I (11247) spi_flash: detected chip: winbond
I (11268) spi_flash: flash io: dio
I (11298) main_task: Started on CPU0
I (11308) main_task: Calling app_main()
I (11308) MAIN: 🚀 Lab 6.2: Multiple Source Files Demo
I (11298) main_task: Started on CPU0
I (11308) main_task: Calling app_main()
I (11308) MAIN: 🚀 Lab 6.2: Multiple Source Files Demo
I (11308) main_task: Calling app_main()
I (11308) MAIN: 🚀 Lab 6.2: Multiple Source Files Demo
I (11308) MAIN: 📍 Main function from file: ./main/lab6_2_multiple_files.c, line: 15
I (11308) MAIN: ESP-IDF Version: v6.0-dev-1002-gbfe5caf58f
I (11308) MAIN: 🚀 Lab 6.2: Multiple Source Files Demo
I (11308) MAIN: 📍 Main function from file: ./main/lab6_2_multiple_files.c, line: 15
I (11308) MAIN: ESP-IDF Version: v6.0-dev-1002-gbfe5caf58f
I (11308) MAIN: 📍 Main function from file: ./main/lab6_2_multiple_files.c, line: 15
I (11308) MAIN: ESP-IDF Version: v6.0-dev-1002-gbfe5caf58f
I (11318) SENSOR: 🔧 Sensor initialized from file: ./main/sensor.c, line: 12
I (11308) MAIN: ESP-IDF Version: v6.0-dev-1002-gbfe5caf58f
I (11318) SENSOR: 🔧 Sensor initialized from file: ./main/sensor.c, line: 12
I (11318) SENSOR: 📡 Sensor module ready for operation
I (11318) DISPLAY: 🖥️  Display initialized from file: ./main/display.c, line: 9
I (11318) DISPLAY: 💡 Display module ready
I (11318) DISPLAY: 💡 Display module ready
I (11318) LED: 💡 LED initialized from file: ./main/led.c, line: 12
I (11318) LED: 🔧 LED module ready
I (11318) DISPLAY: 📢 Displaying from file: ./main/display.c, line: 15
I (11318) DISPLAY: 📺 Message: System Starting...
I (11318) LED: 🚀 Starting LED blink task from file: ./main/led.c, line: 59
I (11328) LED: ✨ LED blink task started from file: ./main/led.c, line: 49
I (11328) LED: ✅ LED ON from file: ./main/led.c, line: 20
I (11328) LED: 🟢 LED is now ON
I (11328) LED: 🔄 LED toggled from file: ./main/led.c, line: 38
I (11328) MAIN: === Loop 0 ===
I (11328) DISPLAY: 🧹 Screen cleared from file: ./main/display.c, line: 28
I (11328) DISPLAY: ✨ Display ready for new content
I (11328) SENSOR: 📊 Reading sensor data from file: ./main/sensor.c, line: 18
I (11338) SENSOR: 🌡️  Temperature: 32.4°C
I (11348) SENSOR: 💧 Humidity: 96.1%
I (11358) DISPLAY: 📊 Data display from file: ./main/display.c, line: 21
I (11358) DISPLAY: 📈 Value 1: 26.50
I (11358) DISPLAY: 📉 Value 2: 61.00
I (11358) DISPLAY: 📢 Displaying from file: ./main/display.c, line: 15
I (11358) DISPLAY: 📺 Message: LED Status: ON
I (13358) MAIN: === Loop 1 ===
I (13358) DISPLAY: 🧹 Screen cleared from file: ./main/display.c, line: 28
I (13358) DISPLAY: ✨ Display ready for new content
I (13358) SENSOR: 📊 Reading sensor data from file: ./main/sensor.c, line: 18
I (13358) SENSOR: 🌡️  Temperature: 28.3°C
I (13358) SENSOR: 💧 Humidity: 69.7%
I (13358) DISPLAY: 📊 Data display from file: ./main/display.c, line: 21
I (13358) DISPLAY: 📈 Value 1: 27.50
I (13358) DISPLAY: 📉 Value 2: 62.00
I (13358) DISPLAY: 📢 Displaying from file: ./main/display.c, line: 15
I (13368) DISPLAY: 📺 Message: LED Status: ON
I (14328) LED: ❌ LED OFF from file: ./main/led.c, line: 27
I (14328) LED: 🔴 LED is now OFF
I (14328) LED: 🔄 LED toggled from file: ./main/led.c, line: 38
I (15368) MAIN: === Loop 2 ===
I (15368) DISPLAY: 🧹 Screen cleared from file: ./main/display.c, line: 28
I (15368) DISPLAY: ✨ Display ready for new content
I (15368) SENSOR: 📊 Reading sensor data from file: ./main/sensor.c, line: 18
I (15368) SENSOR: 🌡️  Temperature: 27.6°C
I (15368) SENSOR: 💧 Humidity: 91.3%
I (15368) DISPLAY: 📊 Data display from file: ./main/display.c, line: 21
I (15368) DISPLAY: 📈 Value 1: 28.50
I (15368) DISPLAY: 📉 Value 2: 63.00
I (15368) DISPLAY: 📢 Displaying from file: ./main/display.c, line: 15
I (15368) DISPLAY: 📺 Message: LED Status: OFF
I (15368) SENSOR: ✅ Sensor status check from file: ./main/sensor.c, line: 30
I (15378) SENSOR: 📈 All sensors operating normally
I (15378) DISPLAY: 📢 Displaying from file: ./main/display.c, line: 15
I (15378) DISPLAY: 📺 Message: Status Check Complete
I (17328) LED: ✅ LED ON from file: ./main/led.c, line: 20
I (17328) LED: 🟢 LED is now ON
I (17328) LED: 🔄 LED toggled from file: ./main/led.c, line: 38
```
## คำถามทบทวน
1. Multiple Source Files: เหตุใดต้องแยก source code เป็นหลายไฟล์?
  - **Ans:**
    - การแยก source codeโดยแต่ละไฟล์สามารถแยกตามหน้าที่หรือโมดูลของโปรแกรม เช่น การจัดการ LED, Sensor, Display เป็นต้น  เป็นหลายไฟล์ช่วยให้โค้ด
    - มีความเป็นระเบียบ
    - แก้ไขและบำรุงรักษาได้ง่าย
    - ลดความซับซ้อนของไฟล์หลัก
    - เอื้อต่อการทำงานเป็นทีม
    
2. CMakeLists.txt Management: การเพิ่มไฟล์ source ใหม่ต้องแก้ไขอะไรบ้าง?
  - **Ans:**
    - ต้องเพิ่มชื่อไฟล์ .c ที่ต้องการเข้าไปในฟิลด์ SRCS ของคำสั่ง idf_component_register() ในไฟล์ main/CMakeLists.txt เช่น sensor.c, display.c, led.c
3. Header Files: บทบาทของไฟล์ .h คืออะไร และทำไมต้องมี?
  - **Ans:**
    - ไฟล์ .h ใช้สำหรับประกาศ prototype ของฟังก์ชันและโครงสร้างข้อมูล เพื่อให้ไฟล์อื่นสามารถใช้งานได้โดยไม่ต้องรู้รายละเอียดการ implement ภายใน เป็นการแยก interface ออกจาก implementation และช่วยให้สามารถ include ไฟล์ในหลายๆ ที่ได้อย่างปลอดภัยด้วย include guard (#ifndef, #define, #endif)
4. Include Directories: เหตุใด CMakeLists.txt ต้องระบุ INCLUDE_DIRS?
  - **Ans:**
    - เพื่อระบุว่า header files (.h) อยู่ในโฟลเดอร์ไหน โดยทั่วไปจะใช้ "." สำหรับโฟลเดอร์ main/ ซึ่งช่วยให้ compiler หาไฟล์ header ได้ถูกต้องเวลามีการ include เช่น #include "sensor.h"
5. Git Ignore: ไฟล์ .gitignore ช่วยอะไรในการจัดการ ESP32 project?
  - **Ans:**
    - ใช้กำหนดไฟล์หรือโฟลเดอร์ที่ไม่ควรให้ Git ติดตาม เช่น build/, *.elf, *.log, *.bin, ไฟล์ของระบบปฏิบัติการ หรือไฟล์ชั่วคราว ช่วยลดความรกของ repository และป้องกันการ commit ไฟล์ที่ไม่จำเป็น
6. Task Management: การใช้ FreeRTOS task ในโมดูล LED ช่วยอะไร?
  - **Ans:**
    - ช่วยให้การกระพริบ LED ทำงานใน background โดยไม่ขัดขวาง loop หลักของโปรแกรม โดยใช้ฟังก์ชัน xTaskCreate() เพื่อสร้าง task ที่รันฟังก์ชัน led_blink_task() ซึ่งควบคุมการเปิด/ปิด LED ทุก 3 วินาที
7. Code Organization: ข้อดีของการแยกโมดูล sensor, display, led เป็นไฟล์แยกคืออะไร?
  - **Ans:**
    - ช่วยให้โค้ดอ่านง่ายขึ้น ดูแลรักษาได้ง่าย และทดสอบแต่ละส่วนได้แยกจากกัน สามารถ reuse โค้ดในโปรเจกต์อื่นได้ และทำงานเป็นทีมได้สะดวกเพราะแต่ละคนสามารถดูแลโมดูลของตนเองได้
  
## บันทึกผลการทดลอง
- ขั้นตอนที่ 1 (เฉพาะ sensor.c):
  จำนวนไฟล์ source: 2  
  ขนาด binary: 163273 bytes
  การทำงาน: โปรแกรมจำลองการอ่านข้อมูลจาก sensor โดยแสดงอุณหภูมิและความชื้นบน console พร้อมแสดงสถานะของ sensor ทุก 3 รอบ
- ขั้นตอนที่ 2 (เพิ่ม display.c):
  จำนวนไฟล์ source: 3
  ขนาด binary: 163981 bytes
  การทำงาน: เพิ่มการแสดงผลบนจอจำลองด้วย display_init(), display_show_message() และ display_show_data() เพื่อแสดงข้อความและค่าที่อ่านได้จาก sensor
- ขั้นตอนที่ 3 (เพิ่ม led.c):
  จำนวนไฟล์ source: 4
  ขนาด binary: 164873 bytes
  การทำงาน: เพิ่มการทำงานของ LED โดยรัน task ให้ LED กะพริบทุก 3 วินาที และแสดงสถานะ LED (ON หรือ OFF) บน display ทุกรอบ loop

## สังเกต:
- การเพิ่มไฟล์ source ส่งผลต่อขนาด binary อย่างไร?
  - **Ans:** เมื่อมีการเพิ่มไฟล์ source (.c) เช่น display.c และ led.c เข้าไปในโปรเจกต์ จะทำให้ขนาด binary เพิ่มขึ้นตามเนื้อหาที่เพิ่ม เช่น ฟังก์ชัน, ตัวแปร, และโค้ดที่ต้อง compile 
- LED กะพริบทุกกี่วินาที?
  - **Ans:** LED จะกะพริบ ทุก 3 วินาที
- แต่ละโมดูลแสดงข้อมูล file และ line อย่างไร?
  - **Ans:** โมดูลต่างๆ จะใช้ __FILE__ และ __LINE__ เพื่อแสดงข้อมูลชื่อไฟล์และบรรทัดในข้อความ Log ซึ่งช่วยให้สามารถติดตามได้ว่าข้อความ Log มาจากส่วนใดของโค้ด
