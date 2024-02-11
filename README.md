# navi at home

The name of the game is FLOPs, VRAM, mass storage, and
high-bandwidth networking.

_can we have navi?_

_Mom: no, we have navi at home_

![serialexperimentslain1](https://github.com/hitorilabs/navi/assets/131238467/fbb66c0e-b6b3-4eb8-b9c4-365544ef1b72)

# User Guide
Github actually has a decent reading experience with markdown, the "happy path" for reading this like a blog is to click the `README.md` file to enter "code preview" and then hit the side menu button to pop out the table of contents.

<img width="1444" alt="screenshot of markdown reader" src="https://github.com/hitorilabs/navi/assets/131238467/907c5cd6-ca61-40b7-ae5d-c346e6b4d943">

# Build Log

*These are not budget build guides, we haven't been grinding normie work just to park the money in a bank.*

#### 2024/02/11

Just bought 1 more 3090 and another 1600W PSU (probably on it's last legs, but it was cheap so I want to play around with it) - now I'm noticing data link errors. Basically, you'll see messages like this when you watch the kernel diagnostic messages `sudo dmesg -w`.

```
[  143.474053] pcieport 0000:00:03.1:    [ 6] BadTLP                
[  143.474055] pcieport 0000:00:03.1: AER: aer_layer=Data Link Layer, aer_agent=Receiver ID
```
Related: [Article from PCI-SIG on Retimers](https://pcisig.com/pci-express®-retimers-vs-redrivers-eye-popping-difference)

I should try out some retimers, but I also don't know how much this impacts performance + system stability for now I can only really monitor the situation until I test them out for myself. So far the impact on performance itself hasn't been very noticeable, but the actual impact might be more insidious.

#### 2023/11/15

PSA if your boot is slow asf (ubuntu-server) for seemingly no reason, I wrote up a [gist](https://gist.github.com/hitorilabs/2ce6eabcf92ec7dd7acbcb72486aaf2e) about how having extra unmapped ports causes your machine will block your boot for several minutes to do a search.

#### 2023/11/10

Attempted to go through the RMA process for some products just to see what it's like. The components are probably working fine, but I just cited some obscure conditions (i.e. power limited, coil whine, etc.). 

EVGA - mostly no questions asked and were actually quite helpful with tech support. If you live far away from the actual repair center (RIP canada bros), you will get absolutely destroyed by shipping costs and conversion fees because they don't cover anything for you (unless maybe you gaslight them into offering it)

ASUS - heard really bad things about them and I don't really want to risk them sending back my cards scratched up - or worse give me some used ones. I have an open RMA, but probably won't go through with it.

**PSA** about PSUs, you should check what cables are actually provided in the box for compatibility. 

I have the EVGA 1600W P+ PSU, but when I RMA'd it they gave me a P2 because it was out of stock at the time. The two PSUs are similar, but the P2 actually had a completely different set of cables that weren't at all compatible.

My ROG STRIX 3090 model expects 3x 8-pin PCI-E single connections (`3 connectors * 3 GPUs = 9 Total`). The support guy helped me figure out that my cards were blinking red because 3090s don't work when using both ends of split cables - you have to use them as single connections and leave one end dangling. This also implies that **running 3 GPUs is effectively the maximum** on a single PSU.

The EVGA 1600W P2 and P+ PSUs only have a total of 9 PCI-E power connector slots on the back
- The P2 comes with 4x 8-pin single connectors and 5x split 6 pin + (6 + 2) pin. 
- The P+ came with 4x 8-pin single connectors and 5x split 8 pin + (6 + 2) pin - so I could actually do the dangling cable thing and make it work.

If I had to choose a PSU, I would've spent the extra cash to buy the T2 model because it has less of a coil whine and comes with the 9x 8-pin single PCI-e connectors that you'll want. 

(see this [video](https://www.youtube.com/watch?v=V3OeKQU8AJE) about the T2 and explaining PSUs in general)

You also can't even buy extra cables online - it seems like the single 8-pin PCI-E cables are always out of stock.

#### 2023/09/30

**NAS Update**: Basically deleted my NAS machine and transplanted all the drives into my primary workstation and setup a regular ZFS pool + NFS server on ubuntu (pleasantly surprised that all the data is retained and it just works). I was watching a bunch of yt videos and was tricked into thinking truenas was any good.

**Workstation Update**: Managed to get a 4090 so I swapped out the 3090 and cobbled together remaining parts for my sister to do blender + game dev. Anything that fits on the single card can often feel nearly 2x faster - probably a combination of higher clock + cores + software gains on ada 

Haven't played a game in a while, but of course I had to play cyberpunk on it - incredible. I was only vaguely keeping track of progress on the gaming/graphics side of things, but DLSS 3.5 w/ Path Tracing + Ray Reconstruction has to be pretty close to magic.

#### 2023/08/30

recently secured a small pile of 3090s through the local social media marketplace and it's actually surprisingly hard to compose a system that's actually capable of running them all on a single machine.

<img width="1444" alt="rig" src="/images/rig.jpeg">

If only I had trusted the [lambdalabs article](https://lambdalabs.com/blog/deep-learning-hardware-deep-dive-rtx-30xx) to begin with, then I wouldn't have gone through countless hours of trying to get 4 3090s running on a single 1600W PSU. Basically, the sweet spot is 3 3090s running on a machine that's outfitted with server parts, since desktop parts will severely limit your total # of PCIE lanes (although you will rarely be memory constrained on multiple PCIE 4.0 x8 slots).

If you are only planning to run 2x GPU configurations as a workstation, you should consider settling for desktop parts and running them on PCIE 4.0 x8 (i.e. i9-13900K/i7-13700K both support 2x8 + 4 PCIE configurations, which leaves room for some weak networking or storage expansion). This way, you won't be dealing with used parts or old software.

Type | Name | Quantity | Unit Cost
-- | -- | -- | --
PSU | EVGA 1600W P+ | 1 | 551.42
GPU | ASUS ROG STRIX RTX 3090 | 3 | 850.00
MOBO | ROMED8-2T/BCM | 1 | 882.52
RAM | Micron 16GB DDR4-3200 RDIMM 1Rx4 (MTA18ASF2G72PZ-3G2R) | 4 | 60.915
STORAGE | WD_BLACK 1TB SN850X NVMe | 1 | 89.00
COOLER | Noctua NH-U9 TR4-SP3 | 1 | 101.64
CASE | Mining Rig Frame for 12GPU, Steel Open Air Miner | 1 | 45.19
RISERS | Thermaltake TT PCI-E 4.0 Riser Cable | 3 | 112.85
CPU | AMD EPYC 7302P 16 cores 3.0GHz 155W | 1 | 195.91

**Total**: 4,997.89 CAD

EDIT: DO NOT BUY THE P+ MODEL FOR YOUR PSU, BUY A T2 (SEE 2023/11/10)

Review on pricing:
- RAM - $60 for a single 16GB stick is robbery, but I couldn't find any 1Rx4 memory on ebay
- RISERS - with one-day delivery on Amazon
- MOBO - got lots of recommendations for this and saw a lot of vast.ai builds that use it
  - bought from ebay at ~$300 off from the Amazon price
  - main advantage is that you get 7 slots with full PCIE 4.0 x16 bandwidth
- STORAGE - pretty smol, but won't be needing a ton on this machine yet because I'll be offloading to other machines
- GPU - a steal considering that the sellers were a very well-off family w/ kids who were probably not thrashing these cards
- CPU - a piece of crap, but I've never dealt with server parts before so I'm starting small. 
  - The ebay guys are surprisingly reliable, I wonder where they get these parts from 🤔
  - I also bought a torque driver that has the 14 lbs/in setting because I saw some comments about it on discord, but it might just be a psyop.

A neat article and chart on power limiting from a [Puget Systems article](https://www.pugetsystems.com/labs/hpc/NVIDIA-GPU-Power-Limit-vs-Performance-2296). This will help you control temperatures and stay comfortably under your power supply's maximum capacity.

<img width="1444" alt="power limiting chart" src="/images/power_limit.jpeg">

#### 2023/05/19

ubuntu-server pilled now. 

Accidentally wiped my root partition and realized what I need is stability. I want my server to be up all the time and feel roughly the same as a vm on `lambdalabs`. I was also trying to put tailscale on my arch linux install, but it was missing some mystery dependency that I'll never figure out.

ubuntu-server had a pretty straightforward install and sensible defaults (launch sshd without login, netplan is pretty straight forward, etc.)

- with tailscale + ubuntu, I can now connect to my DL workstation anywhere and safely reboot it without losing ssh access (unless something goes terribly wrong)
- UX workflow is now pretty much uniform with `lambdalabs` instances

#### 2023/05/11

- workstation w/ cuda
- network attached storage + rsync
- vs code w/ `copilot` + `remote - ssh plugin` + `jupyter notebooks` extension
- `htop` + `nvtop` monitoring on my TV screen
- arch btw

<img width="900" alt="screencap gif of sensor readings + nvtop + htop" src="https://github.com/hitorilabs/navi/assets/131238467/984d8b8c-5b45-4f77-a034-ee0075cfbdd4">

#### 2023/05/08

Built and setup the the workstation over the weekend. For the record, I've never owned a GPU before and my only interaction with linux distros is through docker images on the cloud.
  - can I still say arch btw if I used `archinstall`...
  - moved all the overkill components from NAS to DL workstation
  - never touched networking before, so this was an
  enlightening experience

**Deep Learning Workstation (RETIRED)**

- RTX 3090
- 1x 1TB NVMe (980 Pro) + 2TB NVMe drive (970 Evo Plus)
- Intel i7-13700KF (16-core)
- arch btw

**Specifications**
Type | Name | Quantity | Unit Cost
-- | -- | -- | --
CPU | Intel Core i7-13700KF | 1 | 519.98
COOL | Noctua NH-D15S | 1 | 99.95
MOBO | Asus ROG STRIX Z690-E | 1 | 448.98
RAM | Corsair Vengeance 64 GB (2 x 32 GB) DDR5-6000 | 1 | 319.99
SSD | Samsung 980 Pro 1 TB M.2-2280 NVMe | 1 | 129.97
SSD | Samsung 970 Evo Plus 2 TB M.2-2280 NVMe | 1 | 169.99
GPU | NVIDIA RTX 3090 FE | 1 | 900.00
CASE | Corsair 7000D AIRFLOW | 1 | 299.99
PSU | Corsair RM850x 850W PSU | 1 | 184.99

**Total**: 3073.84 CAD

---

This is clearly not a cheap build, some high-level considerations that were made:
- `CASE` + `MOBO` has enough space + ports for 6 drives and lots of space for fans.
- `MOBO` bundled with M.2 expansion card for 4 extra slots, 2.5GbE LAN, wi-fi
- `SSD` now that I know the `MOBO` came with an M.2 expansion card, I'm most likely going to invest in lots more of these NVMe drives (and give the OS it's own dedicated drives)
- `RAM` leaving room to expand to 128 GB

#### 2023/05/01

I should just buy the machine already, I'm not completely broke. Looking through local marketplaces for honest people selling used 3090. Doing my research on all things hardware.

#### 2023/04/20

I have more than enough storage to dump everything I see in the foreseeable future, but no compute to make any of this productive. There are lots of gains to be made with solid networking and storage, but cloud computing platforms often don't offer much control there. I want to do a mix of inference and training, but none of the options make sense for me.
  - Lambda Labs never has any capacity available when I need it
    - For an A100, it costs `1.10 * 24 * 365 = 9636` to run an  inference server 24/7
    - For an A10 it still costs `0.6 * 24 * 365 = 5256`, but it's not even as good as an RTX 3090
  - Google colab is [doing some whack stuff](https://twitter.com/thechrisperry/status/1649189902079381505)
    - For a V100 expect `5.45 * 0.14 = 0.76` per hour, which is laughable compared to what you get with A10s.
    - For an A100 expect `15 * 0.14 = 2.1` per hour, which is double Lambda Labs pricing. 

#### 2023/04/14

Finished building and setting up TrueNAS Scale over the weekend. Honestly, not super impressed with it. 
  - RAID storage is a psyop
  - Could've just invested in a bunch of NVMe drives and deal with extra storage when the time actually comes.

#### 2023/04/10

Waiting 2 hours for a dataset to finish downloading over wifi, 5 mins for every model to download over the internet... this is the last time I will suffer. 
  - Ordered a bunch of parts and HDDs from Amazon to build a NAS (one-day shipping and scheduled pickup for returns feel illegal)

# TODO

- increase utilization on these machines
