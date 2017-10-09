---
title: aaaHow tooupgrade projecten toohello huidige versie van Azure-hulpprogramma's Hallo | Microsoft Docs
description: Meer informatie over hoe een Azure tooupgrade project in Visual Studio toohello huidige versie van hello Azure-hulpprogramma 's
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 1d64070a-078d-468a-87f4-e6715de6475f
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/18/2016
ms.author: kraigb
ms.openlocfilehash: c89ba43af0f2fd9db46ce0c90f0da3d70dc1510b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooupgrade-projects-toohello-current-version-of-hello-azure-tools-for-visual-studio"></a>Hoe tooupgrade toohello huidige versie van hello Azure Tools voor Visual Studio-projecten
## <a name="overview"></a>Overzicht
Nadat u de huidige release Hallo van hulpprogramma's van Azure hello (of een eerdere versie die nieuwer is dan 1.6) hebt geïnstalleerd, laat u de projecten die zijn gemaakt met een Azure-hulpprogramma's voordat 1.6 (November 2011) zullen automatisch worden bijgewerkt als u deze openen. Als u projecten gemaakt met behulp van Hallo 1,6 (November 2011) versie van deze hulpprogramma's en u nog steeds dat versie geïnstalleerd, kunt u deze projecten openen in een oudere versie van Hallo en later besluit of tooupgrade ze.

## <a name="how-your-project-changes-when-you-upgrade-it"></a>Hoe uw project verandert wanneer u een upgrade uitvoeren
Als een project automatisch bijgewerkt wordt of u dat opgeven wilt u dat tooupgrade, uw project is gewijzigd toowork met de huidige versies van bepaalde assembly's en sommige eigenschappen zijn ook worden gewijzigd zoals in deze sectie wordt beschreven. Als uw project andere wijzigingen toobe die compatibel is met nieuwere versie van de Hallo Hallo-hulpprogramma's vereist, moet u deze wijzigingen handmatig aanbrengen.

* zijn de bijgewerkte tooreference Hallo nieuwere versie van Microsoft.WindowsAzure.Diagnostics.DiagnosticMonitoirTraceListener.dll Hallo web.config-bestand voor web-rollen en Hallo app.config-bestand voor werkrollen.
* Hallo Microsoft.WindowsAzure.StorageClient.dll Microsoft.WindowsAzure.Diagnostics.dll en Microsoft.WindowsAzure.ServiceRuntime.dll assembly's zijn bijgewerkte toohello nieuwe versies.
* Profielen publiceren die zijn opgeslagen in Azure projectbestand hello (.ccproj) worden verplaatst tooa afzonderlijk bestand met de Hallo extensie .azurePubXml in Hallo **publiceren** submap.
* Sommige eigenschappen in Hallo publicatieprofiel bijgewerkte toosupport nieuwe en gewijzigde functies zijn. **AllowUpgrade** wordt vervangen door **DeploymentReplacementMethod** omdat kunt u een geïmplementeerde cloudservice tegelijkertijd of incrementeel bijwerken.
* eigenschap Hallo **UseIISExpressByDefault** wordt toegevoegd en toofalse zo instellen dat hello webserver dat wordt gebruikt voor het opsporen van fouten niet automatisch gewijzigd van Internet Information Services (IIS) tooIIS Express. IIS Express is Hallo standaard webserver voor de projecten die zijn gemaakt met een nieuwere versie van hulpprogramma's Hallo Hallo.
* Als Azure opslaan in cache wordt gehost in een of meer van uw project rollen, worden sommige eigenschappen in Hallo serviceconfiguratie (.cscfg-bestand) en servicedefinitie (csdef-bestand) worden gewijzigd wanneer de upgrade van een project wordt uitgevoerd. Als Hallo project hello Azure Caching NuGet-pakket gebruikt, is het Hallo-project bijgewerkte toohello meest recente versie van het Hallo-pakket. U moet Hallo web.config-bestand openen en controleren dat clientconfiguratie Hallo is slecht onderhouden tijdens het upgradeproces Hallo. Als u opslaan in cache clientassembly voor Hallo verwijzingen tooAzure toegevoegd zonder Hallo NuGet-pakket te gebruiken, kunt u deze assembly's niet bijgewerkt; Deze verwijzingen toohello nieuwe versies, moet u handmatig bijwerken.

> [!IMPORTANT]
> F # projecten, moet u verwijzingen tooAzure assembly's handmatig bijwerken zodat deze verwijzen naar Hallo nieuwere versies van deze assembly's.
> 
> 

### <a name="how-tooupgrade-an-azure-project-toohello-current-release"></a>Hoe een Azure tooupgrade de huidige release toohello project
1. Installatie Hallo huidige versie van Hallo hulpprogramma's van Azure in Hallo-installatie van Visual Studio wilt u toouse voor Hallo geüpgraded project en open vervolgens Hallo-project dat u wilt dat tooupgrade. Als het Hallo-project is gemaakt met de hulpprogramma's van een Azure release voordat 1.6 (November 2011) Hallo-project wordt automatisch bijgewerkt toohello huidige versie. Hallo-project is gemaakt met de Hallo release van November 2011 en of release is nog steeds geïnstalleerd, wordt in deze release Hallo project geopend.
2. Klik in Solution Explorer openen Hallo snelmenu voor het projectknooppunt hello, kies **eigenschappen**, en kies vervolgens Hallo **toepassing** tabblad Hallo dialoogvenster dat wordt weergegeven.
   
    Hallo **toepassing** tabblad Hallo's versie die is gekoppeld aan het Hallo-project bevat. Als de huidige versie Hallo van hulpprogramma's van Azure wordt weergegeven, is al Hallo project bijgewerkt. Als u een nieuwere versie van hulpprogramma's Hallo dan ziet u welke Hallo-tabblad, hebt geïnstalleerd een **Upgrade** knop wordt weergegeven.
3. Kies Hallo **Upgrade** knop tooupgrade een actuele versie van project toohello Hallo-hulpprogramma's.
4. Hallo-project te bouwen en vervolgens los eventuele fouten die uit wijzigingen van de API voortvloeien. Voor informatie over hoe toomodify uw code voor de nieuwe versie hello, Zie de documentatie voor Hallo Hallo specifieke API.

