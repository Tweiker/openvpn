# openvpn

UPGRADING FROM 2.3-ALPHA1 AND EARLIER

OpenVPN Windows installer went through major changes in
2.3-alpha2. To avoid any unexpected behavior, it is strongly
suggested to upgrade as follows.

First backup configuration files and certificates from your
current installation; by default they're in

    C:\Program Files\OpenVPN\config (32-bit Windows)
    C:\Program Files (x86)\OpenVPN\config (64-bit Windows)

After this, stop the openvpn-gui or the openvpn service
wrapper, if either of them is running and uninstall OpenVPN.
Finally, remove the OpenVPN install directory entirely (e.g.
using Windows Explorer as administrator).

Finally, install the new version of OpenVPN and copy over
your configuration files and certificates, which now go to

    C:\Program Files\OpenVPN\config

provided you did not install the 32-bit version on 64-bit
Windows.

IMPORTANT NOTE FOR WINDOWS VISTA/7 USERS

Note that on Windows Vista, you will need to run the OpenVPN
GUI with administrator privileges, so that it can add routes
to the routing table that are pulled from the OpenVPN server.
You can do this by right-clicking on the OpenVPN GUI
desktop icon, and selecting "Run as administrator".

GENERAL QUICKSTART FOR WINDOWS

The OpenVPN Client requires a configuration file
and key/certificate files. You should obtain
these and save them to OpenVPN's configuration
directory, usually C:\Program Files\OpenVPN\config.

You can run OpenVPN as a Windows system service or by using
the client GUI. To use the OpenVPN GUI, double click on the
desktop icon or start menu icon. The OpenVPN GUI is a
system-tray applet, so an icon for the GUI will appear in
the lower-right corner of the screen. Right click on the
system tray icon, and a menu should appear showing the names
of your OpenVPN configuration files, and giving you the
option to connect.

BUILDING OPENVPN FOR WINDOWS

Official OpenVPN Windows releases are cross-compiled on Linux using the
openvpn-build buildsystem:

    https://community.openvpn.net/openvpn/wiki/BuildingUsingGenericBuildsystem

First setup the build environment as shown in the above article. Then fetch the
openvpn-build repository:

    git clone https://github.com/OpenVPN/openvpn-build.git

Review the build configuration:

    openvpn-build/generic/build.vars
    openvpn-build/windows-nsis/build-complete.vars

Build (unsigned):

    cd openvpn-build/windows-nsis
    ./build-complete

Build (signed):

    cd openvpn-build/windows-nsis
    ./build-complete --sign --sign-pkcs12=<pkcs12-file>\
    --sign-pkcs12-pass=<pkcs12-file-password> \
    --sign-timestamp="<timestamp-url>"
