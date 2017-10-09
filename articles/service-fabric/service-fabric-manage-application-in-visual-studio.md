---
title: aaaManage uw toepassingen in Visual Studio | Microsoft Docs
description: Visual Studio toocreate gebruiken, ontwikkelen, pakket, implementeren en foutopsporing van uw Service Fabric-toepassingen en services.
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: timlt
editor: 
ms.assetid: c317cb7e-7eae-466e-ba41-6aa2518be5cf
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/07/2017
ms.author: mikkelhegn
ms.openlocfilehash: b2d5803d85e4f9645dcbece33a2208bc0955498d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-visual-studio-toosimplify-writing-and-managing-your-service-fabric-applications"></a>Gebruik Visual Studio toosimplify schrijven en beheren van uw Service Fabric-toepassingen
U kunt uw Azure Service Fabric-toepassingen en services met Visual Studio kunt beheren. Zodra u hebt [uw ontwikkelomgeving instellen](service-fabric-get-started.md), gebruikt u Visual Studio toocreate Service Fabric-toepassingen, services of pakket, register toevoegen en toepassingen implementeren in uw lokaal ontwikkelcluster.

## <a name="deploy-your-service-fabric-application"></a>Service Fabric-toepassing implementeren
Standaard combineert een toepassing implementeren Hallo stappen te volgen in één bewerking:

1. Hallo-toepassingspakket maken
2. Hallo pakket toohello installatiekopie toepassingsarchief uploaden
3. Type van de toepassing hello registreren
4. Als u een actieve toepassingsexemplaren
5. Maken van een toepassingsexemplaar

In Visual Studio, drukt u op **F5** uw toepassing implementeert en Hallo foutopsporingsprogramma tooall toepassingsexemplaren koppelen. U kunt **Ctrl + F5** toodeploy een toepassing zonder foutopsporing, of u kunt publiceren tooa lokale of externe-cluster met behulp van Hallo publicatieprofiel. Zie voor meer informatie [publiceren van een externe toepassing tooa-cluster met behulp van Visual Studio](service-fabric-publish-app-remote-cluster.md).

### <a name="application-debug-mode"></a>De foutopsporingsmodus toepassing
Visual Studio bieden een eigenschap genaamd **toepassing foutopsporingsmodus**, die bepaalt hoe u wilt dat Visual Studios toohandle toepassingsimplementatie als onderdeel van het opsporen van fouten.

#### <a name="tooset-hello-application-debug-mode-property"></a>tooset hello toepassing foutopsporingsmodus eigenschap
1. Op Hallo Service Fabric-toepassing van het project (*.sfproj) snelmenu kiezen **eigenschappen** (of drukt u op Hallo **F4** sleutel).
2. In Hallo **eigenschappen** venster, set Hallo **toepassing foutopsporingsmodus** eigenschap.

![Toepassing foutopsporing modus eigenschap instellen][debugmodeproperty]

#### <a name="application-debug-modes"></a>Toepassing Foutopsporingsmodi

1. **Vernieuwen van de toepassing** deze modus kunt u tooquickly wijzigen en fouten opsporen in uw code en ondersteunt het bewerken van statische webbestanden tijdens het opsporen van fouten. Deze modus werkt alleen als uw lokaal ontwikkelcluster in [modus 1-Node](/service-fabric-get-started-with-a-local-cluster.md#one-node-and-five-node-cluster-mode).
2. **Toepassing verwijderen** oorzaken Hallo toepassing toobe verwijderd wanneer Hallo foutopsporingssessie wordt beëindigd.
3. **Automatische Upgrade** toepassing hello toorun blijft wanneer Hallo debug-sessie wordt beëindigd. Hallo wordt volgende foutopsporingssessie behandeld Hallo implementatie een upgrade. Hallo-upgradeproces behoudt alle gegevens die u hebt ingevoerd in een vorige foutopsporingssessie.
4. **Toepassing houden** eindigt fouten opsporen in Hallo toepassing houdt in Hallo cluster wanneer hello wordt uitgevoerd. Aan Hallo begin Hallo volgende foutopsporingssessie, worden Hallo toepassing verwijderd.

Voor **automatische Upgrade** gegevens blijven behouden door toe te passen Hallo toepassing upgrade mogelijkheden van Service Fabric. Zie voor meer informatie over het upgraden van toepassingen en hoe u een upgrade kunt uitvoeren in een omgeving met echte [upgrade van de Service Fabric-toepassing](service-fabric-application-upgrade.md).

## <a name="add-a-service-tooyour-service-fabric-application"></a>Een service tooyour Service Fabric-toepassing toevoegen
U kunt nieuwe services tooyour toepassing tooextend functionaliteit ervan toevoegen.  tooensure dat Hallo-service wordt opgenomen in het toepassingspakket toevoegen Hallo-service via Hallo **nieuwe Fabric-Service...**  menu-item.

![Een nieuwe Service Fabric-service toevoegen][newservice]

Selecteer een Service Fabric-project type tooadd tooyour-toepassing en geef een naam voor het Hallo-service.  Zie [kiezen een framework voor uw service](service-fabric-choose-framework.md) toohelp u besluit welke service type toouse.

![Een Service Fabric-service-project type tooadd tooyour toepassing selecteren][addserviceproject]

de nieuwe service Hello wordt toegevoegd tooyour oplossing en bestaande toepassingspakket. Hallo Serviceverwijzingen en een standaard service-exemplaar wordt toegevoegd toohello toepassingsmanifest, waardoor Hallo service toobe gemaakt en gestart Hallo volgende keer dat u de toepassing hello implementeren.

![de nieuwe service Hallo is tooyour toepassingsmanifest toegevoegd][newserviceapplicationmanifest]

## <a name="package-your-service-fabric-application"></a>Uw toepassing Service Fabric-pakket
toodeploy hello toepassing en de services tooa-cluster, moet u toocreate toepassingspakketten.  Hallo pakket ordent toepassingsmanifest hello, service manifesten en andere benodigde bestanden in een specifieke indeling.  Visual Studio instellen en beheren van Hallo-pakket in de map Hallo toepassing van het project, in Hallo 'pkg' directory.  Te klikken op **pakket** van Hallo **toepassing** contextmenu maakt of updates Hallo toepassingspakket.

## <a name="remove-applications-and-application-types-using-cloud-explorer"></a>Verwijderen van toepassingen en toepassingstypen met Cloud Explorer
U kunt basiscluster beheerbewerkingen uitvoeren vanuit Visual Studio gebruikt Cloud Explorer, die u vanuit Hallo starten kunt **weergave** menu. U kunt bijvoorbeeld verwijderen van toepassingen en inrichting van toepassingstypen op lokale of externe clusters.

![Een toepassing verwijderen][removeapplication]

> [!TIP]
> Zie voor uitgebreidere cluster beheerfunctionaliteit, [uw cluster visualiseren met Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).
>
>

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>Volgende stappen
* [Service Fabric-toepassingsmodel](service-fabric-application-model.md)
* [Implementatie van service Fabric-toepassing](service-fabric-deploy-remove-applications.md)
* [Parameters voor de toepassing voor omgevingen met meerdere beheren](service-fabric-manage-multiple-environment-app-configuration.md)
* [Foutopsporing van uw Service Fabric-toepassing](service-fabric-debugging-your-application.md)
* [Uw cluster visualiseren met behulp van Service Fabric Explorer](service-fabric-visualizing-your-cluster.md)

<!--Image references-->
[addserviceproject]:./media/service-fabric-manage-application-in-visual-studio/addserviceproject.png
[manageservicefabric]: ./media/service-fabric-manage-application-in-visual-studio/manageservicefabric.png
[newservice]:./media/service-fabric-manage-application-in-visual-studio/newservice.png
[newserviceapplicationmanifest]:./media/service-fabric-manage-application-in-visual-studio/newserviceapplicationmanifest.png
[debugmodeproperty]:./media/service-fabric-manage-application-in-visual-studio/debugmodeproperty.png
[removeapplication]:./media/service-fabric-manage-application-in-visual-studio/removeapplication.png