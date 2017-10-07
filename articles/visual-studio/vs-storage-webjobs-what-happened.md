---
title: aaaWhat is er gebeurd toomy webtaak project (Visual Studio Azure Storage verbonden service)? | Microsoft Docs
description: Hierin wordt beschreven wat er gebeurd is in een project Azure webtaak nadat tooa storage-account met Visual Studio verbinding services verbonden
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: 36ae7ff7-c22c-47eb-b220-049d61618c74
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-what-happened
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: kraigb
ms.openlocfilehash: ed0ce75f5b23eca3c41dacb48564d6e5b846f395
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="what-happened-toomy-webjob-project-visual-studio-azure-storage-connected-service"></a>Wat is er gebeurd toomy webtaak-project (Visual Studio Azure Storage verbonden service)?
## <a name="references-added"></a>Verwijzingen die zijn toegevoegd
Hello Azure Storage NuGet-pakket is bijgewerkt in Visual Studio-project tooor toegevoegd.  
Dit pakket wordt toegevoegd Hallo .NET verwijzingen te volgen:

* **Microsoft.Data.Edm**
* **Microsoft.Data.OData**
* **Microsoft.Data.Services.Client**
* **Microsoft.WindowsAzure.ConfigurationManager**
* **Microsoft.WindowsAzure.Storage**
* **Newtonsoft.Json**
* **Systeem.gegevens**
* **System.Spatial**

## <a name="connection-string-for-azure-storage-added"></a>Verbindingsreeks voor Azure Storage toegevoegd
Hallo in Hallo App.config-bestand van uw project, **AzureWebJobsStorage** en **AzureWebJobsDashboard** -items zijn bijgewerkt met de verbindingsreeks en de sleutel Hallo geselecteerd van het opslagaccount.

Zie voor meer informatie [documentatiebronnen Azure WebJobs](http://go.microsoft.com/fwlink/?linkid=390226).

