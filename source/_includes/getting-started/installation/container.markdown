## Install Home Assistant Container

{% assign container_image = "homeassistant/home-assistant:stable" %}

These below instructions are for an installation of Home Assistant Container running in your own container environment, which you manage yourself. Any [OCI](https://opencontainers.org/) compatible system can be used, however this guide will focus on installing it with Docker.

<div class='note'>
<b>Prerequisites</b>

This guide assumes that you already have an operating system setup and a container runtime installed (like Docker).
</div>

### Platform Installation

Installation with Docker is straightforward. Adjust the following command so that `/PATH_TO_YOUR_CONFIG` points at the folder where you want to store your configuration and run it.

{% if page.installation_type == 'raspberrypi' %}
  {% include getting-started/installation/container/raspberrypi.markdown %}
{% elsif page.installation_type == 'alternative' %}
  {% include getting-started/installation/container/alternative.markdown %}
{% else %}
  {% include getting-started/installation/container/installation.markdown %}
{% endif %}

### Restart

If you change the configuration you have to restart the server. To do that you have 2 options.

 1. You can go to the **Developer Tools** -> **Services**, select the service `homeassistant.restart` and click "Call Service".
 2. Or you can restart it from a terminal by running `docker restart homeassistant`

### Docker Compose

As the Docker command becomes more complex, switching to `docker-compose` can be preferable and support automatically restarting on failure or system restart. Create a `docker-compose.yml` file:

```yaml
  version: '3'
  services:
    homeassistant:
      container_name: homeassistant
      image: homeassistant/home-assistant:stable
      volumes:
        - /PATH_TO_YOUR_CONFIG:/config
        - /etc/localtime:/etc/localtime:ro
      restart: unless-stopped
      network_mode: host
```

{% tabbed_block %}

- title: Start
  content: |

    ```bash
    docker-compose up -d
    ```

- title: Restart
  content: |

    ```bash
    docker-compose restart
    ```

- title: Update
  content: |

    ```bash
    docker-compose pull
    docker-compose up -d --build homeassistant
    ```

{% endtabbed_block %}

### Exposing Devices

In order to use Z-Wave, Zigbee or other integrations that require access to devices, you need to map the appropriate device into the container. Ensure the user that is running the container has the correct privileges to access the `/dev/tty*` file, then add the device mapping to your Docker instructions:

{% include getting-started/installation/container/expose_devices.markdown %}

{% if page.installation_type == 'macos' %}
<div class='note'>

On Mac, USB devices are [not passed through](https://github.com/docker/for-mac/issues/900) by default. Follow the instructions in [Using USB with Docker for Mac](https://dev.to/rubberduck/using-usb-with-docker-for-mac-3fdd) by Christopher McClellan if your device is not showing up.

</div>
{% endif %}

### Optimizations

The Home Assistant Container is using an alternative memory allocation library [jemalloc](http://jemalloc.net/) for better memory management and Python runtime speedup.

As jemalloc can cause issues on certain hardware, it can be disabled by passing the environment variable `DISABLE_JEMALLOC` with any value, for example: `-e "DISABLE_JEMALLOC=true"`.

The error message `<jemalloc>: Unsupported system page size` is one known indicator.

{% include getting-started/next_step.html step="onboarding" link="/getting-started/onboarding" %}