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

# Home NAS with TrueNAS Scale

Sentdex Home Lab - https://www.youtube.com/watch?v=CIQ20FWs478
Setting up TrueNAS Core - https://www.youtube.com/watch?v=nVRWpV2xyds&t=0s
Setting up a Static IP Address - https://www.youtube.com/watch?v=xUodt6_e5KA

Notes:
- Streaming R/W
- R/W IOPS

I built a server with 36TB of HDD storage configured with `raidz1`. With only 3 disks this is all I didn't really have another option.

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