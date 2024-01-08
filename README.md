# My to do list

<a href="https://hits.seeyoufarm.com"><img src="https://hits.seeyoufarm.com/api/count/incr/badge.svg?url=https%3A%2F%2Fgithub.com%2F007revad%2Ftodo_list&count_bg=%2379C83D&title_bg=%23555555&icon=&icon_color=%23E7E7E7&title=views&edge_flat=false"/></a>
[![](https://img.shields.io/static/v1?label=Sponsor&message=%E2%9D%A4&logo=GitHub&color=%23fe8e86)](https://github.com/sponsors/007revad)
[![committers.top badge](https://user-badge.committers.top/australia/007revad.svg)](https://user-badge.committers.top/australia/007revad)

**If you have an idea for a new script, or suggestions to improve an existing script [leave a comment in Discussions](https://github.com/007revad/todo_list/discussions).**

## Done

- Add support for Plex in docker to Synology_Plex_backup.
- Enable Immutable Snapshots for models older than '20 series.
- Enable using M2D20, M2D18, M2D17 (and E10M20-T1?) in Synology NAS that don't officially support them.
- Add option to auto update synology_hdd_db x days after new version released.
- Test synology_m2_volume DSM 6 code.
- Enable Health Info in storage manager for non-Synology NVMe drives in DSM 7.2 (Synology_enable_M2_volume already does this).
- Enable data deduplication for HDDs.
- Change Synology Config Backup to support two remote backup destinations.
- Update older scripts with "check new version" code.
- Write script to downgrade DSM to previous version.
- Write script to move Packages to another volume.

## To Do

- Add info on how to enable SSH and connect to a Synology via SSH to the readme of all my Synology scripts.
- Update all my Synology scripts to check that they are running on a Synology and give a warning, and instructions, if they aren't.
- Enable Benchmark Tool for NVMe drives in DSM 7.2.
- Find out how DSM 7 does Fast Repair so syno_m2_volume can create the storage pool faster.
- Change syno_m2_volume to check for existing volumes instead of existing partitions.
- Change syno_m2_volume to give more accurate resync time estimates.
- Change syno_m2_volume to offer to skip the resync (like storage manager does).
- Add option to synology_plex_backup to delete backup files older than 14 days
  find $Backup_Directory -type f -mtime +14 -delete
- Work out what makes storage manager change "Cache Drive 1" to "M.2 Drive 1"
- Change syno_hdd_db.sh so a reboot is not needed when the NAS has M.2 drives.
- Create install script for all my repositories.
- Check why DS1515+ DSM 7.1.1 not working with enable_m2_volume script.
- Change m2 volume to show if these are already disabled or enabled:
    - Disabled support disk compatibility.
    - Disabled support memory compatibility.
- Create Synoinfo_switch. A menu with checkboxes to enable/disable all the good options in synoinfo.conf
    - Use fzf
- Allow using non-Synology DAS as expansion units.
- Finish adding install and restore scripts to Syno_Plex_Backup.
    - Add option to delete backups older than x days. See https://www.reddit.com/r/synology/comments/13zgbyl/comment/jn0misx/
- Update Synology Config Backup:
    - To use a config file.
    - To update itself.
    - Add an install script.
- See if I can bypass the 108TB volume size limit (needs 32GB or more memory and you must use RAID 5 or 6 and Btrfs).

