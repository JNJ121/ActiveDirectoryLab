</head>
<body>
    <header>
        <h1>Active Directory Lab Documentation</h1>
        <p>By Jabari Neal-Jackson</p>
            </header>
    <main>
        <section>
            <h2>Objective</h2>
            <p>This lab aims to set up and configure an Active Directory environment to understand its core functionalities, including user and group management, domain configuration, and security policies. This lab will cover the steps to set up Active Directory, DHCP, and the process to connect a client to the domain.</p>
        </section>
        <section>
            <h2>Lab Setup</h2>
            <p>Prerequisites for this lab:</p>
            <ul>
                <li>A virtual machine running Windows Server 2019 ( Windows Server 2022 will work but steps may differ).</li>
                <li>A second VM running Windows 10 client for testing.</li>
                <li>Basic networking setup to allow communication between the VMs.</li>
            </ul>
            <p><strong>Note:</strong> VM installation and OS setup are not included in this documentation.</p>
        </section>
        <section>
            <h2>Steps</h2>
            <ol>
                <li><strong>Promote the Windows Server to a Domain Controller:</strong>
                    <ul>
                        <li>Open <code>Server Manager</code> and select <code>Add Roles and Features</code>.</li>
                        <li>Choose <code>Active Directory Domain Services (AD DS)</code> and complete the wizard.</li>
                        <li>Promote the server to a domain controller using the <code>Active Directory Domain Services Configuration Wizard</code>.</li>
                        <li>Configure a new forest and domain (e.g., <code>mydomain.com</code>).</li>
                     <img src="https://i.imgur.com/5L8yBYN.png" alt="Active Directory Example" style="max-width: 100%; height: auto; display: block; margin: 10px auto;">
                        <li>Select <code>Next</code> to keep all settings default then select <code>Install</code>.</li>
                        <li>Restart the server to apply changes.</li>
                    </ul>
                </li>
                <li><strong>Configure DNS:</strong>
                    <ul>
                        <li>Ensure DNS is installed and running on the domain controller.</li>
                        <li>Under <code>Tools</code> select <code>DNS</code>.</li>
                        <li>Verify forward and reverse lookup zones are created automatically.</li>
                         <img src="https://i.imgur.com/BhAXivO.png" alt="Active Directory Diagram" style="max-width: 100%; height: auto; display: block; margin: 10px auto;">
                    </ul>
                </li>
                <li><strong>Install and Configure DHCP:</strong>
                    <ul>
                       <li>Open <code>Server Manager</code> on your Windows Server.</li>
                       <li>Click <code>Add Roles and Features</code>.</li>
                       <li>Choose <code>Role-based or feature-based installation</code> and click <code>Next</code>.</li>
                       <li>Select your server from the server pool and click <code>Next</code>.</li>
                       <li>In the server roles list, check <code>DHCP Server</code> and click <code>Next</code>.</li>
                       <img src="https://i.imgur.com/Ryz79Aa.png" alt="Active Directory Example" style="max-width: 100%; height: auto; display: block; margin: 10px auto;">
                       <li>Proceed through the wizard and click <code>Install</code>.</li>
                       <li>Once the installation is complete, click <code>Complete DHCP Configuration</code> to finalize the setup.</li>
                       <img src="https://i.imgur.com/CmMapz1.png" alt="Active Directory Diagram" style="max-width: 100%; height: auto; display: block; margin: 10px auto;">
                       <li>Navigate to <code>Tools</code> and select <code>DHCP</code>.</li>
                       <li>Select the drop-down on <code>dc.mydomain.com</code> to see IPv4 and IPv6 options.</li>
                       <li>Right-click <code>IPv4</code> and select <code>New Scope...</code> to open scope wizard.</li>
                       <li>Enter the IP address range as the name for the scope (<code>172.16.0.100-200</code>) then select next.</li>
                       <img src="https://i.imgur.com/TY80mKF.png" alt="Active Directory Configuration" style="max-width: 100%; height: auto; display: block; margin: 10px auto;">
                       <li>The next page is setting the IP range the start IP address will be <code>172.16.0.100</code> and the end IP address will be <code>172.16.0.200</code>. Set the subnet to             <code>24</code> it is identified as <code>Length</code>, it should read <code>255.255.255.0</code>.
                        <li>The lease Duration is the next setting but I kept it at the default 8 days because there is no need to change in this lab. Select <code>next</code> until the default gateway screen.</li>
                       <li>Enter the Router default gateway as <code>172.16.0.1</code> and select <code>Add</code> then next to move forward.</li>
                       <img src="https://i.imgur.com/RZCXcNA.png" alt="Active Directory Server Setup" style="max-width: 100%; height: auto; display: block; margin: 10px auto;">
                        <li>Select until <code>Finsh</code> is and option and select that. Right-click the <code>dc.mydomain.com</code> and select <code>Authorize</code> then right-click the <code>dc.mydomain.com</code> and select <code>Refresh</code>.
                        <img src="https://i.imgur.com/DGJrTo3.png" alt="Active Directory Configuration" style="max-width: 100%; height: auto; display: block; margin: 10px auto;">
                        <li>Both <code>IPv4</code> and <code>IPv6</code> should have a green check to show they are up.</li>
                        <img src="https://i.imgur.com/khN9ca7.png" alt="Active Directory Setup" style="max-width: 100%; height: auto; display: block; margin: 10px auto;">
                   </ul>
                </li>
                <li><strong>Create Admin User Account:</strong>
                    <ul>
                        <li>Open <code>Start</code> menu and select the drop-down menu on <code>Windows Administrative Tools</code> from that drop-down select <code>Active Directory Users and Computers</code>  </li>
                        <img src="https://i.imgur.com/tm2F1xd.png" alt="Active Directory Diagram" style="max-width: 100%; height: auto; display: block; margin: 10px auto;">
                        <li>Right-click <code>_ADMINS</code> hover the cursor over <code>New</code> and from that drop-down select <code>User</code>.</li>
                        <img src="https://i.imgur.com/dhWtYQP.png" alt="DHCP Configuration Example" style="max-width: 100%; height: auto; display: block; margin: 10px auto;">
                        <li>Enter the Information for an admin user. (An easy login name for an admin could be "a" first name initial followed by last name. E.A. <code>a-jjackson</code>)</li>
                        <img src="https://i.imgur.com/A3w6oep.png" alt="Server Configuration Example" style="max-width: 100%; height: auto; display: block; margin: 10px auto;">
                        <li>Select next and give the account a password, uncheck <code>User must change password at next logon</code> and check <code>Password never expires</code> select next and then <code>Finish</code> to confirm.
                    </ul>
                </li>
                <li><strong>Create User Accounts with PowerShell:</strong>
                    <ul>
                        <li>Hold the <code>Windows key + R</code> on the keyboard to open a search bar.</li>
                        <li>Type <code>Powershell ISE</code> and select <code>OK</code>.</li>
                        <li>In the blue cmd enter the command <code>Set-ExecutionPolicy Unrestricted</code> and press enter</li>
                        <li>Next change the directory to wherever the PowerShell script is located using the <code>cd</code> command</li>
                        <li>Open the script by selecting the <code>Folder</code> called <code>Open Script</code>.</li>
                        <li>Select the <code>Green PLay icon</code> to run the script to begin adding the user.</li>
                        <img src="https://i.imgur.com/yEcoJCB.png" alt="Network Configuration Example" style="max-width: 100%; height: auto; display: block; margin: 10px auto;">
                        <li>Some errors may occur this is due to the fact that the name generator can make duplicate names.</li>
                    </ul>
                </li>
                <li><strong>Join a Client to the Domain:</strong>
                    <ul>
                        <li>On the client machine, navigate to <code>Settings</code> and open <code>About</code>.</li>
                        <li>Select <code>Advanced system settings</code>, this will open <code>System Properties</code>.
                        <li>Select <code>Change...</code> under computer name enter <code>CLIENT1</code>.</li>
                        <li>Under Member of select <code>Domain</code> and then enter <code>mydomain.com</code> then select <code>OK</code> then <code>Apply</code> to commit the changes.</li>
                        <img src="https://i.imgur.com/Jb75qY2.png" alt="Server Manager Roles" style="max-width: 100%; height: auto; display: block; margin: 10px auto;">
                    </ul>
                </li>
                <li><strong>Test and Verify:</strong>
                    <ul>
                        <li>To verify that the Client has been given an IP address with DHCP in the Windows 2019 Server navigate to <code>DHCP</code> from <code>Tools</code>.</li>
                        <li>Open the <code>IPv4</code> drop-down then open <code>Scope[172.16.0.0] 172.16.0.100-200</code> and then selecting <code>Address Leases</code>
                        <img src="https://i.imgur.com/rsAoUWi.png" alt="DHCP Configuration Wizard" style="max-width: 100%; height: auto; display: block; margin: 10px auto;">
                        <li>To verify that the Client is in the domain open <code>Active Directory Users and Computers</code> from <code>Tools</code>
                        <li>Select the drop-down from <code>mydomain.com</code> and then open <code>Computers</code> it should show the Client Computer.</li>
                        <img src="https://i.imgur.com/7AFfJKS.png" alt="Server Manager DHCP Role" style="max-width: 100%; height: auto; display: block; margin: 10px auto;">
                        <li>Verify successful domain join by logging in with a domain user account. (It should say Sign in to: <code>MYDOMAIN</code>)</li>
                        <img src="https://i.imgur.com/f4szAu9.png" alt="DHCP Scope Setup" style="max-width: 100%; height: auto; display: block; margin: 10px auto;">
                        <li>Open <code>cmd</code> in the Client machine and enter the command <code>whoami</code>. (It should show the domain and the username for that user)</li>
                        <img src="https://i.imgur.com/SaAt6PP.png" alt="DHCP Lease Example" style="max-width: 100%; height: auto; display: block; margin: 10px auto;">
                    </ul>
                </li>
            </ol>
        </section>
        <section>
            <h2>Conclusion</h2>
            <p>This lab provides hands-on experience with setting up and managing an Active Directory environment, focusing on key concepts like domain controllers, OUs, user management, and group policies.</p>
            <p>For any questions or feedback, please contact me at <a href="mailto:Jabarijnj@gmail.com">Jabarijnj@gmail.com</a>.</p>
        </section>
    </main>
    <footer>
        <p>&copy; 2024 Jabari Neal-Jackson</p>
    </footer>
</body>
