<!--
 * This file is part of RS Cheat Sheets.
 *
 * RS Cheat Sheets is free software: you can redistribute it and/or modify
 * it under the terms of the GNU General Public License as published by
 * the Free Software Foundation, either version 3 of the License, or
 * (at your option) any later version.
 *
 * RS Cheat Sheets is distributed in the hope that it will be useful,
 * but WITHOUT ANY WARRANTY; without even the implied warranty of
 * MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
 * GNU General Public License for more details.
 *
 * You should have received a copy of the GNU General Public License
 * along with RS Cheat Sheets. If not, see <https://www.gnu.org/licenses/>.
 */
-->

[Home](../README.md)

# SystemD
	SystemD is an init system. It is the first program that starts up after boot, it's PID 1, and it starts other programs on startup. It also manages all services that run in the background.

	Units in SystemD are resources that it's able to manage.

	| Unit type | Description                                         |
	|-----------|-----------------------------------------------------|
	| Service   | Background services such as servers, databases, etc |
	| Socket    |                                                     |
	| Device    | Device modules in the Linux device tree             |
	| Mount     | Mounting points for file systems                    |
	| Automount |                                                     |
	| Target    |                                                     |
	| Snapshot  | Saved states of the system                          |
	| Timer     | Used to schedule services or tasks                  |

- `systemctl status <application>`
	- Used to check the status of an application.
	- If Loaded is disabled it won't start up on boot
- `sudo systemctl start <application>`
- `sudo systemctl stop <application>`
- `sudo systemctl restart <application>`
	- Stops and then starts the application
- `sudo systemctl reload <application>`
	- Reloads the unit file/configuration without stopping the application.
- `sudo systemctl enable <application>`
	- Used to enable the application so it starts on boot up.
- `sudo systemctl disable <application>`


These are the SystemD's Unit directories.They are in order of priority. (A unit file in the /etc/... folder overrides any in the /run/... or /lib/... folders.)
1. `/etc/systemd/system`
1. `/run/systemd/system`
1. `/lib/systemd/system`

- `Wants` in the .service files tells SystemD which other unit files need to be ran before this one.
- `After` in the .service files tells SystemD which units to start after this unit starts.
- `sudo systemctl edit <application>.service`
	- Used to make changes to the .service file. It saves those changes in another file and doesn't change the original file.
	- It creates a new folder in `/etc/...` with the name of `<application>.service` and a file called `override.conf`
	- You have to put any changes before `### Edits below this comment will be discarded`
- `sudo systemctl edit --full <application>.service`
	- Overrides the original .service file
- `sudo systemctl daemon-reload`
	- Used to reload the SystemD manager configuration. Used to load in changes to unit files.