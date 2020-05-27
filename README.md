# SmartBackup

[![N|Solid](images/AcuWorkflow-logo-02L.jpg)](http://www.acuworkflow.com)

[![Build Status](https://travis-ci.org/joemccann/dillinger.svg?branch=master)]()

SmartBackup is a cloud-enabled backup utility for [Smartsheet](https://www.smartsheet.com).  Backup all your Smartsheet data. 
(c) 2020 AcuWorkflow

  - Multi-Tenant solution - can take backups of all, groups of or any Smartsheet User
  - Preserve all Sheet formatting, a feature not available from standard Smartsheet
  - Perform snap-shot copy of all your sheets to Smartsheet Workspace of your choice
  - Ideal for individuals or teams wanting to snapshot data after certain events

# Easy to Use

  - You designate any Smartsheet Workspace as Backup Vault. 
  - On the next backup run, all your sheets will be backed-up into Backup Vault group by backup set Folder
  - Restore is a doddle, you simply copy the Sheet from Backup Vault area

# How it works
- SmartBackup can run instantly on demand, on schedule or automated intervals
- SmartBackup will create a new folder with a timestamp in the user defined SmartSheet Vault designating a backup set
- For each configured Smartsheet User (Tenant) it backs up all the sheets owned by that user into designated Vault and Backup set folder.
- Extensive logging and status is provided

# Getting Started

These instructions will get you up and running with SmartBackup.

Steps involved:
  - Install SmartBackup for yourself, team, division or Organization
  - Configure it for your needs
  - Schedule SmartBackup to run  

### Installation

SmartBackup for Windows requires EXE to run.

Install SmartBackup on Backup Machine of your choice.

```sh
$ mk smartbackup
$ cd smartbackup
$ xcopy <source> smartbackup
```

### Setup and Configuration

##### Tenants file
Edit SmartBackup.csv to contain entries for every Smartsheet User(Tenant) you want to backup.  Note column names must be spelled exactly as shown and is case-sensitive.

| Name | Value |
| ------ | ------ |
| Status | Must be set to **'Enabled'** for processing tenant entry.  To disable entry on backup run change to any Status value of your choice |
| Tenant | Name of Tenant e.g. **Joe Blocks** |
| TenantID | Email address of Tenant e.g. **joe.blocks@acme.com** |
| TenantOrg | Organization Name of Tenant e.g. **Acme Corp** |
| TenantToken | Smartsheet **API Token** of Tenant (Backup Source) |
| VaultToken | Smartsheet **API Token** of Vault Tenant. (Backup Target)  Should be the same if Tenant is backing up to a Workspace within his/her environment |
| VaultID | Smartsheet **ID** of Workspace where designated Vault resides |
| VaultLink | Smartsheet **Link** of Workspace where designated Vault resides |

1. You can have multiple Tenant Files each containing differing configurations based on your setup
2. At run time associate the Tenant file you want to use for that particular run
3. To get Smartsheet API tokens or ID's refer to [Smartsheet](https://www.smartsheet.com) 



### Run SmartBackup

##### Optional Arguments
``-t or --tenant path\smartbackup.csv`` Path and filename of *TenantsFile*.  If not supplied will default to SmartBackup.csv in execution folder.  Smartbackup will terminate if file not found.

``-l or --log path\smartbackup.csv`` Path and filename of *LogFile*.  If not supplied will default to SmartBackup.log in execution folder.  If not found will attempt to create one in execution folder.  Smartbackup will terminate if it cannot be created.

```tenanttoken```

##### Run from Windows CMDLine
Invoke Cmdline by clicking on Windows search and type ``cmd``
then invoke as follows:
###### examples
``sbu_r2.3.exe``  or
``sbu_r2.3.exe -t c:\smartbackup\tenants\tenants.csv``

##### Run from Windows Shortcut
Create shortcut pointing to EXE and click on shortcut

##### Run from Windows Explorer
Double click on EXE.  Note this method does not easily allow you to specify arguments

##### Run from Windows Task Scheduler
Open Windows Task Scheduler and configure EXE to a schedule of your choice

##### Run using PowerShell
Script EXE using Powershell

## Authors

* **Deon Pollard** - *Base software R2.3* - [deon pollard & associates](https://deonpollard.com)

See also the list of [contributors](http://www.acusoftware.com) who participated in this project.

## License

[![N|Solid](https://mirrors.creativecommons.org/presskit/buttons/88x31/png/by-nc-sa.png)](https://creativecommons.org/about/cclicenses/)
This project is licensed under the Creative Commons License -  [LICENSE](https://creativecommons.org/about/cclicenses/) for details 

