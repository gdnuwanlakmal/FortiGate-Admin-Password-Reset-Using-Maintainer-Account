<p align="center">
  <img
    src="https://github.com/user-attachments/assets/2717e193-16a6-4886-b904-aa4f038a5d08"
    width="300"
  />
  <br />
</p>

# FortiGate Admin Password Reset (Maintainer Account)
If the admin password is lost and physical access to the FortiGate device is available, you can reset the password using the maintainer account. This process requires a console cable, the device’s serial number, and a terminal program. After rebooting the FortiGate, log in quickly using the username maintainer and the password bcpb + [Serial Number in UPPERCASE]. Once logged in, you can reset the admin password or perform a factory reset if needed. This method does not work on virtual FortiGate units (VMs).

### FortiGate Admin Password Reset Using Maintainer Account

⚠ Warning: This process requires a reboot of the FortiGate unit.

🔐 When to Use:

* Admin password is lost or unknown.

* Physical access to the device is available.

* Applies to physical FortiGate devices (not VMs).

🧰 Requirements

* Physical access to the FortiGate unit.

* Console cable (Serial, RJ-45-to-Serial, or USB depending on model).

* Terminal software (e.g., PuTTY on Windows, Terminal on macOS).

* Serial number of the FortiGate device (e.g., FGT60C3G10XXXXXX).

🔁 Procedure
### 1. Connect to the Device
Plug the console cable into the Console port of the FortiGate and the other end to your PC.

Launch your terminal software and configure it with:

* Baud Rate: 9600

* Data Bits: 8

* Parity: None

* Stop Bits: 1

* Flow Control: None

COM Port: The correct one (check Device Manager on Windows)

### 2. Reboot the FortiGate
* Power cycle the unit (unplug for at least 10 seconds, then plug back in).

### 3. Wait for Login Prompt
* The device will display boot messages and eventually:
```shell
login:
```
### 4. Login with Maintainer Account
Username: maintainer

Password: bcpb + [Serial Number in UPPERCASE]

Example: bcpbFGT60C3G10XXXXXX

⏱ You typically have 14–60 seconds after boot to enter credentials. Prepare them in a text editor and paste quickly.

### 5. Change the Admin Password
If VDOMs are disabled:
```shell
config system admin
edit admin
set password <newpassword>
end
```
If VDOMs are enabled:
```shell
config global
config system admin
edit admin
set password <newpassword>
end
```
### 🏭 (Optional) Factory Reset the Device
If the admin account is deleted and no super-admin account exists:
```shell
execute factoryreset
```
🧼 This will erase all configuration and restore factory defaults.

### 🔒 Maintainer Account Control

🔧 Disable Maintainer Account (for higher security):

```shell
config system global
set admin-maintainer disable
end
```

### ✅ Enable Maintainer Account (if previously disabled):
```shell
config system global
set admin-maintainer enable
end
```

If the system says:
### PASSWORD RECOVERY FUNCTIONALITY IS DISABLED,
the maintainer feature is disabled, and recovery is not possible via this method.
