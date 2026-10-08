# Linux-Gaming-Utils
## Increase the Open File Limit (Crucial for Steam/Wine)
Edit the limits file ```/etc/security/limits.conf```

Add these lines at the bottom (* means for all users):

```
* soft nofile 1048576
* hard nofile 1048576
```
sometimes systemd overrides this so try doing it like this: edit ```/etc/systemd/user.conf```
add the following to the end
```
DefaultLimitNOFILE=1048576:1048576
```

Reboot for this to take effect. You can verify it after rebooting by running ```ulimit -n``` in a terminal; it should show the new high number.
## increase vm.max_map_count
edit the ```/etc/sysctl.conf``` file, add ```vm.max_map_count=2147483642``` to the bottom and then run:
```
sudo sysctl -p
```
systemd might also fuck this up so try this instead:
make a new file called ```/etc/sysctl.d/99-max-map-count.conf```
add this to it
```
vm.max_map_count=2147483642
```
reboot 

## gamescope 
(for upscaling VNs while maintaining aspect ratio) (fullscreen, fit to screen (not fill or stretch) using fsr)
```
gamescope -f -S fit -F fsr -- %command%
```
(other useful flags (cs2 example))
```
gamescope -W 5120 -H 1440 -r 240 -f -b --force-grab-cursor --expose-wayland -- %command%
```

## lsfg-vk 2.0 (for frame generation, create a profile manually or with the UI and call it with this environment variable (make sure to select the lsfg-vk version on your steam settings))
```
LSFGVK_PROFILE="profilename" %command%   
```
# Game examples i use
## The Finals
```
LSFGVK_PROFILE="lsfg" mangohud %command%
```
## Old VNs (ej. Majikoi)
```
gamescope -f -S fit -F fsr -- %command%
```
