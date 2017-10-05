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
# <a name="microsoft-power-bi-embedded-preview-troubleshooting"></a>Probleemoplossing voor Microsoft Power BI Embedded Preview
In dit artikel vindt u antwoorden voor het oplossen van **Power BI Embedded**.

<a name="connection-string"/>

## <a name="setting-sql-server-connection-strings"></a>SQL Server-verbindingsreeksen instellen
Om in te stellen van een SQL-Server verbinding maken met de tekenreeks, moet u een specifieke indeling volgen. Hieronder volgt een voorbeeld van de verbindingsreeks voor SQL Server.

```
"Persist Security Info=False;Integrated Security=true;Initial Catalog=Northwind;server=(local)"
```

Zie voor meer informatie over SQL Server-verbindingsreeksen, de volgende artikelen:

* [SQL Server-verbindingsreeksen](https://msdn.microsoft.com/library/jj653752.aspx)
* [SqlConnection.ConnectionString](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.connectionstring.aspx)

<a name="credentials"/>

## <a name="setting-credentials"></a>referenties instellen
In het geval waar u de referenties voor een ontwikkelings- of testomgeving, zoals gebruikersnaam en wachtwoord hebt, moet u wellicht de referenties die overeenkomen met een productie-oplossing bijwerken.

## <a name="see-also"></a>Zie ook
* [Aan de slag met het voorbeeld](power-bi-embedded-get-started-sample.md)
* [Wat is Power BI Embedded](power-bi-embedded-what-is-power-bi-embedded.md)

