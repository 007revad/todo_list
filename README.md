# My to do list

<a href="https://hits.seeyoufarm.com"><img src="https://hits.seeyoufarm.com/api/count/incr/badge.svg?url=https%3A%2F%2Fgithub.com%2F007revad%2Ftodo_list&count_bg=%2379C83D&title_bg=%23555555&icon=&icon_color=%23E7E7E7&title=hits&edge_flat=false"/></a>
[![](https://img.shields.io/static/v1?label=Sponsor&message=%E2%9D%A4&logo=GitHub&color=%23fe8e86)](https://github.com/sponsors/007revad)

**If you have an idea for a new script, or suggestions to improve an existing script [leave a comment in Discussions](https://github.com/007revad/todo_list/discussions).**

## To do

- Add option to auto update synology_hdd_db x days after new version released.

- Work out what makes storage manager change "Cache Drive 1" to "M.2 Drive 1"
- Change syno_hdd_db.sh so a reboot is not needed when the NAS has M.2 drives.

- Update all my Synology scripts to check that they are running on a Synology and give a warning, and instructions, if they aren't.

- Enable Health Info in storage manager for non-Synology NVMe drives in DSM 7.2. (Synology_enable_M2_volume already does this)

- Enable Benchmark Tool for NVMe drives in DSM 7.2.

- Create install script for all my repositories.

- Test synology_m2_volume DSM 6 code.

- Check why DS1515+ DSM 7.1.1 not working with enable_m2_volume script.

- Change m2 volume to show if these are already disabled or enabled:
    - Disabled support disk compatibility.
    - Disabled support memory compatibility.

- Create Synoinfo_switch. A menu with checkboxes to enable/disable all the good options in synoinfo.conf
    - Use fzf

- Enable RAID F1 without losing SHR.

- Enable data deduplication for HDDs.

- Allow using non-Synology DAS as expansion units.

- Finish adding install and restore scripts to Syno_Plex_Backup.

- Update older scripts with "check new version" code.

- Update Synology Config Backup:
    - To use a config file.
    - To update itself.
    - Add an install script.

- See if I can bypass the 108TB volume size limit (needs 32GB or more memory and you must use RAID 5 or 6 and Btrfs).

- Write script to downgrade DSM to previous version ???

- Write script to move Packages to another volume ???

