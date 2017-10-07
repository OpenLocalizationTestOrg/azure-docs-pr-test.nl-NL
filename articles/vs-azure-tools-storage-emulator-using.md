---
title: aaaConfiguring en Opslagemulator met Visual Studio met behulp van Hallo | Microsoft Docs
description: Configureren en gebruiken van Hallo Opslagemulator met Visual Studio
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: c8e7996f-6027-4762-806e-614b93131867
ms.service: storage
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 8/17/2017
ms.author: kraigb
ms.openlocfilehash: d590f21146c86bcb7bfa6b6164b92c6df5938d5b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-and-using-hello-storage-emulator-with-visual-studio"></a>Configureren en gebruiken van Hallo Opslagemulator met Visual Studio
[!INCLUDE [storage-try-azure-tools](../includes/storage-try-azure-tools.md)]

## <a name="overview"></a>Overzicht
Hello Azure SDK-ontwikkelomgeving omvat opslagemulator hello, een hulpprogramma dat Hallo Blob, wachtrijen en tabellen storage-services beschikbaar zijn in Azure op uw lokale ontwikkelcomputer simuleert. Als u hello Azure storage-services bouwen van een cloudservice die in dienst of alle externe toepassingen schrijven dat aanroepen Hallo storage-services, kunt u uw code lokaal tegen Hallo opslagemulator testen. beheer van de opslagemulator Hallo integreren Hello Azure-hulpprogramma's voor Microsoft Visual Studio in Visual Studio. hulpprogramma's van Azure Hallo Hallo storage emulator database bij het eerste gebruik initialiseren, begint Hallo emulator opslagservice wanneer u uitvoert of fouten opsporen in uw code vanuit Visual Studio en alleen-lezentoegang toohello storage emulator gegevens via hello Azure Storage Explorer biedt.

Zie voor gedetailleerde informatie over de opslagemulator hello, met inbegrip van de systeemvereisten en aangepaste configuratie-instructies [gebruik hello Azure-Opslagemulator voor ontwikkeling en testen](storage/common/storage-use-emulator.md).

> [!NOTE]
> Er zijn bepaalde verschillen in functionaliteit tussen Hallo storage emulator simulatie en hello Azure storage-services. Zie [verschillen tussen Hallo Opslagemulator en Azure Storage-Services](storage/common/storage-use-emulator.md) in hello Azure SDK-documentatie voor informatie over de specifieke verschillen Hallo.
> 
> 

## <a name="configuring-a-connection-string-for-hello-storage-emulator"></a>Een verbindingsreeks configureren voor de opslagemulator Hallo
Hallo opslagemulator tooaccess vanuit de programmacode binnen een rol, zult u tooconfigure een verbinding die punten toohello-opslagemulator tekenreeks en die kan later worden gewijzigd toopoint tooan Azure storage-account. Een verbindingsreeks is een configuratie-instelling die uw rol op runtime tooconnect tooa storage-account kunt lezen. Voor meer informatie over het toocreate verbindingsreeksen, Zie [configureren hello Azure-toepassing](https://msdn.microsoft.com/library/azure/2da5d6ce-f74d-45a9-bf6b-b3a60c5ef74e#BK_SettingsPage).

> [!NOTE]
> U kunt een verwijzing toohello opslagaccount emulator retourneren vanuit uw code met behulp van Hallo **DevelopmentStorageAccount** eigenschap. Deze methode werkt goed als u wilt tooaccess Hallo opslagemulator vanuit uw code, maar als u van plan toopublish uw toepassing tooAzure bent, u moet een tekenreeks verbinding tooaccess toocreate uw Azure storage-account en uw toouse code wijzigen die verbindingsreeks voordat u deze hebt gepubliceerd. Als u tussen Hallo emulator opslagaccount en een Azure storage-account vaak overschakelt, wordt een verbindingsreeks dit proces vereenvoudigen.
> 
> 

## <a name="initializing-and-running-hello-storage-emulator"></a>Initialiseren en uitvoeren van Hallo-opslagemulator
U kunt opgeven dat tijdens het uitvoeren of fouten opsporen in uw service in Visual Studio, Visual Studio wordt automatisch Hallo-opslagemulator gestart. Open in Solution Explorer Hallo snelmenu voor uw **Azure** project en kies **eigenschappen**. Op Hallo **ontwikkeling** tabblad in Hallo **Start Azure-Opslagemulator** Kies **True** (als deze al toothat waarde is niet ingesteld).

Hallo in de eerste keer dat u uitvoert of fouten opsporen in uw service vanuit Visual Studio, Hallo opslagemulator wordt een initialisatieproces gestart. Dit proces lokale poorten zijn gereserveerd voor de opslagemulator hello en Hallo storage emulator database wordt gemaakt. Hierna kunt hoeft dit proces niet toorun opnieuw tenzij Hallo storage emulator database wordt verwijderd.

> [!NOTE]
> Vanaf versie van juni 2012 Hallo Hallo hulpprogramma's van Azure kunt Hallo opslagemulator wordt uitgevoerd, standaard in SQL Express LocalDB. In eerdere versies van Hallo hulpprogramma's van Azure-opslagemulator hello wordt uitgevoerd op een standaardexemplaar van SQL Express 2005 of 2008, die u moet installeren voordat u kunnen hello Azure SDK installeren. U kunt ook de opslagemulator Hallo tegen een benoemd exemplaar van SQL Express of een naam of het standaardexemplaar van Microsoft SQL Server uitvoeren. Als u tooconfigure Hallo storage emulator toorun tegen een exemplaar dan het standaardexemplaar hello moet, Zie [gebruik hello Azure-Opslagemulator voor ontwikkeling en testen](storage/common/storage-use-emulator.md).
> 
> 

Hallo-opslagemulator biedt een interface tooview Hallo Gebruikersstatus van de lokale opslagservices Hallo en toostart, stoppen en opnieuw ingesteld. Als Hallo storage emulator-service is gestart, kunt u Hallo gebruikersinterface weergeven of start of Hallo-service stoppen met de rechtermuisknop op Hallo Systeemvakpictogram voor Microsoft Azure-Emulator in het Windows-taakbalk Hallo Hallo.

## <a name="viewing-storage-emulator-data-in-server-explorer"></a>Storage emulator gegevens in Server Explorer bekijken
Hello Azure Storage-knooppunt in Server Explorer kunt u de gegevens en wijzig instellingen tooview voor blob en tabelgegevens in uw storage-accounts, met inbegrip van Hallo-opslagemulator. Zie [beheren Azure Blob Storage-resources met Opslagverkenner (Preview)](https://docs.microsoft.com/azure/vs-azure-tools-storage-explorer-blobs) voor meer informatie.

