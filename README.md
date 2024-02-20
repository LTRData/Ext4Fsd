
About
-----

    This is a branch of the Ext2Fsd project by Matt Wu where I try to implement support for metadata
    checksums and jbd2. I have also updated the project so it can be compiled with Visual Studio 2017
    and Visual Studio 2019.
    The current status of the development is that all metadata checksums is implemented and jbd2 is
    ported to support 64-bit blocknumbers.
    The driver is now ready to be tested!
    This work is dedicated to my mother Berit Ingegerd Branten.
    Bo Branten <bosse@accum.se>


Signed for Win11?
-----------------

    Help me test a signed version for Windows 11:
    Install program: https://www.accum.se/~bosse/ext2fsd/0.70/Ext2Fsd-setup-signed-win11.exe
    Driver file to upgrade: https://www.accum.se/~bosse/ext2fsd/0.70/ext2fsd.sys


Test
----

    To test this driver run one of the installation programs:
    http://www.accum.se/~bosse/ext2fsd/0.70/Ext2Fsd-0.70b3w10-setup.exe for Windows 8 - Windows 10.
    http://www.accum.se/~bosse/ext2fsd/0.70/Ext2Fsd-0.70b3xp-setup.exe for Windows XP - Windows 7.
    If you compile the driver yourself you only need to run the installation program once, then you can
    copy your driver file over the old in \windows\system32\drivers.
    Now you can read and write ext4 filesystems using the new features metadata checksums and 64-bit
    blocknumbers from Windows.
    (sorry I can not sign drivers so you need to turn of Windows checking for that during testing)
    official site: http://www.ext2fsd.com/
    my site: http://www.accum.se/~bosse/


Introduction
------------

    Ext4Fsd is an ext2/3/4 file system driver for Windows (XP/Vista/7/8/10/11).
    It's a free and open-source software, everyone can modify or distribute under GNU GPLv2.

    
Development Website
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
