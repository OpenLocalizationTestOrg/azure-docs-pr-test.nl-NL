---
title: Probleemoplossing voor Microsoft Power BI Embedded Preview
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
ms.openlocfilehash: f406d23e578acc825514aa5bd9eabcbf160bf9ec
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="microsoft-power-bi-embedded-preview-troubleshooting"></a><span data-ttu-id="c7372-103">Probleemoplossing voor Microsoft Power BI Embedded Preview</span><span class="sxs-lookup"><span data-stu-id="c7372-103">Microsoft Power BI Embedded Preview troubleshooting</span></span>
<span data-ttu-id="c7372-104">In dit artikel vindt u antwoorden voor het oplossen van **Power BI Embedded**.</span><span class="sxs-lookup"><span data-stu-id="c7372-104">This article provides answers for how  to troubleshoot **Power BI Embedded**.</span></span>

<a name="connection-string"/>

## <a name="setting-sql-server-connection-strings"></a><span data-ttu-id="c7372-105">SQL Server-verbindingsreeksen instellen</span><span class="sxs-lookup"><span data-stu-id="c7372-105">Setting SQL Server connection strings</span></span>
<span data-ttu-id="c7372-106">Om in te stellen van een SQL-Server verbinding maken met de tekenreeks, moet u een specifieke indeling volgen.</span><span class="sxs-lookup"><span data-stu-id="c7372-106">To set a SQL Server connecting string, you need to follow a specific format.</span></span> <span data-ttu-id="c7372-107">Hieronder volgt een voorbeeld van de verbindingsreeks voor SQL Server.</span><span class="sxs-lookup"><span data-stu-id="c7372-107">Below is an example connection string for SQL Server.</span></span>

```
"Persist Security Info=False;Integrated Security=true;Initial Catalog=Northwind;server=(local)"
```

<span data-ttu-id="c7372-108">Zie voor meer informatie over SQL Server-verbindingsreeksen, de volgende artikelen:</span><span class="sxs-lookup"><span data-stu-id="c7372-108">To learn more about SQL Server connection strings, see the following articles:</span></span>

* [<span data-ttu-id="c7372-109">SQL Server-verbindingsreeksen</span><span class="sxs-lookup"><span data-stu-id="c7372-109">SQL Server Connection Strings</span></span>](https://msdn.microsoft.com/library/jj653752.aspx)
* [<span data-ttu-id="c7372-110">SqlConnection.ConnectionString</span><span class="sxs-lookup"><span data-stu-id="c7372-110">SqlConnection.ConnectionString</span></span>](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.connectionstring.aspx)

<a name="credentials"/>

## <a name="setting-credentials"></a><span data-ttu-id="c7372-111">referenties instellen</span><span class="sxs-lookup"><span data-stu-id="c7372-111">Setting credentials</span></span>
<span data-ttu-id="c7372-112">In het geval waar u de referenties voor een ontwikkelings- of testomgeving, zoals gebruikersnaam en wachtwoord hebt, moet u wellicht de referenties die overeenkomen met een productie-oplossing bijwerken.</span><span class="sxs-lookup"><span data-stu-id="c7372-112">In the case where you have credentials for a development or staging environment, such as user name and password, you might need to update credentials that match a production solution.</span></span>

## <a name="see-also"></a><span data-ttu-id="c7372-113">Zie ook</span><span class="sxs-lookup"><span data-stu-id="c7372-113">See Also</span></span>
* [<span data-ttu-id="c7372-114">Aan de slag met het voorbeeld</span><span class="sxs-lookup"><span data-stu-id="c7372-114">Get started with sample</span></span>](power-bi-embedded-get-started-sample.md)
* [<span data-ttu-id="c7372-115">Wat is Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="c7372-115">What is Power BI Embedded</span></span>](power-bi-embedded-what-is-power-bi-embedded.md)

