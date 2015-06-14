**Note: This is the old readme before we did a GUI. It might be outdated.**

# Enrollment Station using YubiKey Smart Cards

A Smart Card enrollment station for use in enterprises with Microsoft Active Directory Certificate Services and certificate-based logons. This software package will streamline some operations such as enrolling and terminating Smart Card devices.

This project is an entry in the YubiKing competition and should be considered a work in progress.

### Dependencies
* Windows PKI (Active Directory Certificate Services)
* Enrollment Agent Certificate (see prerequisites)
* CCID smart cards from Yubico (currently Premium NEO and Premium NEO-N)
* (optional) YubiHSM

## Prerequisites
To use this tool you will need an Enrollment Agent Certificate which allows you to enroll certificates on behalf of other users. This certificate template is available on a default Active Directory Certificate Services (Windows CA) installation, but is normally not permitted for any users other than Domain Admins. For added security, create a dedicated user which is used as the enrollment station user.

**A. Setup Enrollment Agent certificate template permissions**
1. Log on to your Windows Certificate Authority
2. Open the Certificate Authority control panel
3. Right click the `Certificate Templates` folder and chose `Manage`
4. Find the `Enrollment Agent` template, right click on it and chose `Properties`
5. In the security tab, allow your enrollment station user to enroll the certificate.

After a while, the template should be available to the enrollment station user through the Certificates snap-in in MMC.

**B. Enroll the Enrollment Agent certificate**
1. Log on to your enrollment station as your enrollment user and open MMC.
2. In MMC, add the Certificates snap-in for the current user, and expand the Personal folder.
3. Right click on the Certificates folder and chose `Request new Certificate`. Follow the wizard, and select the `Enrollment Agent` template when asked for template.

After setting up the Enrollment Agent certificate, you need a YubiKey set to CCID Smart Card mode.

**C. Changing YubiKey to CCID Smart Card mode**
1. Download YubiKey NEO Manager from here https://developers.yubico.com/yubikey-neo-manager/Releases/
2. Under `Devices` select `YubiKey NEO`
3. Click `Change connection mode`
4. Tick `CCID*` and click `OK`

## Documentation
See the documentation PDF

## Todo
* Improve YubiHSM handling (remember choices, fail if missing and previously used)
* Handle more diverse PKI setups (possibly store a favourite CA in an options)
* Add more interactive texts to advise the user when its safe to remove a Yubikey
* Store some strings encrypted (e.g. Management Key)
* Verify data from AD (e.g. specified usernames to enroll on behalf of)
* Describe revoke procedure and requirements thereto (permissions, COM object .. )