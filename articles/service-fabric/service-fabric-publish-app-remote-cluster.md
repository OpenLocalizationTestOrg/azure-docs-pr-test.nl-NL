---
title: aaaPublish een app tooa RAS-cluster met Visual Studio | Microsoft Docs
description: Meer informatie over hoe toopublish een toepassing tooa externe service fabric-cluster met behulp van Visual Studio.
services: service-fabric
documentationcenter: na
author: cawams
manager: timlt
editor: 
ms.assetid: faecd892-eb54-4d9c-8023-c67442afb8e8
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 07/29/2016
ms.author: cawa
ms.openlocfilehash: d0f06f120cc7e22f3f8e73ce0970e1da5823e647
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-remove-applications-using-visual-studio"></a>Implementeren en verwijderen van toepassingen met Visual Studio
> [!div class="op_single_selector"]
> * [PowerShell](service-fabric-deploy-remove-applications.md)
> * [Visual Studio](service-fabric-publish-app-remote-cluster.md)
> * [FabricClient-API's](service-fabric-deploy-remove-applications-fabricclient.md)
> 
> 

<br/>

Hello Azure Service Fabric-extensie voor Visual Studio biedt een eenvoudige, herhaalbare en scriptbare manier toopublish een toepassing tooa Service Fabric-cluster.

## <a name="hello-artifacts-required-for-publishing"></a>Hallo-artefacten die vereist zijn voor publicatie
### <a name="deploy-fabricapplicationps1"></a>Implementeer FabricApplication.ps1
Dit is een PowerShell-script die gebruikmaakt van een profielpad publiceren als een parameter voor publishing Service Fabric-toepassingen. Omdat dit script deel van uw toepassing uitmaakt, bent u Welkom toomodify als nodig is voor uw toepassing.

### <a name="publish-profiles"></a>Profielen publiceren
Een map in Service Fabric-toepassingsproject Hallo aangeroepen **PublishProfiles** bevat XML-bestanden die voor het opslaan van essentiële informatie voor het publiceren van een toepassing, zoals:

* Verbindingsparameters service Fabric-cluster
* Pad tooan toepassing parameterbestand
* Upgrade-instellingen

Standaard uw toepassing bevat drie profielen publiceren: Local.1Node.xml Local.5Node.xml en Cloud.xml. U kunt meer profielen toevoegen door te kopiëren en plakken van een van de standaardbestanden Hallo.

### <a name="application-parameter-files"></a>Parameter voor toepassingsbestanden
Een map in Service Fabric-toepassingsproject Hallo aangeroepen **ApplicationParameters** XML-bestanden voor de gebruiker opgegeven application manifest parameterwaarden bevat. De parameters van Application manifest-bestanden kunnen worden gebruikt zodat u andere waarden voor de implementatie-instellingen gebruiken kunt. Zie toolearn meer informatie over parameters voorzien van uw toepassing [omgevingen met meerdere in Service Fabric beheren](service-fabric-manage-multiple-environment-app-configuration.md).

> [!NOTE]
> Voor actorservices, moet u Hallo project bouwt eerst voordat u probeert tooedit Hallo-bestand in een teksteditor of via Hallo publiceren in het dialoogvenster. Dit is omdat het deel van de manifestbestanden Hallo wordt gegenereerd tijdens het Hallo-build.

## <a name="toopublish-an-application-using-hello-publish-service-fabric-application-dialog-box"></a>toopublish een toepassing met behulp van dialoogvenster Hallo-Service Fabric-toepassing publiceren
Hallo volgende stappen laten zien hoe toopublish wordt gebruikt door een toepassing hello **Service Fabric-toepassing publiceren** geleverd door Hallo Visual Studio Service Fabric-hulpprogramma's in het dialoogvenster.

1. Kies in het snelmenu Hallo van Hallo Service Fabric-toepassing-project, **publiceren...** Hallo tooview **Service Fabric-toepassing publiceren** in het dialoogvenster.
   
    ![Hallo ** publiceren Service Fabric toepassing ** in het dialoogvenster][0]
   
    Hallo bestand geselecteerd in Hallo **profiel als doel** vervolgkeuzelijst is wanneer alle Hallo-instellingen, met uitzondering van **Manifest versies**, worden opgeslagen. U kunt een bestaand profiel gebruiken of een nieuwe maken door te kiezen **< profielen beheren... >** in Hallo **profiel als doel** vervolgkeuzelijst. Wanneer u een publicatieprofiel kiest, wordt de inhoud ervan weergegeven in de overeenkomende velden van het dialoogvenster Hallo Hallo. toosave uw wijzigingen op elk gewenst moment kiezen Hallo **profiel opslaan** koppeling.    
2. In Hallo **verbindingseindpunt** sectie, geeft u een lokale of externe Service Fabric-cluster van publishing eindpunt. tooadd of wijzig verbindingseindpunt hello, klikt u op Hallo **verbindingseindpunt** vervolgkeuzelijst. Hallo-lijst bevat Hallo beschikbaar Service Fabric-cluster verbinding eindpunten toowhich die kunt u publiceren op basis van uw Azure-abonnementen. Houd er rekening mee dat als u niet al aangemeld in tooVisual Studio, kunt u zich na vragen aan gebruiker toodo dus.
   
    Hallo cluster selectie dialoogvenster vak toochoose van Hallo set beschikbare abonnementen en -clusters gebruiken.
   
    ![Hallo ** Selecteer Service Fabric Cluster ** in het dialoogvenster][1]
   
   > [!NOTE]
   > Als u wilt toopublish tooan willekeurig eindpunt (zoals een cluster partij), Zie Hallo **tooan willekeurige clustereindpunt publiceren** hieronder.
   > 
   > 
   
    Nadat u ervoor een eindpunt kiest, valideert Visual Studio Hallo verbinding toohello geselecteerde Service Fabric-cluster. Als het Hallo-cluster niet veilig zijn, kunt Visual Studio tooit onmiddellijk verbinden. Echter, als Hallo cluster beveiligd is, moet u tooinstall een certificaat op de lokale computer voordat u doorgaat. Zie [hoe de verbindingen voor het beveiligen van tooconfigure](service-fabric-visualstudio-configure-secure-connections.md) voor meer informatie. Wanneer u bent klaar, kiest u Hallo **OK** knop. het geselecteerde cluster Hello wordt weergegeven in Hallo **Service Fabric-toepassing publiceren** in het dialoogvenster.
3. In Hallo **toepassing parameterbestand** vervolgkeuzelijst Ga parameterbestand tooan-toepassing. Een parameterbestand toepassing bevat de gebruiker opgegeven waarden voor parameters in het manifestbestand van de toepassing hello. tooadd of wijzig een parameter, kies Hallo **bewerken** knop. Voer of wijzig de waarde van parameter Hallo in Hallo **Parameters** raster. Wanneer u bent klaar, kiest u Hallo **opslaan** knop.
   
    ![Hallo ** bewerken Parameters ** in het dialoogvenster][2]
4. Gebruik Hallo **Upgrade Hallo toepassing** selectievakje toospecify of deze actie is een upgrade. Upgrade publiceert acties die afwijken van de normale publiceert acties. Zie [Service Fabric-toepassing upgraden](service-fabric-application-upgrade.md) voor een lijst van verschillen. upgrade tooconfigure-instellingen, kies Hallo **instellingen configureren voor Upgrade** koppeling. Hallo upgradeparameter editor weergegeven. Zie [configureren van de upgrade van een Service Fabric-toepassing hello](service-fabric-visualstudio-configure-upgrade.md) toolearn meer informatie over parameters voor het bijwerken.
5. Kies Hallo **Manifest versies...** knop tooview hello **versies bewerken** in het dialoogvenster. U moet tooupdate toepassing en Serviceversies voor een upgrade tootake plaats. Zie [upgrade zelfstudie over Service Fabric](service-fabric-application-upgrade-tutorial.md) toolearn hoe een toepassing en service manifest versies invloed op een upgradeproces.
   
    ![Hallo ** bewerken versies ** in het dialoogvenster][3]
   
    Als Hallo-toepassing en Serviceversies gebruikt semantische versioning zoals 1.0.0 of numerieke waarden in de indeling van 1.0.0.0 hello, selecteert u Hallo **automatisch bijwerken van toepassing en Serviceversies** optie. Wanneer u deze optie, het Hallo-service en toepassing versienummers worden automatisch bijgewerkt wanneer een code, configuratie, of gegevens Pakketversie wordt bijgewerkt. Als u liever tooedit Hallo versies handmatig, schakelt u Hallo selectievakje toodisable deze functie.
   
   > [!NOTE]
   > Voor alle pakket-vermeldingen tooappear voor een actor-project, eerst maken Hallo project toogenerate Hallo vermeldingen in Service Manifest Hallo-bestanden.
   > 
   > 
6. Wanneer u klaar bent Hallo opgeven van alle benodigde instellingen hello, kies **publiceren** knop toopublish uw toepassing toohello geselecteerde Service Fabric-cluster. Hallo-instellingen die u hebt opgegeven zijn toegepast toohello publicatieproces.

## <a name="publish-tooan-arbitrary-cluster-endpoint-including-party-clusters"></a>Publiceren van willekeurige clustereindpunt tooan (met inbegrip van derden clusters)
Hallo publishing ervaring voor Visual Studio is geoptimaliseerd voor het publiceren van tooremote clusters die zijn gekoppeld aan een van uw Azure-abonnementen. Het is echter mogelijk toopublish tooarbitrary eindpunten (zoals Service Fabric-clusters voor derden) door rechtstreeks bewerken van Hallo publicatieprofiel XML. Zoals hierboven wordt beschreven, drie profielen publiceren standaard--**Local.1Node.xml**, **Local.5Node.xml**, en **Cloud.xml**--, maar u Welkom toocreate extra profielen voor verschillende omgevingen. Bijvoorbeeld, kunt u toocreate een profiel voor het publiceren van tooparty clusters, mogelijk met de naam **Party.xml**.

Als u verbinding maakt niet beveiligde cluster tooan, alle die vereist zijn verbindingseindpunt Hallo-cluster, zoals is `partycluster1.eastus.cloudapp.azure.com:19000`. In dat geval Hallo verbindingseindpunt in Hallo publiceren profiel zou als volgt uitzien:

```XML
<ClusterConnectionParameters ConnectionEndpoint="partycluster1.eastus.cloudapp.azure.com:19000" />
```

  Als u de beveiligde cluster tooa verbinding maakt, moet u ook tooprovide Hallo details van de clientcertificaat Hallo van Hallo lokale archief toobe gebruikt voor verificatie. Zie voor meer informatie [configureren beveiligde verbindingen tooa Service Fabric-cluster](service-fabric-visualstudio-configure-secure-connections.md).

  Zodra uw publicatieprofiel is ingesteld, kunt u deze in Hallo verwijst het dialoogvenster publish zoals hieronder wordt weergegeven.

  ![Nieuwe publicatieprofiel in het dialoogvenster publish][4]

  Opmerking dat in dit geval Hallo nieuwe publicatieprofiel verwijst tooone van toepassing hello-parameter standaardbestanden. Dit is geschikt als u wilt dat toopublish Hallo toepassing configuratie tooa evenveel omgevingen. Daarentegen in gevallen waar u verschillende configuraties voor elke omgeving die u wilt dat toopublish naar toohave, zou er zin toocreate een bijbehorende parameterbestand van toepassing.

## <a name="next-steps"></a>Volgende stappen
hoe tooautomate Hallo publicatieproces in een omgeving continue integratie zien toolearn [Stel doorlopende integratie van Service Fabric](service-fabric-set-up-continuous-integration.md).

[0]: ./media/service-fabric-publish-app-remote-cluster/PublishDialog.png
[1]: ./media/service-fabric-publish-app-remote-cluster/SelectCluster.png
[2]: ./media/service-fabric-publish-app-remote-cluster/EditParams.png
[3]: ./media/service-fabric-publish-app-remote-cluster/EditVersions.png
[4]: ./media/service-fabric-publish-app-remote-cluster/publish-to-party-cluster.png
