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
                       <li>Right click <code>IPv4</code> and select <code>New Scope...</code> to open scope wizard.</li>
                       <li>Enter the IP address range as the name for the scope (<code>172.16.0.100-200</code>) then select next.</li>
                       <img src="https://i.imgur.com/TY80mKF.png" alt="Active Directory Configuration" style="max-width: 100%; height: auto; display: block; margin: 10px auto;">
                       <li>Enter the Router default gateway as <code>172.16.0.1</code> and select <code>Add</code> then next to move forward.</li>
                       <img src="https://i.imgur.com/RZCXcNA.png" alt="Active Directory Server Setup" style="max-width: 100%; height: auto; display: block; margin: 10px auto;">
                   </ul>
                </li>
                <li><strong>Create User Accounts:</strong>
                    <ul>
                        <li>Create test user accounts within the appropriate OUs.</li>
                        <li>Set passwords and ensure appropriate group memberships.</li>
                    </ul>
                </li>
                <li><strong>Group Policy Configuration:</strong>
                    <ul>
                        <li>Use <code>Group Policy Management</code> to create and link Group Policy Objects (GPOs).</li>
                        <li>Apply policies to enforce settings like password complexity and desktop backgrounds.</li>
                    </ul>
                </li>
                <li><strong>Join a Client to the Domain:</strong>
                    <ul>
                        <li>On the client machine, set the primary DNS to the domain controller's IP address.</li>
                        <li>Join the client to the domain through <code>System Properties</code>.</li>
                        <li>Verify successful domain join by logging in with a domain user account.</li>
                    </ul>
                </li>
                <li><strong>Test and Verify:</strong>
                    <ul>
                        <li>Log in with created user accounts and verify access to shared resources.</li>
                        <li>Check the application of GPOs on the client machine using <code>gpresult /r</code>.</li>
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
