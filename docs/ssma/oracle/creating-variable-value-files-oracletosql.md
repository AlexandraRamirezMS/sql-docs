---
description: "Creating Variable Value Files (OracleToSQL)"
title: "Creating Variable Value Files (OracleToSQL) | Microsoft Docs"
ms.prod: sql
ms.custom: ""
ms.date: "01/19/2017"
ms.reviewer: ""
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords: 
  - "Variable Value File Creation"
  - "Variable Value File, Variable Value File Validation"
ms.assetid: f583d81a-8e34-41b1-8100-ee3a6a82213b
author: cpichuka 
ms.author: cpichuka 
manager: alexiva
---
# Creating Variable Value Files (OracleToSQL)
Variable Value File is an XML file comprising the parameter values of commands like, the source or destination server name that frequently change from one server migration to another. When a large number of database migrations occur, multiple variable files for storing the value of each source server will be created and referenced in a master script file with the **-v** switch at command line. This helps in maintaining static values in a few script files with the variable values in multiple variable files.  
  
> [!NOTE]  
> 1.  Variable names are prefixed and suffixed with a $ (dollar) symbol. If the variables are not assigned a value in the variable value file, you will encounter an error during the parsing of the script file resulting in stalling the console execution process.  
> 2.  The escape character for **$** is **$$**. If the value of a variable or static value of a parameter contains **$** (dollar) symbol, then **$$** must be specified to treat it as a character instead of a variable.  
> 3.  For maintainability purposes, variables can be declared inside `'variable-group'` elements for logical separation of user defined variables.  Usage of this element is not mandatory.  
  
**Examples:**  
  
**Example 1:**  
  
```  
<!--Sample of variable value file commands-->  
  
<variables>  
  
  <variable-group name="ProjectSpecs">  
  
    <variable name="$project_folder$" value="<project-folder>"/>  
  
    <variable name="$project_name$" value="<project-name>"/>  
  
    <variable name="$project_overwrite$" value="<true/false>"/>  
  
    <variable name="$project_type$" value="<project-type>"/>  
  
  </variable-group>  
  
</variables>  
```  
**Example 2:**  
  
```  
<!--Sample of variable value file commands-->  
  
<variables>  
  
  <variable-group name="SQLServerParams">  
  
    <variable-group name="SqlServerConnectionParams">  
  
      <variable name="$TargetServerName$" value="<server-name>"/>  
  
      <variable name="$TargetDB$" value="<database-name>"/>  
  
      <variable name="$TargetUserName$" value="<user-name>"/>  
  
      <variable name="$TargetPassword$" value="<password>"/>  
  
      <variable name="$TrustedConnection$" value="<true/false>"/>  
  
    </variable-group>  
  
    <variable-group name="SqlServerObjectParams">  
  
      <variable name="$ObjectName1$" value="<object-name>"/>  
  
      <variable name="$ObjectName2$" value="<object-name>"/>  
  
    </variable-group>  
  
  </variable-group>  
  
</variables>  
```  
  
## Next Step  
The next step in operating the console is [Creating the Server Connection Files &#40;OracleToSQL&#41;](../../ssma/oracle/creating-the-server-connection-files-oracletosql.md)  
  
## See Also  
[Creating the Server Files (Oracle)](./creating-the-server-connection-files-oracletosql.md)  
