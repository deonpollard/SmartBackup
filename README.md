# SmartBackup

[![N|Solid](images/AcuWorkflow-logo-02L.jpg)](http://www.acuworkflow.com)

[![Build Status](https://travis-ci.org/joemccann/dillinger.svg?branch=master)]() 
![versions](https://img.shields.io/pypi/pyversions/pybadges.svg) [![License: CC BY-NC-ND 4.0](https://img.shields.io/badge/License-CC%20BY--NC--ND%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by-nc-nd/4.0/)

*SmartBackup* is a cloud-enabled backup utility for [Smartsheet](https://www.smartsheet.com).  Backup all your Smartsheet data. 
(c) 2020 AcuWorkflow.

- [x] **Multi-Tenant** solution - can take backups of all, groups-of or any Smartsheet User
-	[x] **Preserve** all Sheet formatting, a feature not available from standard Smartsheet backups
-	[x] Perform **snapshot copy** of all your sheets to a Smartsheet Workspace of your choice
-	[x] **Incremental or full back-ups** you have the option to only backup sheets that have changed in last ```x``` days
-	[x] Ideal for individuals or teams wanting to snapshot data after certain **events milestones**

> Typically *SmartBackup* is used to provide **rolling window of active sheets** one can re-instate, ideal for when inadvertent changes are made and one needs to roll-back invalid copy

# Easy to Use

-	You can designate any Smartsheet Workspace as Backup Vault
-	On the next backup run, all or a subset of your sheets will be backed-up into the Backup Vault group by backup set Folder
-	Restore is a doddle, you simply copy the Sheet or rows from the Backup Vault area
- [User Guides](https://github.com/deonpollard/smartbackup/wiki/)


# How it works

-	*SmartBackup* can run instantly on demand, on schedule, or at automated intervals
- Optionally you can override the backup set scope (e.g. only backup sheets that have been modified last ```x``` days
-	*SmartBackup* will create a new folder with a timestamp in the user defined SmartSheet Vault designating a backup set
-	For each configured Smartsheet User (Tenant) it backs up all/subset of the sheets owned by that user into the designated Vault and Backup set folder
-	Extensive logging and status are provided
- SmartBackup can be run:
  -- headless(no user interface, available as cmdline routine) and possibly be integrated with your other supporting services or
  -- headfull in which case you access it via a web user interface.

[![N|Solid](images/vault01.png)](http://www.acuworkflow.com)


# Getting Started

These instructions will get you up and running with *SmartBackup*.

Steps involved:
  1. **Installation** Install SmartBackup for yourself, team, division, or Organization
  2. **Setup and Configuration** Configure SmartBackup for your needs
  3. **Run SmartBackup** Schedule SmartBackup to run  

## Installation

Install *SmartBackup* on Backup Machine of your choice.  

> The free version is restricted to backing up only 3 sheets.  Contact [AcuWorkflow](http://www.acuworkflow.com) for licensed version with no restrictions.
1. Download from [AcuWorkflow](http://www.acuworkflow.com), run SETUP and follow instructions
2. Choose Full Installation when first time User
3. Choose Custom Installation and unselect Data Files if you are re-installing and want to preserve previous settings

## Using SmartBackup 

1. Invoke SmartBackup by clicking on desktop shortcut or double-click on console.exe in \apps installation folder
2. A cmd Window will appear running the Console Server with slight delay and then a browser view will be opened running the console client

[![N|Solid](images/Home.png)]()










## Setup and Configuration

### Tenants file
The Tenants file is  mandatory and must be supplied.  Edit the SmartBackup.csv file to contain entries for every Smartsheet User(Tenant) you want to backup. Note column names must be spelled exactly as shown and are case-sensitive.

| Name | Description | Example |
| --- | --- | --- |
| Status | Must be set to **'Enabled'** for processing tenant entry. To disable an entry on backup run change to the Status value to **‘Disabled’** | Enabled |
| Tenant | Name of Tenant  | Joe Blocks |
| TenantID | Email address of Tenant |  joe.blocks@acme.com |
| TenantOrg | Organization Name of Tenant | Acme Corp |
| TenantToken | Smartsheet **API Token** of Tenant (Backup Source) | ute0kvn9ol6lq10jwjylky9kdp |
| VaultToken | Smartsheet **API Token** of Vault Tenant (Backup Target). Should be the same if Tenant is backing up to a Workspace within his/her environment | ute0kvn9ol6lq10jwjylky9kdp |
| VaultID | Smartsheet **Workspace ID** of Workspace where designated Vault resides. Be carefull when editing this with Excel, since it will by default transform to exponential number, rather use Notepad for editing | 3458625596352300 |
| VaultLink | Smartsheet **Workspace Link** of Workspace where designated Vault resides | ``https://app.smartsheet.com/workspaces...`` |
| Archive | Link to where files can be archived to | C:\acmecorp\SmartSheet\Archive\ |

- You can have multiple Tenant Files each containing differing configurations based on your setup
- At run time associate the Tenant file you want to use for that particular run
- To get TenantToken 
   - Login to Smartsheet, click on Account top right
   - Select Apps & Integrations, then API, Generate Token
   - **Token** becomes your **TenantToken** in tenantfile, that way the backup knows who you are and therefore what files to backup


### Backup Vault
Once-off configure a Smartsheet Workspace that will act as the backup container.  To do this:
1. Login to Smartsheet, select **Workspaces**, right-click and then select [Create new Workspace](https://www.smartsheet.com)
2. Name the Workspace aptly, such as ``Vault`` or ``Backup Vault`` or ``SmartBackup Vault``
3. Right-click on Vault Workspace and select **Properties**
4. Copy the **Workspace ID** to tenantfile **VaultID**, in so doing it becomes the designated Target Backup area
5. Copy the **Workspace Link** to tenantfile **VaultLink**

> Note, Smartsheet restricts the number of sheets allowed for non-Enterprise [licenses](https://www.smartsheet.com/pricing).  Usually it is 100 per User or aggregate thereof e.g. 10 Users = 1000 Sheets.  In the event that you are running into these restrictions decrease the backup scope.

# Run SmartBackup
- SmartBackup ```R2.4``` is only available for Windows environments 
- MacOS and Linux Versions will shortly be released 
- When invoked from cmdline status and progress for each tenant will be shown as indicated below

[![sbu run](images/cmdline.png)](http://www.acuworkflow.com)

## Optional Arguments
The following parameters can optionally be passed as arguments on cmdline invocation

**-t** or **--tenantfile** Path and filename of *TenantFile*.  If not supplied will default to SmartBackup.csv in current execution folder.  *Smartbackup* will terminate if file not found 
Examples:  
``-t c:\smartbackup\smartbackup.csv``
``--tenantfile \\acmecorp\appserver\smartbackup.csv``

**-l** or **--logfile** Path and filename of *LogFile*.  If not supplied will default to SmartBackup.log in current execution folder.  If not found will attempt to create one in current execution folder.  Smartbackup will terminate if it cannot be created.
Examples:
``--logfile path\smartbackup.csv`` 

**-d** or **--days** Incremental backup by only backing up sheets modified in **days** period.  Default is ``5`` days.  To turn incremental backup into full backup typically do ``-d 9999``
Examples:
``-d 7`` 
``--days 30``

## Run from 

### Run from Windows CMDLine
Invoke Cmdline by clicking on Windows search and type ``cmd``then invoke as follows.
Examples:

> ``sbu_r2.3``  

> ``sbu_r2.3 -t c:\smartbackup\tenants\tenants.csv``

> ``sbu_r2.3 -d 15 -t=c:\smartbackup\sbutenants.csv -l=c:\smartbackup\sbulog.log``

### Run from Windows Shortcut
Create shortcut pointing to EXE and click on shortcut

### Run from Windows Explorer
Double click on EXE.  Note this method does not easily allow you to specify arguments

### Run from Windows Task Scheduler
Open Windows Task Scheduler and configure EXE to a schedule of your choice

### Run using PowerShell
Script EXE using Powershell

# Authors

* **Deon Pollard** - *Base software* - [deon pollard & associates](https://www.deonpollard.com)

> See also list of [contributors](http://www.acuworkflow.com) who participated in this project.

# License

[![N|Solid](images/cc.png)](https://creativecommons.org/about/cclicenses/)
This project is licensed under the Creative Commons License -  [LICENSE](https://creativecommons.org/about/cclicenses/) for details 
