<img width="1386" height="1223" alt="Image" src="https://github.com/user-attachments/assets/ba1e0fc4-ae22-4002-b332-f8c46983655a" />

Palo Alto Networks VPN Planning Tool
A web-based tool for planning and generating Panorama CLI commands for site-to-site VPN configurations on Palo Alto Networks firewalls.
Overview
This tool simplifies the process of configuring site-to-site VPNs by providing an intuitive interface for entering configuration parameters and automatically generating the corresponding Panorama CLI commands. It includes features for BGP routing, static routes, proxy IDs, and comprehensive configuration tracking.
Features
Core Functionality

Auto-generated CLI Commands: Automatically generates Panorama CLI commands based on your configuration
Real-time Preview: See CLI commands update as you configure settings
Configuration Summary: At-a-glance view of all key configuration parameters
Save/Load Configurations: Save multiple VPN configurations and reload them later
Import/Export: Export configurations as JSON files and import them back
Browser Persistence: Configurations are automatically saved to your browser

Configuration Sections
1. Panorama Configuration

Template Name
Device Group
Change Number and Date tracking
Device naming

2. Peer Information

Peer device name and type (AWS, Azure, GCP, Cisco, Palo Alto, Fortigate, Other)
Contact information for coordination
Change management details

3. IKE Gateway

Gateway name (auto-generated from peer name, manually editable)
IKE version (IKEv1/IKEv2)
Local interface and IP addresses (public and private)
Peer IP address
Pre-shared key configuration

4. IKE Crypto Profile

Profile name (auto-generated, manually editable)
Encryption algorithms (AES-256-CBC, AES-128-CBC, AES-256-GCM, AES-128-GCM)
Hash algorithms (SHA-256, SHA-384, SHA-512, SHA-1)
DH Groups (Group 14, 19, 20, 5)
Lifetime configuration

5. IPSec Tunnel

Tunnel name (auto-generated, manually editable)
Tunnel interface assignment
Zone configuration
Anti-replay settings

6. IPSec Crypto Profile

Profile name (auto-generated, manually editable)
Protocol (ESP/AH)
Encryption and authentication algorithms
DH Group and lifetime settings

7. Tunnel IP Configuration

Local and remote tunnel IPs
CIDR subnet selection (/16 to /31)
Auto-populated subnet masks
Support for /30 point-to-point links

8. Proxy ID (Optional)

Enable/disable proxy ID configuration
Local and remote subnet definitions
Auto-generated proxy ID names

9. BGP Configuration (Optional)

Local and peer ASN
BGP peer group and peer names
Local and peer BGP addresses (auto-populated from tunnel IPs)
Hold time and keep-alive intervals
Prefix export/import configuration
Automatic BGP security policy generation

10. Static Routes (Optional)

Multiple static route support
Network and CIDR selection (/16 to /31)
Auto-populated subnet masks
Next-hop IP configuration
Next-hop interface (defaults to tunnel interface)
Peer static routes notes field for documentation

Usage Guide
Getting Started

Open the Tool: Load the HTML file in any modern web browser
Fill Required Fields: Start by entering:

Template Name
Device Group
Peer Name (this auto-generates many other fields)



Configuration Workflow
Step 1: Basic Information

Enter Panorama configuration details
Provide peer information and contact details
Document change management information

Step 2: VPN Core Configuration

Configure IKE Gateway settings
Set up IKE and IPSec crypto profiles
Define tunnel interface and IPs
Enter pre-shared key

Step 3: Optional Features

Enable Proxy ID if policy-based VPN is required
Enable BGP for dynamic routing:

Enter ASNs for both sides
Configure prefixes to advertise and receive
BGP addresses auto-populate from tunnel IPs


Enable Static Routes for static routing:

Add multiple routes as needed
Use CIDR dropdown for easy subnet mask selection
Specify next-hop interface if different from tunnel



Step 4: Review and Export

Check the Configuration Summary table
Review generated CLI commands
Copy CLI commands to clipboard
Save configuration for future reference

Field Auto-Population
The tool automatically generates names based on the peer name:

IKE Gateway: {peer-name}-ike-gw
IPSec Tunnel: {peer-name}-ipsec-tunnel
IKE Crypto Profile: {peer-name}-ike
IPSec Crypto Profile: {peer-name}-ipsec
Proxy ID: Proxy-{peer-name}
BGP Peer Group: pg-{peer-name}
BGP Peer Name: {peer-name}-peer

Note: All auto-generated names can be manually edited if needed.
CIDR and Subnet Mask
The tool provides CIDR dropdowns for easy subnet configuration:

Select a CIDR notation (/16 through /31)
Subnet mask auto-populates
Manual entry still available if needed

Supported CIDR notations:

/16 = 255.255.0.0
/17 = 255.255.128.0
/18 = 255.255.192.0
/19 = 255.255.224.0
/20 = 255.255.240.0
/21 = 255.255.248.0
/22 = 255.255.252.0
/23 = 255.255.254.0
/24 = 255.255.255.0
/25 = 255.255.255.128
/26 = 255.255.255.192
/27 = 255.255.255.224
/28 = 255.255.255.240
/29 = 255.255.255.248
/30 = 255.255.255.252 (most common for VPN tunnels)
/31 = 255.255.255.254

Yellow Highlighting
Fields highlighted in yellow are required or recommended to be filled in. After using "Clear All Settings", all configurable fields will be highlighted yellow to indicate they need attention.
Configuration Summary
The Configuration Summary table provides a side-by-side comparison view:

Left Column: Local firewall configuration
Right Column: Peer firewall configuration
Editable fields allow direct updates
Shows all key parameters at a glance

Special Summary Features

Static Routes: Local routes display automatically; peer static routes can be documented in notes field
BGP Prefixes: Shows import/export prefixes when BGP is enabled
Change Information: Displays change number, date, and contact info at the top

Generated CLI Commands
The tool generates complete Panorama CLI commands including:

IKE crypto profile creation
IKE gateway configuration with DPD and NAT-T
IPSec crypto profile creation
Tunnel interface configuration
IPSec tunnel setup
Proxy ID configuration (if enabled)
Static route configuration (if enabled)
Security policies for ICMP and BGP
Complete BGP configuration including:

Router ID and local AS
Peer group and peer configuration
Export and import policies
Connection parameters



Tips and Best Practices
Tunnel IPs

Use /30 subnets (255.255.255.252) for point-to-point tunnels
Common ranges: 169.254.x.x (link-local) or private IP space
Ensure tunnel IPs don't overlap with other networks

BGP Configuration

BGP addresses auto-populate from tunnel IPs for /30 subnets
Use private ASNs (64512-65535) for internal networks
Document advertised prefixes clearly
Hold time should be 3x keep-alive interval (default: 30s/10s)

Static Routes

Specify next-hop interface if routing through specific interface
Leave next-hop interface blank to default to tunnel interface
Document peer's static routes in the notes field for coordination

Crypto Profiles

Use AES-256 for stronger encryption when supported
SHA-256 or higher for hash algorithms
DH Group 14 minimum (2048-bit), Group 19/20 preferred
Match crypto settings with peer device capabilities

Security Policies

Tool auto-generates ICMP policy for tunnel testing
BGP policy automatically created when BGP is enabled
Add additional security policies manually as needed

Change Management

Always document change numbers and dates
Include contact information for coordination
Save configurations before and after changes

Saved Configurations
Saving

Click "💾 Save Config" to save current configuration
Configurations stored in browser's local storage
Saved with timestamp and peer name

Loading

Click "📋 Saved" to view saved configurations
Click "Load" to restore a saved configuration
Click "Delete" to remove a saved configuration
Click "Clear All" to delete all saved configurations

Browser Storage

Configurations persist across browser sessions
Stored locally in your browser only
Export important configurations as JSON for backup

Import/Export
Exporting

Click "📤 Export Configuration to JSON"
File downloads as vpn-config-{peer-name}.json
Store safely for backup or sharing

Importing

Click "Choose File" under Import Configuration
Select a previously exported JSON file
Configuration loads automatically

Buttons and Controls

💾 Save Config: Save current configuration to browser storage
📋 Saved (n): View and manage saved configurations
🧹 Clear All Settings: Reset all fields to defaults (with confirmation)
📋 Copy CLI: Copy generated CLI commands to clipboard
📤 Export Configuration: Download configuration as JSON file
Enable/Disable Toggles: Green = Enabled, Gray = Disabled

Browser Compatibility
This tool works in all modern browsers:

Chrome/Edge (recommended)
Firefox
Safari
Opera

Technical Details

Framework: React 18
Styling: Tailwind CSS
Storage: Browser localStorage
File Format: JSON for import/export
No Server Required: Runs entirely in browser

Troubleshooting
CLI Commands Not Generating

Ensure Template, Device Group, and Peer Name are filled in
These three fields are required for CLI generation

Auto-population Not Working

Enter Peer Name first
Auto-population only triggers when Peer Name changes
You can manually edit any auto-generated field

Configurations Not Saving

Check if browser allows localStorage
Ensure you're not in private/incognito mode
Some browsers block localStorage in certain modes

Import Failing

Verify JSON file format is correct
Ensure file was exported from this tool
Check for file corruption

Security Considerations

Pre-shared keys are stored in plain text in saved configurations
Local storage is not encrypted by the browser
Export files contain sensitive information in plain text
Best practice: Don't save configurations on shared computers
Recommendation: Use this tool for planning, then secure PSKs properly

Version History
Current Version

Full Panorama CLI command generation
BGP configuration with prefix import/export
Static routes with next-hop interface
CIDR dropdowns for subnet configuration
Editable peer static routes notes
Save/load functionality with localStorage
Import/export JSON configurations
Auto-population of field names
Configuration summary table
Yellow highlighting for required fields
Clear all settings functionality

Support and Contributions
This tool is provided as-is for network planning purposes. Users should:

Verify all generated commands before deployment
Test configurations in lab environment first
Review with security and network teams
Follow organizational change management processes

License
This tool is provided for network planning and configuration assistance. Use at your own discretion and always verify generated configurations before deployment.

Note: This is a planning tool. Always validate generated configurations and follow your organization's change management and security policies before implementing any network changes.
