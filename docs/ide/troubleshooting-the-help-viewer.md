---
redirect_url: /visualstudio/ide/microsoft-help-viewer
---
title: "Troubleshooting the Help Viewer | Microsoft Docs"
ms.custom: ""
ms.date: "11/04/2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "vs-help-viewer"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "troubleshooting [Help Viewer]"
  - "Help Viewer, troubleshooting"
ms.assetid: 461a4553-064a-4142-a2d2-058658b9ba12
caps.latest.revision: 13
author: "gewarren"
ms.author: "gewarren"
manager: ghogen
---
# Troubleshooting the Help Viewer
This topic discusses issues that you might encounter with the Help Viewer.  
  
## Audio doesn't work.  
 The Help Viewer doesn't include an audio player. If you download content that contains audio and nothing happens when you choose **Play**, install an audio player.  
  
## Search doesn't work in Windows Server 2008, Windows Server 2008 with SP1, or Windows Server 2008 R2.  
 The search and filter features in the Help Viewer require the Windows Search service to be installed and on. By default, this service is off in Windows Server 2008, Windows Server 2008 with Service Pack 1 (SP1), and Windows Server 2008 R2.  
  
#### To activate Windows Search service  
  
1.  Start Server Manager.  
  
2.  In the left navigation pane, choose **Roles**.  
  
3.  In the Roles Summary pane, choose **Add Role**.  
  
4.  Choose the File Services role, and then choose the **Next** button.  
  
5.  Choose the Windows Search role service.  
  
## Additional resources  
 You can get more information and provide feedback on the Help Viewer by using the following resources:  
  
-   To provide feedback, see [Microsoft Connect](http://go.microsoft.com/fwlink/?linkid=243983) on the Microsoft website or send email to [hlpfdbk@microsoft.com](mailto:hlpfdbk@microsoft.com).  
  
-   For more information, browse the [Developer Documentation and Help System](http://go.microsoft.com/fwlink/?LinkId=232741) forum.  
  
## See also
[Help Viewer Administrator Guide](http://go.microsoft.com/fwlink/?LinkId=243985)