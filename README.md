# centos8

doc for installing centos8 wifi drivers - broadcom

# some checking 
[root@localhost ~]# lspci -v

13:00.0 Network controller: Broadcom Inc. and subsidiaries BCM43142 802.11b/g/n (rev 01)
	Subsystem: Hewlett-Packard Company Device 804a
	Flags: bus master, fast devsel, latency 0, IRQ 16
	Memory at d3000000 (64-bit, non-prefetchable) [size=32K]
	Capabilities: [40] Power Management version 3
	Capabilities: [58] Vendor Specific Information: Len=78 <?>
	Capabilities: [48] MSI: Enable- Count=1/1 Maskable- 64bit+
	Capabilities: [d0] Express Endpoint, MSI 00
	Capabilities: [100] Advanced Error Reporting
	Capabilities: [13c] Virtual Channel
	Capabilities: [160] Device Serial Number 00-00-e2-ff-ff-aa-d8-5d
	Capabilities: [16c] Power Budgeting <?>
	Kernel driver in use: wl
	Kernel modules: bcma, wl
  
[root@localhost ~]# nmcli device status
DEVICE      TYPE      STATE         CONNECTION 
wlp19s0     wifi      connected     Miaone     
virbr0      bridge    connected     virbr0     
enp7s0      ethernet  disconnected  --         
lo          loopback  unmanaged     --         
virbr0-nic  tun       unmanaged     --

[root@localhost ~]# nmcli general status
STATE      CONNECTIVITY  WIFI-HW  WIFI     WWAN-HW  WWAN    
connected  full          enabled  enabled  enabled  enabled 

root@localhost ~]# systemctl status NetworkManager
● NetworkManager.service - Network Manager
   Loaded: loaded (/usr/lib/systemd/system/NetworkManager.service; enabled; vendor preset: enabled)
   Active: active (running) since Wed 2020-12-02 13:22:10 IST; 10min ago
     Docs: man:NetworkManager(8)
 Main PID: 1008 (NetworkManager)
    Tasks: 3 (limit: 48769)
   Memory: 11.5M
   CGroup: /system.slice/NetworkManager.service
           └─1008 /usr/sbin/NetworkManager --no-daemon
  
# The following packages are prerquistes 

[root@localhost ~]# dnf list installed | grep -i NetworkManager
NetworkManager.x86_64                              1:1.22.8-5.el8_2                               @BaseOS                   
NetworkManager-adsl.x86_64                         1:1.22.8-5.el8_2                               @BaseOS                   
NetworkManager-bluetooth.x86_64                    1:1.22.8-5.el8_2                               @BaseOS                   
NetworkManager-config-server.noarch                1:1.22.8-5.el8_2                               @BaseOS                   
NetworkManager-libnm.x86_64                        1:1.22.8-5.el8_2                               @BaseOS                   
NetworkManager-team.x86_64                         1:1.22.8-5.el8_2                               @BaseOS                   
NetworkManager-tui.x86_64                          1:1.22.8-5.el8_2                               @BaseOS                   
NetworkManager-wifi.x86_64                         1:1.22.8-5.el8_2                               @BaseOS                   
NetworkManager-wwan.x86_64                         1:1.22.8-5.el8_2                               @BaseOS                   
[root@localhost ~]# dnf list installed | grep -i wpa_supp
wpa_supplicant.x86_64                              1:2.9-2.el8                                    @anaconda                 

# update the os
yum update -y

# install the rpm fusion free and non free from the link 
https://rpmfusion.org/Configuration

# execute
sudo dnf config-manager --enable PowerTools

sudo dnf install broadcom-wl

# restart 


