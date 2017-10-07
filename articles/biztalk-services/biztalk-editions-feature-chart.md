---
title: aaaLearn over functies in de edities van BizTalk Services | Microsoft Docs
description: 'Hallo-mogelijkheden van edities van BizTalk Services Hallo vergelijken: vrijmaken, Developer, Basic, Standard en Premium. MABS, WABS.'
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: c589629f-06b1-44bb-b8ca-1db71826ea59
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: 81626fa743a7190e7c78a0fd90b3054a08982b02
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="biztalk-services-editions-chart"></a>BizTalk Services: grafiek van edities

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

Azure BizTalk Services is beschikbaar in verschillende edities. Gebruik dit artikel toodetermine welke editie geschikt voor uw scenario en zakelijke behoeften is.

## <a name="compare-hello-editions"></a>Hallo-edities vergelijken
**Free (Preview)**

Kan hybride verbindingen maken en beheren. Een hybride verbinding is een eenvoudige manier tooconnect een Azure-website tooan on-premises systeem, zoals SQL Server.

**Developer**

Biedt hybride verbindingen, EAI- en EDI-berichtverwerking met een eenvoudig te gebruiken beheerportal voor handelspartners, ondersteuning voor algemene EDI-schema's en uitgebreide EDI-bewerking via X12 en AS2. Algemene EAI-scenario's verbinden van services in de cloud Hallo met een HTTP/S-, REST-, FTP-, WCF- en SFTP-protocollen tooread maakt en berichten schrijven.  Gebruikmaken van connectiviteit tooon-premises LOB-systemen met kant-en-klare SAP, Oracle eBusiness, Oracle DB, Siebel en SQL Server-netwerkadapters. Gebruik een op ontwikkelaars gerichte omgeving met Visual Studio-hulpprogramma’s, zodat u op een eenvoudige manier kunt ontwikkelen en implementeren. Beperkte toodevelopment- en testdoeleinden alleen met niets Service Level Agreement (SLA).

**Basic**

Bevat de meeste mogelijkheden voor Hallo Developer met verbeterde hybride verbindingen, EAI-bruggen, EDI-overeenkomsten en BizTalk Adapter Pack-verbindingen. Biedt ook hoge beschikbaarheid en Hallo optie tooscale met een Service Level Agreement (SLA).

**Standard**

Bevat alle Hallo essentiële mogelijkheden met verbeterde hybride verbindingen, EAI-bruggen, EDI-overeenkomsten en BizTalk Adapter Pack-verbindingen. Biedt ook hoge beschikbaarheid en Hallo optie tooscale met een Service Level Agreement (SLA).

**Premium**

Bevat alle Hallo standaard mogelijkheden met verbeterde hybride verbindingen, EAI-bruggen, EDI-overeenkomsten en BizTalk Adapter Pack-verbindingen. Omvat ook archivering, hoge beschikbaarheid en Hallo optie tooscale met een Service Level Agreement (SLA).

## <a name="editions-chart"></a>Grafiek van edities
Hallo bevat volgende tabel Hallo verschillen.

<table border="1">
<tr bgcolor="FAF9F9">
        <th></th>
        <th>Free (voorbeeld)</th>
        <th>Developer</th>
        <th>Basic</th>
        <th>Standard</th>
        <th>Premium</th>
</tr>

<tr>
<td><strong>Beginprijs</strong></td>
<td colspan="5"><a HREF="http://go.microsoft.com/fwlink/p/?LinkID=304011"> Prijzen van Azure BizTalk Services</a> <br/><br/> <a HREF="http://azure.microsoft.com/pricing/calculator/?scenario=full"> Azure-prijscalculator</a></td>
</tr>
<tr>
<td><strong>Minimale standaardconfiguratie</strong></td>
<td>1 Free-eenheid</td>
<td>1 Developer-eenheid</td>
<td>1 Basic-eenheid</td>
<td>1 Standard-eenheid</td>
<td>1 Premium-eenheid</td>
</tr>
<tr>
<td><strong>Schalen</strong></td>
<td>Schalen niet mogelijk</td>
<td>Schalen niet mogelijk</td>
<td>Ja, in stappen van 1 Basic-eenheid</td>
<td>Ja, in stappen van 1 Standard-eenheid</td>
<td>Ja, in stappen van 1 Premium-eenheid</td>
</tr>
<tr>
<td><strong>Maximaal toegestane uitschaling</strong></td>
<td>Schalen niet mogelijk</td>
<td>Schalen niet mogelijk</td>
<td>Too8-eenheden</td>
<td>Too8-eenheden</td>
<td>Too8-eenheden</td>
</tr>
<tr>
<td><strong>EAI-bruggen per eenheid</strong></td>
<td>Niet inbegrepen</td>
<td>25</td>
<td>25</td>
<td>125</td>
<td>500</td>
</tr>
<tr>
<td><strong>EDI, AS2</strong>
<br/><br/>
Inclusief TPM-overeenkomsten</td>
<td>Niet inbegrepen</td>
<td>Inbegrepen. 10 overeenkomsten per eenheid.</td>
<td>Inbegrepen. 50 overeenkomsten per eenheid.</td>
<td>Inbegrepen. 250 overeenkomsten per eenheid.</td>
<td>Inbegrepen. 1000 overeenkomsten per eenheid.</td>
</tr>
<tr>
<td><strong>Hybride verbindingen per eenheid</strong></td>
<td>5</td>
<td>5</td>
<td>10</td>
<td>50</td>
<td>100</td>
</tr>
<tr>
<td><strong>Gegevensoverdracht in hybride verbindingen (GB) per eenheid</strong></td>
<td>5</td>
<td>5</td>
<td>50</td>
<td>250</td>
<td>500</td>
</tr>
<tr>
<td><strong>BizTalk Adapter Service verbindingen tooon-premises LOB-systemen</strong></td>
<td>Niet inbegrepen</td>
<td>1 verbinding</td>
<td>2 verbindingen</td>
<td>5 verbindingen</td>
<td>25 verbindingen</td>
</tr>
<tr>
<td align="left"><strong>Ondersteunde protocollen/systemen:</strong>
<ul>
<li>HTTP</li>
<li>HTTPS</li>
<li>FTP</li>
<li>SFTP</li>
<li>WCF</li>
<li>Service Bus (SB)</li>
<li>Azure Blob</li>
<li>REST-API’s</li>
</ul>
</td>
<td>Niet inbegrepen</td>
<td>Inbegrepen</td>
<td>Inbegrepen</td>
<td>Inbegrepen</td>
<td>Inbegrepen</td>
</tr>
<tr>
<td><strong>Hoge beschikbaarheid</strong>
<br/><br/>
Voor Service Level Agreements (SLA) raadpleegt u <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=304011">Prijzen van Azure BizTalk Services</a>.
</td>
<td>Niet inbegrepen</td>
<td>Niet inbegrepen</td>
<td>Inbegrepen</td>
<td>Inbegrepen</td>
<td>Inbegrepen</td>
</tr>
<tr>
<td><strong>Back-up en herstel</strong></td>
<td>Niet inbegrepen</td>
<td>Inbegrepen</td>
<td>Inbegrepen</td>
<td>Inbegrepen</td>
<td>Inbegrepen</td>
</tr>
<tr>
<td><strong>Tracering</strong></td>
<td>Niet inbegrepen</td>
<td>Inbegrepen</td>
<td>Inbegrepen</td>
<td>Inbegrepen</td>
<td>Inbegrepen</td>
</tr>
<tr>
<td><strong>Archiveren</strong><br/><br/>
Inclusief niet-afwijzing van ontvangst (NRR) en downloaden van getraceerde berichten</td>
<td>Niet inbegrepen</td>
<td>Inbegrepen</td>
<td>Niet inbegrepen</td>
<td>Niet inbegrepen</td>
<td>Inbegrepen</td>
</tr>
<tr>
<td><strong>Gebruik van aangepaste code</strong></td>
<td>Niet inbegrepen</td>
<td>Inbegrepen</td>
<td>Inbegrepen</td>
<td>Inbegrepen</td>
<td>Inbegrepen</td>
</tr>
<tr>
<td><strong>Gebruik van transformaties, waaronder aangepaste XSLT</strong></td>
<td>Niet inbegrepen</td>
<td>Inbegrepen</td>
<td>Inbegrepen</td>
<td>Inbegrepen</td>
<td>Inbegrepen</td>
</tr>
</table>

> [!NOTE]
> Voor tolerantie tegen hardwarestoringen en hoge beschikbaarheid moet één BizTalk-eenheid meerdere virtuele machines bevatten.
> 
> 

## <a name="faqs"></a>Veelgestelde vragen
#### <a name="what-is-a-biztalk-unit"></a>Wat is een BizTalk-eenheid?
Een 'eenheid' is hello kern van de implementatie van een Azure BizTalk Services. Elke editie wordt geleverd met een eenheid met een andere rekencapaciteit en hoeveelheid geheugen. Een Basic-eenheid heeft bijvoorbeeld meer rekencapaciteit dan een Developer-eenheid, een Standard-eenheid heeft meer rekencapaciteit dan een Basic-eenheid, enzovoort. Wanneer u een BizTalk Service schaalt, schaalt u de eenheden.

#### <a name="what-is-hello-difference-between-biztalk-services-and-azure-biztalk-vm"></a>Wat is Hallo verschil tussen BizTalk Services en virtuele machine van Azure BizTalk?
BizTalk Services biedt een waar Platform-as-a-Service (PaaS)-architectuur voor het bouwen van integratieoplossingen in Hallo cloud. Met Hallo PaaS-model u volledig ligt de nadruk op Hallo toepassingslogica en laat alle Hallo infrastructuur management tooMicrosoft, met inbegrip van:

* Er is geen noodzaak toomanage of patch virtuele machines.
* Microsoft zorgt voor de beschikbaarheid.
* U beheren schaal op aanvraag door te vragen meer of minder capaciteit via hello Azure-portal.

BizTalk Server op virtuele machines van Azure biedt een IaaS-architectuur (Infrastructure-as-a-Service). U virtuele machines maken en configureren zodat deze exact zoals uw on-premises-omgeving, waardoor het gemakkelijker toorun bestaande toepassingen in de cloud Hallo zonder wijzigingen code. Met IaaS bent u nog steeds verantwoordelijk voor het configureren van Hallo virtuele machines, het beheer van Hallo virtuele machines (bijvoorbeeld installeren van software en OS patches) en Hallo-toepassing voor hoge beschikbaarheid worden veranderd.

Als u nieuwe integratieoplossingen wilt bouwen waarbij u zo weinig mogelijk tijd kwijt bent met het beheer van de infrastructuur, gebruikt u BizTalk Services. Als u op zoek bent tooquickly migreren van uw bestaande BizTalk-oplossingen of zoek naar een omgeving op aanvraag toodevelop en test BizTalk Server-toepassingen, gebruikt u BizTalk Server op een virtuele Machine van Azure.

#### <a name="what-is-hello-difference-between-biztalk-adapter-service-and-hybrid-connections"></a>Wat is Hallo verschil tussen BizTalk Adapter Service en hybride verbindingen?
Hallo BizTalk Adapter Service wordt gebruikt door een Azure BizTalk Service. Hallo BizTalk Adapter Service gebruikt Hallo BizTalk Adapter Pack tooconnect tooan on-premises regel van Business (LOB)-systeem. Een hybride verbinding biedt een eenvoudige en handige manier tooconnect Azure-toepassingen, zoals de functie van de Hallo Web Apps in Azure App Service en Azure Mobile Services, tooan on-premises resource.

#### <a name="what-does-hybrid-connection-data-transfer-gb-per-unit-mean-is-this-per-minutehourdayweekmonth-what-happens-when-hello-limit-is-reached"></a>Wat houdt 'Gegevensoverdracht in hybride verbindingen (GB) per eenheid' in? Is dit per minuut/uur/dag/week/maand? Wat gebeurt er wanneer Hallo limiet is bereikt?
Hallo hybride verbinding kosten per eenheid zijn afhankelijk van Hallo BizTalk Services edition. Met andere woorden: de kosten zijn afhankelijk van hoeveel gegevens u overdraagt. Als u bijvoorbeeld dagelijks 10 GB aan gegevens overdraagt, kost dit minder dan wanneer u dagelijks 100 GB overdraagt. Gebruik Hallo [Prijscalculator](https://azure.microsoft.com/pricing/calculator/?scenario=full) voor BizTalk Services toodetermine specifieke kosten. Doorgaans worden Hallo limieten dagelijks afgedwongen. Als u Hallo limiet overschrijdt, wordt er gebracht tegen Hallo tarief $ 1 per GB.

#### <a name="when-i-create-an-agreement-in-biztalk-services-why-does-hello-number-of-bridges-go-up-by-two-instead-of-just-one"></a>Bij het maken van een overeenkomst in BizTalk Services waarom het aantal bruggen Hallo gaat omhoog door twee in plaats van slechts één?
Elke overeenkomst bestaat uit twee verschillende bruggen: een communicatiebrug aan de verzendkant en een communicatiebrug aan de ontvangstkant.

#### <a name="what-happens-when-i-hit-hello-quota-limit-on-hello-number-of-bridges-or-agreements"></a>Wat gebeurt er wanneer ik de quotumlimiet Hallo op Hallo aantal bruggen of overeenkomsten bereikt?
U toodeploy kan niet worden geen nieuwe bruggen of geen nieuwe overeenkomsten maken. meer toodeploy, moet u tooscale toomore eenheden Hallo BizTalk service- of upgrade tooa hogere editie.

#### <a name="how-do-i-migrate-from-one-tier-of-biztalk-services-tooanother"></a>Hoe Migreer ik van één laag van BizTalk Services tooanother
Hallo gratis editie kan niet worden gemigreerd of 'uitgebreide' tooanother laag, en kan niet een back-up en tooanother laag hersteld. Als u een andere laag nodig hebt, maakt u een nieuwe BizTalk Service met de nieuwe laag Hallo. Alle artefacten die zijn gemaakt met behulp van Hallo editie Free, inclusief hybride verbindingen, moeten toobe opnieuw gemaakt in Hallo nieuwe BizTalk Service. 

Voor Hallo andere edities kunt gebruik Hallo back-up en herstel voor het migreren van uw artefacten van één laag tooanother. Bijvoorbeeld: back-up van uw artefacten in Hallo Standard-laag en herstel deze toohello Premium-laag. [BizTalk Services: Back-up en herstel](biztalk-backup-restore.md) worden Hallo ondersteunde migratiepaden beschreven en geeft een lijst van welke artefacten back-up worden gemaakt. Houd er rekening mee dat er geen back-ups worden gemaakt van hybride verbindingen. Na een back-up en herstellen van de nieuwe laag tooa, u vervolgens opnieuw maken Hallo hybride verbindingen.  

#### <a name="is-hello-biztalk-adapter-service-included-in-hello-service-how-do-i-receive-hello-software"></a>Is Hallo BizTalk Adapter Service deel uitmaken van service Hallo? Hoe ontvang ik Hallo-software
Ja, de BizTalk Adapter Service Hallo Hello BizTalk Adapter Pack zijn opgenomen in hello Azure BizTalk Services SDK [downloaden](http://www.microsoft.com/download/details.aspx?id=39087).

## <a name="next-steps"></a>Volgende stappen
toocreate Azure BizTalk Services in Azure portal, ga te Hallo[BizTalk Services: inrichten met Azure-portal Hallo](biztalk-provision-services.md). toostart te maken van toepassingen, ga[Azure BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=235197).

## <a name="additional-resources"></a>Aanvullende bronnen
* [BizTalk Services: Inrichten met hello Azure-portal](biztalk-provision-services.md)<br/>
* [BizTalk Services: statusgrafiek voor de inrichting](biztalk-service-state-chart.md)<br/>
* [BizTalk Services: de tabbladen Dashboard, Bewaken en Schalen](biztalk-dashboard-monitor-scale-tabs.md)<br/>
* [BizTalk Services: back-ups maken en herstellen](biztalk-backup-restore.md)<br/>
* [BizTalk Services: beperking](biztalk-throttling-thresholds.md)<br/>
* [BizTalk Services: naam en sleutel van verlener](biztalk-issuer-name-issuer-key.md)<br/>
* [Hoe gaan gebruiken Azure BizTalk Services SDK Hallo](http://go.microsoft.com/fwlink/p/?LinkID=302335)<br/>

