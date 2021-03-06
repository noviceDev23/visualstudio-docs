---
title: "How to: Suppress Code Analysis Warnings for Generated Code | Microsoft Docs"
ms.custom: ""
ms.date: "11/04/2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "vs-ide-code-analysis"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 3a96434e-d419-43a7-81ba-95cccac835b8
caps.latest.revision: 5
author: "gewarren"
ms.author: "gewarren"
manager: ghogen
ms.workload: 
  - "multiple"
---
# How to: Suppress Code Analysis Warnings for Generated Code
Managed code compilers often generate code that is added to a project to facilitate rapid code development. In addition, developers often use third-party tools to help develop applications quickly. These tools also generate code that is added to the project.  
  
 You might want to see the rule violations that Code Analysis discovers in generated code. However, you might not want to see them if you cannot view and maintain the code that contains the violation.  
  
 The **Suppress results from generated code** check box on the Code Analysis property page of a project enables you to select whether you want to see Code Analysis warnings from code generated by a third-party tool.  
  
> [!NOTE]
>  This option does not suppress Code Analysis errors and warnings from generated code when the errors and warnings appear in forms and templates. You can both view and maintain the source code for a form or a template.  
  
### To suppress warnings for generated code in a project  
  
1.  Right-click the project in Solution Explorer, and then click **Properties**.  
  
2.  Click **Code Analysis**.  
  
3.  Select the **Suppress results from generated code** check box.