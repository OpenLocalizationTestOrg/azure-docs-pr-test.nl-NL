---
title: Transparent Data Encryption voor Stretch Database - Azure aaaEnable | Microsoft Docs
description: Transparante gegevensversleuteling (TDE) voor SQL Server Stretch Database in Azure inschakelen
services: sql-server-stretch-database
documentationcenter: 
author: douglaslMS
manager: barbkess
editor: 
ms.assetid: a44ed8f5-b416-4c41-9b1e-b7271f10bdc3
ms.service: sql-server-stretch-database
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2016
ms.author: douglasl
ms.openlocfilehash: 1d6bff455030ac8851b2184c1e8097afd61361d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-transparent-data-encryption-tde-for-stretch-database-on-azure"></a>Transparante gegevensversleuteling (TDE) inschakelen voor Stretch Database in Azure
> [!div class="op_single_selector"]
> * [Azure Portal](sql-server-stretch-database-encryption-tde.md)
> * [TSQL](sql-server-stretch-database-tde-tsql.md)
>
>

Transparent Data Encryption (TDE) beschermt tegen Hallo dreiging van schadelijke activiteiten door het uitvoeren van realtime versleuteling en ontsleuteling van Hallo-database, gekoppelde back-ups en transactielogboekbestanden in rust zonder wijzigingen toohello de toepassing.

TDE versleutelt Hallo opslag van een volledige database met behulp van een symmetrische sleutel opgeroepen Hallo databaseversleutelingssleutel. Hallo databaseversleutelingssleutel is beveiligd met een ingebouwde servercertificaat. ingebouwde Hallo-servercertificaat is uniek voor elke Azure-server. Microsoft draait automatisch deze certificaten ten minste om de 90 dagen. Zie voor een algemene beschrijving van TDE [Transparent Data Encryption (TDE)].

## <a name="enabling-encryption"></a>Codering inschakelen
tooenable TDE voor een Azure-database die wordt opgeslagen Hallo gegevens gemigreerd uit een database van SQL Server Stretch is ingeschakeld, Hallo dingen te volgen:

1. Open Hallo-database in Hallo [Azure-portal](https://portal.azure.com)
2. Klik op Hallo databaseblade Hallo **instellingen** knop
3. Selecteer Hallo **transparante gegevensversleuteling** optie![][1]
4. Selecteer Hallo **op** instelling en selecteer vervolgens **opslaan**
   ![][2]

## <a name="disabling-encryption"></a>Codering uitschakelen
toodisable TDE voor een Azure-database die wordt opgeslagen Hallo gegevens gemigreerd uit een database van SQL Server Stretch is ingeschakeld, Hallo dingen te volgen:

1. Open Hallo-database in Hallo [Azure-portal](https://portal.azure.com)
2. Klik op Hallo databaseblade Hallo **instellingen** knop
3. Selecteer Hallo **transparante gegevensversleuteling** optie
4. Selecteer Hallo **uit** instelling en selecteer vervolgens **opslaan**

<!--Anchors-->
[Transparent Data Encryption (TDE)]: https://msdn.microsoft.com/library/bb934049.aspx


<!--Image references-->
[1]: ./media/sql-server-stretch-database-encryption-tde/stretchtde1.png
[2]: ./media/sql-server-stretch-database-encryption-tde/stretchtde2.png


<!--Link references-->
