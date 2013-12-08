jhProtominer mod by yvg1900 - optimized miner for ProtoShares mining at ypool.net

*** If you want to stay informed on updates, follow @yvg1900 on Twitter.

DISCLAIMER

The software comes as it is, without warranty of any kind. It is solely your decision to use it or not. 
Use at your own risk, the creator can not be held liable for damage to your system.
If you are in doubt - don't use it.

Please read this file carefully. To achieve better performance consider using fine tuning feature as described in finetuning.txt.
You can check if your miner is actually connected to your account on the pool site in Workers area.

First 30 seconds after start and 30 seconds more for evey running hour miner will mine for its developers to support further performance, 
functionality and compatibility enhancements.

1. Changes to the original build

Following changes are made to increase performance and stability of the miner:
  - Added server pinging to fix NAT connectivity and some other networking and reconnection problems
  - Moved from command-line configuration to multiple executables model in order to benefit from some very specific optimizations
  - Removed -m512,-m256,-m128 etc. command line switches
  - Added possibility to separately specify user name and worker name
  - Added possibility to go above 512M per thread
  - Added algorithm fine tuning feature

2. Which build to use

* Know your machine. Carefully check capabilities of your CPU in order to determine its capabilities. You will need to know:
  - Your operating system
  - Model of your CPU
  - Is it physical or virtualized
  - Does it support SSE, AVX and other modern instruction sets, and if yes - which versions
  - How many physical cores your CPU has
  - Does your CPU support HtperThreading or not
  - How many CPUs your machine has in case you are on multi-CPU machine
  - How much RAM do you have

Build are located in the folders, each folder per build. Folders named as

<operating system name>-<instruction set>-<RAM size per thread>

For example, for 64-bit Linux running on CPU with AVX support and plenty of RAM, take linux64-avx-512M build. 
More builds will become available as soon as there is more demand and sufficient donations.

Feel free to try different builds, but be aware that some may crash due to lack of support for specific instructions on your machine.

3. Running and terminating the miner

You can run it from command prompt, either manually or create a batch file (.bat on Windows) or a shell script (on non-Windows).

To stop miner, kill it by pressing Ctrl+C in the shell window where it runs, or kill it using Task Manager or kill command.

4. Command line arguments

  -o, -O          The miner will connect to this url. You can specifiy any port after the url using -o url:port
  -u              The username (workername) used for login, usually consists of username.workername
  -p              The password used for login (default is x)
  -W              The workername used for login is not needed if -u is specified. If specified it also requires -U
  -U              The username used for login is not needed if -u is specified. If specified it also requires -W
  -X              Number of iterations before exit. You don't need it but you may try if curious. It is useless for you, but needed for developers
  -t <num>        The number of threads for mining (default is to autodetect)
  -A              Enforce CPU Affinity (pin worker threads to CPU cores, Linux only)
  -B              Block attempts to find alternate port after connection failure
  -F <num>        Enable/enforce algorithm selection finetuning
                  When <num> set to 0, perform finetuning and autoselect algo variation (performs suboptimal while finetuning
                  When <num> set to non-zero, skip finetuning autoselection and set algo variation to <num>
  --netdebug      Enable network debug output (useful for connection troubleshooting)
  --no-ping       Disable application-level server ping (default is enabled, ping interval 10 seconds)
  --donate <num>  Set hourly donation duration to <num> seconds (default is 30 seconds, minimum 30 seconds, maximum 3000 seconds)

5. Performance considerations

* RAM
As of current knowledge, it is better to allocate 512M RAM per thread. So decide how many threads you are going to run and calculate if you have enough.

* HyperThreading - on or off?
My tests show that switching HyperThreadin on is beneficial. By the way, this is my personal opinion. Make tests and decide yourself.

* Multiple CPUs
If you are on MP machine, seriously consider running separate process per CPU socket, and specify number of threads accordingly.
Pin your process to the CPU socket (for example, using numactl on linux).

6. Known issues

In some not yet reproduced cases, miner on Linux was exiting by itself. This happened only once during the pool server update with one of development versions.
It is not known if this was a bug but for your safety you can add looping in your shell script that runs the miner.

If your miner shows "collisions/min: 0.0000 Shares total: 0" over an extensive period of time, consider restarting your miner. In most cases this caused by
problems with network connection or temporary pool server unavailability.

7. Contacting authors

At the moment the best way to contact yvg1900 is by PM on ypool.net or just asking in the chat there.
Alternatively, you may follow @yvg1900 on Twitter.

8. Customizations

If you for whatever reason require a version with custom output or no output at all, different default settings or specific auto-configuraton functionality,
PM yvg1900 at ypool.net to discuss the possibilities.

9. Participation in private testing

Authors work on improvements in performance of diffrerent miners and nearly always have faster version in development phase. If you want to get it ahead of others,
let yvg1900 know your offer.

10. Explicit ban on using this software for botnets

It is explicitly prohibited to use this software in botnets, except the cases when participation of the machine in the botnet is arranged intentionally 
by the user, owner or administrator of the machine. Authors treat using this software in botnets as illegal activity.
If you are using, integrating or operating this software in the botnet, you may be subject for legal action.

11. Credits for help

I'd like to thank to clintar, atp1916, mercuryminer, btrider, alphawolf099 and other users of ypool.net for help and assistance.

12. Thanks and Please donate to support this miners progress

PTS: PZxsEQoiMeB6tHcW2ZySBEiCPio1WkxbEL
XPM: AW2388DEWNEfMH4rP9kcj9yKcMq1QywYT4
DTC: D6PmUogMigWvXurgFTqm5VLxQeVpXdYQj3
LTC: Lby4YjhcAxhmbsdHFb4nYydrwGoiJezZt1
BTC: 1FxekeK5La7AuF3oxiLzPKnjXyLMrux6VT

Donations are completely up to you, but appreciated.

Cheers, and have a good luck mining - you'll need it.
yvg1900
