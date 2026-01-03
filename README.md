Ransomware Defense \& Precursor Pack for Microsoft Sentinel

Version: 1.0.0 Author: Johan Brider / HackerStopped



🚨 Overview

This is not just a list of alerts—it is a comprehensive Ransomware Defense System.



Most organizations only detect ransomware when files are already encrypted. The Ransomware Defense Pack is designed to catch the precursors—the specific tools, techniques, and behaviors attackers use in the hours or days before the encryption event.



This pack includes high-fidelity detection rules covering the entire kill chain:



Initial Access \& C2: Cobalt Strike, Metasploit, and RMM abuse (AnyDesk, ScreenConnect).



Evasion: Killing security tools (Defender, EDR), clearing logs, and bypassing AppLocker.



Exfiltration: Data theft tools like Rclone, MEGAsync, and USB mass copying.



Impact: Mass file encryption and Shadow Copy deletion.



📦 What's Included?

This pack contains a consolidated ARM Template (JSON) that deploys the following analytics rules to your Microsoft Sentinel workspace.



🔴 Phase 1: Precursors \& Command and Control (C2)

\[C2] Offensive Frameworks: Detects Beacon, Sliver, and Metasploit payloads and named pipes.



\[RMM] Unauthorized Remote Access: Alerts on ScreenConnect, AnyDesk, and TeamViewer usage (common in modern ransomware ops).



Potential Ransomware activity related to Cobalt Strike: Correlates Cobalt Strike signatures with ransomware staging.



\[Identity] Brute Force / Password Spraying: Detects high-volume authentication failures indicative of initial access attempts.



🟡 Phase 2: Defense Evasion \& Persistence

\[Defense Evasion] BYOVD - Vulnerable Driver Creation: Detects the drop of vulnerable drivers (e.g., mhyprot2.sys) used to kill EDR.



Stopping multiple processes using taskkill: Identifies attempts to mass-terminate security services.



Clearing of forensic evidence (wevtutil): Alerts when attackers attempt to wipe Windows Event Logs to hide tracks.



Tampering with Microsoft Defender Preferences: Detects PowerShell commands disabling RealTimeMonitoring or IOAVProtection.



⚫ Phase 3: Exfiltration \& Impact

\[Ransomware] Mass File Encryption: Detects high-velocity file modification/renaming (the actual encryption event).



Shadow Copy Deletion Attempt: Detects vssadmin or wmic deleting backups to prevent recovery.



\[Exfiltration] Rclone / MEGAsync: Identifies known tools used to steal data prior to encryption (Double Extortion).



Mass File Exfiltration to USB: Detects large-scale file copies to removable media.



🚀 Installation Guide

Option 1: One-Click Deployment (Recommended)

Log into your Azure Portal.



Search for "Deploy a custom template" in the top search bar.



Click "Build your own template in the editor".



Click "Load file" and select Ransomware\_Defense\_Pack.json.



Click Save.



Select your Subscription, Resource Group, and type your Sentinel Workspace Name in the parameter box.



Click Review + create -> Create.



**Option 2: PowerShell / CLI**

New-AzResourceGroupDeployment -ResourceGroupName "YourResourceGroup" -TemplateFile ".\\Ransomware\_Defense\_Pack.json" -workspace "YourWorkspaceName"





⚠️ Disclaimer

Testing: We recommend deploying these rules in a test environment or with "Status: Disabled" first to tune for your specific environment's baselines.



False Positives: Some RMM tools (e.g., TeamViewer) may be legitimate in your environment. You may need to whitelist your specific admin subnets or accounts.

