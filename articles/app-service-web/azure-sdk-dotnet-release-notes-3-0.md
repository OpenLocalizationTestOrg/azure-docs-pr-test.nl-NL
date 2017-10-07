---
title: aaaAzure SDK voor .NET 3.0 Release-opmerkingen | Microsoft Docs
description: Azure SDK voor .NET 3.0 Release-opmerkingen
services: app-service\web
documentationcenter: .net
author: chrissfanos
editor: 
ms.assetid: c83d815b-fc19-4260-821e-7d2a7206dffc
ms.service: app-service
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 03/07/2017
ms.author: juliako
ms.openlocfilehash: 8970b4c9b64de40dc29a33d69006a00ae5e38a50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sdk-for-net-30-release-notes"></a>Azure SDK voor .NET 3.0 release-opmerkingen

Dit onderwerp bevat de releaseopmerkingen voor versie 3.0 van hello Azure SDK voor .NET.

##<a name="azure-sdk-for-net-30-release-summary"></a>Azure SDK voor .NET 3.0 release samenvatting

Releasedatum: 07-03/2017
 
Er zijn geen recente wijzigingen toohello Azure SDK 3.0 zijn geïntroduceerd in deze release. Er is ook geen tooleverage upgradeproces nodig deze SDK met bestaande Cloud Service-projecten. tooallow gebruik van Azure SDK 3.0 Hallo zonder een upgradeproces Azure SDK 3.0 installeert toohello dezelfde directory als de Azure SDK 2.9. De meeste Hallo-onderdelen is niet veranderd met Hallo hoofdversie van 2.9 maar Hallo build-nummer in plaats daarvan zojuist hebt bijgewerkt.

## <a name="visual-studio-2017-rtw"></a>Visual Studio 2017 RTW

- In Visual Studio-2017 is deze release van hello Azure SDK voor .NET ingebouwd in toohello Azure werkbelasting. Alle Hallo-hulpprogramma's, moet u toodo ontwikkelen van Azure zal onderdeel zijn van Visual Studio 2017 voortaan. Voor Visual Studio 2015 steeds Hallo SDK nog beschikbaar is via WebPI. We hebben Azure SDK voor .NET-versies voor Visual Studio 2013 stopgezet nu dat Visual Studio 2017 is vrijgegeven.

### <a name="azure-diagnostics"></a>Azure Diagnostics

- Een gedeeltelijke verbindingsreeks gewijzigde Hallo gedrag tooonly opslaan met Hallo sleutel vervangen door een token voor de verbindingsreeks voor opslag van Cloud Services-diagnostische gegevens. de werkelijke opslagsleutel Hallo worden nu opgeslagen in de map gebruikersprofiel Hallo zodat de toegang kan worden beheerd. Visual Studio wordt Hallo-opslagsleutel lezen uit de map voor lokale foutopsporing en publicatieproces gebruikersprofiel. 
- In het antwoord toohello wijziging die hierboven worden beschreven, team Visual Studio Online verbeterde hello Azure Cloud Services-implementatiesjabloon taak zodat gebruikers Hallo-opslagsleutel voor het instellen van de extensie voor diagnostische gegevens bij het publiceren van tooAzure in continue integratie kunnen opgeven en implementatie.
- We hebben het mogelijke toostore beveiligde verbindingsreeks en tokeniseren voor Azure Diagnostics (af), het oplossen van problemen met configuratie over environements toohelp aangebracht.
 
### <a name="windows-server-2016-virtual-machines"></a>Windows Server 2016 virtuele machines

- Visual Studio ondersteunt nu implementeren Cloudservices tooOS familie 5 (Windows Server 2016) virtuele machines. Voor bestaande cloudservices, kunt u uw instellingen tootarget Hallo van nieuwe OS-familie. Bij het maken van nieuwe cloudservices als u ervoor kiest toocreate Hallo service met .net 4.6 of hoger, wordt standaard Hallo service toouse OS-familie 5.  Voor meer informatie kunt u bekijken Hallo [Gastbesturingssysteemgroep ondersteunen tabel](../cloud-services/cloud-services-guestos-update-matrix.md).

### <a name="known-issues"></a>Bekende problemen

- Azure .NET SDK 3.0 geïntroduceerd om een probleem bij het verwijderen van Visual Studio 2017 in de configuratie van een gelijktijdige met Visual Studio 2015.  Als u hello Azure SDK voor Visual Studio 2015 geïnstalleerd hebt, wordt Hallo Microsoft Azure-Opslagemulator en Microsoft Azure Compute-Emulator verwijderd als u Visual Studio 2017 verwijdert.  Het resultaat is een fout bij het maken en foutopsporing van nieuwe Cloud services-projecten in Visual Studio 2015. In de order toofix dit probleem, hello Azure SDK uit Hallo Web Platform Installer te installeren.  Hallo probleem worden opgelost in een toekomstige update voor Visual Studio 2017.  .

 
### <a name="azure-in-role-cache"></a>Azure In-Role Cache 

- Ondersteuning voor Azure In-Role Cache is gestopt op 30 November 2016. Klik voor meer informatie [hier](https://azure.microsoft.com/blog/azure-managed-cache-and-in-role-cache-services-to-be-retired-on-11-30-2016/).




