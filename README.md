# deep-in-system

## Virtual Machine Part:

1. **Install Ubuntu Server:**
   - Download the latest LTS version of Ubuntu Server.
   - Create a new virtual machine with a 30GB disk size using VirtualBox.
   - During installation, set up the partitions as specified (`swap`, `/`, `/home`, `/backup`).
   - Use your username as `zewas`.
   - Set the hostname as `zewas-host`.

## Network Part:

2. **Set Static Private IP:**
   - Edit the network configuration file:
     ```bash
     sudo nano /etc/netplan/01-netcfg.yaml
     ```
   - Configure the network settings with a static private IP.

3. **Test Internet Connection:**
   ```bash
   ping -c 5 google.com
   ```

## Security Part:

4. **Disable Remote Root Login:**
   - Edit the SSH configuration file:
     ```bash
     sudo nano /etc/ssh/sshd_config
     ```
   - Set `PermitRootLogin no`.

5. **Change SSH Port:**
   - In the SSH configuration file, set `Port 2222`.

6. **Configure Firewall:**
   - Use `ufw` to configure the firewall:
     ```bash
     sudo ufw default deny incoming
     sudo ufw default allow outgoing
     sudo ufw allow 2222
     sudo ufw allow http
     sudo ufw allow https
     sudo ufw allow ftp
     sudo ufw enable
     ```

## User Management Part:

7. **Create Users:**
   ```bash
   sudo adduser luffy
   sudo adduser zoro
   ```

8. **Configure SSH for luffy:**
   - Copy the public key to `/home/luffy/.ssh/authorized_keys`.

9. **Configure Password for zoro:**
   ```bash
   sudo passwd zoro
   ```

## Services Part:

10. **Install FTP Server:**
    - Install vsftpd:
      ```bash
      sudo apt-get update
      sudo apt-get install vsftpd
      ```
    - Configure FTP for user `nami` with read-only access to `/backup`.

## Database Part:

11. **Install MySQL Server:**
    ```bash
    sudo apt-get install mysql-server
    ```

12. **MySQL Security Config:**
    - Run `mysql_secure_installation` to secure MySQL.

13. **Create MySQL User for WordPress:**
    - Log in to MySQL and create a user named `wordpress_user` with appropriate privileges for WordPress.

## WordPress Part:

14. **Install NGINX:**
    - Download NGINX from official site.
    - Create config file `/etc/nginx/sites-available/wordpress` with WordPress details.
   
15. **Install WordPress:**
    - Download and extract WordPress to the web server root directory `/var/www/html`.
    - Configure the `wp-config.php` file with MySQL details.

16. **Verify WordPress Installation:**
    - Access `http://{host}/` and complete the WordPress setup.

## Backup Part:

17. **Set Up Cron Job:**
    - Create backup script:
      ```bash
      sudo nano /home/zewas/backup_script.sh
      ```
    - Edit the crontab:
      ```bash
      crontab -e
      ```
    - Add the following line:
      ```bash
      0 0 * * * /home/zewas/backup_script.sh
      ```
   
