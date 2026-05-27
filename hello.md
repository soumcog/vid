EnpQxuf1y5Moo5IAvM8bD036Fpvvj80dWHjkAqjSyVe8542sZfW4JQQJ99CEACAAAAA6DxLKAAASAZDO3Kp

https://GenAIGarage@dev.azure.com/GenAIGarage/Garage/_git/VZ_GARAGE_OPS_EXCELENCE_POD

# Download NGINX directly
Invoke-WebRequest -Uri "https://nginx.org/download/nginx-1.26.3.zip" -OutFile "C:\nginx.zip"

# Extract it
Expand-Archive -Path "C:\nginx.zip" -DestinationPath "C:\"

# Rename the extracted folder to simply "nginx"
Rename-Item "C:\nginx-1.26.3" "C:\nginx"



---------------


# Download
Invoke-WebRequest -Uri "https://dl.google.com/chrome/install/latest/chrome_installer.exe" -OutFile "$env:USERPROFILE\Downloads\chrome_installer.exe"

# Install silently
Start-Process -FilePath "$env:USERPROFILE\Downloads\chrome_installer.exe" -ArgumentList "/silent /install" -Wait





------------------

--------------

CPCINCHDV715893
10.127.117.255

 Clean and simple — frontend only. Here are all the steps from start:

Step 1: Build the Frontend
Open PowerShell, navigate to the frontend folder:


cd C:\your\cloned\path\master-service-frontend
npm install
npm run build
Wait for it to finish. You'll see a dist\ folder created inside the frontend folder.

Step 2: Copy dist into NGINX

Copy-Item -Recurse "C:\your\cloned\path\master-service-frontend\dist\*" "C:\nginx\html\"
Step 3: Configure NGINX
Paste this entire block into PowerShell:


$config = @'
worker_processes  1;
events { worker_connections 1024; }

http {
    include       mime.types;
    default_type  application/octet-stream;
    sendfile      on;
    keepalive_timeout 65;

    server {
        listen 80;
        server_name localhost;

        root   html;
        index  index.html;

        location / {
            try_files $uri $uri/ /index.html;
        }
    }
}
'@

$config | Out-File -FilePath "C:\nginx\conf\nginx.conf" -Encoding ascii
Step 4: Start NGINX

cd C:\nginx
.\nginx.exe
Step 5: Open Firewall Port

netsh advfirewall firewall add rule name="VZ Garage Frontend" dir=in action=allow protocol=TCP localport=80
Step 6: Open Chrome and Test
On the VM:


http://localhost
From another machine on the same network — first get the VM's IP:


ipconfig
Then open:


http://<VM-IP>
That's it — 6 steps. Tell me what happens at each step.



-------------------

-------------------

Simple fix — just update the server_name in the NGINX config. Paste this in PowerShell:


$config = @'
worker_processes  1;
events { worker_connections 1024; }

http {
    include       mime.types;
    default_type  application/octet-stream;
    sendfile      on;
    keepalive_timeout 65;

    server {
        listen 80;
        server_name CPCINCHDV715893 10.127.117.255;

        root   html;
        index  index.html;

        location / {
            try_files $uri $uri/ /index.html;
        }
    }
}
'@

$config | Out-File -FilePath "C:\nginx\conf\nginx.conf" -Encoding ascii
Then start NGINX:


cd C:\nginx
.\nginx.exe
Open firewall:


netsh advfirewall firewall add rule name="VZ Garage Frontend" dir=in action=allow protocol=TCP localport=80
Now anyone on the network can access it via:


http://CPCINCHDV715893
http://10.127.117.255
Both will work. Try it in Chrome on the VM first.

can i give a public access to anyone on the internet ?
Short answer: Not directly. Here's why and what your options are.

The Problem
10.127.117.255 is a private IP — it only works inside the Cognizant corporate network. The internet cannot reach it directly. It's behind Cognizant's corporate firewall.

Your Options
Option 1 — VPN Access (Easiest, No IT needed)
Anyone who has Cognizant VPN access can already reach it at:


http://10.127.117.255
No extra setup needed. Best for internal team sharing.

Option 2 — Ngrok (Quick public URL, good for demos)
Ngrok creates a temporary public URL that tunnels to your VM. No IT involvement needed.


# Download ngrok
Invoke-WebRequest -Uri "https://bin.equinox.io/c/bNyj1mQVY4c/ngrok-v3-stable-windows-amd64.zip" -OutFile "$env:USERPROFILE\Downloads\ngrok.zip"
Expand-Archive "$env:USERPROFILE\Downloads\ngrok.zip" -DestinationPath "C:\ngrok"

# Run it (NGINX must be running on port 80)
C:\ngrok\ngrok.exe http 80
It gives you a public URL like:


https://abc123.ngrok.io  ← anyone on the internet can access this
Downside: URL changes every time you restart ngrok (free plan). Good for demos, not permanent.

Option 3 — Request IT to Open a Port (Permanent public access)
Raise a request with Cognizant IT/network team to:

Assign a public IP or set up port forwarding on the corporate firewall to your VM's port 80
This is the proper production approach but requires approval and time
Option 4 — Move to Azure (Proper cloud deployment)
Deploy the app to Azure App Service or an Azure VM — then it gets a real public URL like https://vz-garage-ops.azurewebsites.net.

Recommendation
Need	Best Option
Internal team only	VPN (Option 1)
Quick demo for stakeholders	Ngrok (Option 2)
Permanent public access	IT request or Azure (Option 3/4)
What's your use case — internal team or external stakeholders?






