# GSM Server Docker Deployment

This project contains a Dockerized version of the GIGABYTE Server Management (GSM) software, allowing for easier deployment and management of the GSM server in a containerized environment. GSM is a tool that provides remote monitoring and management of multiple GIGABYTE servers via a browser-based GUI. 

## Features

- **Remote server management** using a web-based GUI.
- **Monitoring** of system health, power consumption, and event logs.
- **Remote access** features such as iKVM, power control, and BIOS updates.
- **SNMP and TFTP** capabilities for integration with your existing infrastructure.
- **Dockerized deployment** for easy installation and management.

## Prerequisites

- Docker
- Docker Compose
- Portainer (optional for web-based management)

## Project Structure

```bash
.
├── data                # Subfolder containing the Dockerfile
│   └── Dockerfile      # Dockerfile to build the GSM server image
├── docker-compose.yml  # Docker Compose file to manage services
└── README.md           # This file
```

## Ports Used

The following ports are exposed by the GSM server for remote management and monitoring:

- **8080**: HTTP for web access.
- **8443**: HTTPS for secure web access.
- **162 (UDP)**: SNMP trap listener.
- **69 (UDP)**: TFTP server for firmware updates.
- **5900**: Java KVM (iKVM) for remote console access.

## How to Build and Run the GSM Server

### 1. Clone the Repository

```bash
git clone <repository-url>
cd <repository-directory>
```

### 2. Build and Run the Container

Using Docker Compose, you can build and run the containerized GSM server:

```bash
docker-compose up -d
```

This will:
- Build the Docker image from the Dockerfile located in the `data` subfolder.
- Deploy the container and map the necessary ports.

### 3. Access the GSM Server

Once the container is running, you can access the GSM server via a web browser:

- **HTTP**: `http://localhost:8080`
- **HTTPS**: `https://localhost:8443`

Replace `localhost` with your server's IP address if running on a remote machine.

## Using Portainer for Deployment

If you prefer to use **Portainer** for container management, follow these steps:

1. Go to the **Stacks** section in Portainer.
2. Create a new stack and paste the content of `docker-compose.yml` into the editor.
3. Deploy the stack.

Portainer will handle the rest, and you can manage the GSM server from there.

## Managing the GSM Server

Once the server is up and running, you can use the web-based GUI to:

- Monitor system health, power consumption, and event logs.
- Access the server via KVM over IP using Java (iKVM).
- Manage BIOS updates and remote control of servers.
- Configure SNMP traps and alerts.

## Volumes

The Docker Compose file creates a persistent volume (`gsm_data`) to store GSM server data:

```yaml
volumes:
  gsm_data:
    driver: local
```

This ensures that the server's data remains available even if the container is stopped or removed.

## Troubleshooting

- **Port Conflicts**: Make sure the ports (8080, 8443, 162, 69, and 5900) are available on your host machine.
- **Firewall Issues**: Ensure your firewall allows traffic through the exposed ports.
- **Container Logs**: You can check the logs for troubleshooting by running:
  ```bash
  docker logs gsm_server
  ```

## License

This project uses GSM software, which is proprietary to GIGABYTE. Please refer to the GIGABYTE website for more details on licensing.

## Credits

- **GIGABYTE Technology** for the GSM server software.
- **Docker** for containerizing the application.
- **Portainer** for managing Docker environments easily.
