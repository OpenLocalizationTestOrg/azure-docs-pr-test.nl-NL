---
title: aaaTesting hello prestaties van een service in de cloud | Microsoft Docs
description: Test de prestaties van een cloudservice met behulp van Visual Studio-profiler Hallo Hallo
services: visual-studio-online
documentationcenter: n/a
author: kraigb
manager: ghogen
editor: 
ms.assetid: 7a5501aa-f92c-457c-af9b-92ea50914e24
ms.service: visual-studio-online
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: 98bd775e6ffcf948e737c5ec26399c81f4770fe3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="testing-hello-performance-of-a-cloud-service"></a>Hallo-prestaties van een cloudservice testen
## <a name="overview"></a>Overzicht
U kunt Hallo prestaties van een cloudservice in de volgende manieren Hallo testen:

* Gebruik Azure Diagnostics toocollect informatie over aanvragen en verbindingen en tooreview site statistieken die laten zien hoe Hallo-service uitvoert vanuit het klantperspectief van een. tooget gestart, Zie [diagnostische gegevens configureren voor Azure Cloud Services en virtuele Machines](http://go.microsoft.com/fwlink/p/?LinkId=623009).
* Gebruik Hallo Visual Studio profiler tooget een grondige analyse Hallo rekenkundige aspecten van de manier waarop Hallo-service wordt uitgevoerd. Zoals in dit onderwerp wordt beschreven, kunt u Hallo profiler toomeasure prestaties als een service wordt uitgevoerd in Azure. Zie voor meer informatie over hoe toouse Hallo profiler toomeasure prestaties als een service wordt lokaal uitgevoerd in een rekenemulator [getest Hallo prestaties van een Azure Cloud Service lokaal in Hallo Hallo Compute-Emulator met behulp van Visual Studio Profiler ](http://go.microsoft.com/fwlink/p/?LinkId=262845).

## <a name="choosing-a-performance-testing-method"></a>Een methode voor Prestatietesten kiezen
### <a name="use-azure-diagnostics-toocollect"></a>Gebruik Azure Diagnostics toocollect:
* Statistieken op webpagina's of services, zoals aanvragen en verbindingen.
* Statistieken over de functies, zoals hoe vaak een rol opnieuw wordt opgestart.
* Algemene informatie over geheugengebruik, zoals Hallo percentage tijd dat Hallo garbagecollector duurt of geheugen Hallo instellen van een actieve rol.

### <a name="use-hello-visual-studio-profiler-to"></a>Hallo Visual Studio profiler om te gebruiken:
* Bepalen welke functies tijd in beslag nemen Hallo meeste.
* Bepaal hoe lang duurt van elk deel uitmaakt van een rekenkracht programma.
* Vergelijk de van gedetailleerde prestatierapporten voor twee versies van een service.
* Analyseer geheugentoewijzing in meer detail dan Hallo niveau van de afzonderlijke geheugentoewijzingen.
* Gelijktijdigheidsproblemen in meerdere threads code analyseren.

Wanneer u Hallo profiler gebruikt, kunt u gegevens verzamelen als een cloudservice wordt uitgevoerd, lokaal of in Azure.

### <a name="collect-profiling-data-locally-to"></a>Profileringsgegevens lokaal te verzamelen:
* Hallo-prestaties van een deel van een cloudservice, zoals Hallo uitvoering van specifieke werkrol waarvoor een realistische gesimuleerde belasting niet testen.
* Test de prestaties van de Hallo van een cloudservice in isolatie, gecontroleerd.
* Hallo-prestaties testen van een cloudservice voordat u dit tooAzure implementeren.
* Test de prestaties van de Hallo van een cloudservice privé, zonder dat bestaande Hallo-implementaties.
* Hallo-prestaties van Hallo service testen zonder de kosten voor het uitvoeren in Azure.

### <a name="collect-profiling-data-in-azure-to"></a>Profileringsgegevens in Azure om te verzamelen:
* Test de prestaties van de Hallo van een cloudservice een gesimuleerde of echte wordt belast.
* Hallo instrumentation methode profilering gegevens te verzamelen gebruiken zoals in dit onderwerp wordt beschreven later.
* Hallo-prestaties van Hallo service testen in Hallo dezelfde omgeving als wanneer Hallo-service wordt uitgevoerd in de productieomgeving.

U doorgaans een load tootest cloud-services onder normaal simuleren of stresstest voor de voorwaarden.

## <a name="profiling-a-cloud-service-in-azure"></a>Profileren van een cloudservice in Azure
Wanneer u uw cloudservice vanuit Visual Studio publiceert, kunt u profiel Hallo-service en Hallo profilering instellingen waarmee u informatie die u wilt dat Hallo krijgt opgeven. Een profilering sessie is voor elk exemplaar van een rol gestart. Voor meer informatie over hoe toopublish uw service vanuit Visual Studio, Zie [tooan Azure Cloud Service vanuit Visual Studio publiceren](https://msdn.microsoft.com/library/azure/ee460772.aspx).

toounderstand meer informatie over prestaties profilering in Visual Studio, Zie [beginnende gebruikers handleiding tooPerformance Profiling](https://msdn.microsoft.com/library/azure/ms182372.aspx) en [toepassingsprestaties analyseren by Using Tools voor profilering](https://msdn.microsoft.com/library/azure/z9z62c29.aspx).

> [!NOTE]
> U kunt IntelliTrace of wanneer u uw cloudservice publiceert profilering inschakelen. U kunt beide niet inschakelen.
> 
> 

### <a name="profiler-collection-methods"></a>Profiler verzameling methoden
U kunt verschillende methoden gebruiken voor profilering, op basis van uw prestatieproblemen:

* **CPU-steekproeven** -statistieken die handig voor de eerste analyse van CPU-gebruik problemen zijn door deze methode worden verzameld. CPU-steekproeven is Hallo voorgestelde methode voor het starten van de meeste prestaties onderzoeken. Er is een lage impact op Hallo-toepassing die profileren van wanneer u CPU steekproeven gegevens verzamelt.
* **Instrumentation** -deze methode verzamelt gedetailleerde timinggegevens die nuttig is voor gerichte analyse en voor het analyseren van i/o-prestaties. Hallo instrumentation methode registreert elke vermelding, afsluiten en functieaanroep Hallo functies in een module tijdens een profilering uitvoeren. Deze methode is handig voor het verzamelen van de timing van gedetailleerde informatie over een gedeelte van uw code en voor het Hallo-impact van de invoer en uitvoer bewerkingen op de prestaties van toepassingen begrijpt. Deze methode is uitgeschakeld voor een computer met een 32-bits besturingssysteem. Deze optie is beschikbaar, alleen wanneer u uitvoert Hallo cloudservice in Azure, niet lokaal bij het Hallo-rekenemulator.
* **.NET-geheugentoewijzing** -deze methode toewijzingsgegevens van .NET Framework geheugen met behulp van Hallo steekproeven profilering methode verzameld. Hallo verzamelde gegevens omvatten Hallo aantal en de grootte van toegewezen objecten.
* **Gelijktijdigheid** -deze methode brongegevens conflicten en proces en thread uitvoeringsgegevens die nuttig is bij het analyseren van toepassingen met meerdere threads en meerdere processen worden verzameld. Hallo gelijktijdigheid methode verzamelt gegevens voor elke gebeurtenis die blokken uitvoering van code, zoals wanneer een thread wacht vergrendeld toegang tooan toepassing resource toobe vrijgemaakt. Deze methode is handig voor het analyseren van toepassingen met meerdere threads.
* U kunt ook inschakelen **laag interactie profilering**, waarmee u meer informatie over Hallo uitvoeringstijden van synchrone ADO.NET-aanroepen in de functies van multi-tiered toepassingen die met een of meer communiceren databases. U kunt laag interactie gegevens verzamelen met behulp van Hallo profilering methoden. Zie voor meer informatie over laag interactie profilering [laag Interacties weergave](https://msdn.microsoft.com/library/azure/dd557764.aspx).

## <a name="configuring-profiling-settings"></a>Profileringsoptimalisaties instellingen configureren
Hallo van de volgende afbeelding ziet u hoe tooconfigure uw profilering-instellingen van Hallo Publish Azure Application dialoogvenster.

![Profileren van de instellingen configureren](./media/vs-azure-tools-performance-profiling-cloud-services/IC526984.png)

> [!NOTE]
> Hallo tooenable **inschakelen profilering** selectievakje, moet u Hallo profiler op Hallo van de lokale computer dat u van toopublish uw cloudservice gebruikmaakt geïnstalleerd hebben. Hallo profiler is standaard geïnstalleerd tijdens de installatie van Visual Studio.
> 
> 

### <a name="tooconfigure-profiling-settings"></a>profileren van instellingen tooconfigure
1. Open de snelmenu Hallo voor uw Azure-project in Solution Explorer en kies vervolgens **publiceren**. Voor gedetailleerde stappen voor het toopublish een cloudservice, Zie [publiceren van een cloud service gebruikmaakt van Azure-hulpprogramma's Hallo](http://go.microsoft.com/fwlink/p?LinkId=623012).
2. In Hallo **Publish Azure Application** dialoogvenster, gekozen Hallo **geavanceerde instellingen** tabblad.
3. tooenable profilering, selecteer Hallo **inschakelen profilering** selectievakje.
4. tooconfigure uw profilering instellingen, kies Hallo **instellingen** hyperlink. Hallo profilering instellingen dialoogvenster wordt weergegeven.
5. Van Hallo **welke methode voor het samenstellen van profiel wilt u toouse** keuzerondjes, kiest u Hallo-type van het profiel dat u nodig hebt.
6. toocollect hello laag interactie profileringsgegevens, selecteer Hallo **inschakelen laag interactie profilering** selectievakje.
7. toosave Hallo-instellingen, kies Hallo **OK** knop.
   
    Wanneer u deze toepassing publiceert, zijn deze instellingen gebruikt toocreate Hallo profileren van de sessie voor elke rol.

## <a name="viewing-profiling-reports"></a>Profileren van rapporten weergeven
Een profilering sessie wordt gemaakt voor elk exemplaar van een rol in uw cloudservice. tooview uw profilering rapporten van elke sessie vanuit Visual Studio, kunt u Hallo Server Explorer-venster weergeven en kies vervolgens hello Azure Compute knooppunt tooselect een exemplaar van een rol. U kunt vervolgens Hallo profilering rapport, zoals wordt weergegeven in de volgende illustratie Hallo weergeven.

![Profileren van rapport van Azure weergeven](./media/vs-azure-tools-performance-profiling-cloud-services/IC748914.png)

### <a name="tooview-profiling-reports"></a>profileren van rapporten tooview
1. tooview hello Server Explorer-venster in Visual Studio op Hallo menu balk Kies in de weergave Server Explorer.
2. Kies hello Azure Compute-knooppunt, en kies hello Azure-implementatie knooppunt voor de cloudservice Hallo of dat u tooprofile geselecteerd wanneer u gepubliceerd vanuit Visual Studio.
3. profileren van tooview rapporten voor een exemplaar Hallo rol in Hallo-service, open Hallo snelmenu voor een specifiek exemplaar en kies **profilering rapport weergeven**.
   
    Hallo-rapport, een bestand .vsp wordt nu gedownload van Azure en Hallo status van Hallo downloaden weergegeven in hello Azure Activity Log. Wanneer Hallo downloaden is voltooid, Hallo profileren van rapport wordt weergegeven op een tabblad in de editor voor Visual Studio met de naam Hallo <Role name>  *<Instance Number>*  <identifier>.vsp. Samenvattingsgegevens voor Hallo rapport wordt weergegeven.
4. verschillende weergaven van Hallo-rapport in de lijst van de huidige weergave hello, toodisplay kiezen Hallo type weergave die u wilt. Zie voor meer informatie [extra rapportweergaven profilering](https://msdn.microsoft.com/library/azure/bb385755.aspx).

## <a name="next-steps"></a>Volgende stappen
[Foutopsporing van Cloud-Services](https://msdn.microsoft.com/library/azure/ee405479.aspx)

[Publishing tooan Azure Cloud Service vanuit Visual Studio](https://msdn.microsoft.com/library/azure/ee460772.aspx)

