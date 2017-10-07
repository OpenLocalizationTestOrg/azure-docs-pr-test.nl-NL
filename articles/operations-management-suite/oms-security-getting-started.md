---
title: aaaGetting de slag met beveiliging van Operations Management Suite en Audit oplossing | Microsoft Docs
description: Dit document helpt u tooget gestart met de beveiliging van Operations Management Suite en Audit oplossing mogelijkheden toomonitor uw hybride cloud.
services: operations-management-suite
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: 754796ef-a43e-468a-86c9-04a2eda55b5b
ms.service: operations-management-suite
ms.custom: oms-security
ms.topic: get-started-article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2017
ms.author: yurid
ms.openlocfilehash: 5cb3e5dbb3e60f9702a34c9413ddc1bf2b14b411
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-operations-management-suite-security-and-audit-solution"></a>Aan de slag met Beveiliging en controle van Operations Management Suite
In dit document worden alle opties beschreven, zodat u snel aan de slag kunt met de mogelijkheden van Beveiliging en controle van Operations Management Suite (OMS).

## <a name="what-is-oms"></a>Wat is OMS?
Microsoft Operations Management Suite (OMS) is een cloudoplossing voor IT-beheer van Microsoft waarmee u uw on-premises en cloudinfrastructuur kunt beheren en beveiligen. Lees voor meer informatie over OMS Hallo-artikel [Operations Management Suite](https://technet.microsoft.com/library/mt484091.aspx).

## <a name="oms-security-and-audit-dashboard"></a>OMS-dashboard Beveiliging en controle
Hallo OMS beveiligings- en Audit oplossing biedt een uitgebreid overzicht van uw organisatie IT beveiligingspostuur met ingebouwde zoekquery's voor problemen die aandacht vereisen die uw aandacht vereisen. Hallo **beveiligings- en Audit** dashboard is Hallo startscherm voor van alles aan elkaar gerelateerd toosecurity in OMS. Het biedt op hoog niveau inzicht in de Hallo beveiligingsstatus van uw computers. Dit omvat ook Hallo mogelijkheid tooview alle gebeurtenissen uit Hallo afgelopen 24 uur, 7 dagen of een andere aangepaste tijdsbestek. Hallo tooaccess **beveiligings- en Audit** dashboard als volgt te werk:

1. In Hallo **Microsoft Operations Management Suite** hoofddashboard Klik **instellingen** tegel in Hallo links.
2. In Hallo **instellingen** blade onder **oplossingen** klikt u op **beveiligings- en Audit** optie.
3. Hallo **beveiligings- en Audit** dashboard wordt weergegeven:
   
    ![OMS-dashboard Beveiliging en controle](./media/oms-security-getting-started/oms-getting-started-fig1-ga.png)

Als u toegang dit dashboard voor Hallo eerst tot en u geen apparaten die worden bewaakt door OMS hebt, Hallo tegels niet ingevuld met gegevens die zijn verkregen van Hallo-agent. Als u Hallo-agent installeren, sommige toopopulate tijd kan duren, daarom Zie in eerste instantie mogelijk ontbreken bepaalde gegevens als ze nog steeds toohello cloud uploadt.  In dit geval is het normale toosee sommige tegels zonder concrete informatie. Lees [verbinding maken met Windows-computers rechtstreeks tooOMS](https://technet.microsoft.com/library/mt484108.aspx) voor meer informatie over het tooinstall OMS-agent in een Windows-systeem en [verbinding maken met Linux-computers tooOMS](https://technet.microsoft.com/library/mt622052.aspx) voor meer informatie over het tooperform deze taak in een Linux-systeem.

> [!NOTE]
> Hallo agent verzamelt Hallo-informatie op basis van Hallo huidige gebeurtenissen die zijn ingeschakeld, bijvoorbeeld computernaam, IP-adres en de gebruiker de naam. Maar er worden geen document-/bestandsgegevens, databasenaam of persoonlijke gegevens verzameld.   
> 
> 

Oplossingen omvatten een verzameling logische, visualisatie- en gegevensverzamelingsregels waarmee klanten hun belangrijkste uitdagingen kunnen aangaan. Beveiliging en controle is één oplossing. Andere oplossingen kunnen afzonderlijk worden toegevoegd. Hallo-artikel lezen [oplossingen toevoegen](https://technet.microsoft.com/library/mt674635.aspx) voor meer informatie over hoe u een nieuwe oplossing tooadd.

Hallo OMS beveiligings- en Audit dashboard is onderverdeeld in vier hoofdcategorieën:

* **Beveiligingsdomeinen**: op dit gebied kunt u zich kunt toofurther beveiligingsrecord verkennen gedurende een bepaalde periode, toegang tot de evaluatie van schadelijke software, bijwerken assessment, netwerkbeveiliging, informatie over identiteit en toegang, computers met beveiligingsgebeurtenissen en snel hebben toegang tooAzure Security Center-dashboard.
* **Problemen die aandacht vereisen**: deze optie kunt u tooquickly Hallo aantal actieve problemen identificeren en Hallo ernst van deze problemen.
* **Detecties (Preview)**: kunt u tooidentify aanvalspatronen met beveiligingswaarschuwingen visualiseren als zij op basis van uw resources plaatsvinden.
* **Dreiging Intelligence**: Hiermee kunt u tooidentify aanvalspatronen door het totaal aantal servers met uitgaand schadelijk IP-verkeer, Hallo schadelijke threat type en een kaart die laat waar deze IP-adressen afkomstig zijn zien van hello te visualiseren. 
* **Algemene query's voor beveiliging**: deze optie biedt u een lijst met de meest voorkomende beveiliging Hallo query's waarmee u toomonitor uw omgeving kunt. Wanneer u op een van de query's klikt, deze wordt geopend Hallo **Search** blade met Hallo resultaten voor deze query.

> [!NOTE]
> Lees 'How OMS secures your data' (Uw gegevens beveiligen met OMS) voor meer informatie over hoe uw gegevens met OMS worden beveiligd.
> 
> 

## <a name="security-domains"></a>Beveiligingsdomeinen
Bij de bewaking van resources, is het belangrijk toobe kunnen tooquickly toegang Hallo huidige status van uw omgeving. Het is echter ook belangrijk toobe kunnen tootrack back gebeurtenissen die is opgetreden in de afgelopen Hallo die tooa beter inzicht te krijgen van wat er in uw omgeving op een bepaald punt in tijd gebeurt kan leiden. 

> [!NOTE]
> bewaren van gegevens is toohello OMS prijsstelling volgens. Voor meer informatie gaat u naar Hallo [Microsoft Operations Management Suite](https://www.microsoft.com/server-cloud/operations-management-suite/pricing.aspx) pagina met prijzen.
> 
> 

Incident antwoord forensisch onderzoek scenario's en rechtstreeks profiteren van Hallo resultaten beschikbaar in Hallo **beveiligingsrecord na verloop van tijd** tegel.

![Beveiligingsrecords in de loop van de tijd](./media/oms-security-getting-started/oms-getting-started-fig2.JPG)

Wanneer u op deze tegel klikt, Hallo **Search** blade wordt geopend, waarin de resultaten van een query voor **beveiligingsgebeurtenissen** (Type = SecurityEvents) met gegevens die zijn gebaseerd op Hallo afgelopen zeven dagen, zoals hieronder weergegeven:

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

![Beveiligingsrecords in de loop van de tijd](./media/oms-security-getting-started/oms-getting-started-fig3.JPG)

Hallo zoekresultaat is onderverdeeld in twee deelvensters: Hallo linkerdeelvenster biedt u een uitsplitsing van Hallo aantal beveiligingsgebeurtenissen die zijn gevonden, waarin deze gebeurtenissen zijn gevonden, Hallo aantal accounts die zijn gedetecteerd op deze computers en typen Hallo Hallo-computers activiteiten. Hallo rechterdeelvenster biedt u Hallo totaal aantal resultaten en een chronologische weergave van beveiligingsgebeurtenissen Hallo met de naam en de gebeurteniscode activiteit Hallo van de computer. U kunt ook klikken op **meer weergeven** tooview om meer details over deze gebeurtenis, zoals gebeurtenisgegevens hello, Hallo gebeurtenis-ID en de gebeurtenisbron Hallo.

> [!NOTE]
> Lees [OMS search reference](https://technet.microsoft.com/library/mt450427.aspx) (Engelstalig) voor meer informatie over zoekquery’s in OMS.
> 
> 

### <a name="antimalware-assessment"></a>Antimalware-evaluatie
Met deze optie kan u tooquickly identificatie van computers met onvoldoende beveiliging en computers die door een onderdeel van malware worden getroffen. Evaluatie van schadelijke software status gedetecteerde bedreigingen op Hallo bewaakte servers worden gelezen en vervolgens Hallo gegevens verzonden toohello OMS-service in de cloud Hallo voor verwerking. Servers met gedetecteerde bedreigingen en servers met onvoldoende beveiliging worden weergegeven in Hallo malware assessment dashboard, dat kan geopend worden nadat u op in Hallo **Antimalware Assessment** tegel. 

![malware-evaluatie](./media/oms-security-getting-started/oms-getting-started-fig4-ga.png)

Net als elke andere live tegel beschikbaar in de OMS-Dashboard wanneer u erop klikt, Hallo **Search** blade geopend met Hallo queryresultaat. Voor deze optie als u in Hallo op **niet rapporteren** onder de optie **beveiligingsstatus**, hebt u Hallo queryresultaat waarin deze één vermelding met Hallo computernaam en de positie als Hieronder wordt weergegeven:

![zoekresultaat](./media/oms-security-getting-started/oms-getting-started-fig5.png)

> [!NOTE]
> *positie* is een beoordeling geven tooreflect Hallo status van Hallo-beveiliging (op uitgeschakeld, wordt bijgewerkt, etc.) en bedreigingen die zijn gevonden. Hebben die een aantal helpt toomake aggregaties.
> 
> 

Als u in de naam van de computer van de Hallo klikt, hebt u Hallo chronologische weergave van de beveiligingsstatus Hallo voor deze computer. Dit is zeer nuttig voor scenario's waarin u toounderstand moet als Hallo antimalware is ooit eerder geïnstalleerd en op een bepaald moment is verwijderd.   

### <a name="update-assessment"></a>Update-evaluatie
Deze optie kunt u tooquickly bepalen Hallo algehele blootstelling toopotential beveiligingsproblemen, en of of hoe essentieel deze updates zijn voor uw omgeving. OMS beveiligings- en Audit oplossing alleen Hallo visualisatie van deze updates bieden, Hallo echte gegevens vandaan [Update beheeroplossingen](oms-solution-update-management.md), dit is een andere module binnen OMS. Hier wordt een voorbeeld van Hallo updates:

![systeemupdates](./media/oms-security-getting-started/oms-getting-started-fig6-new.png)

> [!NOTE]
> Lees [De oplossing voor updatebeheer in OMS](oms-solution-update-management.md) voor meer informatie over de oplossing voor updatebeheer.
> 
> 

### <a name="identity-and-access"></a>Identiteit en toegang
Identiteit moet Hallo besturingselement vlak voor uw onderneming, het beveiligen van uw identiteit moet de hoogste prioriteit. Hoewel in de afgelopen Hallo verbindingen rond organisaties zijn en deze verbindingen een van de primaire defensive grenzen Hallo zijn, wordt tegenwoordig met meer gegevens en meer apps verplaatsen toohello cloud Hallo identiteit Hallo nieuwe perimeternetwerk. 

> [!NOTE]
> momenteel Hallo gegevens alleen is gebaseerd op beveiligingsgebeurtenissen aanmeldgegevens (gebeurtenis-ID 4624) in Hallo toekomstige Office365 aanmeldingen en Azure AD-gegevens ook worden opgenomen.
> 
> 

Door de bewaking van uw identiteit activiteiten kunt u zich kunt tootake proactief kunt optreden voordat een incident plaats of reactieve acties toostop een aanval poging. Hallo **identiteits- en toegangsbeheer** dashboard biedt u een overzicht van de status van uw identiteit, waaronder het aantal mislukte pogingen toolog op Hallo gebruikersaccount die werden gebruikt tijdens deze pogingen, accounts die zijn vergrendeld, Hallo accounts met gewijzigd of opnieuw instellen van wachtwoord en momenteel aantal accounts die zijn aangemeld. 

Wanneer u klikt op in Hallo **identiteits- en toegangsbeheer** tegel ziet u Hallo dashboard te volgen:

![identiteit en toegang](./media/oms-security-getting-started/oms-getting-started-fig7-ga.png)

Hallo-informatie beschikbaar is in dit dashboard nut onmiddellijk tooidentify een potentiële verdachte activiteit. Er zijn bijvoorbeeld 338 pogingen toolog op als **beheerder** en 100% van deze pogingen is mislukt. Dit kan worden veroorzaakt door een beveiligingsaanval op dit account. Als je dit account op wordt u meer informatie die u kan helpen toodetermine hello doelbron deze potentiële aanval verkrijgen:

![zoekresultaten](./media/oms-security-getting-started/oms-getting-started-fig8.JPG)

Hallo gedetailleerd rapport vindt u belangrijke informatie over deze gebeurtenis, met inbegrip van: doelcomputer hello, Hallo type aanmelden (in dit geval aanmelding bij het netwerk), Hallo activiteit (in dit geval gebeurtenis 4625) en een uitgebreide tijdlijn van elke poging. 

### <a name="computers"></a>Computers
Deze tegel gebruikte tooaccess alle computers met beveiligingsgebeurtenissen actief kan zijn. Wanneer u in deze tegel klikt ziet u Hallo lijst met computers met beveiligingsgebeurtenissen en het aantal gebeurtenissen Hallo op elke computer:

![Computers](./media/oms-security-getting-started/oms-getting-started-fig9.JPG)

U kunt uw onderzoek om door te klikken op elke computer te gaan en bekijkt hello beveiligingsgebeurtenissen die zijn gemarkeerd.

### <a name="threat-intelligence"></a>Bedreigingsinformatie

Hallo dreigingen optie beschikbaar in de OMS-beveiligings- en Audit gebruikt, IT-beheerders identificeren bedreigingen van Hallo-omgeving, bijvoorbeeld, als een bepaalde computer deel uitmaakt van een botnet identificeren. Computers kunnen knooppunten in een botnet worden wanneer aanvallers vastlegt kwaadaardige software die heimelijk deze computer toohello opdracht en controle verbindt moet worden geïnstalleerd. Er kunnen ook potentiële bedreigingen mee worden geïdentificeerd die afkomstig zijn van underground communicatiekanalen zoals darknet. Meer informatie over dreigingen door te lezen [bewakings- en reageert toosecurity waarschuwingen in de beveiliging van Operations Management Suite en Audit oplossing](oms-security-responding-alerts.md) artikel.

In sommige scenario's ziet u mogelijk een potentieel schadelijke IP-adres dat is geopend vanaf een bewaakte computer:

![kaart met gegevens van bedreigingen](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig6.png)

Deze waarschuwing en anderen binnen dezelfde categorie Hallo, via de OMS-beveiliging worden gegenereerd door gebruik te [Microsoft dreigingen](https://youtu.be/O4WtxgUrDc8). Hallo dreigingen gegevens is verzameld door Microsoft evenals van toonaangevende leveranciers van threat intelligence aangeschaft. Deze gegevens vaak wordt bijgewerkt en aangepast bedreigingen toofast verplaatsen. Vanwege de aard van tooits, moet deze worden gecombineerd met andere bronnen van beveiligingsgegevens tijdens [onderzoeken](https://blogs.technet.microsoft.com/msoms/2016/12/08/investigating-suspicious-activity-in-a-hybrid-cloud-with-oms-security/) een beveiligingswaarschuwing. 

### <a name="baseline-assessment"></a>Basislijnevaluatie

Microsoft definieert samen met brancheorganisaties en overheidsinstanties overal ter wereld een Windows-configuratie die garandeert dat maximaal beveiligde serverimplementaties worden gebruikt. Deze configuratie bestaat uit een verzameling registersleutels, controlebeleidsinstellingen en beveiligingsbeleidsinstellingen, gecombineerd met waarden die door Microsoft voor deze instellingen worden aanbevolen. Deze verzameling staat bekend als de beveiligingsbasislijn. Lees [Basislijnevaluatie in de oplossing Beveiliging en controle in Operations Management Suite](oms-security-baseline.md) voor meer informatie over deze optie.

### <a name="azure-security-center"></a>Azure Security Center
Deze tegel is in feite een snelkoppeling tooaccess Azure Security Center-dashboard. Lees [Aan de slag met Azure Security Center](../security-center/security-center-get-started.md) voor meer informatie over deze oplossing.

## <a name="notable-issues"></a>Problemen die aandacht vereisen
Hallo belangrijkste bedoeling van deze groep van opties is tooprovide een snelle weergave van Hallo problemen die u in uw omgeving, hebt door ze categoriseren in kritiek, waarschuwing en ter informatie. Hallo actieve kwestie type tegel is een visualisatie van deze problemen, maar u kunt geen tooexplore meer details over deze daarvoor moet u toouse Hallo onderste gedeelte van deze tegel met de naam Hallo van Hallo probleem (naam), het aantal objecten hebben dit gebeurt (aantal) en hoe essentieel het is (ERNST).

![Problemen die aandacht vereisen](./media/oms-security-getting-started/oms-getting-started-fig10.JPG)

U ziet dat deze problemen zijn al worden besproken in verschillende gebieden van Hallo **beveiligingsdomeinen** groep Hallo bedoeling van deze weergave versterkt: visualiseren Hallo meest belangrijke problemen in uw omgeving vanaf één locatie.

## <a name="detections-preview"></a>Detecties (preview)
Hallo belangrijkste bedoeling van deze optie is tooallow IT tooquickly potentiële bedreigingen tootheir omgeving via en Hallo ernst van deze dreiging identificeren.

![Bedreigingsinformatie](./media/oms-security-getting-started/oms-getting-started-fig12.png)

Deze optie kan ook worden gebruikt tijdens een [respons op incidenten onderzoek](https://blogs.msdn.microsoft.com/azuresecurity/2016/11/30/investigating-suspicious-activity-in-a-hybrid-cloud-with-oms-security/) tooperform Hallo beoordeling en meer informatie vinden over Hallo-aanval.

> [!NOTE]
> Voor meer informatie over het toouse OMS voor Incident Response Bekijk deze video: [hoe tooLeverage Azure Security Center & Operations Management Suite van Microsoft hello voor een Incident Response](https://channel9.msdn.com/Blogs/Taste-of-Premier/ToP1703).
> 
> 

## <a name="threat-intelligence"></a>Bedreigingsinformatie
nieuwe bedreiging intelligence sectie van de beveiligings- en Audit oplossing Hallo Hallo mogelijke aanvalspatronen op verschillende manieren visualiseren Hallo: totaal aantal servers met uitgaand schadelijk IP-verkeer Hallo, Hallo schadelijke threat type en een toewijzing die laat waar zien deze IP-adressen afkomstig zijn uit. U kunt communiceren met de Hallo kaart en klikt u op Hallo IP-adressen voor meer informatie.

Gele markeringspunten op Hallo kaart aangeven inkomend verkeer van schadelijke IP-adressen. Het is niet ongewoon voor servers die zijn blootgesteld toohello internet toosee binnenkomende schadelijk verkeer, maar het is raadzaam deze pogingen toomake ervoor dat geen van beide is geslaagd controleren. Deze indicatoren zijn gebaseerd op IIS-logboeken, WireData en logboeken van Windows Firewall.  

![Bedreigingsinformatie](./media/oms-security-getting-started/oms-getting-started-fig11-ga.png)

## <a name="common-security-queries"></a>Algemene beveiligingsquery's
Hallo-lijst met algemene beveiliging-query's beschikbaar kan nuttig zijn voor u toorapidly toegang resourcegegevens en aanpassen op basis de behoeften van uw omgeving. Deze algemene query's zijn onder meer:

* Alle beveiligingsactiviteiten
* Beveiligingsactiviteiten op de computer van de Hallo 'computer01.contoso.com' (vervangen door uw eigen computernaam)
* Beveiligingsactiviteiten op Hallo computer 'computer01.contoso.com' voor account 'Administrator (vervangen door uw eigen computer- en accountnaam)
* Aanmeldingsactiviteit per computer
* Accounts waarmee Microsoft Antimalware op een computer is beëindigd
* Computers waarop Hallo Microsoft-antimalwareproces is beëindigd
* Computers waarop hash.exe is uitgevoerd (vervangen door een andere procesnaam)
* Alle procesnamen die zijn uitgevoerd
* Aanmeldingsactiviteit per account
* Accounts die op afstand worden aangemeld bij de computer van de Hallo 'computer01.contoso.com' (vervangen door uw eigen computernaam)

## <a name="see-also"></a>Zie ook
In dit document zijn u geïntroduceerd tooOMS beveiligings- en Audit-oplossing. toolearn meer informatie over OMS-beveiliging, Zie Hallo artikelen te volgen:

* [Overzicht van Operations Management Suite (OMS)](operations-management-suite-overview.md)
* [Bewaking en reageren tooSecurity waarschuwingen in de beveiliging van Operations Management Suite en Audit-oplossing](oms-security-responding-alerts.md)
* [Resources bewaken in de oplossing Beveiliging en controle van Operations Management Suite ](oms-security-monitoring-resources.md)

