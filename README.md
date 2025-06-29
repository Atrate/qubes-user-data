# Qubes User Data

[![License: AGPL v3](https://img.shields.io/badge/License-AGPLv3-blue.svg)](https://www.gnu.org/licenses/agpl-3.0.en.html) 

## Description

This script is designed for QubesOS. It makes use of the `vm.config` feature to
execute scripts in any type of Qube, even DisposableVMs. The script's content is
configured from `dom0` directly. Inspired by [this forum
thread](https://forum.qubes-os.org/t/customize-a-named-disposable-using-the-vm-config-feature/34207).
Naming inspired by a similar AWS EC2 feature. The script accepts plaintext or
base64-encoded input.

## Usage

1. Download `qubes-user-data.service` and copy it over to your TemplateVM(s)
2. Inside your TemplateVM copy the file to `/etc/systemd/system`
3. Also inside that VM, execute `sudo systemctl daemon-reload && sudo systemctl
   enable qubes-user-data`
4. Shut your TemplateVM down
5. Enable the `qubes-user-data` service for your named DispVM (or other VM)
   through the Qube Manager's `services` tab
6. Write a script (one-liners are best due to newline issues) and optionally
   encode it with `base64 -w 0 FILENAME` (when base64-encoded you do not have to
   worry about newlines or special characters)
7. In `dom0`, execute `qvm-features QUBENAME vm-config.user-data
   ONELINER/BASE64ENCODEDSCRIPT`
8. Enjoy! Check the status of the script in your DispVM after launching via
   `sudo systemctl status qubes-user-data`

## License
This project is licensed under the [AGPL-3.0-or-later](https://www.gnu.org/licenses/agpl-3.0.html).

[![License: AGPLv3](https://www.gnu.org/graphics/agplv3-with-text-162x68.png)](https://www.gnu.org/licenses/agpl-3.0.html)
