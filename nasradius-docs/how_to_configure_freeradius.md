
# How to Configure FreeRADIUS with Django REST API

This guide outlines the steps to set up FreeRADIUS to authenticate against a Django REST API, specifically tailored for integration with MikroTik routers.

## Step 1: Install FreeRADIUS

### On Ubuntu/Debian:

```bash
sudo apt-get update
sudo apt-get install freeradius freeradius-rest
```

### On CentOS/RHEL:

```bash
sudo yum update
sudo yum install freeradius freeradius-rest
```

### On Fedora:

```bash
sudo dnf install freeradius freeradius-rest
```

## Step 2: Configure FreeRADIUS to Use the Django REST API

### 2.1 Enable `rlm_rest` Module:

Locate the `rlm_rest` module configuration, typically found in `/etc/freeradius/3.0/mods-enabled/rest`. If not present, link it from `mods-available`.

```bash
cd /etc/freeradius/3.0/mods-enabled/
sudo ln -s ../mods-available/rest
```

Edit the `rest` configuration file:

```bash
sudo nano /etc/freeradius/3.0/mods-enabled/rest
```

Configure the endpoint URLs for your Django API:

```conf
rest {
    tls {
        # Configure TLS if using HTTPS
    }
    authenticate {
        uri = "https://www.yourdomain.com/api/customers/radius/auth"
        method = 'post'
        body = 'json'
    }
    # Configure sections for accounting and authorization as needed
}
```

### 2.2 Configure Clients:

Define network devices in `/etc/freeradius/3.0/clients.conf`:

```conf
client your_network_device {
    ipaddr = 192.168.1.1
    secret = your_shared_secret
    require_message_authenticator = no
}
```

### 2.3 Integrate `rlm_rest` with Server Configuration:

Edit `/etc/freeradius/3.0/sites-enabled/default`, adding `rest` to the `authorize` and `authenticate` sections:

```conf
authorize {
    rest
}
authenticate {
    Auth-Type REST {
        rest
    }
}
```

### 2.4 Test Configuration:

Run FreeRADIUS in debugging mode to test:

```bash
sudo radiusd -X
```

### 2.5 Start/Restart FreeRADIUS Service:

```bash
# Ubuntu/Debian
sudo systemctl restart freeradius.service

# CentOS/RHEL/Fedora
sudo systemctl restart radiusd.service
```

## Additional Tips:

- Ensure network accessibility between FreeRADIUS and your Django app.
- Use HTTPS for the Django API and configure SSL verification in `rlm_rest`.
- Secure the communication with API tokens or secret keys.
- Monitor FreeRADIUS logs for security and performance.

