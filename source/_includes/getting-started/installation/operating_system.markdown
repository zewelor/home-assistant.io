## Install Home Assistant Operating System

{% assign haos_version = "5.9" %}
{% assign haos_release_base_url = "https://github.com/home-assistant/operating-system/releases/download" %}

{% if page.installation_type == 'odroid' %}
  {% assign board = "ODROID" %}
  {% assign installation_media = "eMMC module/SD card" %}
{% elsif page.installation_type == 'raspberrypi' %}
  {% assign board = "Raspberry Pi" %}
  {% assign installation_media = "SD card" %}
{% elsif page.installation_type == 'tinkerboard' %}
  {% assign board = "ASUS Tinkerboard" %}
  {% assign installation_media = "eMMC module/SD card" %}
{% endif %}

Follow this guide if you want to get started with Home Assistant easily or if you have little to no Linux experience

{% if page.installation_type == "raspberrypi" or page.installation_type == "odroid" or page.installation_type == "tinkerboard" %}
{% if page.installation_type == 'raspberrypi' %}

### Suggested Hardware

We will need a few things to get started with installing Home Assistant. Links below lead to Amazon US. If you’re not in the US, you should be able to find these items in web stores in your country.

- [Power Supply](https://www.raspberrypi.org/help/faqs/#powerReqs) (at least 3A)
- [Micro SD Card](https://amzn.to/2X0Z2di). Ideally get one that is [Application Class 2](https://www.sdcard.org/developers/overview/application/index.html) as they handle small I/O much more consistently than cards not optimized to host applications. A 32 GB or bigger card is recommended.
- SD Card reader. This is already part of most laptops, but you can purchase a [standalone USB adapter](https://amzn.to/2WWxntY) if you don't have one. The brand doesn't matter, just pick the cheapest.
- Ethernet cable. Home Assistant can work with Wi-Fi, but an Ethernet connection would be more reliable.

{% endif %}

{% include getting-started/installation/operating_system_write.markdown %}

### Start up your {{board}}

1. Insert the installation media ({{installation_media}}) you just created
2. Attach a ethernet cable for network.
{%- if page.installation_type == 'raspberrypi' or page.installation_type == 'tinkerboard' %}
   - [For Wi-Fi instructions see here]()
{%- endif %}
4. Attach a cable for power
5. Within a few minutes you will be able to reach Home Assistant on <a href="http://homeassistant.local:8123" target="_blank">homeassistant.local:8123</a>. If you are running an older Windows version or have a stricter network configuration, you might need to access Home Assistant at <a href="http://homeassistant:8123" target="_blank">homeassistant:8123</a> or `http://X.X.X.X:8123` (replace X.X.X.X with your {{board}}’s IP address).

{% include getting-started/next_step.html step="onboarding" link="/getting-started/onboarding" %}

{% else %}

### Download the appropriate image

{% if page.installation_type == 'nuc' %}
- [Intel NUC][intel-nuc]
{% else %}

- [VirtualBox][vdi] (.vdi)
- [KVM][qcow2] (.qcow2)
{% if page.installation_type == 'windows' or page.installation_type == 'linux' %}
- [Vmware Workstation][vmdk] (.vmdk)
{% elsif page.installation_type == 'alternative' %}
- [VMware ESXi/vSphere][Virtual Appliance] (.ova)
{% elsif page.installation_type == 'windows' %}
- [Hyper-V][vhdx] (.vhdx)
{% endif %}
{% endif %}
{% if page.installation_type == "raspberrypi" or page.installation_type == "odroid" or page.installation_type == "nuc" or page.installation_type == "tinkerboard" %}
1. Put the SD card in your card reader.
2. Open balenaEtcher, select the Home Assistant image and flash it to the SD card.
3. Unmount the SD card and remove it from your card reader.
{% else %}

### Create the Virtual Machine

Load the appliance image into your virtual machine software. (Note: You are free to assign as much resources as you wish to the VM, please assign enough based on your add-on needs)

Minimum recommended assignments:

- 2GB RAM
- 32GB Storage
- 1vCPU

_All these can be extended if your usage calls for more resources._

### Hypervisor specific configuration

{% tabbed_block %}

- title: VirtualBox
  content: |
    1. Create a new virtual machine
    2. Select “Other Linux (64Bit)
    3. Select “Use an existing virtual hard disk file”, select the VDI file from above
    4. Edit the “Settings” of the VM and go “System” then Motherboard and Enable EFI
    5. Then “Network” “Adapter 1” Bridged and your adapter.

- title: KVM
  content: |
    1. Create a new virtual machine in `virt-manager`
    2. Select “Import existing disk image”, provide the path to the QCOW2 image above
    3. Choose “Generic Default” for the operating system
    4. Check the box for “Customize configuration before install”
    5. Select your bridge under “Network Selection”
    6. Under customization select “Overview” -> “Firmware” -> “UEFI x86_64: …”.****

{% if page.installation_type == 'windows' or page.installation_type == 'linux' %}

- title: Vmware Workstation
  content: |
    1. Create a new virtual machine
    2. Select “Custom”, make it compatible with the default of Workstation and ESX
    3. Choose “I will install the operating system later”, select “Linux” -> “Other Linux 5.x or later kernel 64-bit”
    4. Select “Use Bridged Networking”
    5. Select “Use an existing virtual disk” and select the VMDK file above,

    After creation of VM go to “Settings” and “Options” then “Advanced” and select “Firmware type” to “UEFI”.

{% elsif page.installation_type == 'alternative' %}

- title: VMware ESXi/vSphere
  content: |
    Use the “E1001” or “E1001E” virtual network adapater. There are confirmed mDNS/Multicast discovery issues when using VMware’s “VMXnet3” virtual network adapter.

{% elsif page.installation_type == 'windows' %}
- title: Hyper-V
  content: |
    <div class='note warning'>
        Hyper-V does not have USB support
    </div>

    1. Create a new virtual machine
    2. Select “Generation 2”
    3. Select “Connection -> “Your Virtual Switch that is bridged”
    4. Select “Use an existing virtual hard disk” and select the VHDX file from above

    After creation go to “Settings” -> “Security” and deselect “Enable Secure Boot”.
{% endif %}

{% endtabbed_block %}
{% endif %}

{% include getting-started/next_step.html step="onboarding" link="/getting-started/onboarding" %}
{% endif %}
[pi3-32]: https://github.com/home-assistant/operating-system/releases/download/5.8/hassos_rpi3-5.8.img.xz
[pi3-64]: https://github.com/home-assistant/operating-system/releases/download/5.8/hassos_rpi3-64-5.8.img.xz
[pi4-32]: https://github.com/home-assistant/operating-system/releases/download/5.8/hassos_rpi4-5.8.img.xz
[pi4-64]: https://github.com/home-assistant/operating-system/releases/download/5.8/hassos_rpi4-64-5.8.img.xz
[tinker]: https://github.com/home-assistant/operating-system/releases/download/5.8/hassos_tinker-5.8.img.xz
[odroid-c2]: https://github.com/home-assistant/operating-system/releases/download/5.8/hassos_odroid-c2-5.8.img.xz
[odroid-c4]: https://github.com/home-assistant/operating-system/releases/download/5.8/hassos_odroid-c4-5.8.img.xz
[odroid-n2]: https://github.com/home-assistant/operating-system/releases/download/5.8/hassos_odroid-n2-5.8.img.xz
[odroid-xu4]: https://github.com/home-assistant/operating-system/releases/download/5.8/hassos_odroid-xu4-5.8.img.xz
[intel-nuc]: https://github.com/home-assistant/operating-system/releases/download/5.8/hassos_intel-nuc-5.8.img.xz
[vmdk]: https://github.com/home-assistant/operating-system/releases/download/5.8/hassos_ova-5.8.vmdk.xz
[vhdx]: https://github.com/home-assistant/operating-system/releases/download/5.8/hassos_ova-5.8.vhdx.xz
[vdi]: https://github.com/home-assistant/operating-system/releases/download/5.8/hassos_ova-5.8.vdi.xz
[qcow2]: https://github.com/home-assistant/operating-system/releases/download/5.8/hassos_ova-5.8.qcow2.xz
[Virtual Appliance]: https://github.com/home-assistant/operating-system/releases/download/5.8/hassos_ova-5.8.ova
