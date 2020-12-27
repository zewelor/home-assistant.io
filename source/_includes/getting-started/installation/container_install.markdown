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
      --name="home-assistant" \
      -v /etc/localtime:/etc/localtime:ro \
      -v {{ docker_install_local_path }}:/config \
      {{ network }} \
      {{ container_image }}
    ```

- title: Update
  content: |

    ```{{ docker_install_highlight }}
    docker pull {{ container_image }}  # if this returns "Image is up to date" then you can stop here
    docker stop home-assistant  # stop the running container
    docker rm home-assistant  # remove it from Docker's list of containers
    docker run --init -d \
      --name="home-assistant" \
      -e "TZ=America/New_York" \
      -v {{ docker_install_local_path }}:/config \
      {{ network }} \
      {{ container_image }} # finally, start a new one
    ```

- title: Remove
  content: |

    ```{{ docker_install_highlight }}
    docker stop home-assistant  # stop the running container
    docker rm home-assistant  # remove it from Docker's list of containers
    ```

{% endtabbed_block %}