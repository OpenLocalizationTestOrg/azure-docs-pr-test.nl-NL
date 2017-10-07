---
title: aaaCommand regel build voor Azure | Microsoft Docs
description: Opdrachtregelprogramma build voor Azure
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 94b35d0d-0d35-48b6-b48b-3641377867fd
ms.service: multiple
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/05/2017
ms.author: kraigb
ms.openlocfilehash: 295b61ba162dd4373ee3f56cc1462decb3e16762
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="building-azure-projects-from-hello-command-line"></a>Azure projecten vanaf de opdrachtregel Hallo bouwen
Hallo Microsoft bouwen Engine (MSBuild) gebruikt, kunt u producten in de build-omgevingen waarin Visual Studio niet is geïnstalleerd. MSBuild maakt gebruik van een XML-indeling voor bestanden in dat de uitbreidbare en volledig wordt ondersteund door Microsoft. Hallo MSBuild-bestandsindeling gebruikt, kunt u aangeven welke items moeten worden gebouwd voor een of meer platforms en configuraties.

U kunt ook MSBuild uitvoeren op de opdrachtregel Hallo en dit onderwerp wordt beschreven die benadering. Door het instellen van eigenschappen op Hallo-opdrachtregel, kunt u specifieke configuraties van een project maken. Op deze manier kunt u ook Hallo-doelen die MSBuild voortbouwt definiëren. Zie voor meer informatie over opdrachtregelparameters en MSBuild [MSBuild-Naslaggids](https://msdn.microsoft.com/library/ms164311.aspx).

## <a name="msbuild-parameters"></a>MSBuild-parameters
Hallo eenvoudigste manier toocreate een pakket is toorun MSBuild Hello `/t:Publish` optie. Met deze opdracht maakt standaard een map in de relatie toohello-hoofdmap voor Hallo-project, zoals `<ProjectDirectory>\bin\Configuration\app.publish\`. Wanneer u een Azure-project maakt, twee bestanden worden gegenereerd: Hallo pakketbestand zelf en de bijbehorende configuratie-bestand Hallo:

* Bestand van het pakket (`project.cspkg`)
* Configuratiebestand (`ServiceConfiguration.TargetProfile.cscfg`)

Elke Azure-project bevat standaard één service-configuratiebestand voor de lokale (foutopsporing) builds en een andere voor builds cloud (fasering of productie). U kunt echter toevoegen of verwijderen van bestanden van de configuratie van de service zo nodig. Wanneer u een pakket vanuit Visual Studio maakt, wordt u gevraagd welke service-configuratiebestand tooinclude naast Hallo-pakket. Als u een pakket met behulp van MSBuild bouwen, is Hallo lokale service-configuratiebestand standaard. tooinclude een andere service-configuratie-bestand, set Hallo `TargetProfile` eigenschap Hallo MSBuild-opdracht (`MSBuild /t:Publish /p:TargetProfile=ProfileName`).

Als u wilt dat toouse een alternatieve map voor Hallo pakket- en bestanden opgeslagen, Hallo pad instellen met behulp van Hallo `/p:PublishDir=Directory\` optie, met inbegrip van Hallo afsluitende backslash scheidingsteken.

## <a name="next-steps"></a>Volgende stappen
Nadat het Hallo-pakket is gebouwd, kunt u deze tooAzure implementeren. Voor een zelfstudie die u laat zien hoe tooautomate die verwerken, Zie [continue leveringsmethode voor Cloud-Services in Azure](./cloud-services/cloud-services-dotnet-continuous-delivery.md).

