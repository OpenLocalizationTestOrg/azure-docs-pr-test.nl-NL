---
title: aaaAzure diagnostische gegevens en geschiedenis van extensie schema configuratieversies | Microsoft Docs
description: Relevante toocollecting-prestatiemeteritems in Azure Virtual Machines, VM-Schaalsets, Service Fabric en Cloud-Services.
services: monitoring-and-diagnostics
documentationcenter: .net
author: rboucher
manager: carmonm
editor: 
ms.assetid: 
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/16/2017
ms.author: robb
ms.openlocfilehash: 854ad118f660810aa38703670284794d658142c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-diagnostics-extention-configuration-schema-versions-and-history"></a>Azure Diagnostics extensie schema configuratieversies en geschiedenis
Deze pagina indexen Azure Diagnostics extensie schema versies geleverd als onderdeel van Hallo Microsoft Azure SDK.  

> [!NOTE]
> Hello Azure Diagnostics-extensie is Hallo onderdeel gebruikt toocollect prestatiemeteritems en andere statistieken van:
> - Azure Virtual Machines 
> - Schaalsets voor virtuele machines
> - Service Fabric 
> - Cloudservices 
> - Netwerkbeveiligingsgroepen
> 
> Deze pagina is alleen relevant als u een van deze services.

Hallo-extensie voor diagnostische gegevens van Azure wordt gebruikt met andere Microsoft-producten voor diagnostische gegevens zoals Azure Monitor, Application Insights en Log Analytics. Zie voor meer informatie [hulpprogramma's van Microsoft Bewakingsoverzicht](monitoring-overview.md).

## <a name="azure-sdk-and-diagnostics-versions-shipping-chart"></a>Azure SDK en diagnostische gegevens versies back-upfunctie grafiek  

|Azure SDK-versie | Versie van de Diagnostics-uitbreiding | Model|  
|------------------|-------------------------------|------|  
|1.x               |1.0                            |invoegtoepassing|  
|2.0 - 2.4         |1.0                            |invoegtoepassing|  
|2.5               |1.2                            |De extensie|  
|2.6               |1.3                            |"|  
|2.7               |1.4                            |"|  
|2.8               |1.5                            |"|  
|2.9               |1.6                            |"|
|2.96              |1.7                            |"|
|2.96              |1.8                            |"|
|2.96              |1.8.1                          |"|
|2.96              |1.9                            |"|



 Azure Diagnostics versie 1.0 eerst in een invoegtoepassingsmodel--wat betekent dat wanneer u hello Azure SDK geïnstalleerd, u hebt verkregen Hallo-versie van Azure diagnostics verzonden met het hebt verzonden.  

 Beginnen met de SDK 2.5 (diagnostics versie 1.2), Azure diagnostics is gegaan tooan extensiemodel. Hallo extra tooutilize nieuwe functies zijn alleen beschikbaar in de nieuwere Azure-SDK's, maar alle services die gebruikmaken van Azure diagnostics zou kunnen worden opgepikt Hallo van de meest recente back-upfunctie versie rechtstreeks uit Azure. Bijvoorbeeld zou iemand anders die nog steeds SDK 2.5 worden geladen Hallo van de meest recente versie die wordt weergegeven in de vorige tabel hello, ongeacht als ze Hallo nieuwere functies gebruiken.  

## <a name="schemas-index"></a>Index van de schema 's  
Verschillende versies van Azure diagnostics andere configuratie-schema's gebruiken. 

[Diagnostische gegevens 1.0 configuratieschema](azure-diagnostics-schema-1dot0.md)  

[Diagnostische gegevens 1.2 configuratieschema](azure-diagnostics-schema-1dot2.md)  

[Diagnostische gegevens 1.3 en hoger configuratieschema](azure-diagnostics-schema-1dot3-and-later.md)  

## <a name="version-history"></a>Versiegeschiedenis


### <a name="diagnostics-extension-19"></a>Extensie voor diagnostische gegevens 1,9 
Docker-ondersteuning is toegevoegd.


### <a name="diagnostics-extension-181"></a>Extensie voor diagnostische gegevens 1.8.1 
Kan een SAS-token in plaats van de sleutel van een opslagaccount opgeven in Hallo persoonlijke configuratie. Als een SAS-token is opgegeven, wordt de opslagaccountsleutel Hallo genegeerd.


```json
{
    "storageAccountName": "diagstorageaccount",
    "storageAccountEndPoint": "https://core.windows.net",
    "storageAccountSasToken": "{sas token}",
    "SecondaryStorageAccounts": {
        "StorageAccount": [
            {
                "name": "secondarydiagstorageaccount",
                "endpoint": "https://core.windows.net",
                "sasToken": "{sas token}"
            }
        ]
    }
}
```

```xml
<PrivateConfig>
    <StorageAccount name="diagstorageaccount" endpoint="https://core.windows.net" sasToken="{sas token}" />
    <SecondaryStorageAccounts>
        <StorageAccount name="secondarydiagstorageaccount" endpoint="https://core.windows.net" sasToken="{sas token}" />
    </SecondaryStorageAccounts>
</PrivateConfig>
```


### <a name="diagnostics-extension-18"></a>Extensie voor diagnostische gegevens 1.8 
Toegevoegde opslagtype tooPublicConfig. StorageType mag *tabel*, *Blob*, *TableAndBlob*. *Tabel* Hallo standaard is.


```json
{
    "WadCfg": {
    },
    "StorageAccount": "diagstorageaccount",
    "StorageType": "TableAndBlob"
}
```

```xml
<PublicConfig>
    <WadCfg />
    <StorageAccount>diagstorageaccount</StorageAccount>
    <StorageType>TableAndBlob</StorageType>
</PublicConfig>
```


### <a name="diagnostics-extension-17"></a>Extensie voor diagnostische gegevens 1.7 
Hallo toegevoegde mogelijkheid tooroute tooEventHub.

### <a name="diagnostics-extension-15"></a>1.5-extensie voor diagnostische gegevens
Hallo-element en Hallo mogelijkheid toosend diagnostics-gegevens te sinks toegevoegd[Application Insights](../application-insights/app-insights-cloudservices.md) waardoor het gemakkelijker toodiagnose problemen in uw toepassing, evenals de Hallo system en infrastructuur niveau.

### <a name="azure-sdk-26-and-diagnostics-extension-13"></a>Azure SDK 2.6 en diagnostische gegevens van de extensie 1.3 
Voor Cloud Service-projecten in Visual Studio, zijn Hallo volgende wijzigingen aangebracht. (Deze wijzigingen gelden ook toolater versies van Azure SDK.)

* Hallo lokale emulator ondersteunt nu de diagnostische gegevens. Dit betekent dat u kunt het verzamelen van diagnostische gegevens en zorg ervoor dat uw toepassing maakt Hallo rechts traceringen tijdens het ontwikkelen en testen in Visual Studio. Hallo verbindingsreeks `UseDevelopmentStorage=true` kunt verzamelen van diagnostische gegevens, terwijl u uw cloudserviceproject in Visual Studio uitvoert met behulp van hello Azure-opslagemulator. Alle diagnostische gegevens worden verzameld in opslagaccount hello (ontwikkeling opslag).
* Hallo diagnostics account verbindingsreeks voor opslag (Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString) wordt nog een keer opgeslagen in hello (.cscfg) serviceconfiguratiebestand. In de Azure SDK 2.5 is Hallo diagnostics storage-account opgegeven in Hallo diagnostics.wadcfgx bestand.

Er zijn enkele belangrijke verschillen tussen hoe Hallo-verbindingsreeks in de Azure SDK 2.4 en eerder gegaan en hoe het werkt in de Azure SDK 2.6 en hoger.

* In de Azure SDK 2.4 en eerder is Hallo-verbindingsreeks gebruikt als een runtime door Hallo diagnostics tooget Hallo storage account informatie over de invoegtoepassing voor het overdragen van diagnostische logboeken.
* In Azure SDK 2.6 en hoger worden Hallo diagnostics verbindingsreeks wordt gebruikt door de extensie voor Visual Studio tooconfigure Hallo diagnostische gegevens met gegevens van de juiste opslag Hallo tijdens de publicatie. Hallo-verbindingsreeks kunt u verschillende opslagaccounts voor verschillende configuraties die door Visual Studio wordt gebruikt bij het publiceren van definiëren. Omdat Hallo diagnostics-invoegtoepassing (na de Azure SDK 2,5) niet langer beschikbaar is, kan niet Hallo cscfg-bestand zelf echter Hallo extensie voor diagnostische gegevens inschakelen. U hebt tooenable Hallo extensie afzonderlijk via hulpprogramma's zoals Visual Studio of PowerShell.
* toosimplify hello proces van het Hallo-extensie voor diagnostische gegevens configureren met PowerShell, Hallo pakket uitvoer vanuit Visual Studio bevat ook Hallo openbare configuratie-XML voor Hallo-extensie voor diagnostische gegevens voor elke rol. Visual Studio gebruikt Hallo diagnostics toopopulate Hallo storage account verbindingsinformatie aanwezig is in de openbare configuratie Hallo. Hallo openbare config-bestanden worden gemaakt in de map extensies Hallo en Hallo patroon PaaSDiagnostics volgen. <RoleName>. PubConfig.xml. Alle implementaties op basis van PowerShell kunnen gebruiken dit patroon toomap elke configuratie tooa rol.
* Hallo verbindingsreeks in Hallo .cscfg-bestand wordt ook gebruikt door Hallo Hallo diagnostics-gegevens van Azure portal tooaccess zodat het kan worden weergegeven in Hallo **bewaking** tabblad Hallo-verbindingsreeks is benodigde tooconfigure Hallo service tooshow uitgebreide het bewaken van gegevens in Hallo-portal.

#### <a name="migrating-projects-tooazure-sdk-26-and-later"></a>Migreren projecten tooAzure SDK 2.6 en hoger
Bij het migreren van Azure SDK 2.5 tooAzure SDK 2.6 of hoger, als u een opslagaccount voor diagnostische gegevens opgegeven in Hallo .wadcfgx bestand had vervolgens blijft er. tootake profiteren van Hallo flexibiliteit voor het gebruik van andere opslag van accounts voor opslagconfiguraties verschillende, hebt u toomanually Hallo connection string tooyour project toevoegen. Als u een project waarnaar u migreert van Azure SDK 2.4 of eerdere tooAzure SDK 2.6, Hallo vervolgens diagnostics verbindingsreeksen behouden blijven. Let echter Hallo wijzigingen in hoe verbindingsreeksen worden behandeld in de Azure SDK 2.6 zoals opgegeven in de vorige sectie Hallo.

#### <a name="how-visual-studio-determines-hello-diagnostics-storage-account"></a>Hoe Visual Studio bepaalt Hallo opslagaccount voor diagnostische gegevens
* Als een verbindingsreeks diagnostische gegevens is opgegeven in het .cscfg-bestand hello, Visual Studio gebruikt deze extensie voor diagnostische gegevens van tooconfigure Hallo bij het publiceren en bij het genereren van Hallo openbare configuratie voor XML-bestanden tijdens de verpakking.
* Als geen verbindingsreeks diagnostics is opgegeven in het .cscfg-bestand hello, klikt u vervolgens terugvalt Visual Studio toousing Hallo storage-account opgegeven in Hallo .wadcfgx bestand tooconfigure Hallo extensie voor diagnostische gegevens bij het publiceren en Hallo openbare genereren XML-configuratiebestanden wanneer verpakken.
* Hallo diagnostics verbindingsreeks in Hallo .cscfg-bestand heeft voorrang op Hallo storage-account in Hallo .wadcfgx bestand. Als u een verbindingsreeks diagnostics is opgegeven in Hallo cscfg-bestand, vervolgens Visual Studio wordt gebruikt, wordt en Hallo storage-account in .wadcfgx worden genegeerd.

#### <a name="what-does-hello-update-development-storage-connection-strings-checkbox-do"></a>Wat Hallo 'Bijwerken ontwikkeling storage-verbindingsreeksen...' selectievakje doen?
selectievakje voor Hallo **bijwerken van ontwikkeling storage-verbindingsreeksen voor diagnostische gegevens en opslaan in cache met Microsoft Azure storage-accountreferenties bij het publiceren van tooMicrosoft Azure** beschikt u over een handige manier tooupdate ieder ontwikkeling opslagaccountverbindingsreeksen met hello Azure storage-account is opgegeven tijdens de publicatie.

Stel bijvoorbeeld dat u dit selectievakje inschakelt en Hallo diagnostics verbindingsreeks `UseDevelopmentStorage=true`. Wanneer u Hallo project tooAzure publiceert, wordt Visual Studio Hallo diagnostics verbindingsreeks automatisch bijgewerkt met de Hallo storage-account die u hebt opgegeven in de wizard Publiceren Hallo. Echter, als een echte storage-account is opgegeven als Hallo diagnostische gegevens van de verbindingsreeks, vervolgens dat account wordt gebruikt in plaats daarvan.

### <a name="diagnostics-functionality-differences-between-azure-sdk-24-and-earlier-and-azure-sdk-25-and-later"></a>Diagnostische functionaliteit verschillen tussen Azure SDK 2.4 en eerder en Azure SDK 2,5 en hoger
Als u een uw project van Azure SDK 2.4 tooAzure SDK 2.5 of hoger upgrade uitvoert, moet u er rekening mee Hallo volgende diagnostische functionaliteit verschillen vergeet.

* **Configuratie-API's zijn afgeschaft** – programmatische configuratie van diagnostische gegevens is beschikbaar in de Azure SDK 2.4 of eerdere versies, maar is afgeschaft in Azure SDK 2.5 en hoger. Als uw configuratie van diagnostische momenteel in de code is gedefinieerd, moet u tooreconfigure die instellingen vanaf het begin in gemigreerde Hallo-project in volgorde van diagnostische gegevens tookeep werken. Hallo diagnostics-configuratiebestand voor de Azure SDK 2.4 is diagnostics.wadcfg en diagnostics.wadcfgx voor Azure SDK 2.5 of hoger.
* **Diagnostische gegevens voor cloud-servicetoepassingen kan alleen worden geconfigureerd op Hallo rolniveau, niet op instantieniveau Hallo.**
* **Telkens wanneer u uw app implementeert, configuratie van diagnostische hello wordt bijgewerkt** : dit kan pariteit problemen veroorzaken als u de configuratie van de diagnostische gegevens in Server Explorer te wijzigen en vervolgens uw app te implementeren.
* **In de Azure SDK 2.5 en hoger crashdumps zijn geconfigureerd in Hallo diagnostics-configuratiebestand niet in de code** – als u geconfigureerd in de code crashdumps hebt, hebt u toomanually overdracht Hallo configuratie uit het configuratiebestand van de code toohello, omdat Hallo crashdumps worden niet overgedragen tijdens Hallo migratie tooAzure SDK 2.6.

