---
title: DacFx and SqlPackage release notes
description: Release notes for Microsoft sqlpackage.
ms.custom: "tools|sos"
ms.date: 01/25/2022
ms.prod: sql
ms.reviewer: "llali"
ms.prod_service: sql-tools
ms.topic: conceptual
author: dzsquared
ms.author: drskwier
---
# Release notes for SqlPackage.exe

**[Download the latest version](sqlpackage-download.md)**

This article lists the features and fixes delivered by the released versions of SqlPackage.exe.

## 19.0 sqlpackage

|Platform|Download|Release date|Version|Build
|:---|:---|:---|:---|:---|
|Windows|[MSI Installer](https://go.microsoft.com/fwlink/?linkid=2185764)|January 25, 2022|19.0|16.0.5400.1|
|macOS .NET Core |[.zip file](https://go.microsoft.com/fwlink/?linkid=2185765)|January 25, 2022| 19.0|16.0.5400.1|
|Linux .NET Core |[.zip file](https://go.microsoft.com/fwlink/?linkid=2185670)|January 25, 2022| 19.0|16.0.5400.1|
|Windows .NET Core |[.zip file](https://go.microsoft.com/fwlink/?linkid=2185669)|January 25, 2022| 19.0|16.0.5400.1|


### Features
| Feature | Details |
| :------ | :------ |
|Always Encrypted|Adds support for in-place encryption for Always Encrypted columns. Publish can now leverage a server-side secure enclave to encrypt, decrypt, and re-encrypt database columns in-place. This avoids the expense of moving the data outside of the database. See pre-requisites for in-place encryption in [Configure column encryption in-place using Always Encrypted with secure enclaves](../../relational-databases/security/encryption/always-encrypted-enclaves-configure-encryption.md). Note: In-place encryption is supported only with the offline approach. |
|Azure Synapse Analytics|Adds support for column-level symmetric encryption.|
|Ledger|Adds supports for exporting and importing databases with ledger tables. The following limitations apply to Export: Ledger history tables and dropped ledger tables aren't migrated; the values of `GENERATED ALWAYS` columns and the data in ledger system views isn't migrated; the value of the database-level Ledger property is ignored.|
|Platform|Adds support for .NET 6 as the target framework|
|Platform|References Microsoft.Data.SqlClient (3.0) instead of System.Data.SqlClient in .NET Framework version. Upgrade Microsoft.Data.SqlClient from 2.1.3 to 3.0 for .NET Core version.|
|Platform|Upgrades .NET Framework target version to .NET 4.6.2|
|ScriptDOM|Adds support for Sql160 parser.|



### Fixes
| Feature | Details |
| :------ | :------ |
| Deployment |Fixes issue with interpretation of table distribution on column within a stored procedure. |
| Deployment |Fixes issue with "Drop objects not in source" option during publish operation. |
| Deployment |Fixes for Deploying a dacpac with temporal table having sensitivity classification.  |
| Deployment |Fixes a bug when variables are verified even when DoNotEvaluateSqlCmdVariables is set to true|
| Extract |Fix for Refactor log of referenced dacpac according to includeCompositeObjects selection. |
| Import |Fixes issue with importing database scope configurations that are not supported in target server|
| SQL Project |Fixes issue where incremental statistics caused an issue with the project build when applied to a primary key. |
| SQL Project |Fixes building a project with file tables. |


### Known Issues
| Feature | Details | Workaround |
| :------ | :------ |:------ |
| Deployment | The Azure Synapse Analytics Workload Management feature (Workload Groups and Workload Classifiers) isn't yet supported. | N/A |
| Deployment | The Azure SQL ledger table feature isn't yet supported for extract and publish. | N/A |
| ScriptDOM | Parsing a very large file can result in a stack overflow. | None |


## 18.8 sqlpackage

|Platform|Download|Release date|Version|Build
|:---|:---|:---|:---|:---|
|Windows|[MSI Installer](https://go.microsoft.com/fwlink/?linkid=2164920)|October 4, 2021|18.8|15.0.5282.3|
|macOS .NET Core |[.zip file](https://go.microsoft.com/fwlink/?linkid=2165009)|October 4, 2021| 18.8|15.0.5282.3|
|Linux .NET Core |[.zip file](https://go.microsoft.com/fwlink/?linkid=2165008)|October 4, 2021| 18.8|15.0.5282.3|
|Windows .NET Core |[.zip file](https://go.microsoft.com/fwlink/?linkid=2165007)|October 4, 2021| 18.8|15.0.5282.3|


### Features
| Feature | Details |
| :------ | :------ |
| Export | Adds option VerifyExtraction to change behavior of schema model validation on export |
| Azure SQL | Support for ledger database and tables, including import and export actions. |
| Platform | Upgrade Microsoft.Data.SqlClient from 2.0.0 to 2.1.3 for .NET Core version |
| Azure Synapse Analytics | Support for column encryption with symmetric key  |
| Azure Synapse Analytics | Support for column encryption with CREATE CERTIFICATE |
| Azure Synapse Analytics | Support for MERGE statement |
| Deployment | Variable parameterization for AE columns, new publish property IsAlwaysEncryptedParameterizationEnabled |
| Deployment | Support for IgnoreWorkloadClassifiers & IgnoreDatabaseWorkloadGroups publish properties |
| Deployment | Support for external language runtimes |
| ScriptDOM | Support for ledger database and tables |
| ScriptDOM | Support for INCLUDE columns in inline index definitions |

### Fixes
| Feature | Details |
| :------ | :------ |
| Deployment | Fixed an issue where external user deployment to Managed Instance would fail |
| Deployment | Fix for deployment order involving temporal tables to drop dependencies before turning system versioning off |
| Deployment | Fix for Always Encrypted deployment bug with error "Invalid object name '#tmpErrors'"  |
| Export | Validation for SqlPackage parameters ExcludeObjectType(s) and DoNotDropObjectType(s) |
| Export | Fixed export failure when there are change data capture (CDC) objects in database by excluding |
| Extract | Adds a retry to extract validation when first time fails due to race condition |
| Import | Fixed occasional deadlocks when importing to Azure by setting MAXDOP to 1 |
| Import | Fixed import failure when temporal table has dependency on security policy with schema binding on |
| Platform | DacFramework.msi is now signed by "Microsoft SQL Server Data-Tier Application Framework" instead of "SQL Server 2012" |
| Platform | Default to large arrays in x64 SqlPackage, fixes some scenarios involving large databases |
| Schema Compare | Fix for schema compare failing for equal databases with database scoped configurations |
| Schema Compare | Fixed schema compare with columnstore indexes |
| SQL Project | Fixed a bug with build error for "GRANT EXECUTE ANY EXTERNAL SCRIPT" |
| SQL Project | Fixed a bug where database project with columnstore index and a (n)varchar(max) column builds successfully but fails at deployment |
| SQL Project | Fixed unresolved reference warnings for table distribution columns within Stored Procedures |


### Known Issues
| Feature | Details | Workaround |
| :------ | :------ |:------ |
| Deployment | The Azure Synapse Analytics Workload Management feature (Workload Groups and Workload Classifiers) isn't yet supported | N/A |
| Deployment | The Azure SQL ledger table feature isn't yet supported | N/A |

## 18.7.1 sqlpackage

|Platform|Download|Release date|Version|Build
|:---|:---|:---|:---|:---|
|Windows|[MSI Installer](https://go.microsoft.com/fwlink/?linkid=2165211)|June 2, 2021|18.7.1|15.0.5164.1|
|macOS .NET Core |[.zip file](https://go.microsoft.com/fwlink/?linkid=2165132)|June 2, 2021| 18.7.1|15.0.5164.1|
|Linux .NET Core |[.zip file](https://go.microsoft.com/fwlink/?linkid=2165213)|June 2, 2021| 18.7.1|15.0.5164.1|
|Windows .NET Core |[.zip file](https://go.microsoft.com/fwlink/?linkid=2165212)|June 2, 2021| 18.7.1|15.0.5164.1|

### Features
| Feature | Details |
| :------ | :------ |
| Auditing | Adds support for [EXTERNAL_MONITOR](/azure/azure-sql/managed-instance/auditing-configure). |
| Azure Synapse Analytics | Adds support for [PREDICT](../../t-sql/queries/predict-transact-sql.md). |
| Logging | Adds SqlPackage version and architecture information to diagnostic log file. |

### Fixes
| Feature | Details |
| :------ | :------ | 
| Export | Fixed an issue where exporting a table with text or image in the first column would fail without a clustered index. |
| Export | Fixed an issue where exporting a table  without a clustered index that has the order of columns in a statistic in a different order than the table create script would fail. |

## 18.7 sqlpackage

|Platform|Download|Release date|Version|Build
|:---|:---|:---|:---|:---|
|Windows|[MSI Installer](https://go.microsoft.com/fwlink/?linkid=2157201)|March 10, 2021|18.7|15.0.5084.2|
|macOS .NET Core |[.zip file](https://go.microsoft.com/fwlink/?linkid=2157203)|March 10, 2021| 18.7|15.0.5084.2|
|Linux .NET Core |[.zip file](https://go.microsoft.com/fwlink/?linkid=2157202)|March 10, 2021| 18.7|15.0.5084.2|
|Windows .NET Core |[.zip file](https://go.microsoft.com/fwlink/?linkid=2157302)|March 10, 2021| 18.7|15.0.5084.2|

### Features
| Feature | Details |
| :------ | :------ |
| Deployment | Extract/Publish Big Data to/from Azure Storage. For more info, see [SqlPackage for Big Data](sqlpackage-for-azure-synapse-analytics.md) |
| Azure Synapse Analytics | Row level security support (inline table-valued function, security policy, security predicate)  |
| Azure Synapse Analytics | Workload classification support |
| Azure SQL Edge | External streaming job support |
| Azure SQL Edge | Added table and database options for data retention. |
| Import | Added 2 new index option properties for import operation. *DisableIndexesForDataPhase* (Disable indexes before importing data into SQL Server, default true) and *RebuildIndexesOfflineForDataPhase* (Rebuild indexes offline after importing data into SQL Server, default false) |
| Logging | Added property for all operations (HashObjectNamesInLogs) that will turn all object names into a hash string in log messages. |
| Performance | Improvements to import and export performance, including additional logging to assist in determining additional bottlenecks. |
| SQLCMD | Added property for Deployment and Schema Compare (DoNotEvaluateSqlCmdVariables) that specifies whether SQLCMD variables will be replaced with values. |



### Fixes
| Feature | Details |
| :------ | :------ | 
| Deployment | Default MAXDOP changed from 0 to 8 for [Azure SQL](https://techcommunity.microsoft.com/t5/azure-sql/changing-default-maxdop-in-azure-sql-database/ba-p/1538528), updating schema model default in DacFx | 
| Schema Compare | Stored procedures using OUT and OUTPUT keywords to be ignored as a difference |
| Deployment | Additional validation for Big Data tokens |
| Build/Deployment | Full schema model cleanup of temp external tables for final dacpac consistency.  |
| Build/Deployment | Adding error handling and fixing non-Edge 150 RE. |
| Import/Deployment | Sequence value restored during deployment |
| Deployment | Fixed an issue where changing the compression option on clustered index caused the table to be recreated instead of alter index. |
| Deployment | Fixed an issue where a clustered columnstore index was dropped and recreated if table column changed. |
| Deployment | Fixed external users getting dropped and recreated during deployment. |
| Schema Compare | Fixed schema compare issue with external streaming job. |
| Import | Null reference exception raised when enabling ambient setting ReliableDdlEnabled scripting a deployment report.|
| Deployment | Fixed an issue where deployment steps containing system versioning would be created in the incorrect order. |
| Deployment | Fixed an issue where schema compare update or dacpac deploy failed due to target containing temporal tables. |
| Deployment | Reseeds identity value after deployment based on target's previous last value. |

### Known Issues
| Feature | Details | Workaround |
| :------ | :------ |:------ |
| Deployment | The Azure Synapse Analytics Workload Management feature (Workload Groups and Workload Classifiers) isn't yet supported | N/A |
| Deployment | In an incremental deploy scenario, when the user is dropping a temporal table along with dropping objects that are dependent on it, like functions, stored procedures etc. the deployment can fail. The script generation order tries to turn off SYSTEM_VERSIONING on the table that is a pre-req for dropping the table, but the order of generated steps is incorrect. [Work item](https://github.com/microsoft/azuredatastudio/issues/14655) | Generate the deployment script, move the System_Versioning OFF step to just before the table being dropped and then run the script. |

## 18.6 sqlpackage

|Platform|Download|Release date|Version|Build
|:---|:---|:---|:---|:---|
|Windows|[MSI Installer](https://go.microsoft.com/fwlink/?linkid=2143544)|September 18, 2020|18.6|15.0.4897.1|
|macOS .NET Core |[.zip file](https://go.microsoft.com/fwlink/?linkid=2143659)|September 18, 2020| 18.6|15.0.4897.1|
|Linux .NET Core |[.zip file](https://go.microsoft.com/fwlink/?linkid=2143497)|September 18, 2020| 18.6|15.0.4897.1|
|Windows .NET Core |[.zip file](https://go.microsoft.com/fwlink/?linkid=2143496)|September 18, 2020| 18.6|15.0.4897.1|

### Features
| Feature | Details |
| :------ | :------ |
| Platform | Updated sqlpackage for .NET Core version to .NET Core 3.1 |
| Always Encrypted | Added support for secure enclave import and export for SQL Server 2019 |
| Deployment | Added support to ignore change data capture enabled tables when exporting from Azure SQL Database |
| Deployment | Added support for index option OPTIMIZE_FOR_SEQUENTIAL_KEY in Azure SQL Database |
| Deployment | Added support for identity columns for Azure Synapse Analytics | 
| Help | Output the sqlpackage version in the help (/?) and support the /version parameter | 

### Fixes
| Feature | Details |
| :------ | :------ | 
| Deployment | Fixed an incorrect deployment script generated when targeting Azure SQL Managed Instance as a non-sysadmin user  | 
| Deployment | Fixed loading deployment contributors when running script actions | 
| Help | Output correct elapsed time in sqlpackage when operation take longer than 1 day | 
| Deployment | Fixed dacpac registration when deploying for .NET Core | 
| Deployment | Fixed sqlpackage on .NET Core handling of the /accessToken (/at) parameter | 
| Deployment | Allow ALTER TABLE statements in stored procedures as non-top level statements | 
| Deployment | Fixed Azure Synapse Analytics validation of materialized views to be case insensitive | 

### Known Issues
| Feature | Details |
| :------ | :------ |
| Deployment | The Azure Synapse Analytics Workload Management feature (Workload Groups and Workload Classifiers) isn't yet supported | 

## 18.5.1 sqlpackage

|Platform|Download|Release date|Version|Build
|:---|:---|:---|:---|:---|
|Windows|[MSI Installer](https://go.microsoft.com/fwlink/?linkid=2134206)|June 24, 2020|18.5.1|15.0.4826.1|
|macOS .NET Core |[.zip file](https://go.microsoft.com/fwlink/?linkid=2134312)|June 24, 2020| 18.5.1|15.0.4826.1|
|Linux .NET Core |[.zip file](https://go.microsoft.com/fwlink/?linkid=2134311)|June 24, 2020| 18.5.1|15.0.4826.1|
|Windows .NET Core |[.zip file](https://go.microsoft.com/fwlink/?linkid=2134310)|June 24, 2020| 18.5.1|15.0.4826.1|

### Fixes
| Feature | Details |
| :------ | :------ |
| Deployment | Fixed a regression that was introduced in 18.5 causing there to be an "Incorrect syntax near 'type'" error when deploying a dacpac or importing a bacpac with a user with external login to on premise | 

## 18.5 sqlpackage

|Platform|Download|Release date|Version|Build
|:---|:---|:---|:---|:---|
|Windows|[MSI Installer](https://go.microsoft.com/fwlink/?linkid=2128142)|April 28, 2020|18.5|15.0.4769.1|
|macOS .NET Core |[.zip file](https://go.microsoft.com/fwlink/?linkid=2128145)|April 28, 2020| 18.5|15.0.4769.1|
|Linux .NET Core |[.zip file](https://go.microsoft.com/fwlink/?linkid=2128144)|April 28, 2020| 18.5|15.0.4769.1|
|Windows .NET Core |[.zip file](https://go.microsoft.com/fwlink/?linkid=2128143)|April 28, 2020| 18.5|15.0.4769.1|

### Features
| Feature | Details |
| :------ | :------ |
| Deployment | Data Sensitivity classification now supported for SQL Server 2008 and up, Azure SQL Database, and Azure Synapse Analytics |
| Deployment | Add Azure Synapse Analytics support for table constraints |
| Deployment | Add Azure Synapse Analytics support for ordered clustered column store index |
| Deployment | Add support for External Data Source (Oracle, Teradata, MongoDB/CosmosDB, ODBC, Big Data Cluster) and External Table for SQL Server 2019 Big Data Cluster |
| Deployment | Add SQL Database Edge Instance as supported edition |
| Deployment | Support Managed Instance server names of the form '\<server>.\<dnszone>.database.windows.net' |
| Deployment | Add support for copy command in Azure Synapse Analytics |
| Deployment | Add deployment option 'IgnoreTablePartitionOptions' during Publish to avoid table recreation when there is change in partition function on table for Azure Synapse Analytics |
| .NET Core | Add support for Microsoft.Data.SqlClient in .NET Core version of sqlpackage |
| &nbsp; | &nbsp; |

### Fixes
| Fix | Details |
| :-- | :------ |
| Deployment | Fix parsing json path as expression |
| Deployment | Fix generating GRANT statements for AlterAnyDatabaseScopedConfiguration and AlterAnySensitivityClassification permissions |
| Deployment | Fix External Script permission not being recognized |
| Deployment | Fix for inline property - the implicit addition of the property should not show in difference but explicit mention should show through script |
| Deployment | Resolved an issue where changing a Table referenced by a Materialized View (MV) causes Alter View statements to be generated. Alter View statements are not supported for MVs for Azure Synapse Analytics. |
| Deployment | Fix publish failing when adding column to a table with data for Azure Synapse Analytics |
| Deployment | Fix update script should move data to a new table when changing the distribution column type (data loss scenario) for Azure Synapse Analytics |
| ScriptDom | Fix ScriptDom bug where it couldn't recognize inline constraints defined after an inline index |
| ScriptDom | Fix ScriptDom SYSTEM_TIME missing closing parenthesis when in a batch statement |
| Always Encrypted | Fix #tmpErrors table failing to drop if sqlpackage reconnects and the temp table is already gone because the temporary table goes away when the connection dies |
| &nbsp; | &nbsp; |

### Known Issues
| Feature | Details |
| :------ | :------ |
| Deployment |  A regression was introduced in 18.5 causing there to be an "Incorrect syntax near 'type'" error when deploying a dacpac or importing a bacpac with a user with external login to on premise. Workaround is to use sqlpackage 18.4 and it will be fixed in the next sqlpackage release. | 
| .NET Core | Importing bacpacs with sensitivity classification fails with "Internal connection fatal error" because of this [known issue](https://github.com/dotnet/SqlClient/issues/559) in Microsoft.Data.SqlClient. This will be fixed in the next sqlpackage release. |
| &nbsp; | &nbsp; |

## 18.4.1 sqlpackage

|Platform|Download|Release date|Version|Build
|:---|:---|:---|:---|:---|
|Windows|[MSI Installer](https://go.microsoft.com/fwlink/?linkid=2113703)|December 13, 2019|18.4.1|15.0.4630.1|
|macOS .NET Core |[.zip file](https://go.microsoft.com/fwlink/?linkid=2113705)|December 13, 2019| 18.4.1|15.0.4630.1|
|Linux .NET Core |[.zip file](https://go.microsoft.com/fwlink/?linkid=2113331)|December 13, 2019| 18.4.1|15.0.4630.1|
|Windows .NET Core |[.zip file](https://go.microsoft.com/fwlink/?linkid=2113704)|December 13, 2019| 18.4.1|15.0.4630.1|

### Fixes
| Fix | Details |
| :-- | :------ |
| ScriptDom |  A ScriptDom parsing regression was introduced in 18.3.1 where 'RENAME' is incorrectly treated as a top-level token, cause parsing to fail.
| &nbsp; | &nbsp; |

### Known Issues 

| Feature | Details |
| :------ | :------ |
| Deployment |  A regression was introduced in 18.4.1 causing there to be an "Object reference not set to an instance of an object." error when deploying a dacpac or importing a bacpac with a user with external login. Workaround is to use sqlpackage 18.4 and it will be fixed in the next sqlpackage release. | 
| &nbsp; | &nbsp; |

## 18.4 sqlpackage

|Platform|Download|Release date|Version|Build
|:---|:---|:---|:---|:---|
|Windows|[MSI Installer](https://go.microsoft.com/fwlink/?linkid=2108813)|October 29, 2019|18.4|15.0.4573.2|
|macOS .NET Core |[.zip file](https://go.microsoft.com/fwlink/?linkid=2108815)|October 29, 2019| 18.4|15.0.4573.2|
|Linux .NET Core |[.zip file](https://go.microsoft.com/fwlink/?linkid=2108814)|October 29, 2019| 18.4|15.0.4573.2|
|Windows .NET Core |[.zip file](https://go.microsoft.com/fwlink/?linkid=2109019)|October 29, 2019| 18.4|15.0.4573.2|

### Features

| Feature | Details |
| :------ | :------ |
| Deployment | Add support to deploy to Azure Synapse Analytics. | 
| Platform | sqlpackage .NET Core generally available for macOS, Linux, and Windows. | 
| Security | Remove SHA1 code signing. |
| Deployment | Add support for new Azure database editions: GeneralPurpose, BusinessCritical, Hyperscale |
| Deployment | Add Managed Instance support for Azure Active Directory user and groups. |
| Deployment | Support the /AccessToken parameter for sqlpackage on .NET Core. |
| &nbsp; | &nbsp; |

### Known Issues 

| Feature | Details |
| :------ | :------ |
| ScriptDom |  A ScriptDom parsing regression was introduced in 18.3.1 where 'RENAME' is incorrectly treated as a top-level token, cause parsing to fail. This will be fixed in the next sqlpackage release. | 
| &nbsp; | &nbsp; |

### Known Issues for .NET Core

| Feature | Details |
| :------ | :------ |
| Import |  For .bacpac files with compressed files over 4GB in size, you might need to use the .NET Core version of sqlpackage to perform the import.  This behavior is due to how .NET Core generates zip headers, which although valid, are not readable by the .NET Full Framework version of sqlpackage. | 
| Deployment | The parameter /p:Storage=File isn't supported. Only Memory is supported on .NET Core. | 
| Always Encrypted | sqlpackage .NET Core doesn't support Always Encrypted columns. | 
| Security | sqlpackage .NET Core doesn't support the /ua parameter for multi-factor authentication. | 
| Deployment | Older V2 dacpac and bacpac files that use json data serialization aren't supported. |
| &nbsp; | &nbsp; |

## 18.3.1 sqlpackage

|Platform|Download|Release date|Version|Build
|:---|:---|:---|:---|:---|
|Windows|[MSI Installer](https://go.microsoft.com/fwlink/?linkid=2102893)|September 13, 2019|18.3.1|15.0.4538.1|
|macOS .NET Core (preview)|[.zip file](https://go.microsoft.com/fwlink/?linkid=2102894)|September 13, 2019| 18.3.1|15.0.4538.1|
|Linux .NET Core (preview)|[.zip file](https://go.microsoft.com/fwlink/?linkid=2102978)|September 13, 2019| 18.3.1|15.0.4538.1|
|Windows .NET Core (preview)|[.zip file](https://go.microsoft.com/fwlink/?linkid=2102979)|September 13, 2019| 18.13.1|15.0.4538.1|

### Features

| Feature | Details |
| :------ | :------ |
| Deployment | Add support to deploy to Azure Synapse Analytics (preview). | 
| Deployment | Add /p:DatabaseLockTimeout=(INT32 '60') parameter to sqlpackage. | 
| Deployment | Add /p:LongRunningCommandTimeout=(INT32) parameter to sqlpackage. |
| Export/Extract | Add /p:TempDirectoryForTableData=(STRING) parameter to sqlpackage. |
| Deployment | Allow deployment contributors to be loaded from additional locations. Deployment contributors will be loaded from the same directory as the target .dacpac being deployed, the Extensions directory relative to the sqlpackage.exe binary, and the /p:AdditionalDeploymentContributorPaths=(STRING) parameter added to sqlpackage where additional directory locations can be specified. |
| Deployment | Add support for OPTIMIZE_FOR_SEQUENTIAL_KEY. |
| &nbsp; | &nbsp; |

### Fixes

| Fix | Details |
| :-- | :------ |
| Deployment | Fix to ignore automatic indexes so that they are not dropped on deployment. | 
| Always Encrypted | Fix for handling Always Encrypted varchar columns. | 
| Build/Deployment | Fix to resolve the nodes() method for xml column sets.| 
| ScriptDom | Fix additional cases where the 'URL' string was interpreted as a top level token. | 
| Graph | Fix generated SQL for pseudo column references in constraints.  | 
| Export | Generate random passwords that meet complexity requirements. | 
| Deployment | Fix to honor command timeouts when retrieving constraints. | 
| .NET Core (preview) | Fix diagnostic logging to a file. | 
| .NET Core (preview) | Use streaming to export table data to support large tables. | 
| &nbsp; | &nbsp; |

## 18.2 sqlpackage

|Platform|Download|Release date|Version|Build
|:---|:---|:---|:---|:---|
|Windows|[MSI Installer](https://go.microsoft.com/fwlink/?linkid=2087429)|April 15, 2019|18.2|15.0.4384.2|
|macOS .NET Core (preview)|[.zip file](https://go.microsoft.com/fwlink/?linkid=2087247)|April 15, 2019 | 18.2 |15.0.4384.2|
|Linux .NET Core (preview)|[.zip file](https://go.microsoft.com/fwlink/?linkid=2087431)|April 15, 2019 | 18.2 |15.0.4384.2|

### Features

| Feature | Details |
| :------ | :------ |
| Graph | Add graph table support for edge constraints and edge constraint clauses. |
| Deployment | Enabled model validation rule to support 32 columns for index keys for SQL Server 2016 and up. |
| &nbsp; | &nbsp; |

### Fixes

| Fix | Details |
| :-- | :------ |
| Deployment | Fix reverse engineering a SQL Server 2016 RTM database due to an unsupported query hint being used. |
| Deployment | Fix deployment ordering of auto close alter statements to occur before create filegroup statements. |
| ScriptDom | Fix ScriptDom parsing regression where the 'URL' string was interpreted as a top level token. |
| Deployment | Fix a null reference exception when parsing an alter table add index statement. | 
| Schema Compare | Fixed schema compare for nullable persisted computed columns always showing as different.|
| &nbsp; | &nbsp; |

## 18.1 sqlpackage

Release date: &nbsp; February 1, 2019  
Build: &nbsp; 15.0.4316.1  
Preview release.

### Features

| Feature | Details |
| :------ | :------ |
| Deployment | Added support for UTF8 collations. |
| Deployment | Enabled nonclustered columnstore indexes on an indexed view. |
| Platform | Moved to .NET Core 2.2. | 
| Schema Compare | Use memory backed storage for schema compare on .NET Core. |
| &nbsp; | &nbsp; |

### Fixes

| Fix | Details |
| :-- | :------ |
| Performance | Performance fix to use the legacy cardinality estimator for reverse engineering queries. | 
| Performance | Fixed a significant schema compare performance issue when generating a script. | 
| Schema Compare | Fixed the schema drift detection logic to ignore certain extended event (xevent) sessions. |
| Graph | Fixed import ordering for graph tables. | 
| Export | Fixed exporting external tables with object permissions. |
| &nbsp; | &nbsp; |

### Known issues

This release includes cross-platform preview builds of sqlpackage that target .NET Core 2.2. The sqlpackage can run on macOS and Linux.

| Known issue | Details |
| :---------- | :------ |
| Deployment | For .NET Core, build and deployment contributors aren't supported. | 
| Deployment | For .NET Core, older dacpac and bacpac files that use json data serialization aren't supported. | 
| Deployment | For .NET Core referenced dacpacs (for example master.dacpac) may not resolve due to issues with case-sensitive file systems. A workaround is to capitalize the name of the reference file (for example MASTER.BACPAC). |
| &nbsp; | &nbsp; |

## 18.0 sqlpackage

Release date: &nbsp; October 24, 2018  
Build: &nbsp; 15.0.4200.1

### Features

| Feature | Details |
| :------ | :------ |
| Deployment | Added support for database compatibility level 150. | 
| Deployment | Added support for Managed Instances. | 
| Performance | Added MaxParallelism command-line parameter to specify the degree of parallelism for database operations. | 
| Security | Added AccessToken command-line parameter to specify an authentication token when connecting to SQL Server. | 
| Import | Added support to stream BLOB/CLOB data types for imports. | 
| Deployment | Added support for scalar UDF 'INLINE' option. | 
| Graph | Added support for graph table 'MERGE' syntax. |
| &nbsp; | &nbsp; |

### Fixes

| Fix | Details |
| :-- | :------ |
| Graph | Fixed unresolved pseudo-column for graph tables. |
| Deployment | Fixed creating a database with memory optimized file groups when memory optimized tables are used. |
| Deployment | Fixed including extended properties on external tables. |
| &nbsp; | &nbsp; |

## 17.8 sqlpackage

Release date: &nbsp; June 22, 2018  
Build: &nbsp; 14.0.4079.2

### Features

| Feature | Details |
| :------ | :------ |
| Diagnostics | Improved error messages for connection failures, including the SqlClient exception message. |
| Deployment | Support index compression on single partition indexes for import/export. |
| &nbsp; | &nbsp; |

### Fixes

| Fix | Details |
| :-- | :------ |
| Deployment | Fixed a reverse engineering issue for XML column sets with SQL 2017 and later. | 
| Deployment | Fixed an issue where scripting the database compatibility level 140 was ignored for Azure SQL Database. |
| &nbsp; | &nbsp; |

## 17.4.1 sqlpackage

Release date: &nbsp; January 25, 2018  
Build: &nbsp; 14.0.3917.1

### Features

| Feature | Details |
| :------ | :------ |
| Import/Export | Added ThreadMaxStackSize command-line parameter to parse Transact-SQL with a large number of nested statements. |
| Deployment | Database catalog collation support. | 
| &nbsp; | &nbsp; |

### Fixes

| Fix | Details |
| :-- | :------ |
| Import | When importing an Azure SQL Database bacpac to an on-premises instance, fixed errors due to _Database master keys without password are not supported in this version of SQL Server_. |
| Graph | Fixed an unresolved pseudo column error for graph tables. |
| Schema Compare | Fixed SQL authentication to compare schemas. | 
| &nbsp; | &nbsp; |

## 17.4.0 sqlpackage

Release date: &nbsp; December 12, 2017  
Build: &nbsp; 14.0.3881.1

### Features

| Feature | Details |
| :------ | :------ |
| Deployment |  Added support for _temporal retention policy_ on SQL 2017+ and Azure SQL Database. | 
| Diagnostics | Added /DiagnosticsFile:"C:\Temp\sqlpackage.log" command-line parameter to specify a file path to save diagnostic information. | 
| Diagnostics | Added /Diagnostics command-line parameter to log diagnostic information to the console. |
| &nbsp; | &nbsp; |

### Fixes

| Fix | Details |
| :-- | :------ |
| Deployment | Do not block when encountering a database compatibility level that isn't understood. Instead, the latest Azure SQL Database or on-premises platform will be assumed. |
| &nbsp; | &nbsp; |