---
title: aaaCommon oorzaken van Cloud Service-rollen recyclen | Microsoft Docs
description: De functie van een cloud-service die plotseling wordt gerecycled kan leiden tot aanzienlijke downtime. Hier volgen enkele veelvoorkomende problemen die ertoe leiden rollen-toobe gerecycled dat, waarmee u de uitvaltijd beperken.
services: cloud-services
documentationcenter: 
author: simonxjx
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: 533930d1-8035-4402-b16a-cf887b2c4f85
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 7/26/2017
ms.author: v-six
ms.openlocfilehash: 8fa152b33d2b22a8a02f834d4bc38519b4272f7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="common-issues-that-cause-roles-toorecycle"></a>Veelvoorkomende problemen die leiden rollen toorecycle tot
In dit artikel worden enkele algemene oorzaken van problemen met implementatie Hallo besproken en vindt u toohelp probleemoplossing tips u deze problemen oplossen. Geeft aan dat er een probleem met een toepassing is is wanneer Hallo rolinstantie toostart mislukt of het replicatiecycli tussen Hallo initialiseren bezet en stoppen statussen.

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="missing-runtime-dependencies"></a>Ontbrekende runtime-afhankelijkheden
Als een rol in uw toepassing afhankelijk is van de assembly's die geen deel uitmaakt van Hallo .NET Framework of hello Azure beheerde bibliotheek, moet u expliciet die assembly in het toepassingspakket Hallo opnemen. Houd er rekening mee dat andere Microsoft-frameworks niet standaard beschikbaar in Azure. Als uw rol is afhankelijk van een dergelijke framework, moet u deze assembly's toohello application-pakket toevoegen.

Controleer voordat u bouwen en de toepassing van het pakket, Hallo volgende:

* Als Visual studio gebruikt, moet u ervoor dat Hallo **lokale kopie** eigenschap is ingesteld, te**True** voor elke assembly in uw project die geen deel uitmaakt van hello Azure SDK verwezen of Hallo van .NET Framework.
* Zorg ervoor dat Hallo web.config-bestand verwijst niet naar alle ongebruikte-assembly's in Hallo compilatie-element.
* Hallo **Build Action** van elke .cshtml bestand te ingesteld**inhoud**. Dit zorgt ervoor dat Hallo bestanden juist wordt weergegeven in het Hallo-pakket en andere tooappear bestanden waarnaar wordt verwezen in Hallo pakket kunt.

## <a name="assembly-targets-wrong-platform"></a>Assembly doelen onjuist platform
Azure is een 64-bits-omgeving. .NET-assembly's die voor een 32-bits-doel is gecompileerd werkt daarom niet op Azure.

## <a name="role-throws-unhandled-exceptions-while-initializing-or-stopping"></a>Rol van niet-verwerkte uitzonderingen genereert tijdens het initialiseren van of stoppen
Eventuele uitzonderingen die worden veroorzaakt door methoden Hallo Hallo [RoleEntryPoint] klasse, waaronder Hallo [OnStart], [OnStop], en [uitvoeren]methoden, zijn niet-verwerkte uitzonderingen. Als een niet-verwerkte uitzondering in een van deze methoden optreedt, wordt Hallo-rol gerecycled. Als het Hallo-rol is herhaaldelijk recyclen, er het mogelijk een onverwerkte uitzondering telkens wanneer die wordt geprobeerd toostart.

## <a name="role-returns-from-run-method"></a>Rol wordt geactiveerd vanuit Run-methode
Hallo [uitvoeren] methode is bedoeld toorun voor onbepaalde tijd. Als uw code Hallo overschrijft [uitvoeren] methode, dat deze moet slapen voor onbepaalde tijd. Als hello [uitvoeren] methode retourneert Hallo-rol wordt gerecycled.

## <a name="incorrect-diagnosticsconnectionstring-setting"></a>Onjuiste DiagnosticsConnectionString-instelling
Als de toepassing gebruikmaakt van Azure Diagnostics, uw serviceconfiguratiebestand Hallo moet opgeven `DiagnosticsConnectionString` configuratie-instelling. Deze instelling moet een HTTPS-verbinding tooyour storage-account in Azure opgeven.

tooensure die uw `DiagnosticsConnectionString` instelling juist is voordat u uw toepassing pakket tooAzure implementeert, controleert u of de volgende Hallo:  

* Hallo `DiagnosticsConnectionString` punten tooa geldig storage-account instellen in Azure.  
  Deze instelling wijst standaard toohello geëmuleerde storage-account, dus u deze instelling expliciet wijzigen moet voordat u uw toepassingspakket implementeren. Als u deze instelling niet wijzigt, wordt een uitzondering gegenereerd wanneer de rolinstantie hello toostart Hallo diagnostische monitor probeert. Hierdoor kunnen Hallo rol exemplaar toorecycle voor onbepaalde tijd.
* Hallo verbindingstekenreeks is opgegeven in de volgende Hallo [indeling](../storage/common/storage-configure-connection-string.md). (Hallo protocol moet worden opgegeven als HTTPS). Vervang *MyAccountName* met Hallo-naam van uw opslagaccount en *MyAccountKey* door uw toegangssleutel:    

        DefaultEndpointsProtocol=https;AccountName=MyAccountName;AccountKey=MyAccountKey

  Als u uw toepassing ontwikkelt met behulp van Azure-hulpprogramma's voor Microsoft Visual Studio, kunt u Hallo eigenschap pagina's tooset deze waarde gebruiken.

## <a name="exported-certificate-does-not-include-private-key"></a>Geëxporteerde certificaat bevat geen persoonlijke sleutel
toorun een Webrol onder SSL, moet u ervoor zorgen dat uw geëxporteerde beheercertificaat Hallo persoonlijke sleutel bevat. Als u Hallo *Windows Certificate Manager* tooexport Hallo certificaat ervoor tooselect worden **Ja** voor Hallo **Export Hallo persoonlijke sleutel** optie. Hallo-certificaat moet worden geëxporteerd in Hallo PFX-indeling, dit de enige indeling Hallo momenteel niet ondersteund is.

## <a name="next-steps"></a>Volgende stappen
Meer [probleemoplossing artikelen](https://azure.microsoft.com/documentation/articles/?tag=top-support-issue&product=cloud-services) voor cloudservices.

Bekijk meer rollen recyclen van scenario's op [blogreeks van Kevin Williamson](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).

[RoleEntryPoint]: https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleentrypoint.aspx
[OnStart]: https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx
[OnStop]: https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleentrypoint.onstop.aspx
[uitvoeren]: https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx
