{% tabbed_block %}

- title: Install
  content: |

    ```bash
    docker run --init -d \
      --name homeassistant \
      --restart=unless-stopped \
      -v /etc/localtime:/etc/localtime:ro \
      -v /PATH_TO_YOUR_CONFIG:/config \
      --network=host \
      {{ container_image }}
    ```

- title: Update
  content: |

    ```bash
    # if this returns "Image is up to date" then you can stop here
    docker pull {{ container_image }}
    ```

    ```bash
    # stop the running container
    docker stop homeassistant
    ```

    ```bash
    # remove it from Docker's list of containers
    docker rm homeassistant
    ```

    ```bash
    # finally, start a new one
    docker run --init -d \
      --name homeassistant \
      --restart=unless-stopped \
      -v /PATH_TO_YOUR_CONFIG:/config \
      -v /etc/localtime:/etc/localtime:ro \
      --network=host \
      {{ container_image }}
    ```

{% endtabbed_block %}
