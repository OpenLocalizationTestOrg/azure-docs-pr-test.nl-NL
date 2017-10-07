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
# <a name="microsoft-power-bi-embedded-preview-troubleshooting"></a>Probleemoplossing voor Microsoft Power BI Embedded Preview
In dit artikel vindt u antwoorden voor het tootroubleshoot **Power BI Embedded**.

<a name="connection-string"/>

## <a name="setting-sql-server-connection-strings"></a>SQL Server-verbindingsreeksen instellen
tooset een tekenreeks van SQL Server-verbinding probeert te maken, moet u toofollow een specifieke indeling. Hieronder volgt een voorbeeld van de verbindingsreeks voor SQL Server.

```
"Persist Security Info=False;Integrated Security=true;Initial Catalog=Northwind;server=(local)"
```

toolearn meer informatie over SQL Server-verbindingsreeksen, Zie Hallo artikelen te volgen:

* [SQL Server-verbindingsreeksen](https://msdn.microsoft.com/library/jj653752.aspx)
* [SqlConnection.ConnectionString](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.connectionstring.aspx)

<a name="credentials"/>

## <a name="setting-credentials"></a>referenties instellen
In geval van Hallo waar u referenties voor een ontwikkelings- of testomgeving, zoals gebruikersnaam en wachtwoord hebt, moet u mogelijk tooupdate referenties die overeenkomen met een oplossing voor productie.

## <a name="see-also"></a>Zie ook
* [Aan de slag met het voorbeeld](power-bi-embedded-get-started-sample.md)
* [Wat is Power BI Embedded](power-bi-embedded-what-is-power-bi-embedded.md)

