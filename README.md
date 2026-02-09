
[![N|Solid](images/AcuWorkflow-logo-02L.jpg)](http://www.acuworkflow.com)

# SmartBackup V10.0.0 (7 July 2025)
``` Stable Release. Major Release ```
Include internal releases Version V9.5 & V9.6
## Strategic Outlook
### **Smartsheet API’s** 
SmartBackup interface with Smartsheet via their published API set.  Smartsheet have deprecated quite a few, most notably the /GET Home, whilst applying several restrictions/changes to others.   Amongst others, they nullify the response for how many pages a result set contains, which makes paging or anticipating the size of API results extremely difficult.  For example, the well-used sheetCount for each user is now indicated as -1, removing actual values.   For these reasons AcuWorkflow had to re-think its approach and modify substantial portions of the SmartBackup platform.   V10 contains several new and modified capabilities to align to the latest Smartsheet API direction.

### **ShadowCopy** 
With the need to redo Export due to deprecated API’s a new direction was taken to simplify and bolster performance at the same time.  Our knowledge gained over the last four years of SaaS processing, particularly Smartsheet allowed us to rethink the ideal way to make external copies of Smartsheet.  Improvements stellar, where old Export used to take 30mins plus for same activity it can now be accomplished in minutes.

### **Internal scheduled services** 
The re-architecture also allowed us to offer internal persistent scheduled services.  It should make setup and operations a lot easier.  For example, one can now switch on ShadowCopy at an interval of convenience without needing to setup tasks in Windows Task Manager. 

### **Moving forward**
V10 designates the beginning of the next generation platform for SmartBackup.  Export completely renewed with ShadowCopy, Archive has been mostly renewed and big enhancements to the Console and others.  The next phase is Backup which will be tackled in some of the next releases.  V10 is also transitioning to new way of Reporting status with a mixture of old and new.  Plan is only the new way in next releases.

## Platform enhancements and changes
   - APJ Region Support - SBU have region support for newly announced Asia-Pacific Smartsheet region
   - New capability ShadowCopy – functional replacement for Export
   - New Capability RefreshMembers 
   - New Capability DRPReporting
   - New Capability - New Housekeeping services that can be scheduled internally, aiming to make things simpler
   - New Capability Runbook introduction for those who want to have more sophisticated processing


# SmartBackup V9.1.1 (27 February 2025)
``` Bug fix Upgrade Release ```

## Bug Fix
   - Fix Backup to include attachments if attachments are requested

## Cosmetics
   - Modify strap-lines Licensing, Setup, Readme and Console dates to read 2021-2025


# SmartBackup V9.1.0 (10 December 2024)
``` Upgrade Release ```

## Enhancements

   - Offline Licensing
     - Optionally allow processing to continue if Licensing Server is unavailable.

   - Cosmetics
     - Administrator Notification
       - Improve wording and syntax
       - Remove Error and Totals columns in section 3
       - Improve Column Headings
     - Remove User Notifications from the UI Settings
       - Can still optionally be invoked by editing the config.yml file and set <usernotify> to true


# SmartBackup V9.0.0 (16 September 2024)
``` Stable Release. Major Release ```

## Enhancements
   - Backup
     - Cater for Plan Ownership Smartsheet change
     - Attachments can now be excluded from Backup copies

   - Export
     - Cater for Plan Ownership Smartsheet change

   - Archive
     - Cater for Plan Ownership Smartsheet change
     - New rinse option

   - New Vaults utility


## Corrections
   -  Show the existing Task Scheduler tasks that have been setup.
   -  Correct Notification Reports for Export runs are showing that “No sheets exported”, but in fact there were sheets exported.
   -  Remove “/” at the top of the notification reports
   -  Stop Export Outline option from exporting content.
   -  Correct Alert Notification email link
   -  Cosmetic enhancements


# SmartBackup V8.1.0 (23 July 2024)
``` Stable Release. Focus on bringing Platform to latest underlying software releases ```
## Enhancements
   - Export **Duplicate Folder** – Export now continues processing users with duplicated folders/workspaces.  Does so by adding numeric tiebreaker when duplicate folder condition is detected in same root.  Note tiebreaker may not be consecutive.  Note also this is different to same file-names where a timestamp is appended.
   - SMTP Address - New default SMTP address and password for Acuworkflow

## Internal Improvements
   - Internal Software Upgrades - Move platform to latest underlying supporting software
     - Py 3.8 -> 3.12, Pandas 1.8 -> 2.2, Flask pre 3 -> Waitress 3.0 


***


# SmartBackup V8.0.0 (16 November 2023)
``` Major Release. ```

## Enhancements
   - Console UI Enhancements
     - shows Status of Users from the perspective of SmartBackup and Smartsheet
       - SmartBackup Status **[Enabled, Disabled, Pending, Blocked]**
       - Smartsheet Status **[ACTIVE, DECLINED, PENDING, DEACTIVATED]**
       - Only users marked ```Enabled``` and ```ACTIVE``` will be processed by Backup, Archive and Export 
       - **NOTE**
         >Smartsheet status hold in SmartBackup may differ from the most recent status in Smartsheet if not recently refreshed.
         >even if User marked as **Enabled** **ACTIVE** it may not be processed by Backup, Archive, Export if most recent status not **ACTIVE**
     - Console UI refinements
       - Members list Recommend renaming of several column headers (refer to tab #2)
       - Members list Recommend realignment/order of various columns (refer to tab #2)
   - Users with SheetCount >= 1000 will by default get a **Blocked** SmartBackup Status
     - therefore these users will be ignored by Backup, Archive & Export
     - optionally one can alter **Blocked** Status to **Enabled** thus including user for processing
   - Dealing with Users that are deactivated by Smartsheet Administrators
     - Deactivated status will be shown based on the last refresh of Users from Smartsheet
     - Deactivated users will be ignored by Backup, Archive & Export
     - Backup, Archive & Export will now check the latest Smartsheet Status of each user prior to processing
       - If found ```DEACTIVATED``` it will not be processed
       - Smartsheet Status details will only be updated in Smartbackup based on the refresh 
       - To get the most recent Smartsheet status Backup, Archive & Export will now check Smartsheet status prior to processing  
   - Tenant Mode is no longer visible from Console UI.  In the event, one absolutely needs to access it, change config.yml sysadminmode=false
   - Administrator email can now notify multiple email recipients
   - Archive can now archive files to a UNC name, bring it in line with Export
   - Queue processing now also for Backups & Archive so that a user or groups of users can be processed separately (included in this release)
   - Limits for Reports & others removed, pagination
   - Sign all with new USB based token
     - Now signing each .exe as well so exe may be duplicated to other non-install folders

## Fixes
   - Duplicate Vaults :issue where duplicate Vaults are created when accessLevel is “ADMIN” or “OWNER”
   - Doc links pointing to new doc site
   - Remove email notification for duplicate folders during export – will just print console messages and process next user
   - .GOV base Relativity hotfix (included in this release)
   - Deal with Deactivated User
   - Cater for notLogin yet conditions
   - rules/ruleset fixed
   - Dashboard 100 limit removed

## Corrections
   - "bool" error. Seems to fail when transitioning between users
   - sysAdmin Error  After doing an "Upgrade install" - coded new upgrade process script adding column to Members.csv
   - Export Specific Report    Gives and "attachments" error, but does save the report
   - Export Report Location  It does not get saved under the User folder?


## Including
   > Interim update and internal releases 7.0.3 - 7.2.3
#### 7.2.3
     - Deal with Deactivated user
     - Introduce Blocked Users
#### 7.2.2
     - disable notification of IMS notifications for dupe folders
     - Support for Multi-groups in email for admin, similar to IMS
     - Support for Archive to archive to a UNC name location; bring in line with Export 
     - Remove Tenant Mode
     - Doc Link
     - CreateVault check for Owner and Admin
#### 7.2.0
     - Archive - fix Deletefolder attempts plus dealing with 500's
     - Support for Queue processing Backup and Archive, bring in line with Export
#### 7.1.0
     - INTERNAL copy 7.0.3 and reversion as 7.1.0
#### 7.0.3
     - Fix the Attachment Packing note. files were empty and needed to point to [1]





# SmartBackup V7.0.2 (10 April 2023)
``` Major release. ```
## Compatibility
    - V6.5.2 is available for existing License Server whilst V7.0.2 operate using new Licensing Server
## Fixes and Enhancements
### New capabilities
    - Cater for UNC path name when exporting data
    - Notifications can now be sent using an SMTP server requiring no login 
### Enhancements and fixes
    - Fix Business Edition SheetCount issue
    - Some general improvements, enhance performance when using Export specific
    - Backup options hidden

# SmartBackup V6.5.0  (24 November 2022)
``` Update release. ```
## Fixes and Enhancements
### 6.5.0
    - General maintenance release inclusive of 6.3.1 to 6.3.7
    - Remove dev message on Console 
### 6.3.7
   - fix the slowdown issue introduced by 6.3.6 break out of the loop
### 6.3.6
   - fix the issue whereby attachments were not written out
### 6.3.5
   - fix r exception
### 6.3.4
   - move most print statements to logs
   - add new -v --verbose option so one can show or not the progress bars
   - introduce progress bars similar to backup
   - handle long names during zip process and email escalate
### 6.3.3
   - retry on attachment download, to deal with Smartsheet loads and timeouts.  
### 6.3.2
   - test for the existence of key totalCount when checking for attachments or rules
### 6.3.1
   - Change Attachment download from all to iterative buffer chunks of 5MB / revert
   - Accept download return code of 200-299 as successful

# SmartBackup V6.3.0  (01 August 2022)
``` Update release. ```
## Enhancements
### New Alerts - new Alert function for Archive, Backup & Export that will alert on certain conditions or critical failures. 
    - Alerts will be via email and can be sent to multiple participants separated by commas.
    - Ability to send Test Message
### New Incident Management System(IMS)interface 
    - Alerts via email can be sent to an Incident Management System so that alerts can be processed 
       by an automated system
    - Structure of message notification is keyword driven so that the automated system can easier parse the message
    - Message still human-readable
### New ability to be notified via own SMTP Server
    - Notifications can be done via the AcuWorkflow SMTP Server or an SMTP Server of your choice
    - In the case of the latter either a SSL or TLS server is supported

# SmartBackup V6.0.2  (30 April 2022)
``` Update release ```
## Bug fixes and enhancements
   - V6.0.1 Vault naming convention changed.  User unique id is now also affixed to cater for shared environments. 
   - V6.0.2 Bug Fix Sheets are not exported in deep nested folders

# SmartBackup V6.0.0  (22 March 2022)
``` Major release ```
Include beta releases 7 Feb beta 1; 16 Feb beta2; 22 Feb beta3

## Feature Enhancements

### Backup Enhancements
   - Backup runs by default in semi-silent mode with new progress bars. Added new ```-v``` or ```--verbose``` argument.  When chosen do not display progress bars in windows cmd.

### Regional and Government Support
   - Added Smartsheet [Regional](https://help.smartsheet.com/articles/2482446-introducing-smartsheet-regions?iOS=) support.  
   - Administrator can choose in which Smartsheet region **SmartBackup** should operate in. Select from **Settings**
   - Added support for US Government Customers who need to meet [government requirements](https://help.smartsheet.com/articles/2482446-introducing-smartsheet-regions?iOS=) support. 

### Member Enhancements
   - All member settings now preserved.  Therefore when one do a REFRESH from Smartsheet existing member settings in SmartBackup will be preserved
   - New Recurring Refresh.  Will Refresh every 24hours and automatically define Vaults.  Note this is different to single Refresh which do not automatically define Backup Vaults
     - Scheduling not preserved.  Recurring actions will stop on next reboot and/or stopping of Console Server
     - Will automatically define Backup Vaults and correct links for all enabled Users

### Export Enhancements
   - Added new sophisticated rate limiter for Smartsheet rate-exceeded(429) conditions.  When downloading attachments will wait for 60s if 429, then another 90s if still 429, then 120s and if still 429 will shut down.  **Note only implemented for Attachment downloads**

### Console Enhancements
    - Introduce a new **splash screen** that will be shown while the Console is loading.
    - Home Screen
     - Archive now calculates and display number of archive files and space occupied
     - Export now calculates and display number of export files and space occupied
     - Heatmap centers automatically based on current date and only display 6 month view
   - Members Screen - Enterprise Users
     - New button ```Refresh every day``` that will fetch latest list of Users from Smartsheet every 24hrs
     - In list Vault column now will turn green if Vault is correct and active and greyed out if not

## Minor enhancements, cosmetics and bug fixes

- Bug fix 701 errors in Export
- **Config** changes
  - Admin email notify off 
  - Admin email name change 
  - Archive remove if successful On
  - GOV support
- Other
  - New ICON for Uninstall 
  - Add Installation to Program Menu, set to auto which means if program not detected will prompt during installation 
  - Reframed message for status update on last backup run 
  - remove red error color status
  - Updated footer and other text and various text improvements




# SmartBackup V5.0.3  (1 December 2021)
``` Update release ```
Include beta releases Beta 1 v5.0.1 29 October 2021, Beta 2 v5.0.3 26 November 2021
## Feature Enhancements
   - Ability to backup Dashboards, Folders & Reports, therefore Sheets, Dashboards, Reports and Folders can now be backed-up.  Summary as follows:
![Image of SmartBackup Banner](https://github.com/deonpollard/SmartBackup/blob/master/images/cap.png)

> Smartsheet API does not allow Reports to be copied, therefore when wanting to backup Reports, the folder containing the Reports should be specified.  
   - Bolster backup operations by introducing **specific requests** which allows one to backup specific things.
   - Backup function can now: 
     - backup **all** sheets and dashboards
     - backup **specific** sheets, dashboards and folders (reports) 
     - backup **incremental** sheets and dashboards
     - backup allow you to optionally turn **cellLinks** on/off, this means for Sheets/Folders you can now decide to backup or not:
       - cellLinks
       - shares
       - rules 
   - Streamline Notifications and Alerts
     - Notifications allowed not a premier feature anymore, starter edition can now also enable it
     - Administrator can now be separately notified via email about completion status of jobs
     - User Notifications via email (each user is notified about status) is now be set for all operations, e.g. Backup, Archive and Exports
   - Console Enhancements
     - Added support for User to be displayed in Backup screen.  This way easier to see by User any backups taken.
     - Added support to switch/hide columns in Backup screen
     - Improved UI standard reactive layout with headline description, pop-overs, link to documentation and actions.  
     - Theme Top-bar darken blue accent with host of smaller modifications to simplify and improve 
     - Message notifications now always top right, irrespective of scroll state and will be green (success), blue (information) or red (error)
   - Improving the way the front-end UI console interact with the back-end console server
     - Will now display error message if it detects no response from Console server 

## Bugs
   - Fix number of issues most significant security context when export incremental in tenant mode

## Additional Considerations
    - Known issue slow startup.  Application may have a delay of 1-2 minutes to start up due to unpacking of files
    - Added cheat sheet in documentation


## SmartBackup V4.3.0  (7 October 2021)
``` Update release ```
1. Make Beta the production copy, general release
1. New Code signing with EV certificate for Installation

## SmartBackup V4.3.0  (22 September 2021)
``` Beta release ```
1. Export
   - Automation Rules in Sheets can now be exported.  It will reside in a Rules Packing Note within the zipped file
   - Dealing with call rate limits for attachments.  When limits are experienced it will wait 60s then 90s. 
   - Logging - now similar to Logging in Backups; use rotational logging, invoke by -l=info
   - Adding a lot more error checking
1. Console - Lot of usability enhancements
   - Path Name can be supplied with/wo trailing slash
   - Dropdown for Enabled/Disabled
   - New Actions button with mark all and save as csv options in Members
   - Order display of Backups
   - VaultSheetID added so it can be search on
1. Backup
   - Ability to add sheetid to backup name in the Vault e.g. zz2.1234567890123456.name… Name will be truncated to fit Smartsheet 50 char limit.
1. Archive
   - By changing Backup Vault Folders YY to “na” in name zz2.YYMMDD folder content will not be archived therefore zz2.na210930.. will not be archived
   - Any folder name in Vault not adhering to naming convention e.g. zz2.yymmdd will get a warning display “foreign folder name” and be ignored

## SmartBackup V4.2.0  (24 August 2021)
``` Update release```
1. Fix Vault Backup Folder - Truncate username plus datetimestamp because Sheetname length that cannot exceed 50 chars.
1. Fix Archive to translate special characters in sheet names not allowed in filesystem " \ / : | < > * ?

## SmartBackup V4.1.0  (17 July 2021)
``` Update release```
1. EE change in how we obtain the User list. Now based on the groupAdmin email… in other words when we pull the Userlist from Smartsheet we use the groupAdmin user to check for a license instead of the first user as previously the case.
1. Improve Logging in Backup.  It will rotate on 3 Backup Log files (switch automatically to the next when > 5MB)
    -	One can optionally invoke with parameter backup.exe -l=warning or –log=warning where “warning” can also be info or debug each with more information
    -	It forms a hierarchy: debug, info, warning, error, critical so when choosing  info it will also report warnings, errors or critical
    -	Note that Logging results could be unpredictable if logging turned on and Backup jobs run simultaneously
    -	Also note where previously -l= parameter pointed to a file, now not the case anymore, it will automatically create files in ..data\ and rotate them.  You now use -l= to turn it on and select a level of logging.  Hope it make sense.


## SmartBackup V4.0.0  (25 June 2021)
``` Major release```
1. Include minor fixes release v3.3.7  (11 June 2021) and v3.3.8 (17 June 2021)
1. Archive component now sysadmin enabled which means you only need sysadmin token for archiving
1. New Automation component allowing interaction with TaskScheduler
1. Improve Console Interface and error handling

## SmartBackup V3.3.6  (17 May 2021)
``` Improvement release```
1. Include stability release v3.3.5  (6 May 2021)
1. Fixes and improvements - Improved Regex checking on folder and sheet names for invalid characters when exporting
1. Improve Installation process and better error checking for api returns
1. For SysAdmin Users, only include active and add the rest with Smartsheet status

## SmartBackup V3.3.4  (2 May 2021)
``` Major functional release```

### Feature Updates
| **Component** | **Feature** | **Description** |**Notes** |
| :-: | :-- | :-- |:-: |
| **BACKUP** | SYSADMIN token capability | No more specifying for each user user api token and manually collect and define user details. In sysadmin mode only the single superuser token is required to have access to all users. To configure click on Settings and turn sysadmin in  ``On`` or ``Off`` |:new: |﻿
| **BACKUP** | Auto provision Vaults | No more asking each User to define their own backup Vault. It can centrally be provisioned or removed |:new: |﻿
| **EXPORT** | User Email| Users can now be notified after every Export | :new: |﻿
| **EXPORT** | Major Improvements | Check Sheetname/Folders for special characters. | improvement |﻿
| **CONSOLE** | Range of improvements | Cleanup of the UI, new switches and options | improvement |﻿
| Installation | Installation Process | Simplify and now only offer ```new``` or ```upgrade``` options | improvement |﻿

## SmartBackup V3.3.1  (6 April 2021)
```Include update releases V3.2.1 - V3.2.6 and Beta v3.3.0B on 22 March```

### Feature Updates
| **Component** | **Feature** | **Description** |**Notes** |
| :-: | :-- | :-- |:-: |
| **EXPORT** | SYSADMIN token capability | No more specifying for each user user api token and manually collect and define user details. In sysadmin mode only the single superuser token is required to have access to all users. To configure click on Settings, then Config and turn sysadmin in Export ``On`` or ``Off`` |:new: |﻿
| **EXPORT** | Queue parallel capability | Optional to use but when applied allow Exports to happen in paralel.  Each User or group of users can be associated with a Queue name. By using the ``-q=,<queue-name>`` a particular run will only process that queue. | :new: |﻿
| **EXPORT** | Incremental Export | Though incremental available for Backup this feature now also available for Export | :new: |﻿
| **EXPORT** | Specific request | Previously the list of specific Sheets or Reports was specified via a YML file with limitations.  Now converted to a database table with access via Console so that users can easily add specific entries. | improvement |﻿
| **CONSOLE** | Range of improvements | Cleanup of the UI with Member directory and Specific requests enhancements | improvement |﻿

#### Notes
1. Users can now export:
   - All export everything
   - Outline export only the folder structures
   - Specific export only specific sheets and reports
   - Incremental export only sheets/reports that was changed during x period
1. All of the above available through neat menu in Console or cmdline parameters

---

## SmartBackup V3.2.0 (20 February 2021)
```Latest stable release.  Include interim releases V3.1.1 of 8 Jan and V3.1.2 of 27 Jan 2021```

### Feature Updates
| **Component** | **Feature** | **Description** |**Notes** |
| :-: | :-- | :-- |:-: |
| **Backup** |Add Shares Policy | When backing up a Sheet one can set account wide policy to include/exclude Shares for the backed up sheet.  To configure click on Settings, then Config and turn Shares in Backup ``On`` or ``Off`` |:new: |﻿
| **Backup** |Add Rules Policy | When backing up a Sheet one can set account wide policy to include/exclude Rules/Rulesets for the backed up sheet.  To configure click on Settings, then Config and turn Rules in Backup ``On`` or ``Off`` | :new: |﻿
| **Administration** |More secure API's | More secure API's using OAUTH2 with authorization headers for non SmartSheet services ||﻿
| **All** |Bug fixes and improvements | Better more graceful ways to deal when some of the services are not available <br /> Improving License Administration <br /> Dealing with SMTP errors when site does not allow outbound smtp traffic||﻿
| **Installation** |Improving Installation| Refine way to do Installations, offering the following options <br /> `New Installation` (for people installing for first time or want a complete refresh) <br /> `Standard Upgrade` (for people upgrading from lower release with existing Catalog and settings are retained) <br /> `Special Upgrade`  (reserved for future use to upgrade the in-flight catalog data) | :cool:|


#### Notes
1. Existing Users are advised to choose ``Standard Upgrade Installation`` and un-select the Data checkbox to ensure existing Catalog entries are retained.  Please see :bookmark_tabs: [Installation Guide](Installation-Guide)

---

## SmartBackup V3.1.0 (29 December 2020)
```Enhancements```
1. Bug fixes
   1. Archive, correct counters when archive is set to delete
   1. Backups, Remove Ruleset and rules when creating a copy, one get a double notification, now optional parameter
   1. Exports, If no files in yml config to export it incorrectly overwrite archive status value
1. Enhancements
   1. Exports - rewrite the way the Folder tree is handled
   1. Reporting now to Admin on all License Types
   1. Improve Installation process, now default to New Installation
   1. Add ComputerName to Admin

---

## SmartBackup V3.0.0 (1 December 2020)
```Major Release ```
1. Online License checking
1. Reports Support
1. Major enhancements to export, cater for DRP
> Can now export complete user address space to local storage, maintain folder tree hierarchy

---

## SmartBackup V2.11.0 (16 September 2020)
```Usability improvements - latest stable release```
1. Improve Backup to include backup of automation rules
1. Improve License handling
1. Allow Program to be invoked automatically after successful installation
1. Improved Tenant Editing (form filed validation)

## SmartBackup V2.10.0 (1 September 2020)
> Usability and bug fixes
### Archive
1. Enhance support in config.yml
1. Email Notifications
### Backup
1. Enhance support in config.yml
1. Supertype now zz2.
### Export
1. Deal with MimeTypes for attachments

## SmartBackup V2.9.1 - V2.9.2 (31 August 2020) Internal Releases
1. Bug Fixes
1. Small enhancements

## SmartBackup V2.9.0 (26 August 2020)
```Major release ```
> New Export component
1. Enhance the Console UI

## SmartBackup V2.8.0 (8 August 2020)
> New Web Console UI using micro web framework and reactive web ui
1. Adding a Catalog to keep track of Backups/Archives
1. Integrated Heatmap showing Smartsheet last modifieds

## SmartBackup V2.6.2 - V2.7.0 (25 July 2020) Internal Releases
1. License file
1. Catalog Database
1. Test with mod dates + correlation with changes

## SmartBackup V2.6.1 (20 July 2020)
```Smartsheet cloud enabled backup ```
1. Clean up Tenants fil

## SmartBackup V2.6.1 (20 July 2020)
```Smartsheet cloud enabled backup ```
1. Clean up Tenants file
1. Minor cosmetics email notification

## SmartBackup V2.6.0 (9 July 2020)
1. Fix License for Archive
1. Backup Analyzer Chord Diagram

## SmartBackup V2.5.1 (2 July 2020)
1. Fix API Pagination with more than 100 sheets
1. Fix Backup Sheetname length, can only be 50 chars
1. Lab Heatmap 
1. Rigorous testing with User environment 600-1000+ sheets

## SmartBackup V2.5.0 (22 June 2020)
1. Base Backup routine
1. Include new License checking and email notifications
1. Include Archive as separate routine for now

## SmartBackup V2.4.1- V2.4.4 Internal Releases
### SmartBackup R2.4.4 Minor Release (20 June 2020)
  1. Bring all together, integrated testing
  1. Deal with Installer and new setup for upcoming release
  1. Deal with Figlet not shipping
### SmartBackup R2.4.3 Minor Release (17 June 2020)
  1. Status email Notification
### SmartBackup R2.4.2 Minor Release (11 June 2020)
  1. Ability to archive
### SmartBackup R2.4.1 Minor Release (8 June 2020)
  1. Remove Debugging Option
  1. Add Banner

## SmartBackup V2.4.0 (5 June 2020) Release
1. Enhancements - Track Folder not created
2. Fix Bug - Token treated as string

## SmartBackup V2.3.0 (29 May 2020)
1. Add Incremental Backups
2. Create Windows wizard like Setup install
3. Review Documentation and smarten up

## SmartBackup V2.2.0 (25 May 2020)
1. Improve Logging with message id's
2. Improve run status with Progress bars

## SmartBackup V2.1.0 (25 May 2020)
1. [GitHub Documentation](https://github.com/deonpollard/SmartBackup)

## SmartBackup V2.0.0 (23 May 2020)
1. Major enhancements
   - Concept of Folder within Vault to contain Backup set
   - Improve overall functionality - more parameters
2. Cosmetic Enhancements, program documentation

## SmartBackup V1.0.0 (2 May 2020)
1. Release candidate for SmartBackup from AcuWorkflow
2. Use Smartsheet API's with Python modules
3. Basic sheet copy functionality
4. Using TenantFile to drive backup configuration
5. Early shake-down walkthru 7 May 2020

---

# Authors

* **Deon Pollard** - *Base software* - [deon pollard & associates](https://www.deonpollard.com)

> See also list of [contributors](http://www.acuworkflow.com) who participated in this project.

# License

[![N|Solid](images/cc.png)](https://creativecommons.org/about/cclicenses/)
This project is licensed under the Creative Commons License -  [LICENSE](https://creativecommons.org/about/cclicenses/) for details 
