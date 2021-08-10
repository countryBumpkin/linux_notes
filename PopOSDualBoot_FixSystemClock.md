# Fix System Clock
When dual booting Windows and Pop! OS the Windows system clock is always messed up. It gets shifted 7 or so hours off of the time settings in Pop! OS. According to [Dual Boot Windows 10 Alongside Pop!_OS](https://support.system76.com/articles/dual-booting/) this can actually be fixed using the steps below.

# Work Log
| Date       | Description |
| :--------: | :---------: |
| 12/18/2020 | Started looking for ways to improve dual boot options for Windows and Pop!_OS and stumbled across the time settings |

# Linux Commands
| Command | Description |
| :---:   | :---:       |
| timedatectl | accesses the system time settings(prints them) and allows modification |

# Method
Use the following commands to duplicate my changes in Pop!_OS. These were taken from the article referenced above.

	timedatectl set-local-rtc 1 --adjust-system-clock #changes settings to fix difference
	timedatectl # check if changes were applied, true if "RTC in local TZ: yes"
