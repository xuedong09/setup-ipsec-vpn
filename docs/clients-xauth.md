﻿## Configure IPsec/XAuth VPN Clients

*Read this in other languages: [English](clients-xauth.md), [简体中文](clients-xauth-zh.md).*

*To connect using IPsec/L2TP mode, see: [Configure IPsec/L2TP VPN Clients](clients.md)*

After <a href="https://github.com/hwdsl2/setup-ipsec-vpn" target="_blank">setting up your own VPN server</a>, follow these steps to configure your devices. IPsec/XAuth ("Cisco IPsec") is natively supported by Android, iOS and OS X. There is no additional software to install. Windows users can use the free <a href="https://www.shrew.net/download/vpn" target="_blank">Shrew Soft client</a>. In case you are unable to connect, first check to make sure the VPN credentials were entered correctly.

`IPsec/XAuth` mode is also called "Cisco IPsec". Compared to `IPsec/L2TP`, it is generally faster with less overhead.

---
* Platforms
  * [Windows](#windows)
  * [OS X (macOS)](#os-x)
  * [Android](#android)
  * [iOS (iPhone/iPad)](#ios)

### Windows ###

**Note:** You can also connect using [IPsec/L2TP mode](clients.md). No additional software is required.

1. Download and install the free <a href="https://www.shrew.net/download/vpn" target="_blank">Shrew Soft VPN client</a>.
1. Click Start Menu -> All Programs -> ShrewSoft VPN Client -> VPN Access Manager
1. Click the **Add (+)** button on toolbar.
1. Enter `Your VPN Server IP` in the **Host Name or IP Address** field.
1. Click the **Authentication** tab. Select **Mutual PSK + XAuth** from the **Authentication Method** drop-down menu.
1. Click the **Credentials** tab below. Enter `Your VPN IPsec PSK` in the **Pre Shared Key** field.
1. Click the **Phase 1** tab. Select **main** from the **Exchange Type** drop-down menu.
1. Click **Save** to save the VPN connection details.
1. Select the new VPN connection. Click the **Connect** button on toolbar.
1. Enter `Your VPN Username` in the **Username** field.
1. Enter `Your VPN Password` in the **Password** field.
1. Click **Connect**.

Once connected, you will see **tunnel enabled** in the VPN Connect status window. You can verify that your traffic is being routed properly by <a href="https://encrypted.google.com/search?q=my+ip" target="_blank">looking up your IP address on Google</a>. It should say "Your public IP address is `Your VPN Server IP`".

<a id="regkey"></a>
If you get an error when trying to connect, see <a href="#troubleshooting">Troubleshooting</a>.

**Note:** This <a href="https://documentation.meraki.com/MX-Z/Client_VPN/Troubleshooting_Client_VPN#Windows_Error_809" target="_blank">one-time registry change</a> is required if the VPN server and/or client is behind NAT (e.g. home router). Refer to the linked web page, or run the following from an <a href="http://www.winhelponline.com/blog/open-elevated-command-prompt-windows/" target="_blank">elevated command prompt</a>. You must reboot your computer when finished.
- For Windows Vista, 7, 8 and 10
  ```console
  REG ADD HKLM\SYSTEM\CurrentControlSet\Services\PolicyAgent /v AssumeUDPEncapsulationContextOnSendRule /t REG_DWORD /d 0x2 /f
  ```

- For Windows XP ONLY
  ```console
  REG ADD HKLM\SYSTEM\CurrentControlSet\Services\IPSec /v AssumeUDPEncapsulationContextOnSendRule /t REG_DWORD /d 0x2 /f
  ```

### OS X ###
1. Open System Preferences and go to the Network section.
1. Click the **+** button in the lower-left corner of the window.
1. Select **VPN** from the **Interface** drop-down menu.
1. Select **Cisco IPSec** from the **VPN Type** drop-down menu.
1. Enter anything you like for the **Service Name**.
1. Click **Create**.
1. Enter `Your VPN Server IP` for the **Server Address**.
1. Enter `Your VPN Username` for the **Account Name**.
1. Enter `Your VPN Password` for the **Password**.
1. Click the **Authentication Settings** button.
1. In the **Machine Authentication** section, select the **Shared Secret** radio button and enter `Your VPN IPsec PSK`.
1. Leave the **Group Name** field blank.
1. Click **OK**.
1. Check the **Show VPN status in menu bar** checkbox.
1. Click **Apply** to save the VPN connection information.

To connect to the VPN: Use the menu bar icon, or go to the Network section of System Preferences, select the VPN and choose **Connect**. You can verify that your traffic is being routed properly by <a href="https://encrypted.google.com/search?q=my+ip" target="_blank">looking up your IP address on Google</a>. It should say "Your public IP address is `Your VPN Server IP`".

### Android ###
1. Launch the **Settings** application.
1. Tap **More...** in the **Wireless & Networks** section.
1. Tap **VPN**.
1. Tap **Add VPN Profile** or the **+** icon at top-right of screen.
1. Enter anything you like in the **Name** field.
1. Select **IPSec Xauth PSK** in the **Type** drop-down menu.
1. Enter `Your VPN Server IP` in the **Server address** field.
1. Leave the **IPSec identifier** field blank.
1. Enter `Your VPN IPsec PSK` in the **IPSec pre-shared key** field.
1. Tap **Save**.
1. Tap the new VPN connection.
1. Enter `Your VPN Username` in the **Username** field.
1. Enter `Your VPN Password` in the **Password** field.
1. Check the **Save account information** checkbox.
1. Tap **Connect**.

**Note:** Android 6 (Marshmallow) users should edit `/etc/ipsec.conf` on the VPN server and append `,aes256-sha2_256` to both `ike=` and `phase2alg=` lines. Then add a new line `sha2-truncbug=yes` immediately after those. Indent lines with two spaces. When finished, run `service ipsec restart`. (<a href="https://libreswan.org/wiki/FAQ#Android_6.0_connection_comes_up_but_no_packet_flow" target="_blank">Reference</a>)

Once connected, you will see a VPN icon in the notification bar. You can verify that your traffic is being routed properly by <a href="https://encrypted.google.com/search?q=my+ip" target="_blank">looking up your IP address on Google</a>. It should say "Your public IP address is `Your VPN Server IP`".

### iOS ###
1. Go to Settings -> General -> VPN.
1. Tap **Add VPN Configuration...**.
1. Tap **Type**. Select **IPSec** and go back.
1. Tap **Description** and enter anything you like.
1. Tap **Server** and enter `Your VPN Server IP`.
1. Tap **Account** and enter `Your VPN Username`.
1. Tap **Password** and enter `Your VPN Password`.
1. Leave the **Group Name** field blank.
1. Tap **Secret** and enter `Your VPN IPsec PSK`.
1. Tap **Done**.
1. Slide the **VPN** switch ON.

Once connected, you will see a VPN icon in the status bar. You can verify that your traffic is being routed properly by <a href="https://encrypted.google.com/search?q=my+ip" target="_blank">looking up your IP address on Google</a>. It should say "Your public IP address is `Your VPN Server IP`".

## Troubleshooting

### Windows Error 809

> The network connection between your computer and the VPN server could not be established because the remote server is not responding.

To fix this error, follow <a href="#regkey">the steps above</a> to add a registry key and reboot your computer.

### Windows Error 628

> The connection was terminated by the remote computer before it could be completed.

To fix this error, please follow these steps:

1. Right-click on the wireless/network icon in system tray, select **Open Network and Sharing Center**.
1. On the left, click **Change adapter settings**. Right-click on the new VPN and choose **Properties**.
1. Click the **Security** tab. Select "Layer 2 Tunneling Protocol with IPsec (L2TP/IPSec)" for **Type of VPN**.
1. Click **Allow these protocols**. Check "Challenge Handshake Authentication Protocol (CHAP)" and uncheck all others.
1. Click **OK** to save the VPN connection details.

![Select only CHAP in VPN connection properties](https://cloud.githubusercontent.com/assets/5104323/16024310/b113e9b6-3186-11e6-9e03-12f5455487ba.png)

### Other Errors

Please refer to <a href="https://documentation.meraki.com/MX-Z/Client_VPN/Troubleshooting_Client_VPN#Common_Connection_Issues" target="_blank">this document</a> for more troubleshooting tips.

## Credits

This document was adapted from the <a href="https://github.com/jlund/streisand" target="_blank">Streisand</a> project by Joshua Lund and contributors.

## License

Copyright (C) 2016 Lin Song   
Based on <a href="https://github.com/jlund/streisand/blob/master/playbooks/roles/l2tp-ipsec/templates/instructions.md.j2" target="_blank">the work of Joshua Lund</a> (Copyright 2014-2016)

This program is free software: you can redistribute it and/or modify it under the terms of the <a href="https://www.gnu.org/licenses/gpl.html" target="_blank">GNU General Public License</a> as published by the Free Software Foundation, either version 3 of the License, or (at your option) any later version.

This program is distributed in the hope that it will be useful, but WITHOUT ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the GNU General Public License for more details.
