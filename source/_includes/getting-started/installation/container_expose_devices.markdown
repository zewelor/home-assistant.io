{% if page.installation_type == 'windows' %}
  {% assign docker_expose_device_highlight = "powershell" %}
  {% assign docker_expose_device_local_path = '"//c/Users/<your login name>/homeassistant"' %}
  {% assign network = "--port 8123:8123" %}
{% else %}
  {% assign docker_expose_device_highlight = "bash" %}
  {% assign docker_expose_device_local_path = "/PATH_TO_YOUR_CONFIG" %}
  {% assign network = "--network=host" %}
{% endif %}

{% tabbed_block %}

- title: Docker CLI
  content: |

    ```{{ docker_expose_device_highlight }}
    docker run --init -d \
      --name="home-assistant" \
      -v /etc/localtime:/etc/localtime:ro \
      -v {{ docker_expose_device_local_path }}:/config \
      --device /dev/ttyUSB0:/dev/ttyUSB0 \
      {{ network }} \
      homeassistant/home-assistant:stable
    ```

- title: Docker Compose
  content: |

    ```yaml
      version: '3'
      services:
        homeassistant:
          container_name: home-assistant
          image: homeassistant/home-assistant:stable
          volumes:
            - /PATH_TO_YOUR_CONFIG:/config
            - /etc/localtime:/etc/localtime:ro
          devices:
            - /dev/ttyUSB0:/dev/ttyUSB0
            - /dev/ttyUSB1:/dev/ttyUSB1
            - /dev/ttyACM0:/dev/ttyACM0
          restart: always
          network_mode: host
    ```

{% endtabbed_block %}