---
title: aaaChange KVSActorStateProvider instellingen in Azure microservices | Microsoft Docs
description: Meer informatie over het configureren van stateful actoren van het type KVSActorStateProvider Azure Service Fabric.
services: Service-Fabric
documentationcenter: .net
author: sumukhs
manager: timlt
editor: 
ms.assetid: dbed72f4-dda5-4287-bd56-da492710cd96
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 6/29/2017
ms.author: sumukhs
ms.openlocfilehash: e003512678556e68a8926b1b9c6c28d9ae3979d2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-reliable-actors--kvsactorstateprovider"></a>Reliable Actors--KVSActorStateProvider configureren
U kunt de standaardconfiguratie Hallo van KVSActorStateProvider wijzigen door Hallo settings.xml bestand die wordt gegenereerd in Hallo Microsoft Visual Studio pakket hoofdmap onder Hallo Config-map voor de opgegeven actor Hallo wijzigen.

Hello Azure Service Fabric-runtime gezocht naar vooraf gedefinieerde sectienamen in Hallo settings.xml bestand en Hallo configuratiewaarden die tijdens het maken van de runtime-onderdelen van de onderliggende hello verbruikt.

> [!NOTE]
> Voer **niet** verwijderen of wijzigen van sectienamen Hallo Hallo configuraties in Hallo settings.xml-bestand dat is gegenereerd op Hallo Visual Studio-oplossing te volgen.
> 
> 

## <a name="replicator-security-configuration"></a>Replicator Beveiligingsconfiguratie
Replicator beveiligingsconfiguraties zijn gebruikte toosecure Hallo-communicatiekanaal dat wordt gebruikt tijdens de replicatie. Dit betekent dat services elkaars replicatieverkeer, om te garanderen dat Hallo-gegevens die maximaal beschikbaar is ook beveiligde kunnen niet zien.
Standaard wordt een lege beveiligingsconfiguratiesectie voorkomen dat replicatiebeveiliging.

### <a name="section-name"></a>De sectienaam van de
&lt;ActorName&gt;ServiceReplicatorSecurityConfig

## <a name="replicator-configuration"></a>Configuratie van de Replicator
Configuraties voor replicator configureren Hallo replicator die verantwoordelijk is voor het maken van Hallo Actor State-Provider staat maximaal betrouwbare.
Hallo standaardconfiguratie wordt gegenereerd door Hallo Visual Studio-sjabloon en moet voldoende zijn. Deze sectie wordt gesproken over aanvullende configuraties die beschikbaar tootune Hallo replicator zijn.

### <a name="section-name"></a>De sectienaam van de
&lt;ActorName&gt;ServiceReplicatorConfig

### <a name="configuration-names"></a>Configuratienamen
| Naam | Eenheid | Standaardwaarde | Opmerkingen |
| --- | --- | --- | --- |
| BatchAcknowledgementInterval |Seconden |0.015 |De periode voor welke replicator Hallo op Hallo secundaire Wacht na de ontvangst van een bewerking voor het verzenden van weer een bevestiging toohello primaire. Andere bevestigingen-toobe verzonden voor bewerkingen binnen dit interval verwerkt worden verzonden als een reactie. |
| ReplicatorEndpoint |N.v.t. |Er is geen standaard--vereiste parameter |IP-adres en poort op die de primaire en secundaire replicator Hallo toocommunicate gebruikt met andere replicaties in Hallo replicaset. Dit moet verwijzen naar een resource TCP-eindpunt in Hallo servicemanifest. Raadpleeg te[Service manifest resources](service-fabric-service-manifest-resources.md) tooread meer over het definiëren van endpoint-resources in Hallo servicemanifest. |
| retryInterval |Seconden |5 |De periode na welke Hallo replicator opnieuw verzendt een bericht als deze niet een bevestiging voor een bewerking ontvangt. |
| MaxReplicationMessageSize |Bytes |50 MB |Maximale grootte van de replicatiegegevens die kunnen worden overgebracht in één bericht. |
| MaxPrimaryReplicationQueueSize |Aantal bewerkingen |1024 |Maximum aantal bewerkingen in Hallo primaire wachtrij. Een bewerking wordt vrijgemaakt nadat Hallo primaire replicator een bevestiging van alle secundaire Hallo-replicaties ontvangt. Deze waarde moet groter zijn dan 64 en een macht van 2 zijn. |
| MaxSecondaryReplicationQueueSize |Aantal bewerkingen |2048 |Maximum aantal bewerkingen in de secundaire wachtrij Hallo. Een bewerking wordt vrijgemaakt nadat u de status maximaal beschikbaar is via persistentie. Deze waarde moet groter zijn dan 64 en een macht van 2 zijn. |

## <a name="store-configuration"></a>Configuratie van gegevensarchief
Store-configuraties zijn gebruikte tooconfigure Hallo lokale archief dat is gebruikt toopersist Hallo status die wordt gerepliceerd.
Hallo standaardconfiguratie wordt gegenereerd door Hallo Visual Studio-sjabloon en moet voldoende zijn. Deze sectie wordt gesproken over aanvullende configuraties die beschikbaar tootune Hallo lokale archief zijn.

### <a name="section-name"></a>De sectienaam van de
&lt;ActorName&gt;ServiceLocalStoreConfig

### <a name="configuration-names"></a>Configuratienamen
| Naam | Eenheid | Standaardwaarde | Opmerkingen |
| --- | --- | --- | --- |
| MaxAsyncCommitDelayInMilliseconds |milliseconden |200 |Hiermee stelt u Hallo maximum interval voor duurzame lokale archief doorvoeracties batchverwerking. |
| MaxVerPages |Het aantal pagina 's |16384 |Hallo kunt u het maximale aantal pagina's de versie in Hallo lokale database worden opgeslagen. Bepaalt de Hallo kunt u het maximum aantal openstaande transacties. |

## <a name="sample-configuration-file"></a>Voorbeeld van configuratiebestand
```xml
<?xml version="1.0" encoding="utf-8"?>
<Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <Section Name="MyActorServiceReplicatorConfig">
      <Parameter Name="ReplicatorEndpoint" Value="MyActorServiceReplicatorEndpoint" />
      <Parameter Name="BatchAcknowledgementInterval" Value="0.05"/>
   </Section>
   <Section Name="MyActorServiceLocalStoreConfig">
      <Parameter Name="MaxVerPages" Value="8192" />
   </Section>
   <Section Name="MyActorServiceReplicatorSecurityConfig">
      <Parameter Name="CredentialType" Value="X509" />
      <Parameter Name="FindType" Value="FindByThumbprint" />
      <Parameter Name="FindValue" Value="9d c9 06 b1 69 dc 4f af fd 16 97 ac 78 1e 80 67 90 74 9d 2f" />
      <Parameter Name="StoreLocation" Value="LocalMachine" />
      <Parameter Name="StoreName" Value="My" />
      <Parameter Name="ProtectionLevel" Value="EncryptAndSign" />
      <Parameter Name="AllowedCommonNames" Value="My-Test-SAN1-Alice,My-Test-SAN1-Bob" />
   </Section>
</Settings>
```
## <a name="remarks"></a>Opmerkingen
Hallo BatchAcknowledgementInterval parameter bepaalt replicatielatentie. Een waarde van '0' resulteert in Hallo laagst mogelijke latentie, Hallo kosten van doorvoer (zoals meer bevestigingsberichten moeten worden verzonden en verwerkt, elk met minder bevestigingen).
Hello hoger Hallo-waarde voor BatchAcknowledgementInterval, Hallo hoger Hallo totale doorvoer van replicatie, op Hallo kosten van hogere latentie van de bewerking. Hierdoor kan het rechtstreeks toohello latentie van transactie doorvoeracties.

