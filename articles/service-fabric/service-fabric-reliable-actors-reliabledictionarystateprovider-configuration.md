---
title: aaaChange ReliableDictionaryActorStateProvider instellingen in Azure microservices | Microsoft Docs
description: Meer informatie over het configureren van stateful actoren van het type ReliableDictionaryActorStateProvider Azure Service Fabric.
services: Service-Fabric
documentationcenter: .net
author: sumukhs
manager: timlt
editor: 
ms.assetid: 79b48ffa-2474-4f1c-a857-3471f9590ded
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 6/29/2017
ms.author: sumukhs
ms.openlocfilehash: 44c85a41c90a17669ba874401d7921c94e7be9ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-reliable-actors--reliabledictionaryactorstateprovider"></a>Reliable Actors--ReliableDictionaryActorStateProvider configureren
U kunt de standaardconfiguratie Hallo van ReliableDictionaryActorStateProvider wijzigen door Hallo settings.xml bestand dat wordt gegenereerd in Hallo Visual Studio pakket hoofdmap onder Hallo Config-map voor de opgegeven actor Hallo wijzigen.

Hello Azure Service Fabric-runtime gezocht naar vooraf gedefinieerde sectienamen in Hallo settings.xml bestand en Hallo configuratiewaarden die tijdens het maken van de runtime-onderdelen van de onderliggende hello verbruikt.

> [!NOTE]
> Voer **niet** verwijderen of wijzigen van sectienamen Hallo Hallo configuraties in Hallo settings.xml-bestand dat is gegenereerd op Hallo Visual Studio-oplossing te volgen.
> 
> 

Er zijn ook algemene instellingen die van invloed zijn op Hallo configuratie van ReliableDictionaryActorStateProvider.

## <a name="global-configuration"></a>Globale configuratie
Hallo globale configuratie is opgegeven in het clustermanifest Hallo voor Hallo cluster onder Hallo KtlLogger sectie. Hierdoor kan de configuratie van Hallo gedeeld logboek locatie en grootte plus Hallo globale geheugenlimieten gebruikt door Hallo berichtenlogboek. Houd er rekening mee dat wijzigingen in het clustermanifest Hallo invloed zijn op alle services die gebruikmaken van ReliableDictionaryActorStateProvider en betrouwbare stateful services.

Hallo clustermanifest is een XML-bestand met instellingen en configuraties die van toepassing zijn tooall knooppunten en -services in het Hallo-cluster. Hallo-bestand wordt doorgaans ClusterManifest.xml genoemd. U kunt zien Hallo clustermanifest voor uw cluster met behulp van powershell-opdracht Get-ServiceFabricClusterManifest Hallo.

### <a name="configuration-names"></a>Configuratienamen
| Naam | Eenheid | Standaardwaarde | Opmerkingen |
| --- | --- | --- | --- |
| WriteBufferMemoryPoolMinimumInKB |KB |8388608 |Minimum aantal KB tooallocate in de kernelmodus voor Hallo berichtenlogboek buffergroep geheugen schrijven. Deze geheugengroep wordt gebruikt voor het opslaan van informatie over de status voordat toodisk worden geschreven. |
| WriteBufferMemoryPoolMaximumInKB |KB |Geen limiet |Maximale grootte toowhich Hallo logboek schrijven geheugen buffergroep kan worden uitgebreid. |
| SharedLogId |GUID |"" |Hiermee geeft u een unieke GUID toouse voor het identificeren van Hallo gedeelde standaardlogboekbestand gebruikt door alle betrouwbare services op alle knooppunten in cluster Hallo die geen Hallo SharedLogId in hun specifieke configuratie van de service opgeven. Als SharedLogId is opgegeven, moet klikt u vervolgens SharedLogPath ook worden opgegeven. |
| SharedLogPath |Naam van het volledig gekwalificeerde pad |"" |Hiermee geeft u de volledig gekwalificeerde pad Hallo waar Hallo logboekbestand gebruikt door alle betrouwbare services op alle knooppunten in cluster Hallo die geen Hallo SharedLogPath in hun specifieke serviceconfiguratie opgeven gedeeld. Echter, als SharedLogPath is opgegeven, klikt u vervolgens SharedLogId moet ook worden opgegeven. |
| SharedLogSizeInMB |Megabytes |8192 |Geeft Hallo aantal MB aan schijfruimte toostatically voor gedeelde logboek Hallo toewijzen. Hallo-waarde moet 2048 of groter zijn. |

### <a name="sample-cluster-manifest-section"></a>Voorbeeld cluster manifest-sectie
```xml
   <Section Name="KtlLogger">
     <Parameter Name="WriteBufferMemoryPoolMinimumInKB" Value="8192" />
     <Parameter Name="WriteBufferMemoryPoolMaximumInKB" Value="8192" />
     <Parameter Name="SharedLogId" Value="{7668BB54-FE9C-48ed-81AC-FF89E60ED2EF}"/>
     <Parameter Name="SharedLogPath" Value="f:\SharedLog.Log"/>
     <Parameter Name="SharedLogSizeInMB" Value="16383"/>
   </Section>
```

### <a name="remarks"></a>Opmerkingen
Hallo logboek heeft een algemene groep van het geheugen toegewezen van de voor niet-wisselbaar kernelgeheugen dat beschikbaar tooall betrouwbare services op een knooppunt voor het opslaan van gegevens van de gebruikersstatus voordat toohello toegewezen logboek die zijn gekoppeld aan Hallo betrouwbare service replica wordt geschreven. Hallo-groepsgrootte wordt bepaald door Hallo WriteBufferMemoryPoolMinimumInKB en WriteBufferMemoryPoolMaximumInKB instellingen. WriteBufferMemoryPoolMinimumInKB geeft u zowel de begingrootte van deze geheugengroep Hallo en Hallo laagste grootte toowhich hello geheugengroep kan verkleinen. WriteBufferMemoryPoolMaximumInKB is Hallo hoogste grootte toowhich hello geheugengroep kan groeien. Elke replica betrouwbare service die wordt geopend kan Hallo grootte van de geheugengroep Hallo vergroten door een systeem bepaald bedrag van tooWriteBufferMemoryPoolMaximumInKB. Als er meer aanvraag voor het geheugen van Hallo geheugen dan beschikbaar is, worden aanvragen voor het geheugen wordt uitgesteld tot geheugen beschikbaar is. Daarom als Hallo schrijven buffergroep geheugen te klein voor een specifieke configuratie is vervolgens tot slechtere prestaties.

Hallo SharedLogId en SharedLogPath instellingen zijn altijd gebruikte samen toodefine Hallo GUID en locatie voor Hallo standaard logboek voor alle knooppunten in cluster Hallo gedeeld. Hallo standaard gedeelde logboek wordt gebruikt voor alle betrouwbare services die geen Hallo-instellingen in settings.xml Hallo voor specifieke Hallo-service opgeven. Voor de beste prestaties worden gedeelde logboekbestanden op schijven die worden gebruikt voor het Hallo gedeeld log-bestand tooreduce conflicten geplaatst.

SharedLogSizeInMB geeft Hallo en de hoeveelheid schijfruimte toopreallocate voor Hallo standaard gedeelde logboekbestanden op alle knooppunten.  SharedLogId en SharedLogPath hoeft niet in volgorde voor SharedLogSizeInMB toobe opgegeven opgegeven toobe.

## <a name="replicator-security-configuration"></a>Replicator Beveiligingsconfiguratie
Replicator beveiligingsconfiguraties zijn gebruikte toosecure Hallo-communicatiekanaal dat wordt gebruikt tijdens de replicatie. Dit betekent dat de services van elkaars replicatieverkeer niet zien, zorgt Hallo-gegevens die maximaal beschikbaar is ook veilig is.
Standaard wordt een lege beveiligingsconfiguratiesectie voorkomen dat replicatiebeveiliging.

### <a name="section-name"></a>De sectienaam van de
&lt;ActorName&gt;ServiceReplicatorSecurityConfig

## <a name="replicator-configuration"></a>Configuratie van de Replicator
Replicator configuraties zijn gebruikte tooconfigure Hallo replicator die verantwoordelijk is voor Hallo Actor State-Provider staat maximaal betrouwbare door repliceren en persistent maken van lokaal Hallo-status.
Hallo standaardconfiguratie wordt gegenereerd door Hallo Visual Studio-sjabloon en moet voldoende zijn. Deze sectie wordt gesproken over aanvullende configuraties die beschikbaar tootune Hallo replicator zijn.

### <a name="section-name"></a>De sectienaam van de
&lt;ActorName&gt;ServiceReplicatorConfig

### <a name="configuration-names"></a>Configuratienamen
| Naam | Eenheid | Standaardwaarde | Opmerkingen |
| --- | --- | --- | --- |
| BatchAcknowledgementInterval |Seconden |0.015 |De periode voor welke replicator Hallo op Hallo secundaire Wacht na de ontvangst van een bewerking voor het verzenden van weer een bevestiging toohello primaire. Andere bevestigingen-toobe verzonden voor bewerkingen binnen dit interval verwerkt worden verzonden als een reactie. |
| ReplicatorEndpoint |N.v.t. |Er is geen standaard--vereiste parameter |IP-adres en poort op die de primaire en secundaire replicator Hallo toocommunicate gebruikt met andere replicaties in Hallo replicaset. Dit moet verwijzen naar een resource TCP-eindpunt in Hallo servicemanifest. Raadpleeg te[Service manifest resources](service-fabric-service-manifest-resources.md) tooread meer over het definiëren van endpoint-resources in servicemanifest. |
| MaxReplicationMessageSize |Bytes |50 MB |Maximale grootte van de replicatiegegevens die kunnen worden overgebracht in één bericht. |
| MaxPrimaryReplicationQueueSize |Aantal bewerkingen |8192 |Maximum aantal bewerkingen in Hallo primaire wachtrij. Een bewerking wordt vrijgemaakt nadat Hallo primaire replicator een bevestiging van alle secundaire Hallo-replicaties ontvangt. Deze waarde moet groter zijn dan 64 en een macht van 2 zijn. |
| MaxSecondaryReplicationQueueSize |Aantal bewerkingen |16384 |Maximum aantal bewerkingen in de secundaire wachtrij Hallo. Een bewerking wordt vrijgemaakt nadat u de status maximaal beschikbaar is via persistentie. Deze waarde moet groter zijn dan 64 en een macht van 2 zijn. |
| CheckpointThresholdInMB |MB |200 |De hoeveelheid ruimte in logboekbestand waarna Hallo status gecontroleerd wordt. |
| MaxRecordSizeInKB |KB |1024 |Record maximumgrootte Hallo replicator mogelijk in Hallo logboek schrijven. Deze waarde moet een meervoud van 4 en groter zijn dan 16. |
| OptimizeLogForLowerDiskUsage |Booleaanse waarde |De waarde True |Indien true, is Hallo-logboek zo geconfigureerd dat hello toegewezen logboekbestand van de replica wordt gemaakt met een NTFS-sparse bestand. Hierdoor wordt verlaagd Hallo werkelijke gebruik van schijfruimte voor het Hallo-bestand. Als deze eigenschap ONWAAR is, wordt Hallo-bestand gemaakt met vaste toewijzingen, dat het beste schrijven prestaties Hallo bieden. |
| SharedLogId |GUID |"" |Hiermee geeft u een unieke guid toouse voor het identificeren van Hallo gedeelde logboekbestand gebruikt in combinatie met deze replica. Services moeten normaal gesproken niet gebruiken voor deze instelling. Echter, als SharedLogId is opgegeven, klikt u vervolgens SharedLogPath moet ook worden opgegeven. |
| SharedLogPath |Naam van het volledig gekwalificeerde pad |"" |Hiermee geeft u de volledig gekwalificeerde pad Hallo waar Hallo gedeelde logboekbestand voor deze replica wordt gemaakt. Services moeten normaal gesproken niet gebruiken voor deze instelling. Echter, als SharedLogPath is opgegeven, klikt u vervolgens SharedLogId moet ook worden opgegeven. |

## <a name="sample-configuration-file"></a>Voorbeeld van configuratiebestand
```xml
<?xml version="1.0" encoding="utf-8"?>
<Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <Section Name="MyActorServiceReplicatorConfig">
      <Parameter Name="ReplicatorEndpoint" Value="MyActorServiceReplicatorEndpoint" />
      <Parameter Name="BatchAcknowledgementInterval" Value="0.05"/>
      <Parameter Name="CheckpointThresholdInMB" Value="180" />
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

Hallo CheckpointThresholdInMB parameter besturingselementen Hallo hoeveelheid schijfruimte die Hallo replicator kunt toostore statusinformatie in de toegewezen logboekbestand van de replica van de Hallo gebruiken. Hogere tooa hogere waarde dan Hallo standaard kan leiden tot herconfiguratie sneller worden wanneer een nieuwe replica toohello set wordt toegevoegd. Dit is vanwege toohello gedeeltelijke statusoverdracht die uitgevoerd vanwege toohello beschikbaarheid van meer geschiedenis van bewerkingen in Hallo logboek wordt. Hierdoor kan de hersteltijd Hallo van een replica mogelijk na een crash toenemen.

Als u OptimizeForLowerDiskUsage tootrue instelt, ruimte in logboekbestand worden te veel ingerichte zodat actieve replica's kunnen meer informatie over de status opslaan in de logboekbestanden, terwijl minder schijfruimte wordt gebruikt door inactieve replica's. Dit maakt het mogelijk toohost meer replica's op een knooppunt. Als u OptimizeForLowerDiskUsage toofalse instelt, wordt informatie over de status van de Hallo toohello logboekbestanden sneller geschreven.

Hallo MaxRecordSizeInKB instelling definieert Hallo maximale grootte van een record die kan worden geschreven door Hallo replicator in Hallo logboekbestand. In de meeste gevallen is de standaardgrootte 1024 KB record Hallo optimaal. Echter, als Hallo service groter gegevens items toobe gedeelte van de informatie over de status van hello veroorzaakt, deze waarde moet mogelijk toobe verhoogd. Er is weinig voordeel bij het maken van MaxRecordSizeInKB kleiner zijn dan 1024, zoals kleinere records alleen Hallo ruimte die nodig zijn voor kleinere Hallo-record gebruiken. We verwachten dat deze waarde toobe slechts in uitzonderlijke gevallen gewijzigd moet.

Hallo SharedLogId en SharedLogPath instellingen zijn altijd gebruikte samen toomake een service-gebruik een afzonderlijke gedeelde logboek uit Hallo standaard gedeelde logboek van Hallo-knooppunt. Voor een optimale efficiency zoveel services mogelijk Hallo moeten opgeven dezelfde gedeelde logboek. Gedeelde logboekbestanden moeten worden geplaatst op schijven die uitsluitend voor Hallo gedeelde logboekbestand tooreduce bewegingen conflicten worden gebruikt. We verwachten dat deze waarden toobe slechts in uitzonderlijke gevallen gewijzigd moet.

