**Task: Timezone Alignment**

In the daily standup, it was noted that the timezone settings across the Nautilus Application Servers in the Stratos Datacenter are inconsistent with the local datacenter's timezone, currently set to Australia/Adelaide.
Synchronize the timezone settings to match the local datacenter's timezone (Australia/Adelaide).

**Solution:**

To synchronize the timezone settings across the Nautilus Application Servers in the Stratos Datacenter, you will use the timedatectl utility. This is the standard modern tool for managing the system clock and its settings under systemd.

You should perform these steps on App Server 1, 2, and 3.

The Implementation Command
Run the following command on each server:

sudo timedatectl set-timezone Australia/Adelaide
Breakdown of the Command
timedatectl: The command-line utility for controlling the system time and date.

set-timezone: The specific directive to update the system's timezone configuration.

Australia/Adelaide: The specific ZoneInfo (tz) database name for the South Australian timezone.

Verification
Once you have executed the change, you should verify that the server has correctly updated its local time and universal time (UTC) offset:

timedatectl
Expected Output:

Plaintext
      Local time: Sat 2026-03-28 21:15:59 ACDT
  Universal time: Sat 2026-03-28 10:45:59 UTC
        RTC time: Sat 2026-03-28 10:45:59
       Time zone: Australia/Adelaide (ACDT, +1030)
(Note: ACDT stands for Australian Central Daylight Time, which has an offset of +10:30 from UTC during March.)

Manual Alternative (The Symbolic Link)
On older Linux systems where timedatectl might not be available, the manual way to do this is by updating the /etc/localtime symbolic link:

sudo ln -sf /usr/share/zoneinfo/Australia/Adelaide /etc/localtime

