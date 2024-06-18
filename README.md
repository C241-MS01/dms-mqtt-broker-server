# MQTT Broker Server

## Description

These are [Docker](https://www.docker.com/) Compose file and configuration files to run an MQTT broker server using [Mosquitto](https://mosquitto.org/). Additionally, the compose file includes [Node-RED](https://nodered.org/) to provide a web interface for interacting with the broker and creating flows. Finally, [Caddy](https://caddyserver.com/) serves as a reverse proxy, securing connections to both the broker and Node-RED.

### Configuration

- `mosquitto.conf`: Mosquitto configuration file.
- `settings.js`: Node-RED configuration file.
- `Caddyfile`: Caddy configuration file.

## Getting Started

1. Ensure you have [Docker](https://www.docker.com/) installed on your system.

    ```bash
    docker --version
    ```

2. Configure the Mosquitto MQTT broker in the `mosquitto.conf` file as needed.

3. Change the domain name in the `Caddyfile` to your own domain name.

    ```bash
    mqtt.example.com { # Change this to your domain name
        reverse_proxy mosquitto:1883
    }
    ```

4. Configure Node-RED in the `settings.js` file. It is recommended to change the users and passwords in the `adminAuth` section.

    ```javascript
    adminAuth: {
        type: "credentials",
        users: [{
            username: "admin",             // Change this to your desired username
            password: "$2a$08$1J9Z6z7...", // Change this to your hashed password by bcrypt
            permissions: "*"               // Change this to your desired permissions
        }]
    }
    ```

5. Run the following command to start the services.

    ```bash
    docker compose up -d
    ```

## License

This project is licensed under the [MIT License](LICENSE), providing an open and permissive licensing approach for further development and distribution.
