---
title: SAMBA on Windows 10
tags:
  - samba
  - windows
  - smb
categories:
  - notes
header:
  overlay_filter: "0.5"
  overlay_color: "#000"
  teaser: /assets/the-most-terrifying.png
  overlay_image: /assets/the-most-terrifying.png
excerpt: Windows 10 disable anonymous guest.
---

On a bright day, Windows 10 suddenly:

```powershell
C:\> net use * \\[SAMBA_IP]\shares /user:user *
Type the password for \\[SAMBA_IP]\shares:
System error 1272 has occurred.

You can't access this shared folder because your organization's security policies block unauthenticated guest access. These policies help protect your PC from unsafe or malicious devices on the network.

```

Configure in Regedit.exe:

```ini
[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\LanmanWorkstation\Parameters]
"AllowInsecureGuestAuth"
```

from `dword(0)` to `dword(1)`.

Thus:

```powershell
C:\> net use * \\[SAMBA_IP]\shares /user:user *
Type the password for \\[SAMBA_IP]\shares:
Drive Z: is now connected to \\[SAMBA_IP]\shares.

The command completed successfully.

```

Just put random password there.

Source:
* [Guest access in SMB2 disabled by default in Windows](https://support.microsoft.com/en-us/help/4046019/guest-access-in-smb2-disabled-by-default-in-windows-10-and-windows-ser)

