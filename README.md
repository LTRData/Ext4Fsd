# Ext4Fsd — LTRData fork

This is an LTRData fork of [Bo Branten's Ext4Fsd](https://github.com/bobranten/Ext4Fsd), itself based on Matt Wu's Ext2Fsd. The filesystem feature descriptions and Bo Branten's development notes below are preserved from upstream.

The source on `master` is based on the February 2024 upstream snapshot, with [two LTRData commits from 1 March 2024](https://github.com/LTRData/Ext4Fsd/compare/e5acade8ef427e221b16b578194a8290b1ba98c2...6a9c283a8579705f5ef3ceafc4fcd3cc7e8239c0) for build compatibility and signing-package preparation. This fork should not be assumed to track current upstream.

## Local changes and building

- Project settings select Windows SDK 10.0.19041.0. The `Ext2Mgr` and `Ext2Srv` applications use the `v142` C++ toolset; `Ext2Mgr` also uses MFC. The driver uses the `WindowsKernelModeDriver10.0` WDK toolset.
- Driver changes include header/declaration compatibility fixes and ARM/ARM64 guards around local CRT replacements.
- [`Ext4Fsd/mkcab.cmd`](Ext4Fsd/mkcab.cmd) and a dummy INF add a local CAB packaging/signing workflow.

To work on this fork:

```sh
git clone --branch master https://github.com/LTRData/Ext4Fsd.git
cd Ext4Fsd
```

Open [`Ext4Fsd.sln`](Ext4Fsd.sln) with the selected C++ toolset, MFC components, SDK and WDK installed. The solution contains the filesystem driver, volume manager (`Ext2Mgr`) and service (`Ext2Srv`). The driver has Win32, x64, ARM and ARM64 configurations; the manager and service have Win32/x64 configurations and are not selected for build in the solution's ARM/ARM64 configurations. The driver output retains the filename `Ext2Fsd.sys`.

The CAB script expects staged Release outputs and the `stampinf`, `inf2cat`, `cabarc` and `signtool` utilities. It contains a fixed signing-certificate selection and timestamp URL that must be adapted for another environment. Its final signing command signs the CAB; running it does not itself produce a Microsoft-signed driver. The OS list passed to the packaging tools is not a tested-platform list.

## Inherited upstream README

The signed-driver downloads, installation guidance, development status and contact details below refer to Bo Branten's upstream project. Those downloads should not be assumed to contain the LTRData changes described above.

---


New
---

    Signed driver for Windows 11:
    https://www.accum.se/~bosse/ext2fsd/0.70/Ext2Fsd-setup-signed-win11.exe
    Signed driver for Windows 10:
    https://www.accum.se/~bosse/ext2fsd/0.70/Ext2Fsd-setup-signed-win10.exe


About
-----

    This is a branch of the Ext2Fsd project by Matt Wu where I try to
    implement support for metadata checksums and jbd2. I have also
    updated the project so it can be compiled with Visual Studio 2019
    and Visual Studio 2022.
    The current status of the development is that all metadata checksums
    is implemented and jbd2 is ported to support 64-bit blocknumbers.
    The driver is now ready to be tested!
    This work is dedicated to my mother Berit Ingegerd Branten.
    Bo Branten <bosse@accum.se>


Test
----

    To test this driver run one of the installation programs:
    Signed driver for Windows 11:
    https://www.accum.se/~bosse/ext2fsd/0.70/Ext2Fsd-setup-signed-win11.exe
    Signed driver for Windows 10:
    https://www.accum.se/~bosse/ext2fsd/0.70/Ext2Fsd-setup-signed-win10.exe
    Signed driver files for manual install: (even ARM/ARM64)
    https://www.accum.se/~bosse/ext2fsd/0.70/signed/
    Unsigned driver for older Windows:
    For Windows 8 - Windows 10:
    https://www.accum.se/~bosse/ext2fsd/0.70/Ext2Fsd-0.70b3w10-setup.exe
    For Windows XP - Windows 7:
    https://www.accum.se/~bosse/ext2fsd/0.70/Ext2Fsd-0.70b3xp-setup.exe

    If you compile the driver yourself you only need to run the installation
    program once, then you can copy your driver file over the old in
    \windows\system32\drivers.
    Now you can read and write ext4 filesystems using the new features
    metadata checksums and 64-bit blocknumbers from Windows.
    my site: http://www.accum.se/~bosse/


Introduction
------------

    Ext4Fsd is an ext2/3/4 file system driver for Windows (XP/Vista/7/8/10/11).
    It's a free and open-source software, everyone can modify or distribute
    under GNU GPLv2.

    
Old Development Website
-------------------

    Matt Wu <mattwu@163.com>
    http://www.ext2fsd.com


Active Developers
-----------------

    Matt Wu : http://github.com/matt-wu
              http://blog.dynox.cn

    KaHo Ng : http://github.com/ngkaho1234

    Bo Branten : http://github.com/bobranten
                 http://www.accum.se/~bosse

    Thanks to Olof Lagerkvist https://github.com/LTRData
    for important help to this project!


Supported Features by Ext4Fsd
-----------------------------

    1, flexible inode size: > 128 bytes, up to block size
    2, dir_index:    htree directory index
    3, filetype:     extra file mode in dentry
    4, large_file:   > 4G files supported
    5, sparse_super: super block backup in group descriptor
    6, uninit_bg:    fast fsck and group checksum
    7, extent:       full support with extending and shrinking.
    8, journal:      only support replay for internal journal
    9, flex_bg:      first flexible metadata group
    10, symlink and hardlink
    11, mount-as-user: specifed uid/gid by user


Unsupported Ext3/4 Features
---------------------------

    1, journal: log-based operations, external journal
    2, EA (extended attributes), ACL support
