# Desktop and Launcher App Configuration
Below are the resources and instructions for installing apps for users/system, adding apps to launcher w/ icons, and resource links.

# Work Log
| Date       | Description | 
| :--------: | :---------: |
| 12/16/2020 | Realized that I needed more control over installation and launching of Godot than flatpak gave me. |
| 12/17/2020 | Uninstalled all flatpak app files for Sublime Text and Godot, reinstalled from web downloads and configured using online tutorials |

# Commands Used
| Command    | Description | 
| :--------: | :---------: |
| ln -s      | created soft links to installation locations |
| mv, cp, rm | did some basic file moving and shaking |
| vim		 | edited `.desktop` files |

# Resources and Things Learned
[Add Linux Applications to Launcher by Creating .desktop File](https://technastic.com/add-linux-apps-app-launcher-desktop-file/)

Learned that applications installed for a single user are installed at `~/.local/share/applications` or in the `flatpak` directory under `share`. 

Applications installed for all users of a system are installed in `/usr/bin` and their desktop config files are installed in `/usr/share/applications`. **Note:** executable files are not installed in `applications`.

### `.desktop` File Contents
Place the following in a file such as `app-name.desktop`. This allows any OS launcher to run the executable and associate an icon with the file for beautification.

	[Desktop Entry]
	Encoding=UTF-8
	Version=1.0
	Type=Application
	Terminal=false
	Exec=/path/to/executable
	Name=Name of Application
	Icon=/path/to/icon

It is possible to add other settings, but I have not looked into this yet.