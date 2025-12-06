
# Configuring MikroTik for FreeRADIUS Authentication

This guide provides instructions on how to configure a MikroTik router to use FreeRADIUS for authentication services. This is useful for networks where access control and accounting are required for services like Wi-Fi, VPN, etc.

## Step 1: Access MikroTik Router

First, access your MikroTik router using one of the following methods:
- **WinBox**: A graphical interface provided by MikroTik.
- **WebFig**: The web-based interface accessible through a browser.
- **SSH**: Command-line interface for advanced users.

## Step 2: Open RADIUS Settings

Navigate to the RADIUS settings in your router:
- **WinBox**: Go to `Radius` under the main menu.
- **WebFig**: Look for the `Radius` option in the menu.

## Step 3: Add a RADIUS Server

Click on the `+` button to add a new RADIUS server configuration with the following details:
- **Service**: Select the service (e.g., `wireless`) you want to authenticate via RADIUS.
- **Address**: Enter the IP address of your FreeRADIUS server.
- **Secret**: Specify the shared secret configured in your FreeRADIUS `clients.conf` file.
- **Timeout**: (Optional) Set the timeout for requests.
- **Authentication Port**: Usually 1812, unless changed in your FreeRADIUS setup.
- **Accounting Port**: Usually 1813, for accounting services.

## Step 4: Configure NAS (MikroTik Router) for RADIUS

For services like Wi-Fi, navigate to the respective settings and enable RADIUS:
- **WinBox**: Go to `Wireless`, select `Security Profiles`, choose/create a profile, and enable `Use RADIUS`.
- **WebFig**: Similar to WinBox, adjust the security profile settings.

## Step 5: Test Your Configuration

After configuring, test the setup by attempting to use the service (e.g., connecting to a Wi-Fi network) and observe the authentication process through the MikroTik and FreeRADIUS logs.

## Additional Notes:

- Ensure the FreeRADIUS server firewall allows incoming connections on ports 1812 (authentication) and 1813 (accounting) from the MikroTik router.
- The IP address in the FreeRADIUS `clients.conf` must match the MikroTik router's IP address.
- Keep your systems updated for enhanced security and performance.

