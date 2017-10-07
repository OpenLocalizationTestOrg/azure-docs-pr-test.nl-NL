---
title: aaaDesigning maximaal beschikbare toepassingen met behulp van Azure leestoegang geografisch redundante opslag (RA-GRS) | Microsoft Docs
description: Hoe toouse Azure RA-GRS opslag tooarchitect een maximaal beschikbare toepassing flexibel genoeg toohandle storingen.
services: storage
documentationcenter: .net
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 8f040b0f-8926-4831-ac07-79f646f31926
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 1/19/2017
ms.author: robinsh
ms.openlocfilehash: e4a9fe7ef33eecd894408b3c1ef59920a248d1bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="designing-highly-available-applications-using-ra-grs"></a>Maximaal beschikbare toepassingen met behulp van RA-GRS ontwerpen

Een algemene functie van de cloud-gebaseerde infrastructuur is dat ze een maximaal beschikbare platform voor het hosten van toepassingen. Ontwikkelaars van toepassingen op basis van een cloud moeten rekening houden met zorgvuldig hoe tooleverage dit platform toodeliver maximaal beschikbare toepassingen tootheir gebruikers. In dit artikel is gericht specifiek op hoe ontwikkelaars van hello Azure Storage geografisch redundante opslag met leestoegang (RA-GRS) toomake gebruikmaken kunnen hun toepassingen meer beschikbaar.

Er zijn vier opties voor de redundantie – LRS (lokaal redundante opslag), ZRS (Zone-redundante opslag), (Geo-Redundant Storage) GRS en RA-GRS (leestoegang Geo-Redundant Storage). We gaan toodiscuss GRS en RA-GRS in dit artikel. Met GRS worden in Hallo primaire regio die u hebt geselecteerd bij het instellen van het opslagaccount Hallo drie kopieën van uw gegevens bewaard. Drie extra kopieën worden asynchroon worden bijgehouden in een secundaire regio die is opgegeven door Azure. RA-GRS is hetzelfde als GRS hello, behalve dat u leestoegang toohello secundaire exemplaar hebt. Zie voor meer informatie over verschillende opties voor Azure Storage redundantie Hallo [Azure Storage-replicatie](https://docs.microsoft.com/en-us/azure/storage/storage-redundancy). Hallo replicatie ook wordt uitgelegd Hallo koppelingen van Hallo primaire en secundaire regio's.

Er zijn codefragmenten die zijn opgenomen in dit artikel en een koppeling tooa compleet codevoorbeeld aan Hallo einde die u kunt downloaden en uitvoeren.

## <a name="key-features-of-ra-grs"></a>Belangrijke functies van RA-GRS

Voordat we hoe uitleggen toouse RA-GRS-opslag, iets over de eigenschappen en het gedrag.

* Azure-opslag onderhoudt een alleen-lezen kopie van Hallo-gegevens die u in de primaire regio in een secundaire regio opslaat; zoals eerder vermeld, bepaalt de opslagservice Hallo Hallo-locatie van de secundaire regio Hallo.

* Hallo alleen-lezen kopie is [uiteindelijk consistent](https://en.wikipedia.org/wiki/Eventual_consistency) met gegevens in de primaire regio Hallo Hallo.

* Voor blobs, tabellen en wachtrijen, kunt u een query Hallo secundaire regio voor een *tijd van laatste synchronisatie* waarde die aangeeft wanneer de laatste replicatie Hallo van Hallo primaire toohello secundaire regio is opgetreden. (Dit wordt niet ondersteund voor Azure File storage die geen RA-GRS redundantie op dit moment.)

* U kunt Hallo Storage-clientbibliotheek toointeract gebruiken met Hallo-gegevens in beide Hallo primaire of secundaire regio. U kunt ook omleiden lezen aanvragen automatisch toohello secundaire regio als een leesaanvraag toohello primaire regio een optreedt time-out.

* Als er een grote probleem met betrekking tot toegankelijkheid Hallo Hallo-gegevens in de primaire regio hello, activeren hello Azure team mogelijk een geo-failover, waarna de clientzijdebewaking Hallo DNS-vermeldingen die wijst toohello primaire regio gewijzigde toopoint toohello secundaire regio worden.

* Als een geo-failover optreedt, wordt Azure selecteert u een nieuwe secundaire locatie en repliceren Hallo toothat gegevenslocatie vervolgens Hallo secundaire DNS-vermeldingen tooit verwijzen. secundair eindpunt Hallo is pas beschikbaar als Hallo storage-account is klaar met repliceren. Zie voor meer informatie [welke toodo als een Azure Storage-storing optreedt,](https://docs.microsoft.com/en-us/azure/storage/storage-disaster-recovery-guidance).

## <a name="application-design-considerations-when-using-ra-grs"></a>Toepassing Ontwerpoverwegingen bij het gebruik van RA-GRS

Hallo belangrijkste doel van dit artikel is tooshow u hoe een toepassing die toofunction (maar in een beperkte capaciteit) wordt voortgezet zelfs in geval van een noodgeval op de primaire gegevensbron Hallo Hallo toodesign center. U doen dit door uw toepassing toohandle tijdelijke of langdurige problemen door tooread overschakelen van de secundaire regio Hallo terwijl er een probleem is en weer schakelen wanneer de primaire regio Hallo weer beschikbaar is.

### <a name="using-eventually-consistent-data"></a>Met behulp van uiteindelijk consistent gegevens

Deze voorgestelde oplossing wordt ervan uitgegaan dat het is niet erg tooreturn wat verouderde gegevens toohello aanroepende toepassing kan worden. Omdat secundaire gegevens Hallo uiteindelijk consistent is, is het mogelijk dat Hallo-gegevens zijn geschreven toohello primaire maar Hallo update toohello secundaire niet was voltooid repliceren wanneer de primaire regio Hallo werd niet toegankelijk.

Bijvoorbeeld een update die is geslaagd door uw klant kan verzenden en vervolgens Hallo primaire kan uitvallen voordat hello update doorgegeven toohello secundaire is. In dit geval als Hallo klant wordt vervolgens gevraagd tooread Hallo gegevens terug, ontvangt hij Hallo verouderde gegevens in plaats van de gegevens van Hallo bijgewerkt. U moet beslissen als dit is acceptabel en zo ja, hoe u Hallo klant wordt weergegeven. U ziet hoe toocheck Hallo tijd van laatste synchronisatie op de secundaire gegevensbron Hallo verderop in dit artikel toosee als secundaire Hallo is bijgewerkt.

### <a name="handling-services-separately-or-all-together"></a>Afhandeling van de services afzonderlijk of Alles samenvoegen

Tijdens het niet waarschijnlijk is het mogelijk voor één service toobecome niet beschikbaar terwijl hello andere services nog steeds volledig functioneel zijn. U kunnen ingang Hallo pogingen en alleen-lezenmodus voor elke service afzonderlijk (blobs, wachtrijen, tabellen), of kunt u nieuwe pogingen algemeen voor alle Hallo storage-services tegelijk verwerken.

Bijvoorbeeld, als u wachtrijen en blobs in uw toepassing gebruikt, besluiten u tooput in afzonderlijke toohandle herstelbare codefouten voor elk van deze. Klik als u een nieuwe poging van Hallo blob-service krijgt, maar Hallo queue-service is nog steeds werken, worden slechts een deel van uw toepassing die verantwoordelijk is voor blobs Hallo beïnvloed. Als u besluit toohandle alle opslagservice algemeen pogingen en een aanroep toohello blob-service retourneert een herstelbare fout vervolgens aanvragen tooboth Hallo blob-service en Hallo queue-service worden beïnvloed.

Uiteindelijk hangt dit Hallo complexiteit van uw toepassing. Desgewenst kunt u geen toohandle Hallo fouten door service, maar in plaats daarvan tooredirect schijfleesaanvragen voor alle storage services toohello secundaire regio en Hallo-toepassing uitvoeren in de modus alleen-lezen wanneer u een probleem met een storage-service in de primaire regio Hallo detecteren.

### <a name="other-considerations"></a>Andere overwegingen

Dit zijn andere overwegingen worden besproken in de rest van dit artikel Hallo Hallo.

*   Verwerking van nieuwe pogingen van leesaanvragen Hallo Circuitonderbreker patroon

*   Uiteindelijk consistent gegevens en Hallo tijd van laatste synchronisatie

*   Testen

## <a name="running-your-application-in-read-only-mode"></a>Uitvoeren van uw toepassing in de modus alleen-lezen

toouse RA-GRS-opslag, moet de leesaanvragen kunnen toohandle beide is mislukt en mislukte updateaanvragen (met de update in dit geval betekenis invoeg-, updates en verwijderingen). Als hello primaire data center mislukt, lezen aanvragen kunnen worden omgeleid toohello secundaire Datacenter, maar verzoeken om te werken niet omdat Hallo secundaire alleen-lezen is. Daarom moet u enkele toorun manier uw toepassing in de modus alleen-lezen.

U kunt bijvoorbeeld een vlag die wordt gecontroleerd vóór het verzenden van een update aanvragen toohello storage-service instellen. Wanneer een van de aanvragen van Hallo bijwerken via komt, kunt u dit overslaan en retourneren een juiste reactie toohello klant. U kunt zelfs toodisable wilt bepaalde functies helemaal tot Hallo probleem opgelost is en laat gebruikers weten dat deze functies tijdelijk niet beschikbaar zijn.

Als u fouten toohandle voor elke service afzonderlijk, moet u ook toohandle Hallo mogelijkheid toorun uw toepassing in de modus alleen-lezen door de service. Er kan alleen-lezen vlaggen voor elke service die kunnen worden ingeschakeld en uitgeschakeld en ingang Hallo geschikte vlag op de juiste plaatsen Hallo in uw code.

Kan toorun wordt uw toepassing in de modus alleen-lezen heeft een ander voordeel van de zijde: dit biedt u Hallo mogelijkheid tooensure beperkte functionaliteit tijdens een upgrade van de primaire toepassing. U kunt uw toepassing toorun in alleen-lezen-modus en punt toohello secundaire Datacenter, activeren zodat niemand toegang heeft tot gegevens in de primaire regio Hallo Hallo terwijl u upgrades wilt aanbrengen.

## <a name="handling-updates-when-running-in-read-only-mode"></a>Verwerken van wijzigingen in de modus alleen-lezen

Er zijn veel manieren toohandle update aanvragen in de modus alleen-lezen. We dit uitvoerig won't verrekend, maar er zijn in het algemeen een aantal patronen waarmee u rekening houden.

1.  U kunt reageren tooyour gebruiker en laat dat u bent momenteel accepteert geen updates. Een contactpersoon beheersysteem klanten tooaccess contactgegevens inschakelen maar updates niet maken.

2.  U kunt de updates in een andere regio in de wachtrij plaatsen. In dit geval zou u de update in behandeling zijnde aanvragen tooa wachtrij schrijven in een andere regio en vervolgens hebben een tooprocess manier deze aanvragen nadat de primaire Datacenter Hallo online wordt gezet opnieuw. In dit scenario laat Hallo klant weten later worden verwerkt in de wachtrij staat Hallo update aangevraagd.

3.  U kunt updates van uw opslagaccount tooa schrijven in een andere regio. Wanneer de primaire Datacenter Hallo weer online komt, kunt hebt u een manier toomerge die updates in de primaire gegevens hello, afhankelijk van het Hallo-structuur van Hallo-gegevens. Bijvoorbeeld, als u afzonderlijke bestanden met een datum/tijd-stempel in de naam van de Hallo maakt, kunt u deze bestanden back toohello primaire regio. Dit werkt voor sommige werkbelastingen zoals logboekregistratie en iOT-gegevens.

## <a name="handling-retries"></a>Verwerking van nieuwe pogingen

Hoe wilt u weten welke fouten herstelbare? Dit wordt bepaald door de storage-clientbibliotheek Hallo. Een 404-fout (resource niet gevonden) is bijvoorbeeld niet-herstelbare omdat deze opnieuw proberen niet waarschijnlijk tooresult in geslaagd is. Op Hallo daarentegen een 500 fout is herstelbare omdat het een serverfout is opgetreden, en dit eenvoudig een tijdelijk probleem komen kan. Bekijk voor meer informatie Hallo [openen van de broncode voor Hallo ExponentialRetry klasse](https://github.com/Azure/azure-storage-net/blob/87b84b3d5ee884c7adc10e494e2c7060956515d0/Lib/Common/RetryPolicies/ExponentialRetry.cs) in Hallo .NET storage-clientbibliotheek. (Zoek naar Hallo ShouldRetry methode).

### <a name="read-requests"></a>Alleen aanvragen

Als er een probleem met de primaire opslag, kunnen alleen aanvragen omgeleide toosecondary opslag worden. Als opgemerkt in [uiteindelijk consistente gegevens met behulp van](#using-eventually-consistent-data), deze moet acceptabele voor uw toepassing toopotentially verouderde gegevens lezen. Als u Hallo opslag client bibliotheek tooaccess RA-GRS gegevens gebruikt, kunt u Hallo opnieuw gedrag van een leesaanvraag opgeven door een waarde voor Hallo **LocationMode** tooone van Hallo volgende eigenschap:

*   **PrimaryOnly** (Hallo standaard)

*   **PrimaryThenSecondary**

*   **SecondaryOnly**

*   **SecondaryThenPrimary**

Als u instelt dat Hallo **LocationMode** te**PrimaryThenSecondary**als eerste Hallo lezen aanvraag toohello primaire eindpunt is mislukt met een herstelbare fout, Hallo client maakt automatisch een andere lezen secundair eindpunt toohello aanvragen. Als Hallo-fout een time-out van de server is, klikt u vervolgens hebben Hallo client toowait voor Hallo time-out tooexpire voordat het een herstelbare fout van Hallo-service ontvangt.

Er zijn in feite twee scenario's tooconsider wanneer u bepaalt hoe toorespond tooa herstelbare fout:

*   Dit is een probleem met geïsoleerde en volgende aanvragen toohello primaire eindpunt niet een herstelbare fout retourneert. Een voorbeeld van wanneer dit gebeurt mogelijk is wanneer er een tijdelijke fout.

    In dit scenario wordt er is geen aanzienlijke prestaties voor het hebben van **LocationMode** instellen te**PrimaryThenSecondary** als dit alleen zelden gebeurt.

*   Dit is een probleem met ten minste één van de opslagservices Hallo in de primaire regio Hallo en alle volgende aanvragen toothat-service in de primaire regio Hallo zijn waarschijnlijk tooreturn herstelbare fouten voor een bepaalde periode. Een voorbeeld hiervan is als de primaire regio Hallo volledig niet toegankelijk.

    In dit scenario is het een op de prestaties omdat uw leesaanvragen wordt Probeer eerst de primaire eindpunt hello, op Hallo time-out tooexpire wachten en schakel toohello secundair eindpunt.

Voor deze scenario's, moet u bepalen dat er een lopende probleem met de primaire eindpunt Hallo en verzendt alle schijfleesaanvragen direct toohello secundair eindpunt door in te stellen Hallo **LocationMode** eigenschap te **SecondaryOnly**. Op dit moment moet u ook Hallo toepassing toorun in de modus alleen-lezen te wijzigen. Deze aanpak wordt ook wel Hallo [Circuitonderbreker patroon](https://msdn.microsoft.com/library/dn589784.aspx).

### <a name="update-requests"></a>Verzoeken om te werken

Hallo Circuitonderbreker patroon kan ook worden toegepast tooupdate aanvragen. Updateaanvragen kunnen echter niet dat omgeleide toosecondary-opslag alleen-lezen is. Voor deze aanvragen, laat u Hallo **LocationMode** eigenschappenset te**PrimaryOnly** (Hallo standaard). toohandle deze fouten kunt u een aanvragen metrische toothese – zoals 10 fouten in een rij – toepassen en als de drempelwaarde wordt voldaan, schakelt u Hallo-toepassing in de modus alleen-lezen. U kunt dezelfde methoden voor het retourneren van tooupdate-modus als die hieronder wordt beschreven in de volgende sectie Hallo over Hallo Circuitonderbreker patroon Hallo.

## <a name="circuit-breaker-pattern"></a>Patroon voor Circuitonderbreker

Hallo Circuitonderbreker patroon gebruiken in uw toepassing kunt voorkomen dat deze opnieuw wordt geprobeerd een bewerking die waarschijnlijk toofail herhaaldelijk is. Kunt u Hallo toepassing toocontinue toorun in plaats van tijd in beslag bij bewerking Hallo exponentieel wordt herhaald. Daarnaast wordt gedetecteerd wanneer Hallo-fout is opgelost, waarmee de toepassing hello Hallo opnieuw kunt proberen.

### <a name="how-tooimplement-hello-circuit-breaker-pattern"></a>Hoe tooimplement Circuitonderbreker patroon Hallo

tooidentify dat er een actieve probleem met een primaire eindpunt is, kunt u controleren hoe vaak Hallo client er een herstelbare fout optreedt. Omdat elk geval niet hetzelfde is, hebt u toodecide Hallo drempel toouse voor Hallo besluit tooswitch toohello secundair eindpunt en Hallo toepassing uitvoeren in de modus alleen-lezen. U kan bijvoorbeeld tooperform Hallo switch besluit als er 10 fouten in een rij met geen uitkomsten. Een ander voorbeeld is tooswitch als 90% van het Hallo-aanvragen in een periode van 2 minuten mislukken.

Voor het eerste scenario hello, kunt u gewoon een telling van fouten van Hallo houden en als er een geslaagde alvorens maximale, stel Hallo aantal back-toozero Hallo. Voor het tweede scenario Hallo Hallo eenrichtingssessie tooimplement is toouse MemoryCache-object (in .NET). Voor elke aanvraag een CacheItem toohello cache toevoegen, Hallo waarde toosuccess (1) ingesteld of mislukt (0) en Hallo verlopen tijd too2 minuten ingesteld van nu (of wat uw tijdsbeperking is). Wanneer een vermelding verlooptijd is bereikt, wordt Hallo-vermelding automatisch verwijderd. Hierdoor krijgt u een venster met rolling 2 minuten. Telkens wanneer u een aanvraag toohello storage-service u eerst gebruiken een Linq-query in Hallo MemoryCache object toocalculate Hallo percentage geslaagd door het Hallo-waarden op te tellen en te delen door Hallo aantal. Als percentage geslaagd Hallo zakt onder sommige drempelwaarde (zoals 10%), stelt u Hallo **LocationMode** eigenschap voor schijfleesaanvragen te**SecondaryOnly** en schakel over naar de toepassing hello in alleen-lezenmodus voordat u kunt doorgaan.

Hallo-drempelwaarde voor fouten gebruikt toodetermine wanneer toomake Hallo switch van service tooservice in uw toepassing, afwijken kan zodat u kunt overwegen om deze parameters kunnen worden geconfigureerd. Dit is ook u besluiten het toohandle herstelbare fouten van elke service afzonderlijk of als een, zoals eerder besproken.

Een andere overweging is hoe toohandle meerdere exemplaren van een toepassing, en welke toodo wanneer u herstelbare fouten in elke instantie detecteren. Bijvoorbeeld wellicht 20 VM's die worden uitgevoerd met Hallo dezelfde toepassing geladen. Verwerkt u elke instantie afzonderlijk? Als één exemplaar begint problemen, wilt u toch toolimit Hallo antwoord toojust dat één exemplaar of wilt u toch tootry toohave alle exemplaren reageren in Hallo dezelfde manier als één exemplaar een probleem is? Hallo exemplaren afzonderlijk verwerking is veel eenvoudiger dan het antwoord van toocoordinate Hallo onder te brengen, maar hoe u dit doen is afhankelijk van de architectuur van uw toepassing.

### <a name="options-for-monitoring-hello-error-frequency"></a>Opties voor het bewaken van Hallo fout frequentie

Hebt u drie belangrijkste mogelijkheden voor het bewaken van Hallo frequentie van nieuwe pogingen in de primaire regio Hallo in volgorde toodetermine wanneer tooswitch via toohello secundaire regio en wijzig Hallo toorun toepassing in de modus alleen-lezen.

*   Toevoegen van een handler voor Hallo [ **opnieuw proberen** ](http://msdn.microsoft.com/en-us/library/microsoft.windowsazure.storage.operationcontext.retrying.aspx) gebeurtenis op Hallo [ **OperationContext** ](http://msdn.microsoft.com/en-us/library/microsoft.windowsazure.storage.operationcontext.aspx) object u tooyour opslag aanvragen doorgeeft – dit Hallo is methode weergegeven in dit artikel en gebruikt in Hallo begeleidende voorbeeld. Deze gebeurtenissen worden geactiveerd wanneer het Hallo-client een aanvraag opnieuw, zodat u hoe vaak tootrack Hallo client herstelbare fouten op een primaire eindpunt optreedt.

    ```csharp 
    operationContext.Retrying += (sender, arguments) =>
    {
        // Retrying in hello primary region
        if (arguments.Request.Host == primaryhostname)
            ...
    };
    ```

*   In Hallo [ **Evaluate** ](http://msdn.microsoft.com/en-us/library/microsoft.windowsazure.storage.retrypolicies.iextendedretrypolicy.evaluate.aspx) methode in een beleid voor aangepaste opnieuw proberen, kunt u aangepaste code uitvoeren telkens wanneer een nieuwe poging plaatsvindt. In aanvulling toorecording wanneer een nieuwe poging gebeurt, wordt dit ook hebt u kans toomodify Hallo uw gedrag voor het opnieuw.

    ```csharp 
    public RetryInfo Evaluate(RetryContext retryContext,
    OperationContext operationContext)
    {
        var statusCode = retryContext.LastRequestResult.HttpStatusCode;
        if (retryContext.CurrentRetryCount >= this.maximumAttempts
        || ((statusCode &gt;= 300 && statusCode &lt; 500 && statusCode != 408)
        || statusCode == 501 // Not Implemented
        || statusCode == 505 // Version Not Supported
            ))
        {
        // Do not retry
            return null;
        }

        // Monitor retries in hello primary location
        ...

        // Determine RetryInterval and TargetLocation
        RetryInfo info =
            CreateRetryInfo(retryContext.CurrentRetryCount);

        return info;
    }
    ```

*   Hallo derde aanpak is een aangepaste bewakingsonderdeel in uw toepassing die voortdurend uw eindpunt primaire opslag met dummy pingt tooimplement toodetermine aanvragen (zoals het lezen van een kleine blob) de status lezen. Deze zou resources, maar een aanzienlijke duren. Wanneer een probleem is gedetecteerd dat de drempel bereikt, u wilt uitvoeren, Hallo switch te**SecondaryOnly** en alleen-lezen-modus.

Op een bepaald moment zult u tooswitch back toousing Hallo primaire eindpunt en updates toestaan. Als een van de eerste twee methoden Hallo die hierboven worden genoemd, kan u gewoon overschakelen back toohello primaire eindpunt en updatemodus inschakelen nadat een willekeurig geselecteerde hoeveelheid tijd of het aantal bewerkingen zijn uitgevoerd. Vervolgens kunt u deze opnieuw Hallo Pogingslogica doorlopen. Als Hallo probleem is opgelost, wordt de toouse Hallo primaire eindpunt gaan en updates toestaan. Als u nog steeds een probleem is, zal deze zodra er meer back toohello secundaire eindpunt en alleen-lezenmodus overschakelen lukt Hallo criteria die u hebt ingesteld.

Hallo derde scenario wanneer pingen Hallo primaire opslag eindpunt weer mislukt, kunt u activeren Hallo switch terug te**PrimaryOnly** en doorgaan updates toestaan.

## <a name="handling-eventually-consistent-data"></a>Uiteindelijk consistente gegevens verwerken

RA-GRS werkt door transacties van Hallo primaire toohello secundaire regio te repliceren. Dit replicatieproces zorgt ervoor dat gegevens in de secundaire regio Hallo Hallo is *uiteindelijk consistent*. Dit betekent dat alle Hallo transacties in de primaire regio Hallo uiteindelijk wordt weergegeven in de secundaire regio hello, maar dat er mogelijk een vertraging voordat ze worden weergegeven en of er is geen garantie Hallo transacties binnenkomen in de secundaire regio Hallo in dezelfde als volgorde Hallo die waarin ze oorspronkelijk zijn toegepast in de primaire regio Hallo. Als uw transacties in de secundaire regio Hallo volgorde plaatsvinden, u *mogelijk* Houd rekening met uw gegevens in Hallo secundaire regio toobe in een inconsistente status totdat het Hallo-service de resultaten.

Hallo volgende tabel toont een voorbeeld van wat er gebeuren kan wanneer u de details van een werknemer toomake Hallo bijwerken haar lid zijn van Hallo *beheerders* rol. Voor Hallo mogelijk te houden in dit voorbeeld, hiervoor moet u bijwerken Hallo **werknemer** entiteit en update een **beheerdersrol** entiteit met een telling van totaal aantal beheerders Hallo. U ziet hoe Hallo updates volgorde in Hallo secundaire regio worden toegepast.

| **Tijd** | **Transactie**                                            | **Replicatie**                       | **Tijd van laatste synchronisatie** | **Resultaat** |
|----------|------------------------------------------------------------|---------------------------------------|--------------------|------------| 
| T0       | Transactie A: <br> Werknemer invoegen <br> entiteit in primaire |                                   |                    | Een transactie ingevoegd tooprimary,<br> nog niet gerepliceerd. |
| T1       |                                                            | Een transactie <br> gerepliceerd naar<br> secundaire | T1 | Een transactie toosecondary gerepliceerd. <br>Tijd van laatste synchronisatie is bijgewerkt.    |
| T2       | Transactie B:<br>Update<br> werknemer-entiteit<br> in primaire  |                                | T1                 | Transactie B tooprimary, geschreven<br> nog niet gerepliceerd.  |
| T3       | Transactie C:<br> Update <br>Beheerder<br>de entiteit rol in<br>primaire |                    | T1                 | Transactie C tooprimary, geschreven<br> nog niet gerepliceerd.  |
| *T4*     |                                                       | Transactie C <br>gerepliceerd naar<br> secundaire | T1         | Transactie C toosecondary gerepliceerd.<br>LastSyncTime niet bijgewerkt, omdat <br>transactie B is nog niet gerepliceerd.|
| *T 5*     | Entiteiten lezen <br>secundaire                           |                                  | T1                 | U opvragen Hallo verouderde waarde voor werknemer <br> entiteit omdat de transactie B nog niet <br> nog gerepliceerd. Ophalen van de nieuwe waarde Hallo voor<br> Administrator-rol entiteit omdat C<br> gerepliceerd. Tijd van laatste synchronisatie is nog steeds niet<br> is bijgewerkt, omdat de transactie B<br> nog niet gerepliceerd. U kunt zien de<br>Administrator-rol entiteit komt niet overeen <br>omdat Hallo entiteit datum/tijd na <br>Hallo tijd van laatste synchronisatie. |
| *T6*     |                                                      | Transactie B<br> gerepliceerd naar<br> secundaire | T6                 | *T6* – alle transacties via C hebben <br>zijn gerepliceerd, tijd van laatste synchronisatie<br> is bijgewerkt. |

In dit voorbeeld wordt ervan uitgegaan Hallo client switches tooreading van de secundaire regio Hallo op t 5. Het Hallo kan lezen **beheerdersrol** entiteit op dit moment maar Hallo entiteit bevat een waarde voor Hallo aantal beheerders die is niet consistent met de Hallo aantal **werknemer** entiteiten die zijn gemarkeerd als beheerders in de secundaire regio Hallo op dit moment. De client kan deze waarde, met Hallo risico dat het inconsistente informatie is gewoon weergeven. U kunt ook Hallo-client kan proberen toodetermine die Hallo **beheerdersrol** heeft een mogelijk inconsistente status omdat het Hallo-updates is een ongeldige volgorde en vervolgens informeert Hallo gebruiker van dit feit.

toorecognize dat er mogelijk inconsistente gegevens, Hallo-client kunt Hallo waarde gebruiken Hallo *tijd van laatste synchronisatie* dat u op elk gewenst moment ophalen kunt door het opvragen van een storage-service. Weet u Hallo tijd waarop het Hallo-gegevens in de secundaire regio Hallo laatst consistent en wanneer Hallo service waren toegepast alle transacties voorafgaande toothat punt in tijd Hallo. In het bovenstaande nadat het Hallo-service wordt ingevoegd Hallo voorbeeld Hallo **werknemer** entiteit in de secundaire regio Hallo Hallo tijd van laatste synchronisatie is ingesteld te*T1*. Blijft *T1* totdat het Hallo-service-updates voor Hallo **werknemer** entiteit in de secundaire regio hello te is ingesteld*T6*. Als client Hallo Hallo tijd van laatste synchronisatie Hallo-entiteit bij het lezen opgehaald *t 5*, deze kan worden vergeleken met Hallo tijdstempel op Hallo entiteit. Als Hallo tijdstempel op Hallo entiteit later dan Hallo is gesynchroniseerd op tijd, en vervolgens hello entiteit is een mogelijk inconsistente status heeft en u kunt nemen wat de juiste actie Hallo voor uw toepassing is. In dit veld is vereist dat u weet wanneer Hallo laatste update toohello primaire is voltooid.

## <a name="testing"></a>Testen

Het is belangrijk tootest die uw toepassing werkt zoals verwacht wanneer herstelbare fouten worden aangetroffen. Bijvoorbeeld, moet u tootest die toepassing switches toohello secundaire hello en in de modus alleen-lezen wanneer er een probleem gedetecteerd en activeren wanneer de primaire regio Hallo weer beschikbaar is. toodo, u moet een manier toosimulate herstelbare fouten en bepalen hoe vaak ze voorkomen.

U kunt [Fiddler](http://www.telerik.com/fiddler) toointercept en HTTP-antwoorden in een script te wijzigen. Dit script kunt identificeren van reacties die afkomstig van uw primaire eindpunt zijn en wijzig Hallo HTTP-status code tooone die Hallo die Storage-clientbibliotheek wordt herkend als een herstelbare fout. Dit codefragment toont een eenvoudig voorbeeld van een script Fiddler die antwoorden tooread aanvragen op basis van Hallo onderschept **employeedata** tabel tooreturn status 502:

```java
static function OnBeforeResponse(oSession: Session) {
    ...
    if ((oSession.hostname == "\[yourstorageaccount\].table.core.windows.net")
      && (oSession.PathAndQuery.StartsWith("/employeedata?$filter"))) {
        oSession.responseCode = 502;
    }
}
```

U kan een groter aantal aanvragen voor dit voorbeeld toointercept uitbreiden en alleen wijzigen Hallo **responseCode** op sommige van deze toobetter een Praktijkscenario simuleren. Zie voor meer informatie over het aanpassen van Fiddler scripts [wijzigen van een aanvraag of antwoord](http://docs.telerik.com/fiddler/KnowledgeBase/FiddlerScript/ModifyRequestOrResponse) in Hallo Fiddler documentatie.

Als u hebt aangebracht Hallo drempelwaarden voor het overschakelen van uw toepassing tooread alleen-lezen-modus worden geconfigureerd, worden deze eenvoudiger tootest Hallo gedrag met niet-productieve transactie volumes.

## <a name="next-steps"></a>Volgende stappen

* Zie voor meer informatie over leestoegang geografische redundantie, met inbegrip van een ander voorbeeld van hoe Hallo LastSyncTime is ingesteld, neem [Windows Azure-opslagopties redundantie en geografisch redundante opslag met leestoegang](https://blogs.msdn.microsoft.com/windowsazurestorage/2013/12/11/windows-azure-storage-redundancy-options-and-read-access-geo-redundant-storage/).

* Zie voor een compleet codevoorbeeld die laat zien hoe toomake heen en weer schakelen tussen de primaire en secundaire eindpunten Hallo Hallo, [Azure Samples – met Hallo Circuitonderbreker patroon met RA-GRS storage](https://github.com/Azure-Samples/storage-dotnet-circuit-breaker-pattern-ha-apps-using-ra-grs).
