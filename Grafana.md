Download Grafana GPG Key

'''
curl -q -o gpg.key https://rpm.grafana.com/gpg.key
'''

Explanation: Downloads Grafana security key.

Import GPG Key
---
sudo rpm --import gpg.key
---
Explanation: Adds the Grafana key to RPM trust list.

Create Grafana Repo File
---
vi /etc/yum.repos.d/grafana.repo
---
Explanation: Opens repository configuration file.

Add below content:

[grafana]
name=grafana
baseurl=https://rpm.grafana.com
repo_gpgcheck=1
enabled=1
gpgcheck=1
gpgkey=https://rpm.grafana.com/gpg.key
sslverify=1
sslcacert=/etc/pki/tls/certs/ca-bundle.crt

Explanation: Configures Grafana package repository.

Install Grafana
---
sudo dnf install grafana -y
---
Explanation: Installs Grafana package.

Reload Systemd
---
systemctl daemon-reload
---
Explanation: Reloads system services.

Start Grafana Service
---
systemctl start grafana-server
---
Explanation: Starts Grafana server.

Enable Grafana Service
---
systemctl enable grafana-server
---
Explanation: Starts Grafana automatically after reboot.

Check Service Status
---
systemctl status grafana-server
---

Explanation: Checks Grafana running status.

Open Grafana Port
---
netstat -lntp
---

Explanation: Allows Grafana web access on port 3000.

Access Grafana
---
http://<Server-IP>:3000
---
