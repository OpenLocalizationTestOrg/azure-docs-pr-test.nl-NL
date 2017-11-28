---
title: aaaMicrosoft Power BI Embedded Preview probleemoplossing
description: Probleemoplossing voor Microsoft Power BI Embedded Preview
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: c8aee652-ed8b-4c66-9c63-f798b7a655b4
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 01/06/2017
ms.author: asaxton
ms.openlocfilehash: a0a25cd73977c0ea0bd6b7c82e215412245771bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-power-bi-embedded-preview-troubleshooting"></a><span data-ttu-id="a57dc-103">Probleemoplossing voor Microsoft Power BI Embedded Preview</span><span class="sxs-lookup"><span data-stu-id="a57dc-103">Microsoft Power BI Embedded Preview troubleshooting</span></span>
<span data-ttu-id="a57dc-104">In dit artikel vindt u antwoorden voor het tootroubleshoot **Power BI Embedded**.</span><span class="sxs-lookup"><span data-stu-id="a57dc-104">This article provides answers for how  tootroubleshoot **Power BI Embedded**.</span></span>

<a name="connection-string"/>

## <a name="setting-sql-server-connection-strings"></a><span data-ttu-id="a57dc-105">SQL Server-verbindingsreeksen instellen</span><span class="sxs-lookup"><span data-stu-id="a57dc-105">Setting SQL Server connection strings</span></span>
<span data-ttu-id="a57dc-106">tooset een tekenreeks van SQL Server-verbinding probeert te maken, moet u toofollow een specifieke indeling.</span><span class="sxs-lookup"><span data-stu-id="a57dc-106">tooset a SQL Server connecting string, you need toofollow a specific format.</span></span> <span data-ttu-id="a57dc-107">Hieronder volgt een voorbeeld van de verbindingsreeks voor SQL Server.</span><span class="sxs-lookup"><span data-stu-id="a57dc-107">Below is an example connection string for SQL Server.</span></span>

```
"Persist Security Info=False;Integrated Security=true;Initial Catalog=Northwind;server=(local)"
```

<span data-ttu-id="a57dc-108">toolearn meer informatie over SQL Server-verbindingsreeksen, Zie Hallo artikelen te volgen:</span><span class="sxs-lookup"><span data-stu-id="a57dc-108">toolearn more about SQL Server connection strings, see hello following articles:</span></span>

* [<span data-ttu-id="a57dc-109">SQL Server-verbindingsreeksen</span><span class="sxs-lookup"><span data-stu-id="a57dc-109">SQL Server Connection Strings</span></span>](https://msdn.microsoft.com/library/jj653752.aspx)
* [<span data-ttu-id="a57dc-110">SqlConnection.ConnectionString</span><span class="sxs-lookup"><span data-stu-id="a57dc-110">SqlConnection.ConnectionString</span></span>](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.connectionstring.aspx)

<a name="credentials"/>

## <a name="setting-credentials"></a><span data-ttu-id="a57dc-111">referenties instellen</span><span class="sxs-lookup"><span data-stu-id="a57dc-111">Setting credentials</span></span>
<span data-ttu-id="a57dc-112">In geval van Hallo waar u referenties voor een ontwikkelings- of testomgeving, zoals gebruikersnaam en wachtwoord hebt, moet u mogelijk tooupdate referenties die overeenkomen met een oplossing voor productie.</span><span class="sxs-lookup"><span data-stu-id="a57dc-112">In hello case where you have credentials for a development or staging environment, such as user name and password, you might need tooupdate credentials that match a production solution.</span></span>

## <a name="see-also"></a><span data-ttu-id="a57dc-113">Zie ook</span><span class="sxs-lookup"><span data-stu-id="a57dc-113">See Also</span></span>
* [<span data-ttu-id="a57dc-114">Aan de slag met het voorbeeld</span><span class="sxs-lookup"><span data-stu-id="a57dc-114">Get started with sample</span></span>](power-bi-embedded-get-started-sample.md)
* [<span data-ttu-id="a57dc-115">Wat is Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="a57dc-115">What is Power BI Embedded</span></span>](power-bi-embedded-what-is-power-bi-embedded.md)

