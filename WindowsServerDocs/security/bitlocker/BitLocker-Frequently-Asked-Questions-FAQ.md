---
title: BitLocker Frequently Asked Questions (FAQ)
description: "Windows Server Security"
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: security-bitlocker
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 474d852b-6ce3-49af-9f27-0de9a54e67d5
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
---
# BitLocker Frequently Asked Questions (FAQ)

>Applies To: Windows Server&reg; 2016, Windows Server&reg; 2012 R2, Windows Server&reg; 2012

This topic for the IT professional answers frequently asked questions concerning the requirements to use, upgrade, deploy and administer, and key management policies for BitLocker.

BitLocker Drive Encryption is a data protection feature available in all editions of Windows Server and certain editions of the Windows operating systems. BitLocker encrypts the hard drives on your computer to provide enhanced protection against data theft or exposure on computers and removable drives that are lost or stolen, and more secure data deletion when BitLocker\-protected computers are decommissioned as it is much more difficult to recover deleted data from an encrypted drive than from a non\-encrypted drive.

-   [Overview and requirements](bitlocker-frequently-asked-questions-faq.md#BKMK_Overview)

-   [Upgrading](bitlocker-frequently-asked-questions-faq.md#BKMK_Upgrading)

-   [Deployment and administration](bitlocker-frequently-asked-questions-faq.md#BKMK_Deploy)

-   [Key management](bitlocker-frequently-asked-questions-faq.md#BKMK_KeyManagement)

-   [BitLocker To Go](bitlocker-frequently-asked-questions-faq.md#BKMK_BTGsect)

-   [Active Directory Domain Services \(AD??DS\)](bitlocker-frequently-asked-questions-faq.md#BKMK_ADDS)

-   [Security](bitlocker-frequently-asked-questions-faq.md#BKMK_Security)

-   [BitLocker Network Unlock](bitlocker-frequently-asked-questions-faq.md#BKMK_BNUsect)

-   [Other questions](bitlocker-frequently-asked-questions-faq.md#BKMK_Other)

## <a name="BKMK_Overview"></a>Overview and requirements

### <a name="BKMK_WhatIsBitLocker"></a>How does BitLocker work?
**How BitLocker works with operating system drives**

You can use BitLocker to mitigate unauthorized data access on lost or stolen computers by encrypting all user files and system files on the operating system drive, including the swap files and hibernation files, and checking the integrity of early boot components and boot configuration data.

**How BitLocker works with fixed and removable data drives**

You can use BitLocker to encrypt the entire contents of a data drive. You can use Group Policy to require that BitLocker be enabled on a drive before the computer can write data to the drive. BitLocker can be configured with a variety of unlock methods for data drives, and a data drive supports multiple unlock methods.



### <a name="BKMK_MultifactorSupport"></a>Does BitLocker support multifactor authentication?
Yes, BitLocker supports multifactor authentication for operating system drives. If you enable BitLocker on a computer that has a TPM version??1.2 or 2.0, you can use additional forms of authentication with the TPM protection.


> [!NOTE]
> Dynamic disks are not supported by BitLocker.  Dynamic data volumes will not be displayed in the Control Panel.  Although the operating system volume will always be displayed in the Control Panel, regardless of whether it is a Dynamic disk, if it is a dynamic disk it is cannot be protected by BitLocker.

### <a name="BKMK_Partitions"></a>Why are two partitions required? Why does the system drive have to be so large?
Two partitions are required to run BitLocker because pre\-startup authentication and system integrity verification must occur on a separate partition from the encrypted operating system drive. This configuration helps protect the operating system and the information in the encrypted drive.


### <a name="BKMK_HaveTPM"></a>How can I tell if a TPM is on my computer?


### <a name="BKMK_NoTPM"></a>Can I use BitLocker on an operating system drive without a TPM?
Yes, you can enable BitLocker on an operating system drive without a TPM version 1.2 or 2.0, if the BIOS or UEFI firmware has the ability to read from a USB flash drive in the boot environment. This is because BitLocker will not unlock the protected drive until BitLocker's own volume master key is first released by either the computer's TPM or by a USB flash drive containing the BitLocker startup key for that computer. However, computers without TPMs will not be able to use the system integrity verification that BitLocker can also provide.

To help determine whether a computer can read from a USB device during the boot process, use the BitLocker system check as part of the BitLocker setup process. This system check performs tests to confirm that the computer can properly read from the USB devices at the appropriate time and that the computer meets other BitLocker requirements.



### <a name="BKMK_BIOSSupport"></a>How do I obtain BIOS support for the TPM on my computer?
Contact the computer manufacturer to request a Trusted Computing Group \(TCG\)\-compliant BIOS or UEFI boot firmware that meets the following requirements:

-   It is compatible with and has passed the logo tests where applicable for those versions designated in the **Applies To** list at the beginning of this topic.

-   It is compliant with the TCG standards for a client computer.

-   It has a secure update mechanism to help prevent a malicious BIOS or boot firmware from being installed on the computer.

### <a name="BKMK_privs"></a>What credentials are required to use BitLocker?
To turn on, turn off, or change configurations of BitLocker on operating system and fixed data drives, membership in the local **Administrators** group is required. Standard users can turn on, turn off, or change configurations of BitLocker on removable data drives.


### <a name="BKMK_bootorder"></a>What is the recommended boot order for computers that are going to be BitLocker\-protected?
You should configure the startup options of your computer to have the hard disk drive first in the boot order, before any other drives such ach as CD\/DVD drives or USB drives. If the hard disk is not first and you typically boot from hard disk, then a boot order change may be detected or assumed when removable media is found during boot.??The boot order typically affects the system measurement that is verified by BitLocker and a change in boot order will cause you to be prompted for your BitLocker recovery key. For the same reason, if you have a laptop with a docking station, ensure that the hard disk drive is first in the boot order both when docked and undocked.


## <a name="BKMK_Upgrading"></a>Upgrading

### <a name="BKMK_upgradeV27"></a>Can I upgrade my Windows??7???based computer to Windows??8\-based computer with BitLocker enabled?
Yes. To upgrade from Windows??7 to Windows 8 or Windows 8.1 without decrypting the operating system drive, open the **BitLocker Drive Encryption** Control Panel item in Windows??7, click **Manage BitLocker**, and then and click **Suspend**. Suspending protection does not decrypt the drive; it disables the authentication mechanisms used by BitLocker and uses a clear key on the drive to enable access. Proceed with the upgrade process by using your Windows 8 DVD or Windows 8.1 upgrade. After the upgrade has completed, open Windows Explorer, right\-click the drive, and then click **Resume Protection**. This reapplies the BitLocker authentication methods and deletes the clear key.

### <a name="BKMK_DisableDecrypt"></a>What is the difference between suspending and decrypting BitLocker?
**Decrypt** completely removes BitLocker protection and fully decrypts the drive.

**Suspend** keeps the data encrypted but encrypts the BitLocker volume master key with a clear key. The clear key is a cryptographic key stored unencrypted and unprotected on the disk drive. By storing this key unencrypted, the **Suspend** option allows for changes or upgrades to the computer without the time and cost of decrypting and re\-encrypting the entire drive. After the changes are made and BitLocker is again enabled, BitLocker will reseal the encryption key to the new values of the measured components that changed as a part of the upgrade, the volume master key is changed, the protectors are updated to match and the clear key is erased.

### <a name="BKMK_DecryptFirst"></a>Do I have to decrypt my BitLocker\-protected drive to download and install system updates and upgrades?
The following table lists what action you need to take before you perform an upgrade or update installation.

|Type of update|Action|
|---------|-----|
|Windows Anytime Upgrade|Decrypt|
|Upgrade from Windows??7 to Windows 8|Suspend|
|Non\-Microsoft software updates, such as:<br /><br />-   Computer manufacturer firmware updates<br />-   TPM firmware updates<br />-   Non\-Microsoft application updates that modify boot components|Suspend|
|Software and operating system updates from Microsoft Update|These updates do not require drive decryption or that you disable or suspend BitLocker.|
|||

> [!NOTE]
> If you have suspended BitLocker, you can resume BitLocker protection after you have installed the upgrade or update. Upon resuming protection, BitLocker will reseal the encryption key to the new values of the measured components that changed as a part of the upgrade or update. If these types of upgrades or updates are applied without suspending BitLocker, your computer will enter recovery mode when restarting and will require a recovery key or password to access the computer.

## <a name="BKMK_Deploy"></a>Deployment and administration

### <a name="BKMK_Automate"></a>Can BitLocker deployment be automated in an enterprise environment?
Yes, you can automate the deployment and configuration of BitLocker and the TPM using either WMI or Windows PowerShell scripts. How you choose to implement the scripts depends on your environment. You can also use the BitLocker command\-line tool, Manage\-bde.exe, to locally or remotely configure BitLocker. For additional information about writing scripts that use the BitLocker WMI providers, see the MSDN topic [BitLocker Drive Encryption Provider](http://go.microsoft.com/fwlink/?LinkId=80600).  For additional information about using Windows PowerShell cmdlets with BitLocker Drive Encryption see [BitLocker Cmdlets in Windows PowerShell](http://technet.microsoft.com/library/jj649829(v=wps.620).aspx).

### <a name="BKMK_OS"></a>Can BitLocker encrypt more than just the operating system drive?
Yes. In Windows Vista, BitLocker could only encrypt operating system drives. Windows Vista SP1 and Windows Server 2008 added support for encrypting fixed data drives. Capabilities introduced in Windows Server??2008??R2 and Windows??7 permit BitLocker to also encrypt removable data drives.

### <a name="BKMK_Performance"></a>Is there a noticeable performance impact when BitLocker is enabled on a Windows??8???based computer?
Generally it imposes a single\-digit percentage performance overhead.

### <a name="BKMK_LongEncrypt"></a>How long will initial encryption take when BitLocker is turned on?
Although BitLocker encryption occurs in the background while you continue to work, and the system remains usable, encryption times vary depending on the type of drive that is being encrypted, the size of the drive, and the speed of the drive. If you are encrypting very large drives, you may want to set encryption to occur during times when you will not be using the drive.

Capabilities introduced in Windows 8 and  Windows Server 2012 , allow you to choose whether or not BitLocker should encrypt the entire drive or just the used space on the drive when you turn on BitLocker. On a new hard drive, encrypting just the used spaced can be considerably faster than encrypting the entire drive. When this encryption option is selected, BitLocker automatically encrypts data as it is saved, ensuring that no data is stored unencrypted.

### <a name="BKMK_TurnOff"></a>What happens if the computer is turned off during encryption or decryption?
If the computer is turned off or goes into hibernation, the BitLocker encryption and decryption process will resume where it stopped the next time Windows starts. This is true even if the power is suddenly unavailable.

### <a name="BKMK_EntireDisk"></a>Does BitLocker encrypt and decrypt the entire drive all at once when reading and writing data?
No, BitLocker does not encrypt and decrypt the entire drive when reading and writing data. The encrypted sectors in the BitLocker\-protected drive are decrypted only as they are requested from system read operations. Blocks that are written to the drive are encrypted before the system writes them to the physical disk. No unencrypted data is ever stored on a BitLocker\-protected drive.

### <a name="BKMK_DataUnencryptPart"></a>How can I prevent users on a network from storing data on an unencrypted drive?
Controls introduced in Windows 8, allow you to enable Group Policy settings to require that data drives be BitLocker\-protected before a BitLocker\-protected computer can write data to them.

When these policy settings are enabled, the BitLocker\-protected operating system will mount any data drives that are not protected by BitLocker as read\-only.


### <a name="BKMK_IntegrityFail"></a>What system changes would cause the integrity check on my operating system drive to fail?
The following types of system changes can cause an integrity check failure and prevent the TPM from releasing the BitLocker key to decrypt the protected operating system drive:

-   Moving the BitLocker\-protected drive into a new computer.

-   Installing a new motherboard with a new TPM.

-   Turning off, disabling, or clearing the TPM.

-   Changing any boot configuration settings.

-   Changing the BIOS, UEFI firmware, master boot record, boot sector, boot manager, option ROM, or other early boot components or boot configuration data.



### <a name="BKMK_examplesosrec"></a>What causes BitLocker to start into recovery mode when attempting to start the operating system drive?
Because BitLocker is designed to protect your computer from numerous attacks, there are numerous reasons why BitLocker could start in recovery mode. 

### <a name="BKMK_DriveSwap"></a>Can I swap hard disks on the same computer if BitLocker is enabled on the operating system drive?
Yes, you can swap multiple hard disks on the same computer if BitLocker is enabled, but only if the hard disks were BitLocker\-protected on the same computer. The BitLocker keys are unique to the TPM and operating system drive, so if you want to prepare a backup operating system or data drive for use in case of disk failure, you need to make sure that they were matched with the correct TPM. You can also configure different hard drives for different operating systems and then enable BitLocker on each one with different authentication methods \(such as one with TPM\-only and one with TPM\+PIN\) without any conflicts.

### <a name="BKMK_AltPC"></a>Can I access my BitLocker\-protected drive if I insert the hard disk into a different computer?
Yes, if the drive is a data drive, you can unlock it from the **BitLocker Drive Encryption** Control Panel item just as you would any other data drive by using a password or smart card. If the data drive was configured for automatic unlock only, you will have to unlock it by using the recovery key. If it is an operating system drive mounted on another computer running an operating system version designated in the **Applies To** list at the beginning of this topic, the encrypted hard disk can be unlocked by a data recovery agent \(if one was configured\) or it can be unlocked by using the recovery key.

> [!NOTE]
> Capabilities introduced in Windows 8 makes mounting the hard disk on another computer a quick and straightforward way to recover information from a damaged computer that has a BitLocker\-protected drive on the hard disk.

### <a name="BKMK_noturnon"></a>Why is "Turn BitLocker on" not available when I right\-click a drive?
Some drives cannot be encrypted with BitLocker. Reasons a drive cannot be encrypted include insufficient disk size, an incompatible file system, if the drive is a dynamic disk, or a drive is designated as the system partition. By default, the system drive \(or system partition\) is hidden from display in the Computer window. However, if it is not created as a hidden drive when the operating system was installed due to a custom installation process, that drive might be displayed but cannot be encrypted.

### <a name="BKMK_R2disks"></a>What type of disk configurations are supported by BitLocker?
Any number of internal, fixed data drives can be protected with BitLocker. On some versions ATA and SATA\-based, direct\-attached storage devices are also supported. 

## <a name="BKMK_KeyManagement"></a>Key management

### <a name="BKMK_Key"></a>What is the difference between a TPM owner password, recovery password, recovery key, password, PIN, enhanced PIN, and startup key?
There are multiple keys that can be generated and used by BitLocker. Some keys are required and some are optional protectors you can choose to use depending on the level of security you require.


### <a name="BKMK_RecoveryPass"></a>How can the recovery password and recovery key be stored?
The recovery password and recovery key for an operating system drive or a fixed data drive can be saved to a folder, saved to one or more USB devices, saved to your Microsoft account online, or printed.

For removable data drives, the recovery password and recovery key can be saved to a folder, saved to your Microsoft account online, or printed. By default, you cannot store a recovery key for a removable drive on a removable drive.

A domain administrator can additionally configure Group Policy to automatically generate recovery passwords and store them in Active Directory Domain Services \(AD??DS\) for any BitLocker\-protected drive.


### <a name="BKMK_EnableAuthWODecrypt"></a>Is it possible to add an additional method of authentication without decrypting the drive if I only have the TPM authentication method enabled?
You can use the Manage\-bde.exe command\-line tool to replace your TPM\-only authentication mode with a multifactor authentication mode. For example, if BitLocker is enabled with TPM authentication only and you want to add PIN authentication, use the following commands from an elevated command prompt, replacing *<4\-20 digit numeric PIN>* with the numeric PIN you want to use:

**manage\-bde ???protectors ???delete %systemdrive% \-type tpm**

**manage\-bde ???protectors ???add %systemdrive% \-tpmandpin** *<4\-20 digit numeric PIN>*


### <a name="BKMK_RecoveryInfo"></a>If I lose my recovery information, will the BitLocker\-protected data be unrecoverable?
BitLocker is designed to make the encrypted drive unrecoverable without the required authentication. When in recovery mode, the user needs the recovery password or recovery key to unlock the encrypted drive.

> [!IMPORTANT]
> Store the recovery information in AD??DS, along with your Microsoft account online, or another safe location.

### <a name="BKMK_USBDrive"></a>Can the USB flash drive that is used as the startup key also be used to store the recovery key?
While this is technically possible, it is not a best practice to use one USB flash drive to store both keys. If the USB flash drive that contains your startup key is lost or stolen, you also lose access to your recovery key. In addition, inserting this key would cause your computer to automatically boot from the recovery key even if TPM\-measured files have changed, which circumvents the TPM's system integrity check.

### <a name="BKMK_StartUpKey"></a>Can I save the startup key on multiple USB flash drives?
Yes, you can save a computer's startup key on multiple USB flash drives. Right\-clicking a BitLocker\-protected drive and selecting **Manage BitLocker** will provide you the options to duplicate the recovery keys as needed.

### <a name="BKMK_MultiKeyOneUSB"></a>Can I save multiple \(different\) startup keys on the same USB flash drive?
Yes, you can save BitLocker startup keys for different computers on the same USB flash drive.

### <a name="BKMK_MultiKey"></a>Can I generate multiple \(different\) startup keys for the same computer?
You can generate different startup keys for the same computer through scripting. However, for computers that have a TPM, creating different startup keys prevents BitLocker from using the TPM's system integrity check.

### <a name="BKMK_MultiPIN"></a>Can I generate multiple PIN combinations?
It is not possible to generate multiple PIN combinations.

### <a name="BKMK_EncryptKeys"></a>What encryption keys are used in BitLocker? How do they work together?
Raw data is encrypted with the full volume encryption key, which is then encrypted with the volume master key. The volume master key is in turn encrypted by one of several possible methods depending on your authentication \(that is, key protectors or TPM\) and recovery scenarios.

### <a name="BKMK_KeyStorage"></a>Where are the encryption keys stored?
The full volume encryption key is encrypted by the volume master key and stored in the encrypted drive. The volume master key is encrypted by the appropriate key protector and stored in the encrypted drive. If BitLocker has been suspended, the clear key that is used to encrypt the volume master key is also stored in the encrypted drive, along with the encrypted volume master key.

This storage process ensures that the volume master key is never stored unencrypted and is protected unless you disable BitLocker. The keys are also saved to two additional locations on the drive for redundancy. The keys can be read and processed by the boot manager.

### <a name="BKMK_FuncKey"></a>Why do I have to use the function keys to enter the PIN or the 48\-character recovery password?
The F1 through F10 keys are universally mapped scan codes available in the pre\-boot environment on all computers and in all languages. The numeric keys 0 through 9 are not usable in the pre\-boot environment on all keyboards.

When using an enhanced PIN, users should run the optional system check during the BitLocker setup process to ensure that the PIN can be entered correctly in the pre\-boot environment.

### <a name="BKMK_YouBrute"></a>How does BitLocker help prevent an attacker from discovering the PIN that unlocks my operating system drive?
It is possible that a personal identification number \(PIN\) can be discovered by an attacker performing a brute force attack. A brute force attack occurs when an attacker uses an automated tool to try different PIN combinations until the correct one is discovered. For BitLocker\-protected computers, this type of attack, also known as a dictionary attack, requires that the attacker have physical access to the computer.

The TPM has the built\-in ability to detect and react to these types of attacks. Because different manufacturers' TPMs may support different PIN and attack mitigations, contact your TPM's manufacturer to determine how your computer's TPM mitigates PIN brute force attacks.

After you have determined your TPM's manufacturer ,contact the manufacturer to gather the TPM's vendor\-specific information. Most manufacturers use the PIN authentication failure count to exponentially increase lockout time to the PIN interface. However, each manufacturer has different policies regarding when and how the failure counter is decreased or reset.

### <a name="BKMK_TPMDAM"></a>How can I evaluate a TPM's dictionary attack mitigation mechanism?
The following questions can assist you when asking a TPM manufacturer about the design of a dictionary attack mitigation mechanism:

-   How many failed authorization attempts can occur before lockout?

-   What is the algorithm for determining the duration of a lockout based on the number of failed attempts and any other relevant parameters?

-   What actions can cause the failure count and lockout duration to be decreased or reset?

### <a name="BKMK_PINLength"></a>Can PIN length and complexity be managed with Group Policy?
Yes and No. You can configure the minimum personal identification number \(PIN\) length by using the **Configure minimum PIN length for startup** Group Policy setting and allow the use of alphanumeric PINs by enabling the **Allow enhanced PINs for startup** Group Policy setting. However, you cannot require PIN complexity by Group Policy.

## <a name="BKMK_BTGsect"></a>BitLocker To Go
BitLocker To Go is BitLocker Drive Encryption on removable data drives. This includes the encryption of USB flash drives, SD cards, external hard disk drives, and other drives formatted by using the NTFS, FAT16, FAT32, or exFAT file systems.

## <a name="BKMK_ADDS"></a>Active Directory Domain Services \(AD??DS\)


### What if BitLocker is enabled on a computer before the computer has joined the domain?
If BitLocker is enabled on a drive before Group Policy has been applied to enforce backup, the recovery information will not be automatically backed up to AD??DS when the computer joins the domain or when Group Policy is subsequently applied. However, in Windows 8 you can use the **Choose how BitLocker\-protected operating system drives can be recovered**, **Choose how BitLocker\-protected fixed drives can be recovered** and **Choose how BitLocker\-protected removable drives can be recovered** Group Policy settings to require that the computer be connected to a domain before BitLocker can be enabled to help ensure that recovery information for BitLocker\-protected drives in your organization is backed up to AD??DS.

The BitLocker Windows Management Instrumentation \(WMI\) interface does allow administrators to write a script to back up or synchronize an online client's existing recovery information; however, BitLocker does not automatically manage this process. The Manage\-bde command\-line tool can also be used to manually back up recovery information to AD??DS. For example, to back up all of the recovery information for the C: drive to AD??DS, you would use the following command from an elevated command prompt: **manage\-bde \-protectors \-adbackup C:**.

> [!IMPORTANT]
> Joining a computer to the domain should be the first step for new computers within an organization. After computers are joined to a domain, storing the BitLocker recovery key to AD??DS is automatic \(when enabled in Group Policy\).

### <a name="BKMK_addseventlog"></a>Is there an event log entry recorded on the client computer to indicate the success or failure of the Active Directory backup?
Yes, an event log entry that indicates the success or failure of an Active Directory backup is recorded on the client computer. However, even if an event log entry says "Success," the information could have been subsequently removed from AD??DS, or BitLocker could have been reconfigured in such a way that the Active Directory information can no longer unlock the drive \(such as by removing the recovery password key protector\). In addition, it is also possible that the log entry could be spoofed.

Ultimately, determining whether a legitimate backup exists in AD??DS requires querying AD??DS with domain administrator credentials by using the BitLocker password viewer tool.

### <a name="BKMK_Refresh"></a>If I change the BitLocker recovery password on my computer and store the new password in AD??DS, will AD??DS overwrite the old password?
No. By design, BitLocker recovery password entries do not get deleted from AD??DS; therefore, you might see multiple passwords for each drive. To identify the latest password, check the date on the object.

### <a name="BKMK_adbackupfails"></a>What happens if the backup initially fails? Will BitLocker retry the backup?
If the backup initially fails, such as when a domain controller is unreachable at the time when the BitLocker setup wizard is run, BitLocker does not try again to back up the recovery information to AD??DS.

When an administrator selects the **Require BitLocker backup to AD??DS** check box of the **Store BitLocker recovery information in Active Directory Domain Service \(Windows 2008 and Windows Vista\)** policy setting, or the equivalent **Do not enable BitLocker until recovery information is stored in AD DS for \(operating system | fixed data | removable data\) drives** check box in any of the **Choose how BitLocker\-protected operating system drives can be recovered**, **Choose how BitLocker\-protected fixed data drives can be recovered**, **Choose how BitLocker\-protected removable data drives can be recovered** policy settings, this prevents users from enabling BitLocker unless the computer is connected to the domain and the backup of BitLocker recovery information to AD??DS succeeds. With these settings configured if the backup fails, BitLocker cannot be enabled, ensuring that administrators will be able to recover BitLocker\-protected drives in the organization.

When an administrator clears these check boxes, the administrator is allowing a drive to be BitLocker\-protected without having the recovery information successfully backed up to AD??DS; however, BitLocker will not automatically retry the backup if it fails. Instead, administrators can create a script for the backup.

## <a name="BKMK_Security"></a>Security

### <a name="BKMK_Form"></a>What form of encryption does BitLocker use? Is it configurable?
BitLocker uses Advanced Encryption Standard \(AES\) as its encryption algorithm with configurable key lengths of 128 or 256 bits. The default encryption setting is AES\-128, but the options are configurable by using Group Policy.

### <a name="BKMK_Config"></a>What is the best practice for using BitLocker on an operating system drive?
The recommended practice for BitLocker configuration on an operating system drive is to implement BitLocker on a computer with a TPM version??1.2  or 2.0 and a Trusted Computing Group \(TCG\)\-compliant BIOS or UEFI firmware implementation, plus a PIN. By requiring a PIN that was set by the user in addition to the TPM validation, a malicious user that has physical access to the computer cannot simply start the computer.

### <a name="BKMK_Sleep"></a>What are the implications of using the sleep or hibernate power management options?
BitLocker on operating system drives in its basic configuration \(with a TPM but without advanced authentication\) provides additional security for the hibernate mode. However, BitLocker provides greater security when it is configured to use an advanced authentication mode \(TPM\+PIN, TPM\+USB, or TPM\+PIN\+USB\) with the hibernate mode. This method is more secure because returning from hibernation requires BitLocker authentication. As a best practice, we recommend that sleep mode be disabled and that you use TPM\+PIN for the authentication method.

### <a name="BKMK_Root"></a>What are the advantages of a TPM?
Most operating systems use a shared memory space and rely on the operating system to manage physical memory. A TPM is a hardware component that uses its own internal firmware and logic circuits for processing instructions, thus shielding it from external software vulnerabilities. Attacking the TPM requires physical access to the computer. Additionally, the tools and skills necessary to attack hardware are often more expensive, and usually are not as available as the ones used to attack software. And because each TPM is unique to the computer that contains it, attacking multiple TPM computers would be difficult and time\-consuming.

> [!NOTE]
> Configuring BitLocker with an additional factor of authentication provides even more protection against TPM hardware attacks.

### <a name="BKMK_FIPS"></a>Is Microsoft pursuing any security certification for BitLocker?
All of the versions of BitLocker that have been included with the operating system have obtained the Federal Information Processing Standard \(FIPS\) 140\-2 certification, and have been Common Criteria certified EAL4\+. These certifications have also been completed for Windows 8, and  Windows Server 2012 , and Windows 8.1 and  Windows Server 2012 R2  are in process.

## <a name="BKMK_BNUsect"></a>BitLocker Network Unlock
BitLocker Network Unlock enables easier management for BitLocker\-enabled desktops and servers that use the TPM\+PIN protection method in a domain environment. When a computer that is connected to a wired corporate network is rebooted, Network Unlock allows the PIN entry prompt to be bypassed. It automatically unlocks BitLocker\-protected operating system volumes by using a trusted key that is provided by the Windows Deployment Services server as its secondary authentication method.

To use Network Unlock you must also have a PIN configured for your computer. When your computer is not connected to the network you will need to provide the PIN to unlock it.

BitLocker Network Unlock has software and hardware requirements for both client computers, Windows Deployment services, and domain controllers that must be met before you can use it. 

Network Unlock uses two protectors, the TPM protector and the one provided by the network or by your PIN, whereas automatic unlock uses a single protector, the one stored in the TPM. If the computer is joined to a network without the key protector it will prompt you to enter your PIN. If the PIN is not available you will need to use the recovery key to unlock the computer if it can ot be connected to the network.

## <a name="BKMK_Other"></a>Other questions

### <a name="BKMK_EFS"></a>Can I use EFS with BitLocker?
Yes, you can use Encrypting File System \(EFS\) to encrypt files on a BitLocker\-protected drive. 

### <a name="BKMK_Kernel"></a>Can I run a kernel debugger with BitLocker?
Yes. However, the debugger should be turned on before enabling BitLocker. Turning on the debugger ensures that the correct measurements are calculated when sealing to the TPM, allowing the computer to start properly. If you need to turn debugging on or off when using BitLocker, be sure to suspend BitLocker first to avoid putting your computer into recovery mode.

### <a name="BKMK_ErrorReports"></a>How does BitLocker handle memory dumps?
BitLocker has a storage driver stack that ensures emory dumps are encrypted when BitLocker is enabled.

### <a name="BKMK_Smart"></a>Can BitLocker support smart cards for pre\-boot authentication?
BitLocker does not support smart cards for pre\-boot authentication. There is no single industry standard for smart card support in the firmware, and most computers either do not implement firmware support for smart cards, or only support specific smart cards and readers. This lack of standardization makes supporting them very difficult.

### <a name="BKMK_Driver"></a>Can I use a non\-Microsoft TPM driver?
Microsoft does not support non\-Microsoft TPM drivers and strongly recommends against using them with BitLocker. Attempting to use a non\-Microsoft TPM driver with BitLocker may cause BitLocker to report that a TPM is not present on the computer and not allow the TPM to be used with BitLocker.

### <a name="BKMK_MBR"></a>Can other tools that manage or modify the master boot record work with BitLocker?
We do not recommend modifying the master boot record on computers whose operating system drives are BitLocker\-protected for a number of security, reliability, and product support reasons. Changes to the master boot record \(MBR\) could change the security environment and prevent the computer from starting normally, as well as complicate any efforts to recover from a corrupted MBR. Changes made to the MBR by anything other than Windows might force the computer into recovery mode or prevent it from booting entirely.

### <a name="BKMK_syschkfail"></a>Why is the system check failing when I am encrypting my operating system drive?
The system check is designed to ensure your computer's BIOS or UEFI firmware is compatible with BitLocker and that the TPM is working correctly. The system check can fail for several reasons:

-   The computer's BIOS or UEFI firmware cannot read USB flash drives.

-   The computer's BIOS, uEFI firmware, or boot menu does not have reading USB flash drives enabled.

-   There are multiple USB flash drives inserted into the computer.

-   The PIN was not entered correctly.

-   The computer's BIOS or UEFI firmware only supports using the function keys \(F1???F10\) to enter numerals in the pre\-boot environment.

-   The startup key was removed before the computer finished rebooting.

-   The TPM has malfunctioned and fails to unseal the keys.

### <a name="BKMK_usbkeyfail"></a>What can I do if the recovery key on my USB flash drive cannot be read?
Some computers cannot read USB flash drives in the pre\-boot environment. First, check your BIOS or UEFI firmware and boot settings to ensure that the use of USB drives is enabled. If it is not enabled, enable the use of USB drives in the BIOS or UEFI firmware and boot settings and then try to read the recovery key from the USB flash drive again. If it still cannot be read, you will have to mount the hard drive as a data drive on another computer so that there is an operating system to attempt to read the recovery key from the USB flash drive. If the USB flash drive has been corrupted or damaged, you may need to supply a recovery password or use the recovery information that was backed up to AD??DS. Also, if you are using the recovery key in the pre\-boot environment, ensure that the drive is formatted by using the NTFS, FAT16, or FAT32 file system.

### <a name="BKMK_usbkeynosave"></a>Why am I unable to save my recovery key to my USB flash drive?
The **Save to USB** option is not shown by default for removable drives. If the option is unavailable, it means that a system administrator has disallowed the use of recovery keys.

### <a name="BKMK_noautounlock"></a>Why am I unable to automatically unlock my drive?
Automatic unlocking for fixed data drives requires that the operating system drive also be protected by BitLocker. If you are using a computer that does not have a BitLocker\-protected operating system drive, the drive cannot be automatically unlocked. For removable data drives, you can add automatic unlocking by right\-clicking the drive in Windows Explorer and clicking **Manage BitLocker**. You will still be able to use the password or smart card credentials you supplied when you turned on BitLocker to unlock the removable drive on other computers.

### <a name="BKMK_blsafemode"></a>Can I use BitLocker in Safe Mode?
Limited BitLocker functionality is available in Safe Mode. BitLocker\-protected drives can be unlocked and decrypted by using the **BitLocker Drive Encryption** Control Panel item. Right\-clicking to access BitLocker options from Windows Explorer is not available in Safe Mode.

### <a name="BKMK_lockdata"></a>How do I "lock" a data drive?
Both fixed and removable data drives can be locked by using the Manage\-bde command\-line tool and the ???lock command.

> [!NOTE]
> Ensure all data is saved to the drive before locking it. Once locked, the drive will become inaccessible.

The syntax of this command is:

**manage\-bde** *<driveletter>* **\-lock**

Outside of using this command, data drives will be locked on shutdown and restart of the operating system. A removable data drive will also be locked automatically when the drive is removed from the computer.

### <a name="BKMK_shadowcopy"></a>Can I use BitLocker with the Volume Shadow Copy Service?
Yes. However, shadow copies made prior to enabling BitLocker will be automatically deleted when BitLocker is enabled on software\-encrypted drives. If you are using a hardware encrypted drive, the shadow copies are retained.

### <a name="BKMK_VHD"></a>Does BitLocker support virtual hard disks \(VHDs\)?
BitLocker is not supported on bootable VHDs, but BitLocker is supported on data volume VHDs, such as those used by clusters, if you are running Windows 8, Windows 8.1,  Windows Server 2012  or  Windows Server 2012 R2 .

## More information

-   [BitLocker: How to deploy on Windows Server 2012](bitlocker-how-to-deploy-on-windows-server-2012.md)

-   [BitLocker: Use BitLocker Drive Encryption Tools to manage BitLocker](bitlocker-use-bitlocker-drive-encryption-tools-to-manage-bitlocker.md)

-   [BitLocker: Use BitLocker Recovery Password Viewer](bitlocker-use-bitlocker-recovery-password-viewer.md)

-   [Encrypted Hard Drive](encrypted-hard-drive.md)

-   [BitLocker Cmdlets in Windows PowerShell](http://technet.microsoft.com/library/6f49f904-e04d-4b90-afbc-84bc45d4d30d)

If you have a question about using BitLocker that hasn???t been answered in this FAQ, please post it in the [Windows 8 IT Pro Security Forum](http://social.technet.microsoft.com/Forums/w8itprosecurity/threads).


