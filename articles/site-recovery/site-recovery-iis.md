---
title: aaaReplicate een meerlaagse IIS-webtoepassing met Azure Site Recovery gebaseerd | Microsoft Docs
description: Dit artikel wordt beschreven hoe tooreplicate IIS web-farm virtuele machines met Azure Site Recovery.
services: site-recovery
documentationcenter: 
author: nsoneji
manager: gauravd
editor: 
ms.assetid: 
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: nisoneji
ms.openlocfilehash: 1974265b3cb05f6dc57049876306d2e08424bb97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-a-multi-tier-iis-based-web-application-using-azure-site-recovery"></a>Een meerlaagse op basis van IIS-webtoepassing met Azure Site Recovery repliceren

## <a name="overview"></a>Overzicht


Toepassingssoftware is Hallo-engine van de zakelijke productiviteit in een organisatie. Verschillende webtoepassingen kunnen een ander doel in een organisatie. Sommige van deze zoals salarissen verwerking, financiële toepassingen en websites klantgerichte kan zoveel mogelijk zijn essentieel voor een organisatie. Dit is belangrijk voor Hallo organisatie toohave deze en worden uitgevoerd op alle tijden tooprevent verlies van productiviteit en meer belangrijker nog voorkomen dat geen afbeelding schade toohello merk van Hallo-organisatie.

Kritieke webtoepassingen zijn meestal ingesteld als toepassingen met meerdere lagen met Hallo web, de database en de toepassing op andere niveaus. Naast wordt verdeeld over verschillende lagen, Hallo toepassingen mogelijk ook gebruik van meerdere servers in elke laag tooload saldo Hallo-verkeer. Hallo toewijzingen tussen verschillende lagen en op de webserver Hallo kunnen bovendien worden gebaseerd op vaste IP-adressen. Op failover moet sommige van deze toewijzingen toobe bijgewerkt, met name, als er meerdere websites op de webserver Hallo geconfigureerd. In geval van webtoepassingen met SSL moet-certificaatbindingen toobe bijgewerkt.

Traditionele niet-replicatie op basis herstelmethoden hebben betrekking op een back-up van de verschillende configuratiebestanden, registerinstellingen, bindingen, aangepaste onderdelen (COM of .NET), inhoud en ook certificaten en herstellende Hallo bestanden via een set van handmatige stappen. Deze technieken worden duidelijk lastige fout foutgevoelige en niet schaalbaar. Het is bijvoorbeeld eenvoudig mogelijk dat u tooforget back-ups van certificaten en laten staan geen keuze maar toobuy nieuwe certificaten voor Hallo server na een failover.

Een goede noodhersteloplossing moet modellering van herstelplannen rond Hallo hierboven architecturen voor complexe toepassingen bevatten en ook Hallo mogelijkheid tooadd aangepast stappen toohandle Toepassingstoewijzingen tussen verschillende lagen daarom bieden een één klik ervoor oplossing maken in geval van een noodgeval voorloopspaties tooa Hallo RTO verlagen.


Dit artikel wordt beschreven hoe tooprotect een IIS op basis van web-toepassing gebruikt een [Azure Site Recovery](site-recovery-overview.md). Dit artikel wordt aanbevolen procedures voor het repliceren van een drielaagse uitgelegd IIS op basis van web application tooAzure, hoe u een herstel na noodgevallen detailanalyse kunt doen en hoe kunt u failover Hallo toepassing tooAzure.


## <a name="prerequisites"></a>Vereisten

Voordat u begint, zorg er dan voor dat u begrijpt Hallo volgende:

1. [Een virtuele machine tooAzure repliceren](site-recovery-vmware-to-azure.md)
1. Hoe te[ontwerpen van een netwerk herstel](site-recovery-network-design.md)
1. [Tijdens het doorzoeken van een failover-test tooAzure](./site-recovery-test-failover-to-azure.md)
1. [Tijdens het doorzoeken van een failover-tooAzure](site-recovery-failover.md)
1. Hoe te[repliceren van een domeincontroller](site-recovery-active-directory.md)
1. Hoe te[SQL-Server repliceren](site-recovery-sql.md)

## <a name="deployment-patterns"></a>Implementaties
Hier volgt doorgaans een webtoepassing IIS op basis van een van de volgende implementaties Hallo:

** Implementatie patroon 1 ** webfarm met toepassing aanvragen Routing(ARR), IIS-Server en Microsoft SQL Server op basis van een IIS.

![Patroon van de implementatie](./media/site-recovery-iis/deployment-pattern1.png)

**Implementatie-patroon 2** webfarm met toepassing aanvragen Routing(ARR), IIS-Server, Application Server en Microsoft SQL Server op basis van een IIS.


![Patroon van de implementatie](./media/site-recovery-iis/deployment-pattern2.png)

## <a name="site-recovery-support"></a>Site Recovery-ondersteuning

Voor het doel van het maken van dit artikel virtuele VMware-machines met IIS-Server versie 7.5 op Windows Server 2012 R2 Enterprise Hallo zijn gebruikt. Als de replicatie van site recovery networkdirect van toepassing is, voorziet in Hallo aanbevelingen zijn hier verwachte toohold op de volgende scenario's evenals en voor andere versie van IIS.

### <a name="source-and-target"></a>Bron en doel

**Scenario** | **de secundaire site tooa** | **tooAzure**
--- | --- | ---
**Hyper-V** | Ja | Ja
**VMware** | Ja | Ja
**Fysieke server** | Nee | Ja

## <a name="replicate-virtual-machines"></a>Virtuele machines repliceren

Ga als volgt [in deze richtlijnen](site-recovery-vmware-to-azure.md) toostart tooAzure alle Hallo IIS web farm virtuele machines repliceren.

Als u met behulp van een statische IP-adres opgeven Hallo IP die u wilt dat virtuele machine tootake in Hallo Hallo [ **IP-adres doel** ](./site-recovery-replicate-vmware-to-azure.md#view-and-manage-vm-properties) instellen in de berekenings-en netwerkinstellingen.

![Doel-IP](./media/site-recovery-active-directory/dns-target-ip.png)


## <a name="creating-a-recovery-plan"></a>Een herstelplan maken

Een herstelplan kunt Hallo failover van de verschillende lagen in een toepassing met meerdere lagen, daarom toepassing consistentie van de sequentiëren. Ga als volgt Hallo onderstaande stappen te volgen bij het maken van een herstelplan voor een webtoepassing met meerdere lagen.  [Meer informatie over het maken van een herstelplan](./site-recovery-create-recovery-plans.md).

### <a name="adding-virtual-machines-toofailover-groups"></a>Toevoegen van virtuele machines toofailover groepen
Een typische meerdere lagen IIS-webtoepassing bestaat uit een databaselaag met SQL-virtuele machines, Hallo weblaag gevormd door een IIS-server en een toepassingslaag. Alle deze virtuele machines toodifferent groep toevoegen op basis van een laag als hieronder. [Meer informatie over het aanpassen van herstelplan](site-recovery-runbook-automation.md#customize-the-recovery-plan).

1. Een herstelplan maken. Hallo database laag virtuele machines onder groep 1 tooensure dat zij afsluiten laatste en eerste gebracht toevoegen.

1. Hallo toepassing laag virtuele machines onder groep 2 toevoegen zodat ze beschikbaar komen nadat Hallo databaselaag opstarten.

1. Hallo web laag virtuele machines toevoegen in de groep 3, zodat ze beschikbaar komen nadat de toepassingslaag Hallo opstarten.

1. Load balance virtuele machines in de groep 4 toevoegen zodat ze beschikbaar komen nadat de weblaag Hallo opstarten.


### <a name="adding-scripts-toohello-recovery-plan"></a>Het herstelplan toohello toe te voegen scripts
U moet mogelijk toodo bepaalde bewerkingen op virtuele Azure-machines na failover en testen failover toomake IIS web farm functie Hallo correct. U kunt automatiseren Hallo post failoverbewerking zoals het bijwerken van DNS-vermelding sitebinding wijzigen, wijzigen in de verbindingsreeks door de bijbehorende scripts toevoegen in het herstelplan Hallo zoals hieronder. [Meer informatie over het toevoegen van herstelplan script](./site-recovery-create-recovery-plans.md#add-scripts).

#### <a name="dns-update"></a>DNS-updates
Als Hallo DNS is geconfigureerd voor dynamische DNS-updates vervolgens Hallo DNS virtuele machines meestal met de nieuwe IP-adres Hallo werkt zodra ze starten. Als u wilt dat een expliciete stap tooupdate DNS-Hello tooadd nieuwe IP-adressen van virtuele machines van Hallo voegt u dit [tooupdate IP-adres in DNS-script](https://aka.ms/asr-dns-update) als een post-actie op herstel planningsgroepen.  

#### <a name="connection-string-in-an-applications-webconfig"></a>De verbindingsreeks in het bestand web.config van de toepassing
Hallo-verbindingsreeks bevat Hallo-database die website Hallo communiceert met.

Als verbindingsreeks Hallo Hallo-naam van Hallo database virtuele machine uitvoert, worden geen verdere stappen nodig na failover en Hallo toepassing kan worden gecommuniceerd tooautomatically toohello DB. Ook als Hallo IP-adres voor Hallo database virtuele machine wordt bewaard, is het niet langer nodig tooupdate Hallo-verbindingsreeks. Als het Hallo-verbindingsreeks verwijst toohello database virtuele machine een IP-adres, moet deze toobe bijgewerkt na failover. Bijvoorbeeld Hallo hieronder verbindingsreeks verwijst toohello DB met IP-adres 127.0.1.2

        <?xml version="1.0" encoding="utf-8"?>
        <configuration>
        <connectionStrings>
        <add name="ConnStringDb1" connectionString="Data Source= 127.0.1.2\SqlExpress; Initial Catalog=TestDB1;Integrated Security=False;" />
        </connectionStrings>
        </configuration>

U kunt Hallo-verbindingsreeks in de weblaag bijwerken door toe te voegen [updatescript voor IIS verbinding](https://aka.ms/asr-update-webtier-script-classic) na groep 3 in het herstelplan Hallo.

#### <a name="site-bindings-for-hello-application"></a>Sitebindingen voor de toepassing hello
Elke site bestaat uit het binden van informatie met Hallo-type van de binding, Hallo IP-adres op welke Hallo IIS-server toohello aanvragen voor Hallo-site, Hallo-poortnummer en hostnamen Hallo voor Hallo-site luistert. Bij Hallo een failover moet deze bindingen mogelijk toobe bijgewerkt als er een wijziging in Hallo IP-adres is gekoppeld.

> [!NOTE]
>
> Als u hebt gemarkeerd 'alle niet-toegewezen' voor de sitebinding Hallo Hallo voorbeeld hieronder, hoeft u niet tooupdate deze binding post voor failover. Ook als Hallo IP-adres die zijn gekoppeld aan een site niet is gewijzigd na failover, Hallo sitebinding moet niet worden bijgewerkt (bewaren van Hallo IP-adres, is afhankelijk van Hallo netwerkarchitectuur en subnetten toegewezen toohello primaire en herstelsites en daarom kunnen of kunnen niet mogelijk voor uw organisatie.)

![SSL-Binding](./media/site-recovery-iis/sslbinding.png)

Als u Hallo IP-adres aan een site hebt gekoppeld, moet u tooupdate alle sitebindingen met Hallo nieuwe IP-adres. U kunt toevoegen [updatescript voor IIS-webserver laag](https://aka.ms/asr-web-tier-update-runbook-classic) na groep 3 in recovery plan toochange Hallo sitebindingen.


#### <a name="update-load-balancer-ip-address"></a>IP-adres van load balancer bijwerken
Als u routering van toepassingsaanvragen virtuele machine hebt, voegt u [IIS ARR failover script](https://aka.ms/asr-iis-arrtier-failover-script-classic) na groep 4 tooupdate Hallo IP-adres.

#### <a name="hello-ssl-cert-binding-for-an-https-connection"></a>Hallo SSL-certificaat-binding voor een https-verbinding
Websites kan een bijbehorende SSL-certificaat die helpt om een veilige communicatie tussen het Hallo-webserver en de browser van de gebruiker Hallo hebben. Als het Hallo-website een https-verbinding en een bijbehorende https site binding toohello IP-adres van Hallo IIS-server met een SSL-certificaat-binding heeft, moet een nieuwe sitebinding toobe toegevoegd voor HALLO cert Hello IP-adres van Hallo IIS-virtuele machine na de failover.

Hallo SSL-certificaat kan worden uitgegeven tegen-

een) Hallo volledig gekwalificeerde domeinnaam van Hallo-website<br>
b) naam van de Hallo van Hallo-server<br>
c) een jokertekencertificaat voor Hallo-domeinnaam<br>
d) een IP-adres – als Hallo SSL-certificaat is uitgegeven voor Hallo IP-adres van Hallo IIS-server, een andere behoeften toobe van de SSL-certificaat dat is uitgegeven voor Hallo IP-adres van Hallo IIS-server op Hallo Azure site en een extra SSL-binding voor dit certificaat toobe gemaakt moet. Het is dus raadzaam toonot gebruiken een SSL-certificaat is uitgegeven voor de IP. Dit is een minder gebruikte optie en snel aan de hand van nieuwe wijzigingen van de CA/browser forum wordt afgeschaft.

#### <a name="update-hello-dependency-between-hello-web-and-hello-application-tier"></a>Hallo-afhankelijkheid tussen Hallo web- en Hallo toepassingslaag bijwerken
Als u een specifieke afhankelijkheid van toepassing op basis van IP-adres Hallo Hallo virtuele machines hebt, moet u tooupdate deze afhankelijkheid post voor failover.

## <a name="doing-a-test-failover"></a>Een testfailover uitvoeren
Ga als volgt [in deze richtlijnen](site-recovery-test-failover-to-azure.md) toodo een testfailover.

1.  Ga tooAzure portal en selecteer de Recovery Services-kluis.
1.  Klik op Hallo herstelplan is gemaakt voor IIS-webfarm.
1.  Klik op 'Testfailover'.
1.  Selecteer herstelpunt en het virtuele netwerk van Azure toostart Hallo test failover-proces.
1.  Wanneer secundaire Hallo-omgeving is, kunt u uw validaties kunt uitvoeren.
1.  Zodra Hallo validaties voltooid zijn, kunt u 'Validaties voltooid' en de testfailoveromgeving hello wordt gereinigd.

## <a name="doing-a-failover"></a>U een failover uitvoert
Ga als volgt [in deze richtlijnen](site-recovery-failover.md) bij het uitvoeren van een failover.

1.  Ga tooAzure portal en selecteer de Recovery Services-kluis.
1.  Klik op Hallo herstelplan is gemaakt voor IIS-webfarm.
1.  Klik op 'Failover'.
1.  Selecteer herstelproces punt toostart Hallo failover.

## <a name="next-steps"></a>Volgende stappen
U kunt meer lezen over [andere toepassingen repliceren](site-recovery-workload.md) met Site Recovery.
