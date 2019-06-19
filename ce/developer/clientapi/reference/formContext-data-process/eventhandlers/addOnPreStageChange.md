---
title: "addOnPreStageChange (Client API reference) in Dynamics 365 for Customer Engagement| MicrosoftDocs"
ms.date: 06/19/2019
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 for Customer Engagement (online)
ms.assetid: d18136d2-a3cf-4440-8e6b-1703594acd79
author: msftman
ms.author: deonhe
manager: KVivek
search.audienceType: 
  - developer
search.app: 
  - D365CE
---
# addOnStageChange (Client API reference)

[!INCLUDE[](../../../../../includes/cc_applies_to_update_9_0_0.md)]

[!INCLUDE[./includes/addOnStageChange-description.md](./includes/AddOnPreStageChange-description.md)]

## Syntax

`formContext.data.process.addOnPreStageChange(myFunction);`

## Parameter

Name|Type|Required|Description|
|--|--|--|--|
|myFunction|Function reference|Yes|The function that runs **before** the business process flow stage changes. The function is added to the bottom of the event handler pipeline. The execution context is automatically passed as the first parameter to the function. See [Execution context](../../../clientapi-execution-context.md) for more information.<br/><br/>You should use a reference to a named function rather than an anonymous function if you may later want to remove the event handler.|

### Related topics

- [addOnStageChange](removeOnStageChange.md)
 
- [removeOnStageChange](removeOnStageChange.md)

- [formContext.data.process](../../formContext-data-process.md)
 


