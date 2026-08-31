# Projects-IT-works
IT Projects and IT works
# Building an On-Premises Microsoft AD/Exchange Infrastructure with a Perimeter Security Gateway
**Author:** Technical Engineering Portfolio  
**Target Architecture:** Windows Server 2022/2025 Standard/Datacenter, Exchange Server 2019 Cumulative Update 15, pfSense Security Appliance

## 1. Directory Environment & Identity Database Initialization
This engineering deployment guide establishes a baseline enterprise messaging architecture, utilizing a hardened on-premises Active Directory Domain Services (AD DS) catalog structure as the foundational identity boundaries before integrating upstream cloud sync agents.

### Step 1: Network Parameter Configuration & Interface Assignment
Prior to running server promotions, configure static interface settings natively on the core domain infrastructure host machine:
* Assign a strict **Static IP Address** configuration scheme.
* Map the **Default Gateway IP string** to target your network's physical edge or routing layer appliance (e.g., your configured **pfSense Firewall Appliance** core interface gateway address).
* Define upstream fallback variables, pointing local DNS resolution targets back to high-availability recursive lookup endpoints (`1.1.1.1` and `1.0.0.1`).

### Step 2: Role Ingestion & Directory Domain Promotion
1. Access the host system dashboard workspace via **Server Manager -> Manage -> Add Roles and Features**.
2. Proceed through the role wizard parameters, selecting **Role-based or feature-based installation**.
3. Under the server roles boundary checklist, explicitly select **Active Directory Domain Services** along with **DNS Server**.
4. In the core features window layer, verify the selection mappings for `.NET Framework 3.5/4.8 Features` and the `Group Policy Management` console engine tools.
5. Once installation scripts conclude successfully, trigger the deployment post-configuration phase by selecting **Promote this server to a domain controller**.
6. On the configuration mapping window, define your administrative structural boundaries:
   * Select the operation target action parameter string: **Add a new forest**.
   * Establish your globally valid enterprise namespace parameter line inside the **Root domain name** text box.
7. Set a highly complex administrative access passphrase context to secure your **Directory Services Restore Mode (DSRM)** capability options. Proceed through default paths to confirm the automatically populated **NetBIOS domain name** variables.
8. Accept directory paths for your transactional tracking engines (**Database folder**, **Log files folder**, and **SYSVOL folder**) and run the system check pipeline. Once the baseline verification scripts confirm **All prerequisite checks passed successfully**, execute the **Install** function to prompt the system restart phase.

## 2. Administrative Object Management & Delegation Foundations
Following server initialization cycles, administrative access transitions to dedicated object separation to respect the security principles of **Least Privilege Authorization**:

1. Log into your clean server identity space utilizing standard workstation variables via **Other User** to isolate structural operations.
2. Launch the primary identity container workspace via **Server Manager -> Tools -> Active Directory Users and Computers (ADUC)**.
3. Traverse down to your target local root tree structure, choose your destination directory folder path (**Users**), and execute a **New User Object** generation template.
4. Input specific identity parameters, establishing the login identity naming strings (e.g., User logon name: `David`).
5. Enforce account credential longevity rules context settings, checking the parameters marking **Password never expires** to prevent automation interruptions in lab runtimes.
6. Open the newly generated user object metrics properties console card, click into the **Member Of** assignment section, and add elevated schema authority security group definitions to the account profile context line:
   * `Domain Admins`
   * `Enterprise Admins`
   * `Schema Admins`

## 3. Dynamic IP Mapping & Core Scope Allocation
To ensure connected node endpoint identities communicate reliably across routing fabrics, provision local DHCP distribution layers:

1. Launch your Server Manager workspace tools menu pane, navigate to **Add Roles and Features**, and ingest the **DHCP Server** role asset components.
2. From the resulting administrative workspace window tracking interface, drill into your network configuration root container, view your server node designation (`DC01`), and click into the **IPv4 routing branch**.
3. Under your active Action sub-menu properties toolbar paths, trigger the selection sequence for a **New Scope**.
4. Assign a recognizable, clear administrative identity tracker tag inside the **Scope Name** tracking field (e.g., `Main.Lan`).
5. Delineate assignment boundaries for local endpoints by typing out range limits inside the network boundary configuration sections:
   * **Start IP address block configuration:** (e.g., mapping assignments starting at `.3`).
   * **End IP address block configuration:** (e.g., capping allocations up to `.254`).
6. Set the subnet mask context definition length parameters to a custom or standard length block value (e.g., Length `24` / Subnet mask `255.255.255.0`).
7. Define **Lease Duration metrics parameters** to dictate token persistence limits for downstream entities tracking against your pool resources.
8. Return to your master node tracker index layout structure, navigate directly through the **More Actions** context selection list tool options, and click on **Authorize** to bind execution parameters active across your target domain layer.

## 4. Headless On-Premises Mail Exchange Platform Deployment
This section addresses installing an enterprise email infrastructure layer utilizing an unattended headless layout pipeline.

### Step 1: Runtime Engine Ingestion & Baseline System Features
Prior to mounting the execution volume containing your Microsoft Exchange payload files, install the required third-party utility applications and web handling dependencies:
* Visual C++ Redistributable Packages for Visual Studio (2012-2013 runtimes).
* Unified Communications Managed API (UCMA) 4.0 Runtime execution engine.
* IIS URL Rewrite Module 2.
* Server Ingestion of the Web Server (IIS) role parameters mapping standard Common HTTP Features, Default Documentation variables, and security request filtering blocks.

Open an elevated administrative PowerShell runtime execution engine pane to pull in the mandatory underlying Active Directory Management framework prerequisites:
```powershell
Install-WindowsFeature RSAT-ADDS
```

Enforce silent ingestion configurations for underlying web features components by running the complete system deployment module string block parameters inside your processing interface:
```powershell
Install-WindowsFeature Server-Media-Foundation, NET-Framework-45-Core, NET-Framework-45-ASPNET, NET-WCF-HTTP-Activation45, NET-WCF-Pipe-Activation45, NET-WCF-TCP-Activation45, NET-WCF-TCP-PortSharing45, RPC-over-HTTP-proxy, RSAT-Clustering, RSAT-Clustering-CmdInterface, RSAT-Clustering-Mgmt, RSAT-Clustering-PowerShell, WAS-Process-Model, Web-Asp-Net45, Web-Basic-Auth, Web-Client-Auth, Web-Digest-Auth, Web-Dir-Browsing, Web-Dyn-Compression, Web-Http-Errors, Web-Http-Logging, Web-Http-Redirect, Web-Http-Tracing, Web-ISAPI-Ext, Web-ISAPI-Filter, Web-Metabase, Web-Mgmt-Console, Web-Mgmt-Service, Web-Net-Ext45, Web-Request-Monitor, Web-Server, Web-Stat-Compression, Web-Static-Content, Web-Windows-Auth, Web-WMI, Windows-Identity-Foundation
```
*Note: Execute a full mechanical validation system cycle restart following the configuration task sequence before continuing operation paths.*

### Step 2: Unattended Layout Generation & Schema Extensions
Mount your source Exchange distribution image artifact layer (e.g., verifying drive mounting designation letters inside your local tree infrastructure view paths, such as `D:` or `E:` target spaces). 

Open an active PowerShell administrative prompt workspace, pivot directly to the root source volume tracking folder paths, and run the following precise command sequences in sequence:

1. **Extend Identity Schema Structure Definitions:**
   ```powershell
   .\Setup.exe /IAcceptExchangeServerLicenseTerms_DiagnosticDataON /PrepareSchema
   ```
2. **Instantiate the Core Enterprise Mail Organization Object Boundary Definition:**
   ```powershell
   .\Setup.exe /IAcceptExchangeServerLicenseTerms_DiagnosticDataON /PrepareAD /OrganizationName:"Contoso Corporation"
   ```
3. **Extend Local Domain Boundary Security Group Property Mappings:**
   ```powershell
   .\Setup.exe /IAcceptExchangeServerLicenseTerms_DiagnosticDataON /PrepareDomain
   ```

### Step 3: Complete Mailbox Role Installation
Execute the headless unattended server configuration build command, verifying role mappings are directed inside the primary storage space disk profiles:
```powershell
.\Setup.exe /IAcceptExchangeServerLicenseTerms_DiagnosticDataON /Mode:Install /Roles:Mailbox /TargetDir:"C:\Program Files\Microsoft\Exchange Server\V15"
```
*Note: Monitor the early file validation tracking steps. If progress signals freeze indefinitely near the 16% index execution marker block for more than two hours, run a process restart check cycle on your underlying container instance configuration settings.*

## 5. Architectural Verification & Upstream Perimeter Routing
1. **Verification of Local Node Services:** Launch an active Exchange Management Shell (EMS) instance pane and issue the diagnostic confirmation request tool:
   ```powershell
