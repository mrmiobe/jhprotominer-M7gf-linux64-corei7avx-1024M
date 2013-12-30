yam - Yet Another Miner by yvg1900 - optimized miner for ProtoShares mining

*** If you want to stay informed on updates, follow @yvg1900 on Twitter.

DISCLAIMER

The software comes as it is, without warranty of any kind. It is solely your decision to use it or not. 
Use at your own risk, the creator can not be held liable for damage to your system.
If you are in doubt - don't use it.

Please read this file carefully. To achieve better performance consider using fine tuning feature as described in finetuning.txt.
You can check if your miner is actually connected to your account on the pool site in Workers area.

Miner periodically mines for miner developers to support further performance, functionality and compatibility enhancements.
Explanation of how and when it happens can be found below in "Mining for developers" section.

1. How yam is different from other miners

This miner created completely from scratch, including mining framework, mining algorithms, connection handling, etc.

Comparing to the original jhProtominer by jh00, yam includes following changes and improvements:
  - Much higher performance
  - Configuration file support
  - Completely different connection handling that reduces connection latency and minimizes amount of wasted CPU time, while
    minimizing unnecessary CPU load
  - Server pinging to fix NAT connectivity and some other networking and reconnection problems
  - Dynamic connection timeout system for early detection of connectivity problems
  - Multiple pool connections for mining on secondary pool when primary pool is down
  - SOCKS4A Proxy support (compatible with Tor)
  - Possibility to go above 512M per thread
  - Algorithm fine tuning feature

2. Which build to use

* Know your machine. Carefully check capabilities of your CPU in order to determine its capabilities. You will need to know:
  - Your operating system
  - Model and microarchitecture of your CPU
  - Is it physical or virtualized
  - Does it support SSE, AVX and other modern instruction sets, and if yes - which versions
  - How many physical cores your CPU has
  - Does your CPU support HyperThreading or not
  - How many CPUs your machine has in case you are on multi-CPU machine
  - How much RAM do you have

Build are located in the folders, each folder per build. Folders named as

yam-yvg1900-<miner version>-<operating system name>-<instruction set>

For example, for 64-bit Linux running on Haswell CPU with, take linux64-haswell build. 
More builds will become available as soon as there is more demand and sufficient donations.

Feel free to try different builds, but be aware that some may crash due to lack of support for specific instructions on your machine.

3. Running and terminating the miner

You can run it from command prompt, either manually or create a batch file (.bat on Windows) or a shell script (on non-Windows).

To stop miner, kill it by pressing Ctrl+C in the shell window where it runs, or kill it using Task Manager or kill command.

4. Command line arguments

Command-line only options:
  --help                This message.
  -c [ --config ] arg   Name of configuration file.

Command-line and configuration file options:
  -t [ --threads ] arg       The number of threads for mining (default is to
                             autodetect), when t<=0 use autodetect+t threads.
  -M [ --mine ] arg          Mining target in YAM URI format (protocol, worker
                             name, password, pool address, pool ports, coin
                             type, mining parameters). Multiple mining targets
                             allowed.
  -P [ --mining-params ] arg Mining parameters in parameter list format
                             (coin:param1=value1&param2=value2&param3=value3.
                             Multiple parameter groups allowed.
  --compact-stats arg        Enable compact statistics output (uses less screen
                             space).
  --proxy arg                Proxy server to use in format
                             type://user:password@host:port (check
                             documentation for supported proxy types and usage
                             details).

Easiest way to run miner is to modify example config file provided with the miner and run

yam --config yam.cfg

4.1. Mining target format

The best explanation is example.

Mining target for ypool: xpt2h://yvg1900.defpts:x@mining.ypool.net:10034:8080:8081:8082:8083:8084:8085:8086:8087/pts
Mining target for ptspool: xpt2://PsPhfpU91JWTgt5A4AS4eVyuZJQQXAhrjW:x@112.124.13.238:28988/pts

More protocol support and pools to come.

4.2. Mining parameters format

Mining parameters are coin-specific.

For ProtoShares, allowed parameters are: 
  "av" (algorithm variation, 32 variations in total, 0 activates fine tuning feature), 
  "m" (memory size per thread in megabytes)
  "donation-interval" (in mining rounds).

Mining parameters exampel for ProtoShares: pts:av=19&m=1024&donation-interval=100

4.3. Proxy support

Proxy parameter argument shall be given in URI format. 

For example, for use with Tor, you shall specify socks4a://127.0.0.1:9150 as your proxy.

5. Performance considerations

* RAM
As of current knowledge, it is better to allocate 512M RAM per thread. So decide how many threads you are going to run and calculate if you have enough.

* HyperThreading - on or off?
My tests show that switching HyperThreadin on is beneficial. By the way, this is my personal opinion. Make tests and decide yourself.

* Multiple CPUs
If you are on MP machine, seriously consider running separate process per CPU socket, and specify number of threads accordingly.
Pin your process to the CPU socket (for example, using numactl on linux).

6. Known issues

If your miner shows "PTS Agg. CPM: ?; Rnds C/I: 0/0, Don. C/I: 0/0; Cfg/Thr CPM: ?/? 0" over an extensive period of time, consider restarting your miner. 
In most cases this caused by problems with network connection or temporary pool server unavailability.

7. Mining for developers.

Miner periodically mines for miner developers to support further performance, functionality and compatibility enhancements.

Mining for developers implemented works on complete mining round basis to minimize performance impact. Average amount of time spent on
mining for developers is less than one percent and can be increased with donation-interval parameter in coin mining parameters.
For example, value of 100 will mean that miner will mine 100 complete rounds for the user and then will contribute one round to developers.

Mining for developers does not happen for signle round, but instead miner accumulates several rounds and then mines for developers for 
sligtly longer interval to reduce network load and unnecessary CPU usage.

When mining for developers being activated, miner clearly indicates that by displaying message and includes rounds mined for developers in
"Donated Complete/Incomplete" counters of statistics display, so you can always see how many rounds have been contributed to developers.

Please be aware of the fact that if miner can not connect to developer mining targets withing reasonable time interval, mining may get temporarily blocked.

Additionally to that, if all your mining targets are not available within two minutes, miner will try to mine for developers while continuously trying to 
recover connection to your mining targets. When such thing happen, miner will display appropirate message and will keep displaying it every five minutes
to remind you that you have problems with your network configuration.

8. Contacting authors

At the moment the best way to contact yvg1900 is by PM on ypool.net or just asking in the chat there.
Alternatively, you may follow @yvg1900 on Twitter or send Twitter message to @yvg1900.

8.1. Customizations

If you for whatever reason require a version with custom output or no output at all, different default settings or specific auto-configuraton functionality,
contact yvg1900 at Twitter to discuss the possibilities.

8.2. Participation in private testing

Authors work on improvements in performance of diffrerent miners and nearly always have faster version in development phase. If you want to get it ahead of others,
let yvg1900 know your offer, or contact mercuryminer at ypool.net - he leads independent group of miner testers.

9. Explicit ban on using this software for botnets

It is explicitly prohibited to use this software in botnets, except the cases when participation of the machine in the botnet is arranged intentionally 
by the user, owner or administrator of the machine. Authors treat using this software in botnets as illegal activity.
If you are using, integrating or operating this software in the botnet, you may be subject for legal action.

10. Credits for help

I'd like to thank to clintar, atp1916, mercuryminer, btrider, alphawolf099, doesnotmatter and other users of ypool.net for help and assistance, as well as people
involved in private testing.

Miner uses parts of XPT protocol code developed by jh00 (ypool.net).

11. Thanks and Please donate to support this miners progress

PTS: PZxsEQoiMeB6tHcW2ZySBEiCPio1WkxbEL
XPM: AW2388DEWNEfMH4rP9kcj9yKcMq1QywYT4
DTC: D6PmUogMigWvXurgFTqm5VLxQeVpXdYQj3
LTC: Lby4YjhcAxhmbsdHFb4nYydrwGoiJezZt1
BTC: 1FxekeK5La7AuF3oxiLzPKnjXyLMrux6VT
NMC: N9KXqmzEqP7gB2dGHpEZiRMgFjUHNM38FR

Donations are completely up to you, but appreciated.

Cheers, and have a good luck mining - you'll need it.
yvg1900
