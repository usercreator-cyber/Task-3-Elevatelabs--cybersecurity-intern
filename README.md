# Task-3-Elevatelabs--cybersecurity-intern
Vulnerability Scan Setup Using Nessus Essentials

OBJECTIVE : To use Nessus Essentials to do a simple vulnerability scan on the local system and use free community resources to find any potential vulnerabilities.
Downloaded Nessus Essentials

Used curl to download Nessus installer for Ubuntu:

curl --request GET \
--url 'https://www.tenable.com/downloads/api/v2/pages/nessus/files/Nessus-10.8.4-ubuntu1604_amd64.deb' \
--output 'Nessus-10.8.4-ubuntu1604_amd64.deb'
Installed Nessus

Installed using:

sudo dpkg -i Nessus-10.8.4-ubuntu1604_amd64.deb
sudo apt --fix-broken install
Started Nessus Service

Started and enabled the service:

sudo systemctl start nessusd
sudo systemctl enable nessusd
Faced Plugin Registration Issue

Nessus showed: Did not get a 200 OK response from the server: HTTP/1.1 400 Bad Request

Root Cause: Plugin feed registration failed due to:

Invalid or reused activation code
Plugin download blocked or broken
Feed fetch error from Tenable’s server
Debugging and Mitigation

Unregistered Nessus and cleared cache:

sudo /opt/nessus/sbin/nessuscli fetch --unregister
sudo rm -rf /opt/nessus/var/nessus/*
Retried registration manually:

sudo /opt/nessus/sbin/nessuscli fetch --register <YOUR-CODE> --os ubuntu1604 --accept-eula
Validated Internet and Plugin Access

Checked server response:

curl -I https://plugins.nessus.org
Ensured system had internet access and outbound HTTPS was not blocked.

📌 Key Takeaways:
Proper activation and plugin downloads are mandatory for scan functionality.
Internet access and firewall/proxy settings can directly affect Nessus's ability to fetch updates.
Manual commands like nessuscli fetch and clearing cache are useful for troubleshooting.
Plugin feed error (HTTP 400) is often linked to invalid requests, stale cache, or reused codes.
