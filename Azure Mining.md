# How to setup Azure Mining

## 1.Azure Hardware Setup
For CPU intense mining use:
- Standard_F2s_v2
- Standard_F4s_v2

## 2.Steps required on Mining server
**Create required dirs:**(*Use following PowerShell commnand*)

MkDir C:\CryptoMining\Claymore_CPU_Miner-v3.5
MkDir C:\CryptoMining\XMR-Stak\
MkDir C:\CryptoMining\Claymore_CPU_Miner-v3.8
MkDir C:\CryptoMining\Nheqminer_v0.4b
MkDir C:\CryptoMining\LNK\
MkDir C:\CryptoMining\BAT\

**Add exclussions to Windows Defender:**(*Use following PowerShell commnand*)
Add-MpPreference -ExclusionPath "C:\CryptoMining"
Add-MpPreference -ExclusionProcess "NsCpuCNMiner64.exe"

**Configure Firewall to enable Ping:**(*Use following PowerShell commnand*)
Get-NetFirewallRule | where {$_.DisplayName -like "*ICMPv4*"} | Set-NetFirewallRule -Enabled True

**Stop and Disable Windows Update:**(*Use following PowerShell commnand*)
Get-Service wuauserv | Stop-Service 
Get-Service wuauserv | Set-Service –startup disabled

**Delete any previosly created shortcuts:**(*Use following PowerShell commnand*)
del C:\CryptoMining\*.lnk
del C:\CryptoMining\LNK\*.lnk
del C:\CryptoMining\*.bat
del C:\CryptoMining\BAT\*.bat

**Copy actual shortcuts:**(*Use following PowerShell commnand*)
Copy-Item \\tsclient\c\cryptomining\LNK\*.lnk C:\CryptoMining\LNK
Copy-Item \\tsclient\c\cryptomining\BAT\*.bat C:\CryptoMining\Bat

**Copy mining software:**(*Use following PowerShell commnand*)
Copy-Item \\tsclient\c\CryptoMining\Claymore_CPU_Miner-v3.5\*.*  C:\CryptoMining\Claymore_CPU_Miner-v3.5 -exclude *.log
Copy-item \\tsclient\c\cryptomining\xmr-stak\*.* C:\CryptoMining\XMR-Stak -exclude *.log
Copy-item \\tsclient\c\cryptomining\Claymore_CPU_Miner-v3.8\*.* C:\CryptoMining\Claymore_CPU_Miner-v3.8 -exclude *.log
Copy-item \\tsclient\c\cryptomining\Nheqminer_v0.4b\*.* C:\CryptoMining\Nheqminer_v0.4b -exclude *.log

## 3. Usefull info
**List Claymore Miner Instacess:**
tasklist.exe /FI "imagename eq NsCpuCNMiner64.exe"

