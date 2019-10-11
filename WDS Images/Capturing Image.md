## Capturing the Image

- Prepare the OS
    - Remove old Snapshots
    - Clean Drive/Error Check
    - Change Enviroment Version Value

![Soe Environment Variable](./resources/ENV-SOE.png)
<br>
- Create Snapshot  
<br>
- Run Sysprep
	- Audit Mode
	- Generalized
	- Reboot  

![Sysprep Audit](./resources/sysprep-audit.png)
<br>
- Run Scandisk C:\

![Scan Disk](./resources/scan-disk.png)

- Clean Logs  
<br>
- Create Another snapshot
<br>
- Run Sysprep
	- OOBE
	- Generalized
	- Shutdown

![Sysprep Out Of Box Experince](./resources/sysprep-OOBE.png)

Boot to WDS
Capture Image to Local Storage
