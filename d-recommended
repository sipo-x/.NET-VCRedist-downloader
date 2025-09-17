@echo off
title Dependencies Installer

net session >nul 2>&1
if %errorlevel% neq 0 (
    echo Requesting Administrator Privileges...
    powershell -Command "Start-Process '%~f0' -Verb RunAs"
    exit /b
)

echo ============================================
echo About to download dependencies...
echo ============================================
echo.

echo Downloading .NET 8.0.100 SDK...
powershell -NoLogo -NoProfile -Command ^
    "$ProgressPreference = 'SilentlyContinue'; Invoke-WebRequest -Uri 'https://builds.dotnet.microsoft.com/dotnet/Sdk/8.0.100/dotnet-sdk-8.0.100-win-x64.exe' -OutFile 'dotnet-runtime-100.exe'"

echo Installing .NET 8.0.100 SDK...
dotnet-runtime-100.exe /quiet /norestart
echo .NET 8.0.100 SDK installation completed.
echo.

echo Downloading Visual C++ Redistributables (VC Redist x64)...
powershell -NoLogo -NoProfile -Command ^
    "$ProgressPreference = 'SilentlyContinue'; Invoke-WebRequest -Uri 'https://aka.ms/vs/17/release/vc_redist.x64.exe' -OutFile 'vc_redist.x64.exe'"

echo Installing VC Redist...
vc_redist.x64.exe /quiet /norestart
echo VC Redist installation completed.
echo.

del dotnet-runtime-100.exe
del vc_redist.x64.exe

echo ============================================
echo All dependencies installed successfully!

echo.
choice /M "Do you want to restart your PC now?"
if errorlevel 2 (
    echo Restart cancelled.
) else (
    echo Restarting PC...
    shutdown /r /t 0
)

echo Press any key to exit...
pause >nul
exit
