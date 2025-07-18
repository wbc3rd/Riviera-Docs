Connecting to Riviera
=====================

Global Protect VPN
------------------
In order to connect to the Riviera HPC system you must be connected to CSU's campus network. Remotely this can be achieved by using the Global Protect VPN documented by CSU `here <https://csusystem.freshservice.com/support/solutions/folders/23000047198>`_. Sometimes this VPN will be necessary even when on CSU's campus network due to abnormalities with how it is set up around the campus.

Credentials
-----------
Upon getting access to Riviera users are provided with their username and an initial password to connect to Riviera with. It is important to note that a user's username and password will be separate from the NetID supplied by CSU, and the user's NetID password should not be recycled for use on Riviera. Once connected to Riviera the first time users must change their password to a new secure password. To change the current password on Riviera, run the command ``passwd`` while connected to Riviera via SSH. A prompt will then appear to enter the old password and then to enter in the new password twice. It is likely that while entering passwords no characters will display in the terminal, this is an expected default behavior and for security reasons once a password is reset make sure to save it in a secure location such as a personal password manager.

Secure Shell
------------
When a user has credentials and is connected to the campus's network, Riviera can be accessed through Secure Shell (SSH). To connect to Riviera via SSH a user will run the command ``ssh username@riviera.colostate.edu`` from their terminal of choice. Once prompted the user will enter in their current password, either the one time password supplied initially or the new password they set themselves.