## Update

{% if page.installation == "os" or page.installation == "supervised" %}

Best practice for updating a Home Assistant installation:

1. Backup your installation, using the snapshot functionality Home Assistant offers.
2. Check the release notes for breaking changes on [Home Assistant release notes](https://github.com/home-assistant/home-assistant/releases). Be sure to check all release notes between the version you are running and the one you are upgrading to. Use the search function in your browser (`CTRL + f`) and search for **Breaking Changes**.
3. Check your configuration using the [Check Home Assistant configuration](/addons/check_config/) add-on.
4. If the check passes, you can safely update. If not, update your configuration accordingly.
5. Update Home Assistant.

{% else %}

Check the release notes for breaking changes on [Home Assistant release notes](https://github.com/home-assistant/home-assistant/releases). Be sure to check all release notes between the version you are running and the one you are upgrading to. Use the search function in your browser (`CTRL + f`) and search for **Breaking Changes**.

{% endif %}

{% if page.installation == "os" or page.installation == "supervised" %}

To update Home Assistant Core you have 2 options.

**Option 1 - Using the UI:**

1. Open your Home Assistant UI
2. Navigate to the Supervisor panel
3. On the Dashboard tab you will be presented with an update notification

**Option 2 - Using the CLI in an add-on:**

```bash
ha core update
```

{% elsif page.installation == "container" %}

```bash
ha os upgrade --version {{current_version}}
```

{% elsif page.installation == "core" %}

1. Switch to the user that is running Home Assistant

    ```bash
    sudo -u homeassistant -H -s
    ```

2. Activate the virtual environment that Home Assistant is running in

    ```bash
    source /srv/homeassistant/bin/activate
    ```

3. Download and install the version you want

    ```bash
    pip3 install homeassistant=={{current_version}}
    ```

4. When that is complete restart the service for it to use the new files.

{% endif %}
