Process:
================
The program/script collection will generate root certificates in a "generated"-folder.
The script will guide the team through distributing the files onto the thumb drives.

Roles:
-----------

Escrow:
- Holder for "escrow{1,2}" thumb drives
- Holder for "escrow{1,2}" password
- Observer for "escrow{1,2}"

Critical:
- Operator, Holder for "operative"

CRL-publication (no member of the critical team):
- Holder for CRL-password {1,2}-{1,2}

This persons must not have any other roles:
- Auditor

No person is allowed to have 2 Roles in one of the Blocks "Escrow", "Critical", "CRL-publication". Having more than one role should be avoided at all costs.


Input Artifacts:
-------------------
- A verified live system CD-R (debian)
- A CD-R with the nre-repository (USB or Flashdisk not possible? we check the Checksum)
- A dedicated machine (with atleast 3 usb ports)
- 8 blank, fresh USBthumb drive (named "escrow{1,2}" and "operative", "offlinePassword", "crlPassword{1,2}-{1,2}" )
- The checksums of the source code (on paper)
- pen and paper (for noting fingerprints)
- 2+8 sealable envelopes

Execution:
---------------------------------------

- Physically remove any hard drive and other storage from the computer
- Reconnect only:
    - A CD-ROM drive to read the live system CD
    - A CD-ROM drive to read the nre-repository
- Boot a Debian live CD system based on the same version as the new signer OS. (debian 8 ?)
- Ensure the system has a reasonable real-time clock configuration
- for all (the 8) thumb drives
  - connect theblank, fresh USB thumb drive
  - format the USB thumb drive
- verify the checksums of the nre-repository source code.

- Reboot the live CD system



- Create a timed log of the steps ( "script -ttimelog"):
  - copy the source code into a ramdisk
  - execute "all.sh"
  - execute more sub-scripts (?)
  - copy "generated/offlinePassword.txt" onto "offlinePassword", (remove "offlinePassword.txt" (?) )
  - copy "generated/crlPassword{1-2}-{1-2}" onto "crlPassword{1,2}-{1,2}", ( remove them (?) )
  - copy "generated/offline.tar.gz.aes-256-cbc" onto "escrow1" and "escrow2"
  - copy "generated/gigi-2015.tar.gz", "generated/signer-client-2015.tar.gz", "generated/signer-server-2015.tar.gz", "generated/crls2015...." onto "operative"
  - store dmesg on "operative", "escrow1" and "escrow2" as "dmesg.log"
  - end of log

- store the log on "operative", "escrow1" and "escrow2" as "typescript" with timing information in "timelog"

- unmount, eject and disconnect "operative", "escrow1" and "escrow2"
- &lt;?&gt; copies the contents of "generated/offlinePassword" to two pieces of paper and puts them each into sealed envelope (password not on paper?)

- All 8 thumbdrives are put into individual sealed envelopes.

Post Execution Steps
---------------------
- all witnesses send signed mails to board@lists.cacert.org indicating the successful execution of the process and containing the fingerprints.
- "escrow1" goes to Person(Holder for "escrow1" thumb drive) , "escrow2" goes to Person(Holder for "escrow2" thumb drive)
- the passwords for "escrow{1,2}" go to Person(Holder for "escrow1" password) and Person(Holder for "escrow2"-Password)
- "operative" goes to Person(Operator, Holder for "operative") and will be installed in the new system.
- "crlPassword{1,2}-{1,2}" go to Person(Holder for "CRL-password{1,2}-{1,2}")
  - those persons publish those passwords, one every month and stop publishing when asked to do so by a correctly signed mail from board or other personsentitled to do so by SP.

- Person(Auditor) verifies process execution

- timed transcript, dmesg and new root certificates go public (fingerprints already are via board mailing list)

Output Artifacts:
-----------------------
- thumb drive "escrow"
- thumb drive "operative"
- password lists for unlocking the CRLs (thumb drives "crlPassword{1-2}-{1,2}")
- password for unlocking "escrow"
- transcript (on "escrow" and on "operative")
- fingerprints of the new certificates

Security Considerations
=====================
- encrypt the CRLs independently or chained?
 - independent: lower risk of failing, lower complexity
 - chained: potentially more security
- offline Password on stick or on paper or only in mind.
 -... TODO
- holders of the CRL passwords are to be listed on the key persons list
 
 
Source &amp; Links:
======================
https://wiki.cacert.org/Roots/EscrowAndRecovery/NewRootCertificatesForCAcert
https://wiki.cacert.org/Roots/Contents
https://wiki.cacert.org/Roots/Structure
https://wiki.cacert.org/Roots/EscrowAndRecovery

