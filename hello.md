EnpQxuf1y5Moo5IAvM8bD036Fpvvj80dWHjkAqjSyVe8542sZfW4JQQJ99CEACAAAAA6DxLKAAASAZDO3Kp

https://GenAIGarage@dev.azure.com/GenAIGarage/Garage/_git/VZ_GARAGE_OPS_EXCELENCE_POD

# Download NGINX directly
Invoke-WebRequest -Uri "https://nginx.org/download/nginx-1.26.3.zip" -OutFile "C:\nginx.zip"

# Extract it
Expand-Archive -Path "C:\nginx.zip" -DestinationPath "C:\"

# Rename the extracted folder to simply "nginx"
Rename-Item "C:\nginx-1.26.3" "C:\nginx"



---------------


# Full standalone installer (larger file but more reliable on corporate networks)
Invoke-WebRequest -Uri "https://dl.google.com/tag/s/dl/chrome/install/googlechromestandaloneenterprise64.msi" -OutFile "$env:USERPROFILE\Downloads\chrome.msi"

# Install silently
Start-Process msiexec -ArgumentList "/i $env:USERPROFILE\Downloads\chrome.msi /quiet /norestart" -Wait


