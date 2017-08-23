ISC-DHCPD settings for pxe+uefi

Tested with ESXi 6.5 and Centos 7

dhcpd.conf

option space pxelinux;
option pxelinux.magic code 208 = string;
option pxelinux.configfile code 209 = text;
option pxelinux.pathprefix code 210 = text;
option pxelinux.reboottime code 211 = unsigned integer 32;
option architecture-type code 93 = unsigned integer 16;

class "pxeclients" {
    match if substring (option vendor-class-identifier, 0, 9) = "PXEClient";

    if option architecture-type = 00:09 {
        filename "shim.efi";
    } else {
        filename "pxelinux.0";
    }
}

https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Installation_Guide/chap-installation-server-setup.html

https://wiki.fogproject.org/wiki/index.php?title=BIOS_and_UEFI_Co-Existence

https://rhinstaller.github.io/anaconda/boot-options.html

https://github.com/Linaro/documentation/blob/master/Reference-Platform/EECommon/Install-CentOS-7.md

