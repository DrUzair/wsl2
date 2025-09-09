# Install Ubuntu 22.04
	```bash
   wsl --install -d Ubuntu-22.04
	```
# WSL : Linux distributions
  ```bash
  wsl -l -v # list available instances of wsl
  wsl -d distname # launch linux instance distname
  ```
## Start Ubuntu in WSL2
  ```bash
  wsl -d Ubuntu-22.04
  ```
# WSL reset passwd
  wsl -d Ubuntu-22.04 -u root
  passwd your_username
