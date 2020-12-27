{% if page.installation_type == 'windows' %}
  {% assign docker_install_highlight = "powershell" %}
  {% assign docker_install_local_path = '"//c/Users/<your login name>/homeassistant"' %}
  {% assign network = "--port 8123:8123" %}
{% else %}
  {% assign docker_install_highlight = "bash" %}
  {% assign docker_install_local_path = "/PATH_TO_YOUR_CONFIG" %}
  {% assign network = "--network=host" %}
{% endif %}

{% tabbed_block %}

- title: Install
  content: |

    ```{{ docker_install_highlight }}
    docker run --init -d \
      --name homeassistant \
      --restart=unless-stopped \
      -v /etc/localtime:/etc/localtime:ro \
      -v {{ docker_install_local_path }}:/config \
      {{ network }} \
      {{ container_image }}
    ```

- title: Update
  content: |

    ```{{ docker_install_highlight }}
    # if this returns "Image is up to date" then you can stop here
    docker pull {{ container_image }}
    ```

    ```{{ docker_install_highlight }}
    # stop the running container
    docker stop homeassistant
    ```

    ```{{ docker_install_highlight }}
    # remove it from Docker's list of containers
    docker rm homeassistant
    ```

    ```{{ docker_install_highlight }}
    # finally, start a new one
    docker run --init -d \
      --name homeassistant \
      --restart=unless-stopped \
      -v {{ docker_install_local_path }}:/config \
      -v /etc/localtime:/etc/localtime:ro \
      {{ network }} \
      {{ container_image }}
    ```

{% endtabbed_block %}
