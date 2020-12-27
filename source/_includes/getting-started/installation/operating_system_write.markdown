
### Write the image to your installation media

1. Attach the installation media ({{installation_media}}) to your computer
2. Download and start <a href="https://www.balena.io/etcher" target="_blank">Balena Etcher</a>
3. Select "Flash from URL"
![etcher_from_url](/images/getting-started/installation/etcher1.png)

4. Get the URL for your {{board}}
{% if page.installation_type == 'raspberrypi' %}
{% tabbed_block %}

- title: Raspberry Pi 4 64-bit
  content: |

    ```text
    {{haos_release_base_url}}/{{haos_version}}/hassos_rpi4-64-{{haos_version}}.img.xz
    ```

    _(32-bit is required for GPIO support)_

- title: Raspberry Pi 4 32-bit
  content: |

    ```text
    {{haos_release_base_url}}/{{haos_version}}/hassos_rpi4-{{haos_version}}.img.xz
    ```

    _(64-bit is required for 8 GB model)_

- title: Raspberry Pi 3 64-bit
  content: |

    ```text
    {{haos_release_base_url}}/{{haos_version}}/hassos_rpi3-64-{{haos_version}}.img.xz
    ```

    _(32-bit is required for GPIO support)_

- title: Raspberry Pi 3 32-bit
  content: |

    ```text
    {{haos_release_base_url}}/{{haos_version}}/hassos_rpi4-{{haos_version}}.img.xz
    ```

{% endtabbed_block %}
{% elsif page.installation_type == 'odroid' %}
{% tabbed_block %}

- title: ODROID-N2
  content: |

    ```text
    {{haos_release_base_url}}/{{haos_version}}/hassos_odroid-n2-{{haos_version}}.img.xz
    ```

    [Guide: Flashing Odroid-N2 using OTG-USB](/hassio/flashing_n2_otg/)

- title: ODROID-C2
  content: |

    ```text
    {{haos_release_base_url}}/{{haos_version}}/hassos_odroid-c2-{{haos_version}}.img.xz
    ```

- title: ODROID-C4
  content: |

    ```text
    {{haos_release_base_url}}/{{haos_version}}/hassos_odroid-c4-{{haos_version}}.img.xz
    ```

- title: ODROID-XU4
  content: |

    ```text
    {{haos_release_base_url}}/{{haos_version}}/hassos_odroid-xu4-{{haos_version}}.img.xz
    ```

{% endtabbed_block %}
{% elsif page.installation_type == 'tinkerboard' %}
{% tabbed_block %}

- title: ASUS Tinkerboard
  content: |

    ```text
    {{haos_release_base_url}}/{{haos_version}}/hassos_tinker-{{haos_version}}.img.xz
    ```

{% endtabbed_block %}
{% endif %}

_Select and copy the URL or use the "copy" button that appear when you hover it._

5. Paste the URL for your {{board}} into Balena Etcher and click "OK"
![etcher_from_url_paste](/images/getting-started/installation/etcher2.png)
6. Balena Etcher will now download the image, when that is done click "Select target"
![etcher_select_target](/images/getting-started/installation/etcher3.png)
7. Select the {{installation_media}} you want to use for your {{board}}
![etcher_select_target](/images/getting-started/installation/etcher4.png)
8. Click on "Flash!" to start writing the image
![etcher_select_target](/images/getting-started/installation/etcher5.png)
9. When Balena Etcher is finished writing the image you will get this confirmation
![etcher_select_target](/images/getting-started/installation/etcher6.png)