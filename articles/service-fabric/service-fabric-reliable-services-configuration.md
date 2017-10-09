---
title: betrouwbare Azure microservices aaaConfigure | Microsoft Docs
description: Meer informatie over het configureren van stateful Reliable Services in Azure Service Fabric.
services: Service-Fabric
documentationcenter: .net
author: sumukhs
manager: timlt
editor: vturecek
ms.assetid: 9f72373d-31dd-41e3-8504-6e0320a11f0e
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 6/29/2017
ms.author: sumukhs
ms.openlocfilehash: 1e9c2890b62890a777561f25c04dc0fd11db9f1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-stateful-reliable-services"></a>Stateful betrouwbare services configureren
Er zijn twee sets van configuratie-instellingen voor betrouwbare services. Één set is voor alle betrouwbare services in de cluster Hallo globale terwijl hello andere set specifieke tooa bepaalde betrouwbare service.

## <a name="global-configuration"></a>Globale configuratie
Hallo globale betrouwbare serviceconfiguratie is opgegeven in het clustermanifest Hallo voor Hallo cluster onder Hallo KtlLogger-sectie. Hierdoor kan de configuratie van Hallo gedeeld logboek locatie en grootte plus Hallo globale geheugenlimieten gebruikt door Hallo berichtenlogboek. Hallo clustermanifest is een XML-bestand met instellingen en configuraties die van toepassing zijn tooall knooppunten en -services in het Hallo-cluster. Hallo-bestand wordt doorgaans ClusterManifest.xml genoemd. U kunt zien Hallo clustermanifest voor uw cluster met behulp van powershell-opdracht Get-ServiceFabricClusterManifest Hallo.

### <a name="configuration-names"></a>Configuratienamen
| Naam | Eenheid | Standaardwaarde | Opmerkingen |
| --- | --- | --- | --- |
| WriteBufferMemoryPoolMinimumInKB |KB |8388608 |Minimum aantal KB tooallocate in de kernelmodus voor Hallo berichtenlogboek buffergroep geheugen schrijven. Deze geheugengroep wordt gebruikt voor het opslaan van informatie over de status voordat toodisk worden geschreven. |
| WriteBufferMemoryPoolMaximumInKB |KB |Geen limiet |Maximale grootte toowhich Hallo logboek schrijven geheugen buffergroep kan worden uitgebreid. |
| SharedLogId |GUID |"" |Hiermee geeft u een unieke GUID toouse voor het identificeren van Hallo gedeelde standaardlogboekbestand gebruikt door alle betrouwbare services op alle knooppunten in cluster Hallo die geen Hallo SharedLogId in hun specifieke configuratie van de service opgeven. Als SharedLogId is opgegeven, moet klikt u vervolgens SharedLogPath ook worden opgegeven. |
| SharedLogPath |Naam van het volledig gekwalificeerde pad |"" |Hiermee geeft u de volledig gekwalificeerde pad Hallo waar Hallo logboekbestand gebruikt door alle betrouwbare services op alle knooppunten in cluster Hallo die geen Hallo SharedLogPath in hun specifieke serviceconfiguratie opgeven gedeeld. Echter, als SharedLogPath is opgegeven, klikt u vervolgens SharedLogId moet ook worden opgegeven. |
| SharedLogSizeInMB |Megabytes |8192 |Geeft Hallo aantal MB aan schijfruimte toostatically voor gedeelde logboek Hallo toewijzen. Hallo-waarde moet 2048 of groter zijn. |

In Azure ARM of lokale JSON-sjabloon ziet Hallo voorbeeld hieronder u hoe toochange Hallo Hallo gedeelde transactielogboek die wordt gemaakt tooback worden betrouwbare verzamelingen voor stateful services.

    "fabricSettings": [{
        "name": "KtlLogger",
        "parameters": [{
            "name": "SharedLogSizeInMB",
            "value": "4096"
        }]
    }]

### <a name="sample-local-developer-cluster-manifest-section"></a>Voorbeeld lokale developer cluster manifest-sectie
Als u wilt dat toochange dit op uw lokale ontwikkelingsomgeving, moet u tooedit Hallo lokale clustermanifest.xml bestand.

```xml
   <Section Name="KtlLogger">
     <Parameter Name="SharedLogSizeInMB" Value="4096"/>
     <Parameter Name="WriteBufferMemoryPoolMinimumInKB" Value="8192" />
     <Parameter Name="WriteBufferMemoryPoolMaximumInKB" Value="8192" />
     <Parameter Name="SharedLogId" Value="{7668BB54-FE9C-48ed-81AC-FF89E60ED2EF}"/>
     <Parameter Name="SharedLogPath" Value="f:\SharedLog.Log"/>
   </Section>
```

### <a name="remarks"></a>Opmerkingen
Hallo logboek heeft een algemene groep van het geheugen toegewezen van de voor niet-wisselbaar kernelgeheugen dat beschikbaar tooall betrouwbare services op een knooppunt voor het opslaan van gegevens van de gebruikersstatus voordat toohello toegewezen logboek die zijn gekoppeld aan Hallo betrouwbare service replica wordt geschreven. Hallo-groepsgrootte wordt bepaald door Hallo WriteBufferMemoryPoolMinimumInKB en WriteBufferMemoryPoolMaximumInKB instellingen. WriteBufferMemoryPoolMinimumInKB geeft u zowel de begingrootte van deze geheugengroep Hallo en Hallo laagste grootte toowhich hello geheugengroep kan verkleinen. WriteBufferMemoryPoolMaximumInKB is Hallo hoogste grootte toowhich hello geheugengroep kan groeien. Elke replica betrouwbare service die wordt geopend kan Hallo grootte van de geheugengroep Hallo vergroten door een systeem bepaald bedrag van tooWriteBufferMemoryPoolMaximumInKB. Als er meer aanvraag voor het geheugen van Hallo geheugen dan beschikbaar is, worden aanvragen voor het geheugen wordt uitgesteld tot geheugen beschikbaar is. Daarom als Hallo schrijven buffergroep geheugen te klein voor een specifieke configuratie is vervolgens tot slechtere prestaties.

Hallo SharedLogId en SharedLogPath instellingen zijn altijd gebruikte samen toodefine Hallo GUID en locatie voor Hallo standaard logboek voor alle knooppunten in cluster Hallo gedeeld. Hallo standaard gedeelde logboek wordt gebruikt voor alle betrouwbare services die geen Hallo-instellingen in settings.xml Hallo voor specifieke Hallo-service opgeven. Voor de beste prestaties worden gedeelde logboekbestanden op schijven die worden gebruikt voor het Hallo gedeeld log-bestand tooreduce conflicten geplaatst.

SharedLogSizeInMB geeft Hallo en de hoeveelheid schijfruimte toopreallocate voor Hallo standaard gedeelde logboekbestanden op alle knooppunten.  SharedLogId en SharedLogPath hoeft niet in volgorde voor SharedLogSizeInMB toobe opgegeven opgegeven toobe.

## <a name="service-specific-configuration"></a>Specifieke configuratie van service
U kunt de standaardconfiguraties stateful Reliable Services wijzigen met behulp van het configuratiepakket hello (configuratie) of Hallo service-implementatie (code).

* **Config** -configuratie via Hallo configuratiepakket wordt bereikt door het Hallo Settings.xml-bestand dat is gegenereerd op basis van Hallo Microsoft Visual Studio pakket onder Hallo Config-map voor elke service in de toepassing hello wijzigen.
* **Code** -configuratie via code wordt bereikt door het maken van een ReliableStateManager met behulp van een object ReliableStateManagerConfiguration Hallo opties die van toepassing is ingesteld.

Standaard hello Azure Service Fabric-runtime naar vooraf gedefinieerde sectienamen in Hallo Settings.xml bestand gezocht en Hallo configuratiewaarden die tijdens het maken van de runtime-onderdelen van de onderliggende hello verbruikt.

> [!NOTE]
> Voer **niet** sectienamen Hallo Hallo volgende configuraties in Hallo Settings.xml-bestand dat is gegenereerd op Hallo Visual Studio-oplossing, tenzij u van plan tooconfigure uw service via programmacode bent verwijderen.
> Hallo config pakket of de sectie namen wijzigen vereisen een codewijziging bij het configureren van Hallo ReliableStateManager.
> 
> 

### <a name="replicator-security-configuration"></a>Replicator Beveiligingsconfiguratie
Replicator beveiligingsconfiguraties zijn gebruikte toosecure Hallo-communicatiekanaal dat wordt gebruikt tijdens de replicatie. Dit betekent dat services niet kunnen toosee elkaars replicatieverkeer, ervoor zorgen dat Hallo-gegevens die maximaal beschikbaar is ook secure zal zijn. Standaard wordt een lege beveiligingsconfiguratiesectie voorkomen dat replicatiebeveiliging.

### <a name="default-section-name"></a>De naam van de standaard-sectie
ReplicatorSecurityConfig

> [!NOTE]
> toochange deze sectienaam onderdrukking Hallo replicatorSecuritySectionName parameter toohello ReliableStateManagerConfiguration constructor bij het maken van Hallo ReliableStateManager voor deze service.
> 
> 

### <a name="replicator-configuration"></a>Configuratie van de Replicator
Replicator configuraties configureren Hallo replicator die verantwoordelijk is voor Hallo stateful betrouwbare van de status van Service uiterst betrouwbare door repliceren en persistent maken van lokaal Hallo-status.
Hallo standaardconfiguratie wordt gegenereerd door Hallo Visual Studio-sjabloon en moet voldoende zijn. Deze sectie wordt gesproken over aanvullende configuraties die beschikbaar tootune Hallo replicator zijn.

### <a name="default-section-name"></a>De naam van de standaard-sectie
ReplicatorConfig

> [!NOTE]
> toochange deze sectienaam onderdrukking Hallo replicatorSettingsSectionName parameter toohello ReliableStateManagerConfiguration constructor bij het maken van Hallo ReliableStateManager voor deze service.
> 
> 

### <a name="configuration-names"></a>Configuratienamen
| Naam | Eenheid | Standaardwaarde | Opmerkingen |
| --- | --- | --- | --- |
| BatchAcknowledgementInterval |Seconden |0.015 |De periode voor welke replicator Hallo op Hallo secundaire Wacht na de ontvangst van een bewerking voor het verzenden van weer een bevestiging toohello primaire. Andere bevestigingen-toobe verzonden voor bewerkingen binnen dit interval verwerkt worden verzonden als een reactie. |
| ReplicatorEndpoint |N.v.t. |Er is geen standaard--vereiste parameter |IP-adres en poort op die de primaire en secundaire replicator Hallo toocommunicate gebruikt met andere replicaties in Hallo replicaset. Dit moet verwijzen naar een resource TCP-eindpunt in Hallo servicemanifest. Raadpleeg te[Service manifest resources](service-fabric-service-manifest-resources.md) tooread meer over het definiëren van endpoint-resources in een servicemanifest van de. |
| MaxPrimaryReplicationQueueSize |Aantal bewerkingen |8192 |Maximum aantal bewerkingen in Hallo primaire wachtrij. Een bewerking wordt vrijgemaakt nadat Hallo primaire replicator een bevestiging van alle secundaire Hallo-replicaties ontvangt. Deze waarde moet groter zijn dan 64 en een macht van 2 zijn. |
| MaxSecondaryReplicationQueueSize |Aantal bewerkingen |16384 |Maximum aantal bewerkingen in de secundaire wachtrij Hallo. Een bewerking wordt vrijgemaakt nadat u de status maximaal beschikbaar is via persistentie. Deze waarde moet groter zijn dan 64 en een macht van 2 zijn. |
| CheckpointThresholdInMB |MB |50 |De hoeveelheid ruimte in logboekbestand waarna Hallo status gecontroleerd wordt. |
| MaxRecordSizeInKB |KB |1024 |Record maximumgrootte Hallo replicator mogelijk in Hallo logboek schrijven. Deze waarde moet een meervoud van 4 en groter zijn dan 16. |
| MinLogSizeInMB |MB |0 (systeem bepaald) |De minimumgrootte van Hallo transactionele logboek. Hallo logboek worden niet mogen tootruncate tooa grootte dan deze instelling. 0 geeft aan dat replicator Hallo Hallo minimale logboekgrootte wordt bepaald. Deze waarde verhoogt, Hallo mogelijkheid gedeeltelijke kopie en incrementele back-ups te doen omdat de kans op relevante logboekrecords worden afgekapt wordt verlaagd. |
| TruncationThresholdFactor |Factor |2 |Hiermee wordt bepaald hoe groot van Hallo logboek moet worden afgekapt wordt geactiveerd. Afkappen drempelwaarde wordt bepaald door MinLogSizeInMB TruncationThresholdFactor vermenigvuldigd. TruncationThresholdFactor moet groter dan 1 zijn. MinLogSizeInMB * TruncationThresholdFactor moet kleiner dan MaxStreamSizeInMB. |
| ThrottlingThresholdFactor |Factor |4 |Hiermee wordt bepaald hoe groot logboek Hallo Hallo replica wordt gestart, wordt beperkt. Bandbreedtebeperking drempelwaarde (in MB) wordt bepaald door de maximale ((MinLogSizeInMB * ThrottlingThresholdFactor),(CheckpointThresholdInMB * ThrottlingThresholdFactor)). Bandbreedtebeperking drempelwaarde (in MB) moet groter zijn dan de drempelwaarde (in MB) moet worden afgekapt. Afkappen drempelwaarde (in MB) moet kleiner zijn dan MaxStreamSizeInMB. |
| MaxAccumulatedBackupLogSizeInMB |MB |800 |Maximale verzameld grootte (in MB) van de back-uplogboeken in een keten van de opgegeven back-uplogboek. Een incrementele back-aanvragen mislukt als Hallo incrementele back-up een back-uplogboek waardoor back-uplogboeken Hallo die zijn verzameld sinds Hallo relevante volledige back-up toobe groter is dan deze genereert. In dergelijke gevallen is de gebruiker vereist tootake een volledige back-up. |
| SharedLogId |GUID |"" |Hiermee geeft u een unieke GUID toouse voor het identificeren van Hallo gedeelde logboekbestand gebruikt in combinatie met deze replica. Services moeten normaal gesproken niet gebruiken voor deze instelling. Echter, als SharedLogId is opgegeven, klikt u vervolgens SharedLogPath moet ook worden opgegeven. |
| SharedLogPath |Naam van het volledig gekwalificeerde pad |"" |Hiermee geeft u de volledig gekwalificeerde pad Hallo waar Hallo gedeelde logboekbestand voor deze replica wordt gemaakt. Services moeten normaal gesproken niet gebruiken voor deze instelling. Echter, als SharedLogPath is opgegeven, klikt u vervolgens SharedLogId moet ook worden opgegeven. |
| SlowApiMonitoringDuration |Seconden |300 |Hiermee stelt u Hallo controle-interval voor beheerde API-aanroepen. Voorbeeld: de gebruiker opgegeven back-callback-functie. Nadat hello-interval is verstreken, wordt een statusrapport waarschuwing verzonden toohello Health Manager. |

### <a name="sample-configuration-via-code"></a>Voorbeeldconfiguratie via code
```csharp
class Program
{
    /// <summary>
    /// This is hello entry point of hello service host process.
    /// </summary>
    static void Main()
    {
        ServiceRuntime.RegisterServiceAsync("HelloWorldStatefulType",
            context => new HelloWorldStateful(context, 
                new ReliableStateManager(context, 
        new ReliableStateManagerConfiguration(
                        new ReliableStateManagerReplicatorSettings()
            {
                RetryInterval = TimeSpan.FromSeconds(3)
                        }
            )))).GetAwaiter().GetResult();
    }
}    
```
```csharp
class MyStatefulService : StatefulService
{
    public MyStatefulService(StatefulServiceContext context, IReliableStateManagerReplica stateManager)
        : base(context, stateManager)
    { }
    ...
}
```


### <a name="sample-configuration-file"></a>Voorbeeld van configuratiebestand
```xml
<?xml version="1.0" encoding="utf-8"?>
<Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <Section Name="ReplicatorConfig">
      <Parameter Name="ReplicatorEndpoint" Value="ReplicatorEndpoint" />
      <Parameter Name="BatchAcknowledgementInterval" Value="0.05"/>
      <Parameter Name="CheckpointThresholdInMB" Value="512" />
   </Section>
   <Section Name="ReplicatorSecurityConfig">
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


### <a name="remarks"></a>Opmerkingen
BatchAcknowledgementInterval bepaalt replicatielatentie. Een waarde van '0' resulteert in Hallo laagst mogelijke latentie, Hallo kosten van doorvoer (zoals meer bevestigingsberichten moeten worden verzonden en verwerkt, elk met minder bevestigingen).
Hello hoger Hallo-waarde voor BatchAcknowledgementInterval, Hallo hoger Hallo totale doorvoer van replicatie, op Hallo kosten van hogere latentie van de bewerking. Hierdoor kan het rechtstreeks toohello latentie van transactie doorvoeracties.

Hallo-waarde voor CheckpointThresholdInMB besturingselementen Hallo hoeveelheid schijfruimte die Hallo replicator kunt toostore statusinformatie in de toegewezen logboekbestand van de replica van de Hallo gebruiken. Hogere tooa hogere waarde dan Hallo standaard kan leiden tot herconfiguratie sneller worden wanneer een nieuwe replica toohello set wordt toegevoegd. Dit is vanwege toohello gedeeltelijke statusoverdracht die uitgevoerd vanwege toohello beschikbaarheid van meer geschiedenis van bewerkingen in Hallo logboek wordt. Hierdoor kan de hersteltijd Hallo van een replica mogelijk na een crash toenemen.

Hallo MaxRecordSizeInKB instelling definieert Hallo maximale grootte van een record die kan worden geschreven door Hallo replicator in Hallo logboekbestand. In de meeste gevallen is de standaardgrootte 1024 KB record Hallo optimaal. Echter, als Hallo service groter gegevens items toobe gedeelte van de informatie over de status van hello veroorzaakt, deze waarde moet mogelijk toobe verhoogd. Er is weinig voordeel bij het maken van MaxRecordSizeInKB kleiner zijn dan 1024, zoals kleinere records alleen Hallo ruimte die nodig zijn voor kleinere Hallo-record gebruiken. We verwachten dat deze waarde toobe gewijzigd in alleen zeldzame gevallen moet.

Hallo SharedLogId en SharedLogPath instellingen zijn altijd gebruikte samen toomake een service-gebruik een afzonderlijke gedeelde logboek uit Hallo standaard gedeelde logboek van Hallo-knooppunt. Voor een optimale efficiency zoveel services mogelijk Hallo moeten opgeven dezelfde gedeelde logboek. Gedeelde logboekbestanden moeten worden geplaatst op schijven die worden gebruikt voor het Hallo gedeeld log-bestand tooreduce bewegingen conflicten. We verwachten dat deze waarde toobe gewijzigd in alleen zeldzame gevallen moet.

## <a name="next-steps"></a>Volgende stappen
* [Fouten opsporen in uw Service Fabric-toepassing in Visual Studio](service-fabric-debugging-your-application.md)
* [Referentie voor ontwikkelaars voor Reliable Services](https://msdn.microsoft.com/library/azure/dn706529.aspx)

