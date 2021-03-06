Suppose that an application that you are developing requires some calculation intensive task that you'd like to run on the Seattle network.  In this case, you can bundle (i.e. include) Seattle alongside your application and deploy it on user machines.  This is trivial to do on Windows, OSX and Linux machines.



 == Requirements ==
----
In order for Seattle to function, you need to make sure that Python 2.5 or Python 2.6 is installed on your target system.  The Windows installer has Python 2.5 bundled alongside with it, so manual installation of Python is not needed.



 == Bundling Seattle ==
----

Download the [Seattle installer](https://seattleclearinghouse.poly.edu/html/getdonations) for your target operating system under your Clearinghouse account.  This will provide your Clearinghouse account with donation credits for each installation.  If you do not use installers from your account, then your Clearinghouse account will not be credited with these donations.

You then take the installer from the previous step and include it alongside your application's installer.  This step depends largely on your application's installer, refer to your installer's manual for instructions.  From this point onwards, you follow a standard Seattle installation procedure.  Seattle will automatically start itself when the user's machine reboots.

To monitor if Seattle is running, you can check for ```python nmmain.py``` and ```python softwareupdater.py``` via ```ps``` on Unix-like machines.  nmmain.py is the node manager that interacts with Seattle and also manages the VMs that will run on your target system.  softwareupdater.py will periodically check for the latest version of Seattle, and update your target systems as necessary.
