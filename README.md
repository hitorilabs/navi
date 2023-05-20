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

#### 2023/05/19

ubuntu-server pilled now. 

I accidentally wiped my root partition and realized what I need is stability. I want my server to be up all the time and feel roughly the same as a vm on `lambdalabs`. I was also trying to put tailscale on my arch linux install, but it was missing some mystery dependency that I'll never figure out.

ubuntu-server had a pretty straightforward install and sensible defaults (launch sshd without login, netplan is pretty straight forward, etc.)

- with tailscale + ubuntu, I can now connect to my DL workstation anywhere and safely reboot it without losing ssh access (unless something goes terribly wrong)
- UX workflow is now pretty much uniform with `lambdalabs` instances

#### 2023/05/11

bros... I am hearing colors now

- workstation w/ cuda
- network attached storage + rsync
- vs code w/ `copilot` + `remote - ssh plugin` + `jupyter notebooks` extension
- `htop` + `nvtop` monitoring on my TV screen
- arch btw

it's over -> we're back -> we're connected

<img width="900" alt="screencap gif of sensor readings + nvtop + htop" src="https://github.com/hitorilabs/navi/assets/131238467/984d8b8c-5b45-4f77-a034-ee0075cfbdd4">

(and figured out how to resize panes in tmux)

#### 2023/05/08

Built and setup the the workstation over the weekend. For the record, I've never owned a GPU before and my only interaction with linux distros is through docker images on the cloud.
  - can I still say arch btw if I used `archinstall`...
  - moved all the overkill components from NAS to DL workstation
  - never touched networking before, so this was an
  enlightening experience

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

# Storage

I'm quite fond of my macbook air - I can't see myself
interfacing with anything other than a laptop.

For this reason, it's going to be a bit complicated to
think about how I'm going to deal with storage.

This is not a budget build guide, we haven't been grinding
normie work just to park the money in a bank.

## Things to Consider

It's a little embarrassing that I code for a living, but
I'm not familiar with how to actually evaluate my options.

- Portable External HDD
- Home NAS

I'm going to try both eventually, but first I'll be trying
out the Portable External HDD from Amazon.

## Portable External HDD

I bought a [WD My Passport Ultra](https://www.westerndigital.com/en-ca/products/portable-drives/wd-my-passport-ultra-usb-c-hdd#WDBC3C0010BSL-WESN).

This thing was cool at first, but it has a lot of flaws:
- passively draining all my battery away (don't know why it would even do this)
- it's supposed to have max bandwidth 5Gbps (625MB/s), but it was actually more like 2Gbps
- data can't be accessed without the physical drive being plugged in

Most importantly, I want to have some fun building a NAS.
## Network Attached Storage (NAS)

- 36TB of HDD storage
- 1TB NVMe cache 
- configured with `raidz1` 
- Running TrueNAS Scale

### Specifications
Type | Name | Quantity | Price
-- | -- | -- | --
HDD | Seagate IronWolf 12TB NAS HDD (ST12000VN0008) | 3 | 259.99
CPU | Intel Core i5-11600K 6 Cores up to 4.9 GHz | 1 | 252.15
RAM | Corsair Vengeance LPX 16 GB (2 x 8 GB) DDR4-3200 | 1 | 59.99
PSU | Corsair RM750x 750W PSU | 1 | 149.99
MOBO | MSI MPG Z590 GAMING PLUS | 1 | 204.99
SSD | Samsung 970 EVO Plus 250GB NVMe M.2 (MZ-V7S250/AM) | 2 | 59.97
CASE | Antec VSK4000E-U3_US | 1 | 94.55
COOL | Noctua NH-D15 | 1 | 139.94

**Total**: 1801.52 CAD

---

Most of the cost is coming from the HDDs. To optimize this build for cost:
1. downgrade `MOBO`, `COOL`, `PSU`
2. source most parts locally

Some high-level considerations that were made:
- 3x `HDD` are enough to run RAIDz1 (ideally, I should have at least 4 to run RAIDz2)
- `COOL` NH-D15 is a universally solid cooler, I move it into a more demanding build when appropriate
- `CASE` has space for 5 drives (terrible case and somehow still ~$100)
- `MOBO` supports 2.5GbE LAN (hard to get 10GbE in Canada, can add a network card to support this)
- `RAM` not a big deal at the moment

### Bandwidth over Wi-Fi
Even though I did consider getting high-bandwidth
ethernet, I didn't account for 802.11ax 1.2Gb/s (~150
MB/s) per stream. I thought 2.5 GbE (312.5 MB/s) would be
plenty, but over wifi I get a quarter of this bandwidth. 

I'm most likely going to park a DL workstation next to the
NAS connected via ethernet network switch.

### References for Setup + Inspiration
- Sentdex Home Lab - https://www.youtube.com/watch?v=CIQ20FWs478
- Setting up TrueNAS Core - https://www.youtube.com/watch?v=nVRWpV2xyds&t=0s

# Compute

## Deep Learning Workstation

- RTX 3090
- 1x 1TB NVMe (980 Pro) + 2TB NVMe drive (970 Evo Plus)
- Intel i7-13700KF (16-core)
- arch btw

### Specifications
Type | Name | Quantity | Price
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

### Setup
Trying to save some cash and running _arch btw_ is not easy. 

1. **Software Compatibility**: The Asus ROG Strix Z690-E
motherboard was designed to be compatible with 12th Gen
Intel processors, the BIOS needed an update to support
13th Gen
2. **Hardware Compatibility**: Originally, I wanted to put
my NH-D15 in this, but it was actually incompatible due to
the heatsinks. To avoid headaches, the NH-D15S is the
variant that was designed to be more compatible with most
builds.
3. **Used Components**: Buying a used 3090 can be risky
business, but I ended up with a pretty solid deal
4. **Static IP**: I primarily wanted to SSH into the
machine, so I had to assign a static IP address so that I
don't have to check on the IP on every reboot.
5. **Arch Linux**: `archinstall` is great, but I have zero
concept of how to use the display managers or window
managers. Nothing like minimal install and `tmux` + `vim`

### Configure bluetooth keyboard ([wiki](https://wiki.archlinux.org/title/bluetooth))

- Install `bluez` + `bluez-utils` packages
- check service
  - `systemctl status bluetoothctl`
  - `systemctl start bluetoothctl`
- scan for device
  - `bluetoothctl scan on` 
- connect device
  - `bluetoothctl connect <MAC_ADDRESS>`
  - `bluetoothctl trust <MAC_ADDRESS>` (so that the passcode will show up when pairing)
  - `bluetoothctl pair <MAC_ADDRESS>` (so that the passcode will show up when pairing)

pro tip: 
- connect via usb and turn scan on before entering pairing
- exit pairing and copy device `MAC_ADDRESS`
- trust device and start pairing on machine before
entering pairing mode on keyboard
- when rebooting the computer, you might get stuck on "no keyboard detected"
  - if your bluetooth keyboard has multiple pairing options (HHKB btw) you can cycle the pairing on/off to make it detect the keyboard.

### Setting up ssh ([wiki](https://wiki.archlinux.org/title/OpenSSH))
- check relevant service
  - `systemctl status sshd`
- check state of ip addresses
  - `ip address show`
- check restart service
  - `systemctl restart sshd`

### Configuring static IP using `systemd-networkd` ([wiki](https://wiki.archlinux.org/title/Systemd-networkd))
- check state of ip addresses
  - `ip address show`
  - `ip route show`
- check relevant services
  - `systemctl status sshd`
  - `systemctl status systemd-networkd`
- edit configuration (assuming wired ethernet)
  - `sudo vim /etc/systemd/network/20-ethernet.network`

```
[Network]
DHCP=no
Address=<ip_address_range>
Gateway=<your_gateway>
DNS=<some_dns_address>
IPv6PrivacyExtensions=yes
```
- restart service
  - `systemctl restart systemd-networkd`

### Mount Network Attached Storage (NFS)

- `/etc/fstab` (filesystem table)
```
# <file system> <dir> <type> <options> <dump> <pass>

<static_ip_address>:<path_to_dataset> <path_to_mount_location>  nfs  _netdev,noauto,x-systemd.automount,x-systemd.mount-timeout=10,timeo=14,x-systemd.idle-timeout=1min 0 0
```

# TODO

- increase utilization on these machines
