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



