# Using And Configuring Flatpak
Flatpak is the new command line installer on the block. It has been chosen by Pop!\_OS for it's ability to integrate with the app launcher and provide configuration for users. I have found, however, that it is a frustrating addition out of the box because it defaults to user installations and does not install remote repositories for the system. 

I struggled with this as a result of my attempts to install Godot and Sublime Text 3 in a way that would allow me to launch an external editor from Godot. When I was unable to do so I realized that it was because 
1. Godot didn't have system permissions
2. Flatpak wasn't configured with an option for system installations

Therefore, I went on a circuitous route to configure flatpak and learn how it works in slightly more detail than I knew before. I first attemtpted to solve the problem by installing the apps from aptitude and Godot's website. While this worked, it left the burden of updating and maintaining the installations solely on my shoulders. And since stability is a key factor for game development, I decided this was definitely the grounds for a later disaster. Especially since I will no doubt need to do something similar later.

## Flatpak: A Brief Explanation
Flatpak, like aptitude, makes it easy to install applications across various distributions with minimal configuration on the part of the user. In addition to requiring much more wordy commands to operate, it differentiates between user installations and system installations. This becomes annoying because although Flatpak niftily uses remote repositories to manage available apps, it allows the user to choose the repo or "remote" in the command, and also sets default remotes based on the command's execution level. If executed as a `--user` Flatpak chooses the associated remote which was configured for Flatpak using:

	$ flatpak add-remote remote_name https://remote_location/path

While great for security, pretty evident since it took me 45 minutes to figure out, this adds _another_ step for users to get through and troubleshoot when learning.

**Note:** Pop!\_OS uses Flatpak for the Pop! Shop app whenever possible and, as of the time this was written, I still don't know how to install apps for the system from the shop. To my knowledge it must be done from the command line with: `$ flatpak install --system remote_ref app_name`. 

## Installation Location
When installing with flatpak whether the user installs for system or user using the ``--system`` and ``--user`` tags determines where the application executables and files are installed. 

**User:** ``~/.local/share/flatpak`` or ``~/.var/app/ # according to ostechnix.com``

**System:** ``/var/lib/flatpak/``

## Flatpak Resources and Tutorials
* [OS Technix: How To Use Flatpak](https://ostechnix.com/how-to-install-and-use-flatpak-in-linux/)
* [Flathub: Home of Flatpak](https://flathub.org/home)
* [Flatpak Documentation](https://docs.flatpak.org/en/latest/index.html#)
* [Using an External Editor In Godot](https://github.com/flathub/org.godotengine.Godot#using-an-external-script-editor)
