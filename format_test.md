# Synology: how to increase shutdown temperature

My Synology DS218+ runs with a single SSD disk that has an operating temperature range of **0–70 °C**, which is common for SSDs. Synology, however, has a **default shutdown temperature of 61 °C**, probably due to HDDs and some lazy programming.

I'm a very light user of NAS – all I want is a network attached storage _and silence_. My DS218+ has one 2 TB SSD disk in it and I've changed the system fan for a quieter / slower one.

Everything runs fine but about once in a month, I get this notification:

> [Synology DS218+]Synology shut down due to disk overheating.
>
> Synology shut down automatically, because disk 1 was overheating and reached a temperature of 61°C.

That's really annoying as I have to attend the NAS and turn it on manually. BTW, it happens during longer I/O workloads where my disk usually operates between 58 and 60 °C, so very close to the shutdown threshold; a warmer day is enough to trigger it.

I've contacted Synology support to see if they have any solution for it, but they don't (except for purchasing an officially supported SSD from their compatibility list).

But it's possible to tweak the disk station to support higher shutdown temperatures. Here is how to do it (I wrote this for my specific user account, host name etc.):

## 1. Enable SSH, log in

1. Log in to http://synology.local:5000/.
2. In **Control Center** > **Terminal & SNMP**, tick **Enable SSH service**.
3. Make sure the user is in the `administrators` group.
4. From a local computer, log in with `ssh borekb@synology.local` and provide the password.

## 2. Update the `scemd.xml` file

I'm not that comfortable with vi / vim so I've copied the file to the local machine:

```
ssh borekb@synology.local 'cat /usr/syno/etc.defaults/scemd.xml' > scemd.xml
```

In the XML file, the first two `<fan_config>` sections marked `DUAL_MODE_HIGH` and `DUAL_MODE_LOW` are important:

- `DUAL_MODE_HIGH` is for the "cool mode" (i.e., when Synology keeps things cooler at the expense of noise)
- `DUAL_MODE_LOW` = "quiet mode"

I've updated the "low mode" only, like this:

```diff
<?xml version="1.0" encoding="UTF-8"?>
<scemd>
  <fan_config hibernation_speed="UNKNOWN" type="DUAL_MODE_LOW" threshold="6" period="20">
-   <disk_temperature action="NONE" fan_speed="20%40hz">0</disk_temperature>
-   <disk_temperature action="NONE" fan_speed="30%40hz">46</disk_temperature>
-   <disk_temperature action="NONE" fan_speed="50%40hz">50</disk_temperature>
-   <disk_temperature action="NONE" fan_speed="70%40hz">54</disk_temperature>
-   <disk_temperature action="NONE" fan_speed="99%40hz">58</disk_temperature>
-   <disk_temperature action="SHUTDOWN" fan_speed="99%40hz">61</disk_temperature>
+   <disk_temperature action="NONE" fan_speed="20%40hz">0</disk_temperature>
+   <disk_temperature action="NONE" fan_speed="30%40hz">50</disk_temperature>
+   <disk_temperature action="NONE" fan_speed="50%40hz">55</disk_temperature>
+   <disk_temperature action="NONE" fan_speed="70%40hz">62</disk_temperature>
+   <disk_temperature action="NONE" fan_speed="99%40hz">66</disk_temperature>
+   <disk_temperature action="SHUTDOWN" fan_speed="99%40hz">71</disk_temperature>

    <cpu_temperature action="NONE" fan_speed="20%40hz">0</cpu_temperature>
    <cpu_temperature action="NONE" fan_speed="50%40hz">65</cpu_temperature>
    <cpu_temperature action="NONE" fan_speed="99%40hz">80</cpu_temperature>
    <cpu_temperature action="SHUTDOWN" fan_speed="99%40hz">90</cpu_temperature>
  </fan_config>
  <!-- Etc. -->
</scemd>
```

<details><summary>📋 Copy-paste-friendly snippet</summary>

```xml
<disk_temperature action="NONE" fan_speed="20%40hz">0</disk_temperature>
<disk_temperature action="NONE" fan_speed="30%40hz">50</disk_temperature>
<disk_temperature action="NONE" fan_speed="50%40hz">55</disk_temperature>
<disk_temperature action="NONE" fan_speed="70%40hz">62</disk_temperature>
<disk_temperature action="NONE" fan_speed="99%40hz">66</disk_temperature>
<disk_temperature action="SHUTDOWN" fan_speed="99%40hz">71</disk_temperature>
```

</details>

My disk operates at around 45–50 °C normally (it can be seen in the Storage Manager) so I've only messed with temperatures above that. Full fan speed kicks in at 66 °C and the system shuts down at **71 °C**.

With the file done, save it back to Synology – first upload it to some writable directory like `~`:

```
cat scemd.xml | ssh your-user@synology.local 'cat -> ~/scemd.xml'
```

Then, from an SSH session:

```console
# Become a root
borekb@Synology:~$ sudo -i
Password:

# Move file to its proper location
root@Synology:~# mv /var/services/homes/borekb/scemd.xml /usr/syno/etc.defaults/scemd.xml
```

Lastly, update the `etc/scemd.xml` file:

```
cp /usr/syno/etc.defaults/scemd.xml /usr/syno/etc/scemd.xml
```

## 3. Restart the `scemd` service

From the SSH session:

```
synoservice --restart scemd
```

Or just restart the whole NAS.

### Useful resources

- https://community.synology.com/enu/forum/17/post/82880
- https://return2.net/how-to-make-synology-diskstation-fans-quieter/
