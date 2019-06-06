**********************************
Distributed Simulation
**********************************

.. todo::
	
	Migrate from <http://openems.de/index.php/Remote_SSH.html>


Using the ssh protocol it is possible to run an openEMS simulation on a remote host, even over the internet. Currently this is only possible on Linux, since Windows does not have a native support for ssh. Although it is possible to run openEMS and cygwin on a Windows remote host.

Requirements

    You need a user account on the remote machine
    You will need passwordless ssh access using public/private key's. For more information: [1]
    openEMS must be installed on the remote machine in a known path. e.g.: "/opt/openEMS/openEMS"

You can try if you pass all this requirements by opening a terminal and executing:

ssh <username>@<hostname> /opt/openEMS/openEMS/openEMS.sh

No password must be required and the remote openEMS should give you the welcome screen and possible openEMS options.

Windows Server

This is a small instruction how to setup an openEMS server on Windows (if desired, Linux as server is recommended)

    Install cygwin
    Install cygwin packages "openssh" and "cygrunsrv", see also: [2]
    Open a cygwin terminal (with admin rights) and run:

ssh-host-config -y
cygrunsrv -S sshd

    Create a firewall exception for cygwins sshd (e.g.: "C:\cygwin64\usr\sbin\sshd.exe")
    Download and install openEMS to e.g. "C:\cygwin64\home\<your_user_name>\opt\openEMS"
    Try to login to the server and test run openEMS

That's it! See how to setup your client...

Windows clients

Windows does not have a native support for ssh. We need to use a Putty for that. To setup the passwordless login with Putty: [3]

Finally you need to add to the settings where to find the "putty.exe" binary and your private ssh-key:

Settings.SSH.Putty.Path = '<path/to/putty>'; % path with plink.exe and pscp.exe in it
Settings.SSH.Putty.Key = '<path/to/putty_private_key.ppk';

Single Remote Machine

    To run openEMS on a specific remote maschine, add the following settings to RunOpenEMS:

Settings.SSH.host = '<username>@<hostname>'
Settings.SSH.bin = '<path_to_openEMS>/openEMS.sh'
 
RunOpenEMS(Sim_Path,Sim_File,'',Settings)

This will run openEMS on the given host.

Cluster of Remote Machines

    To run openEMS on one machine in a cluster of remote maschines, add the following settings to RunOpenEMS:

Settings.SSH.host_list = {'<username>@<hostname1>','<hostname2>','<username2>@<hostname3>'}
Settings.SSH.bin = '<path_to_openEMS>/openEMS.sh'
 
RunOpenEMS(Sim_Path,Sim_File,'',Settings)

    This will search for a free host and run openEMS on that machine.
    If all host are busy running openEMS, RunOpenEMS will wait until one of the host is free.

Remote openEMS over the Internet

    Both methods (single & cluster machine) can be used in the same way for a local area network or over the internet.
    Avoid large data dumps since they are copied back after the simulation: Have a look at the technical details below!

Abort a remote simulation

While running a remote simulation pressing e.g. "Ctrl+C" would terminate the ssh connection, effectively aborting the simulation, but all results would remain on the host. To abort an openEMS simulation in a clean way the empty file "ABORT" needs to be created in the remote simulation folder.

    Copy the temp-path from the matlab command window (should look simething like: /tmp/openEMS_O4lDAm0EbN29 and don't use "Ctrl+C" to copy...)
    Open a terminal and execute:

ssh <username>@<hostname> touch /tmp/openEMS_O4lDAm0EbN29/ABORT

Technical details

    When running a remote openEMS simulation, the complete <Sim_Path> will be copied (scp) to a temp folder on the remote host. --> Make sure the simulation path contains only the necessary files to run the simulation, because everything is being copied!
    If the ssh connection is lost during the simulation, the simulation will be aborted and the remote temp folder will not be cleaned up! Linux will cleanup the /tmp folder on the next boot.
    After the simulation, all data are copied back to the client machine, including all openEMS results. If no huge field dumps where performed, this should be fast. If the simulation was carried out over the internet, this may take a longer time, for slow connections and huge data dumps maybe even longer than the actual simulation.
