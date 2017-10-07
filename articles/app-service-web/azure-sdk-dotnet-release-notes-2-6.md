---
title: aaaAzure SDK voor .NET 2.6 Release-opmerkingen
description: Azure SDK voor .NET 2.6 Release-opmerkingen
services: app-service/web
documentationcenter: .net
author: chrissfanos
editor: 
ms.assetid: b45853d5-a2b8-4962-a22d-579cb36ae14c
ms.service: app-service
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 02/24/2017
ms.author: juliako
ms.openlocfilehash: ac613cf20da4f731fab6f35ccbf6dbeaf18c0ec4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sdk-for-net-26-release-notes"></a>Azure SDK voor .NET 2.6 Release-opmerkingen
Dit document bevat Hallo release-opmerkingen voor hello Azure SDK voor .NET 2.6-release. 

U kunt met Azure SDK 2.6 cloud-servicetoepassingen (PaaS) op voorwaarde dat u Hallo doel .NET Framework handmatig op Hallo Cloud Service-rol installeren die gericht is op .NET 4.5.2 of .NET 4.6 ontwikkelen. Zie [.NET installeren op een Cloud Service-functie](http://go.microsoft.com/fwlink/?LinkID=309796).

## <a name="service-bus-updates"></a>Service Bus-updates
* Event Hubs: 
  
  * Nu kunt gerichte toegangsbeheer bij het verzenden van gebeurtenissen bij het blootstellen van aanvullende publisher eindpunt voor Event Hubs.
  * Als u meer stabiliteit en verbetering toegevoegd tooEvent Hubs functie.
  * Ondersteuning van Amqp-protocol toe te voegen via WebSocket voor messaging en Event Hubs.

## <a name="hdinsight-tools-for-visual-studio-updates"></a>HDInsight Tools voor Visual Studio-updates
* **IntelliSense verbetering**: externe metagegevens suggestie
  
    HDInsight Tools voor Visual Studio ondersteunt nu ophalen van externe metagegevens wanneer u uw Hive-script bewerkt. U kunt bijvoorbeeld **Selecteer * FROM** en alle Hallo tabelnamen worden weergegeven. Hallo kolomnamen worden ook weergegeven na het opgeven van een tabel.
* **HDInsight-emulator ondersteuning**
  
    Nu de HDInsight Tools voor Visual Studio-ondersteuning tooHDInsight emulator verbinding te maken zodat u uw Hive-scripts lokaal ontwikkelen kan zonder eventuele kosten die scripts uitvoeren op uw HDInsight-clusters wordt uitgevoerd. 
  
    Voor meer informatie raadpleegt u te[deze handleiding](http://go.microsoft.com/fwlink/?LinkID=529540&clcid=0x409).
* **HDInsight Tools voor Visual Studio-ondersteuning voor algemene Hadoop-clusters** (Preview)
  
    HDInsight Tools voor Visual Studio ondersteunen nu algemeen Hadoop-clusters, zodat u kunt HDInsight Tools voor Visual Studio toodo Hallo volgende gebruiken:
  
  * verbinding maken met tooyour-cluster 
  * Hive-query met verbeterde ondersteuning voor IntelliSense/automatisch aanvullen, schrijven 
  * alle Hallo-taken weergeven in het cluster met een intuïtieve gebruikersinterface. 
    
    Voor meer informatie raadpleegt u te[deze handleiding](http://go.microsoft.com/fwlink/?LinkID=529540&clcid=0x409).

## <a name="in-role-cache-updates"></a>Updates in-Role Cache
* **In-Role Cache** is bijgewerkte toouse **Microsoft Azure-opslag-SDK** versie 4.3. Hallo tot op heden **In-Role Cache** Azure-opslag-SDK versie 1.7 werd gebruikt.
  
    Klanten met behulp van Azure SDK 2.5 of hieronder moet werken tooAzure SDK 2.6 en gaan toohello nieuwe versie van Azure-opslag-SDK. 
  
    Deze versie van de Azure Storage tijd is 2011-08-18 geplande toobe 1 augustus 2016 verwijderd. Alle migraties van In-Role Cache van Azure SDK 2.5 of onder too2.6 moeten zijn voltooid op dit tijdstip. Zie voor meer informatie over Hallo buiten gebruik stellen van Azure Storage versie 2011-08-18 [verwijderen Update voor de versie van Microsoft Azure Storage Service: extensie too2016](http://blogs.msdn.com/b/windowsazurestorage/archive/2015/10/19/microsoft-azure-storage-service-version-removal-update-extension-to-2016.aspx).

> [!IMPORTANT]
> Kondigen we Hallo 30 November 2016, buiten gebruik stellen voor Azure Managed Cache Service en Azure In-Role Cache. Het is raadzaam dat u tooAzure Redis-Cache in voorbereiding op deze buiten gebruik stellen migreert. Zie voor meer informatie over datums en migratie richtlijnen [die Azure Cache aanbieding is geschikt voor mij?](../redis-cache/cache-faq.md#which-azure-cache-offering-is-right-for-me)
> 
> 

## <a name="azure-app-service-tools"></a>Hulpprogramma's van Azure App Service
Hallo volgende items zijn bijgewerkt in hello Azure SDK 2.6-release.

* Azure publishing uitgebreid tooinclude Azure API-Apps. Als het implementatiedoel van een.
* API-Apps inrichten functionaliteit tooenable gebruikers met API-App maken en inrichten van functionaliteit.
* Server Explorer gewijzigd tooreflect nieuwe App Service-knooppunt met mobiele, Web en API apps, gegroepeerd per resourcegroep.
* Voeg toe gebaar van de Azure-API-App-Client toevoegen toomost C#-projecten automatisch genereren van Swagger ingeschakeld API Apps die worden uitgevoerd in Azure-abonnement van een gebruiker wordt inschakelen.
* API-Apps tooling en App Service-knooppunten in Server Explorer zijn alleen beschikbaar in Visual Studio 2013. 

## <a name="azure-resource-manager-tools-updates"></a>Azure Resource Manager-hulpprogramma's zijn bijgewerkt
Hello Azure resource manager-hulpprogramma's zijn bijgewerkt tooinclude sjablonen voor virtuele Machines, netwerken en opslag. Hallo JSON bewerken ervaring is bijgewerkte tooinclude een nieuwe overzichtsweergave voor sjablonen en Hallo mogelijkheid tooedit Hallo sjablonen met behulp van de JSON-codefragmenten zijn. Sjablonen die zijn geïmplementeerd vanuit Visual Studio-project Hallo voorzien zodat alle wijzigingen toohello script wordt gebruikt door Visual Studio PowerShell-script gebruiken.

## <a name="diagnostics-improvements-for-cloud-services"></a>Diagnostische gegevens verbeteringen voor Cloudservices
Azure SDK 2.6 brengt terug ondersteuning voor het verzamelen van diagnostische logboeken in hello Azure-rekenemulator en dragen ze toodevelopment opslag. Diagnostische logboeken (inclusief application trace Logboeken, het Event Tracing voor Windows (ETW)-Logboeken, prestatiemeteritems, infrastructuur logboeken en windows-gebeurtenislogboeken) gegenereerd wanneer Hallo toepassing wordt uitgevoerd in de emulator Hallo kan worden overgedragen toodevelopment opslag tooverify die de logboekregistratie van diagnostische gegevens op uw lokale computer werkt. 

Hallo opslagaccount voor diagnostische gegevens kan nu worden opgegeven in hello (.cscfg) serviceconfiguratiebestand waardoor het gemakkelijker toouse diagnostische gegevens van andere storage-accounts voor verschillende omgevingen. Er zijn enkele belangrijke verschillen tussen hoe Hallo verbindingsreeks Azure SDK 2.4 en Azure SDK 2.6 gewerkt. Voor meer informatie over hoe toouse Hallo Diagnostics opslagverbindingsreeks en hoe dit heeft gevolgen voor uw projecten zien [diagnostische gegevens configureren voor Azure Cloud Services](http://go.microsoft.com/fwlink/?LinkID=532784).

## <a name="breaking-changes"></a>Wijzigingen op te splitsen
### <a name="azure-resource-manager-tools"></a>Azure Resource Manager-hulpprogramma 's
* Hallo **Cloud implementatieprojecten** projecttype beschikbaar in de Azure SDK 2.5 te heeft gekregen Hallo**Azure-resourcegroep**.
* **Cloud implementatieprojecten** type projecten in hello Azure SDK 2.5 gemaakt kan worden gebruikt in 2.6 maar Hallo-sjabloon implementeren vanuit Visual Studio zal mislukken. Echter wordt implementeren met Hallo PowerShell-script nog steeds werken zoals eerder.  Voor meer informatie over toouse **Cloud implementatieprojecten** in 2.6 Lees dit [boeken](http://go.microsoft.com/fwlink/?LinkID=534086).

## <a name="known-issues"></a>Bekende problemen
* Verzamelen van diagnostische logboeken in Hallo-emulator vereist een 64-bits besturingssysteem. Diagnostische logboeken worden niet verzameld wanneer op een 32-bits besturingssysteem wordt uitgevoerd. Dit heeft geen invloed op een andere functionaliteit van de emulator. 
* Azure SDK 2.6 uitgebracht op 4-29-2015 was twee problemen: 
  
  * Universele App kan niet worden geladen in Visual Studio 2015 wanneer Azure SDK 2.6 op Hallo machine is geïnstalleerd.
  * Foutopsporing in een Cloud Service-project mislukken in Visual Studio 2013 en Visual Studio 2015, Visual Studio niet meer reageert waarbij loopt vast bij het weergeven van een dialoogvenster met het Hallo-bericht 'Configuring diagnostische gegevens voor de emulator'.
    
    Een update tooAzure SDK 2.6 is uitgebracht op 5-18-2015. Hallo bijgewerkt versie is 2.6.30508.1601; het bevat oplossingen voor twee problemen die hierboven worden beschreven. U kunt identificeren Hallo build van Hallo SDK vanuit Configuratiescherm -> programma's en onderdelen -> Microsoft Azure-hulpprogramma's voor Microsoft Visual Studio 2013 – v 2.6. de kolom versie Hallo weergegeven Hallo build-nummer.
    
    Als u nog steeds Hallo hierboven problemen worden geconfronteerd, installeer Hallo meest recente versie van Azure 2.6 SDK voor Hallo [tegenover 2012](http://go.microsoft.com/fwlink/p/?linkid=323511&clcid=0x409), [VS 2013](http://go.microsoft.com/fwlink/p/?linkid=323510&clcid=0x409) of [VS 2015](http://go.microsoft.com/fwlink/?linkid=518003&clcid=0x409).

## <a name="see-also"></a>Zie ook
[Ondersteuning en buiten gebruik stellen informatie voor hello Azure SDK voor .NET- en API 's](https://msdn.microsoft.com/library/azure/dn479282.aspx/)

