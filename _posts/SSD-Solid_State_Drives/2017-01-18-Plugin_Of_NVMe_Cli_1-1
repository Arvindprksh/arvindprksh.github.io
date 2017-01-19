---
layout: post
title: What is plugin mode in NVMe-cli-1.1 opensource
subtitle: How to make plugin mode in NVMe-cli-1.1 opensource
category: SSD (Solid State Drives)
tags: [nvme]
permalink: /2017/01/18/Plugin_Of_NVMe_Cli_1-1/
---


## [NVMe-cli-1.1's plugin mode](https://github.com/linux-nvme/nvme-cli#add-a-new-plugin)

From NVMe-cli-1.1, new operation is added for Developers who want to add a new command or possibily an entirely new plug-in for some special extension outside the spec.

For your more information, URL : [Developers of nvme-cli](https://github.com/linux-nvme/nvme-cli#developers)

**BUT**, You can add VU command outside the spec into nvme-cli-1.1 using nvme-builtin.h 

If you want to know how to make VU command using nvme-builtin.h. Please refer to [my another blog](./2017/01/13/NVMe_Cil/)

**BUT**, at this time, I will use the another way, that is adding a new plugin.


### First, Create a header file to define your plugin. 

let's see an example that is introduced on NVMe-clie's official site.

the file of example is where you will give your plugin a name, description, and define all the sub-commands your plugin impelements.


FILE: foo-plugin.h

```c
#undef CMD_INC_FILE
#define CMD_INC_FILE foo-plugin

#if !defined(FOO) || defined(CMD_HEADER_MULTI_READ)
#define FOO

#include "cmd.h"

PLUGIN(NAME("foo", "Foo plugin"),
    COMMAND_LIST(
        ENTRY("bar", "foo bar", bar)
        ENTRY("baz", "foo baz", baz)
        ENTRY("qux", "foo quz", qux)
    )
);

#endif

#include "define_cmd.h"
```

In order to have the complier generate the plugin through the xmacro expansion, you need to include this header in your source file, with pre-defining macro directive to create the commands.

To get started from the above exmple, we just need to define "CREATE_CMD" and include the header :

File:foo-plugin.c

```c
#define CREATE_CMD
#include "foo-plugin.h"
```

**After that, You just need to implement the functions you defined in each ENTRY, then append the object file name to the Makefiles's "OBJS"**


# An example of plugin extensions

## ./nvme --help

Then, let's see the actual example with nvme-cli-1.1

```shell
$ ./nvme --help
nvme-1.1
usage: nvme <command> [<device>] [<args>]

The '<device>' may be either an NVMe character device (ex: /dev/nvme0) or an
nvme block device (ex: /dev/nvme0n1).

The following are all implemented sub-commands:
  list            List all NVMe devices and namespaces on machine
  id-ctrl         Send NVMe Identify Controller
  id-ns           Send NVMe Identify Namespace, display structure
  list-ns         Send NVMe Identify List, display structure
  create-ns       Creates a namespace with the provided parameters
  delete-ns       Deletes a namespace from the controller
  attach-ns       Attaches a namespace to requested controller(s)
  detach-ns       Detaches a namespace from requested controller(s)
  list-ctrl       Send NVMe Identify Controller List, display structure
  get-ns-id       Retrieve the namespace ID of opened block device
  get-log         Generic NVMe get log, returns log in raw format
  fw-log          Retrieve FW Log, show it
  smart-log       Retrieve SMART Log, show it
  error-log       Retrieve Error Log, show it
  get-feature     Get feature and show the resulting value
  set-feature     Set a feature and show the resulting value
  format          Format namespace with new block format
  fw-activate     Activate new firmware slot
  fw-download     Download new firmware
  admin-passthru  Submit arbitrary admin command, return results
  io-passthru     Submit an arbitrary IO command, return results
  security-send   Submit a Security Send command, return results
  security-recv   Submit a Security Receive command, return results
  resv-acquire    Submit a Reservation Acquire, return results
  resv-register   Submit a Reservation Register, return results
  resv-release    Submit a Reservation Release, return results
  resv-report     Submit a Reservation Report, return results
  dsm             Submit a Data Set Management command, return results
  flush           Submit a Flush command, return results
  compare         Submit a Compare command, return results
  read            Submit a read command, return results
  write           Submit a write command, return results
  write-zeroes    Submit a write zeroes command, return results
  write-uncor     Submit a write uncorrectable command, return results
  reset           Resets the controller
  subsystem-reset Resets the controller
  show-regs       Shows the controller registers. Requires admin character device
  discover        Discover NVMeoF subsystems
  connect-all     Discover and Connect to NVMeoF subsystems
  connect         Connect to NVMeoF subsystem
  disconnect      Disconnect from NVMeoF subsystem
  version         Shows the program version
  help            Display this help

See 'nvme help <command>' for more information on a specific command

The following are all installed plugin extensions:
  intel           Intel vendor specific extensions
  lnvm            LightNVM specific extensions
  memblaze        Memblaze vendor specific extensions

See 'nvme <plugin> help' for more information on a plugin
```

As you can see the above result, in the bottom of the above, there are plugin extensions like this :

```
The following are all installed plugin extensions:
  intel           Intel vendor specific extensions
  lnvm            LightNVM specific extensions
  memblaze        Memblaze vendor specific extensions

See 'nvme <plugin> help' for more information on a plugin
```

So I typed 'nvme <plugin(lnvm)> help

```shell
$ ./nvme lnvm help
nvme-1.1
usage: nvme lnvm <command> [<device>] [<args>]

The '<device>' may be either an NVMe character device (ex: /dev/nvme0) or an
nvme block device (ex: /dev/nvme0n1).

LightNVM specific extensions

The following are all implemented sub-commands:
  list            List available LightNVM devices
  info            List general information and available target engines
  id-ns           List geometry for LightNVM device
  init            Initialize media manager on LightNVM device
  create          Create target on top of a LightNVM device
  remove          Remove target from device
  factory         Reset device to factory state
  diag-bbtbl      Diagnose bad block table
  diag-set-bbtbl  Update bad block table
  version         Shows the program version
  help            Display this help

See 'nvme lnvm help <command>' for more information on a specific command
```

## Let's the actual file of lnvm-nvme.c and lnvm-nvme.h

### /nvme-cli-1.1/lnvm-nvme.h

```c
  1 
  2 #undef CMD_INC_FILE
  3 #define CMD_INC_FILE lnvm-nvme
  4 
  5 #if !defined(LNVM_NVME) || defined(CMD_HEADER_MULTI_READ)
  6 #define LNVM_NVME
  7 
  8 #include "cmd.h"
  9 
 10 PLUGIN(NAME("lnvm", "LightNVM specific extensions"),
 11         COMMAND_LIST(
 12                 ENTRY("list", "List available LightNVM devices", lnvm_list)
 13                 ENTRY("info", "List general information and available target engines", lnvm_info)
 14                 ENTRY("id-ns", "List geometry for LightNVM device", lnvm_id_ns)
 15                 ENTRY("init", "Initialize media manager on LightNVM device", lnvm_init)
 16                 ENTRY("create", "Create target on top of a LightNVM device", lnvm_create_tgt)
 17                 ENTRY("remove", "Remove target from device", lnvm_remove_tgt)
 18                 ENTRY("factory", "Reset device to factory state", lnvm_factory_init)
 19                 ENTRY("diag-bbtbl", "Diagnose bad block table", lnvm_get_bbtbl)
 20                 ENTRY("diag-set-bbtbl", "Update bad block table", lnvm_set_bbtbl)
 21         )
 22 );
 23 
 24 #endif
 25 
 26 #include "define_cmd.h"
~                                                                         
```
As you can see the above code. note several lines.

```c
1 
2 #undef CMD_INC_FILE
3 #define CMD_INC_FILE lnvm-nvme
4 
5 #if !defined(LNVM_NVME) || defined(CMD_HEADER_MULTI_READ)
6 #define LNVM_NVME
7 
8 #include "cmd.h"
9 
10 PLUGIN(NAME("lnvm", "LightNVM specific extensions"),
11         COMMAND_LIST(
12                 ENTRY("list", "List available LightNVM devices", lnvm_list)
21         )
22 );
23 
24 #endif
25 
26 #include "define_cmd.h"
```

### /nvme-cli-1.1/lnvm-nvme.c

even this file is the same part is important.

```c
........
14 #define CREATE_CMD
15 #include "lnvm-nvme.h"
16 
17 static int lnvm_init(int argc, char **argv, struct command *cmd, struct plugin *plugin)
18 {
19         const char *desc = "Initialize LightNVM device. A LightNVM/Open-Channel SSD"\
20                            " must have a media manager associated before it can "\
21                            " be exposed to the user. The default is to initialize"
22                            " the general media manager on top of the device.\n\n"
23                            "Example:"
24                            " lnvm-init -d nvme0n1";
25         const char *devname = "identifier of desired device. e.g. nvme0n1.";
26         const char *mmtype = "media manager to initialize on top of device. Default: gennvm.";
27 
28         struct config
29         {
30                 char *devname;
31                 char *mmtype;
32         };
33 
34         struct config cfg = {
35                 .devname = "",
36                 .mmtype = "gennvm",
37         };
38 
39         const struct argconfig_commandline_options command_line_options[] = {
40                 {"device-name",   'd', "DEVICE", CFG_STRING, &cfg.devname, required_argument, devname},
41                 {"mediamgr-name", 'm', "MM",     CFG_STRING, &cfg.mmtype,  required_argument, mmtype},
42                 {NULL}
43         };
44 
45         argconfig_parse(argc, argv, desc, command_line_options, &cfg, sizeof(cfg));
46 
47         if (!strlen(cfg.devname)) {
48                 fprintf(stderr, "device name missing %d\n", (int)strlen(cfg.devname));
49                 return -EINVAL;
50         }
51 
52         return lnvm_do_init(cfg.devname, cfg.mmtype);
53 }
54 
55 static int lnvm_list(int argc, char **argv, struct command *cmd, struct plugin *plugin)
........
```


## Exception situation because of the number of bits in Data type

 if you get int128 from firmware and int128 is split into four pieces in uint32. you have to chage int128 to long double type. 

 that is because it is easy to calculat WAF automatically. 
 
 let's see an example function to change from int128 to long double. 
 
```c

//data variable consists of __u8 * arr[16];

static long double int128_to_double(__u8 *data)
{
        int i;
        long double result = 0;

        for (i = 0; i < 16; i++) {
                result *= 256;
                result += data[15 - i];
        }
        return result;
}
```
 
 
 
