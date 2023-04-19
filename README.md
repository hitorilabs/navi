# storage

I'm quite fond of my macbook air - I can't see myself
interfacing with anything other than a laptop.

If I can acquire some hardware for deep learning before
the AI safety people start regulating GPUs, I'll most
likely be interacting with it through SSH.

For that same reason, it's a little more complicated to
think about how I'm going to deal with storage.

# Things to Consider

It's a little embarrassing that I code for a living, but
I'm not familiar with how to actually evaluate my options.

- Portable External HDD
- Home NAS

I'm going to try both eventually, but first I'll be trying
out the Portable External HDD from Amazon.

I think I generally know what I'm looking out for:
- Read + Write
- Bandwidth Limits over USB, Ethernet, etc.
- Cache Size (if exists)
- Compression
- Encryption

# Portable External HDD

I bought a [WD My Passport Ultra](https://www.westerndigital.com/en-ca/products/portable-drives/wd-my-passport-ultra-usb-c-hdd#WDBC3C0010BSL-WESN).

This thing was cool at first, but it has a lot of flaws:
- passively draining all my battery away (don't know why it would even do this)
- it's supposed to have max bandwidth 5Gbps (625MB/s), but it was actually more like 2Gbps
- data can't be accessed without the physical drive being plugged in

Most importantly, I want to have some fun building a NAS.
# Network Attached Storage (NAS)

- 36TB of HDD storage
- 1TB NVMe cache 
- configured with `raidz1` 
- Running TrueNAS Scale

## Specifications
Type | Name | Quantity
-- | -- | --
HDD | Seagate IronWolf 12TB NAS Internal Hard Drive HDD | 3
CPU | Intel i5-11600K | 1
RAM | Corsair Vengeance LPX 32GB DDR4-3200 | 1
PSU | Corsair RM750x | 1
MOBO | MSI MPG Z590 GAMING PLUS ATX LGA1200 | 1
SSD | Samsung 980 Pro 1 TB M.2-2280 PCIe 4.0 X4 NVME Solid State Drive | 1
SSD | Samsung 970 EVO Plus 250GB NVMe M.2 Internal SSD (MZ-V7S250/AM) | 2
CASE | Corsair 7000D AIRFLOW | 1
COOL | Noctua NH-D15 chromax.black 82.52 CFM CPU Cooler | 1

This is clearly not a budget build, some high-level considerations that were made:
- Boot from two mirrored `SSD` instead of 1 (bought 2x 250GB, but the rest of drive space is completely wasted)
- Setup 1TB `SSD` as Cache VDEV
- 3x `HDD` are enough to run RAIDz1 (ideally, I should have at least 4 to run RAIDz2)
- `CASE` + `MOBO` has enough space + ports for 6 drives (ridiculously expensive, but I'm most likely going to turn it into a deep learning workstation)
- `MOBO` supports 2.5GbE LAN (hard to get 10GbE in Canada, can add a network card to support this)
- `RAM` not a big deal at the moment

## Future Improvements

Honestly, I will only ever work out of my macbook air - so
I want fast file transfers over wifi anywhere at home.

### Bandwidth over Wi-Fi
Even though I did consider getting high-bandwidth
ethernet, I didn't account for packet loss over wifi. I
thought 2.5 GbE (312.5 MB/s) would be plenty, but over
wifi I get a quarter of this bandwidth. 

I don't feel too bad about this because apparently it's
impossible to get affordable 10 GbE boards in Canada. I
would have to buy a separate network card, which is
probably unnecessary at this point.

## References for Setup + Inspiration
- Sentdex Home Lab - https://www.youtube.com/watch?v=CIQ20FWs478
- Setting up TrueNAS Core - https://www.youtube.com/watch?v=nVRWpV2xyds&t=0s