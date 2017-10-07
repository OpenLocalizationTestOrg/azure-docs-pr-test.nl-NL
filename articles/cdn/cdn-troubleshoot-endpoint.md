---
title: aaaTroubleshooting Azure CDN-eindpunten die retourneren 404 status | Microsoft Docs
description: Problemen met 404-responscodes met Azure CDN-eindpunten.
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: b588a1eb-ab69-4fc7-ae4d-157c3e46f4a8
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 450bfbd641c869cfd88169a12c4b69819eaa7c26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-cdn-endpoints-returning-404-statuses"></a>Problemen oplossen voor CDN-eindpunten die 404-statusberichten retourneren
Dit artikel helpt u problemen oplossen met [CDN-eindpunten](cdn-create-new-endpoint.md) 404-fouten retourneren.

Als u meer hulp op elk gewenst moment in dit artikel nodig hebt, kunt u raadplegen hello Azure deskundigen op [hello Azure MSDN en forums Stack Overflow Hallo](https://azure.microsoft.com/support/forums/). U kunt ook kunt u ook een incident voor ondersteuning van Azure bestand. Ga toohello [ondersteuning van Azure site](https://azure.microsoft.com/support/options/) en klik op **Get Support**.

## <a name="symptom"></a>Symptoom
U kunt een CDN-profiel en een eindpunt hebt gemaakt, maar uw inhoud lijkt niet beschikbaar op Hallo CDN toobe.  Gebruikers die de inhoud via Hallo CDN URL ontvangen HTTP 404-statuscodes tooaccess proberen. 

## <a name="cause"></a>Oorzaak
Er zijn verschillende mogelijke oorzaken, inclusief:

* oorsprong Hallo-bestand is niet zichtbaar toohello CDN
* Hallo-eindpunt is onjuist geconfigureerd, waardoor Hallo CDN toolook op de verkeerde plaats Hallo
* Hallo host weigert Hallo host-header van Hallo CDN
* Hallo-eindpunt nog niet was tijd toopropagate in de gehele Hallo CDN

## <a name="troubleshooting-steps"></a>Stappen voor probleemoplossing
> [!IMPORTANT]
> Nadat een CDN-eindpunt is gemaakt, zich het onmiddellijk niet beschikbaar voor gebruik, zoals het duurt voor Hallo registratie toopropagate via Hallo CDN.  Voor <b>Azure CDN van Akamai</b> profielen, doorgeven voltooit meestal binnen één minuut.  Profielen van <b>Azure CDN van Verizon</b> worden doorgaans binnen 90 minuten doorgegeven, maar in sommige gevallen kan dit langer duren.  Als u Hallo stappen in dit document en u bent nog steeds 404-responsberichten, overweeg een paar uur toocheck weer aan voordat u een ondersteuningsticket openen.
> 
> 

### <a name="check-hello-origin-file"></a>Hallo-bronbestand controleren
We moeten eerst Hallo verifiëren dat we willen dat in de cache Hallo-bestand beschikbaar is op onze oorsprong en openbaar toegankelijk is.  Hallo snelste manier toodo die in een sessie In privé- of Incognito tooopen een browser en Blader rechtstreeks toohello-bestand.  NET Typ of plak Hallo-URL in het vak Hallo-adres en Zie als die resulteert in het Hallo-bestand die u verwacht.  Bijvoorbeeld, ga ik toouse een bestand hebben een Azure Storage-account, toegankelijk is op `https://cdndocdemo.blob.core.windows.net/publicblob/lorem.txt`.  Zoals u ziet het Hallo-test met succes wordt doorgegeven.

![Success!](./media/cdn-troubleshoot-endpoint/cdn-origin-file.png)

> [!WARNING]
> Hoewel dit Hallo snelste is en gemakkelijkste manier tooverify uw bestand openbaar beschikbaar, is enkele netwerkconfiguraties in uw organisatie kunnen geven Hallo u illusie dat dit bestand openbaar beschikbaar is wanneer het is, in feite is alleen zichtbaar toousers van uw netwerk ( zelfs als deze wordt gehost in Azure).  Als u een externe browser van waaruit u testen, hebt kunt zoals een mobiel apparaat dat is niet verbonden tooyour organisatienetwerk of een virtuele machine in Azure, zou die worden aanbevolen.
> 
> 

### <a name="check-hello-origin-settings"></a>Controleer de instellingen van de oorsprong Hallo
Nu dat u hebt gecontroleerd Hallo bestand openbaar beschikbaar is op Hallo van internet, moet we onze oorsprong instellingen controleren.  In Hallo [Azure Portal](https://portal.azure.com), blader tooyour CDN-profiel en klik op Hallo eindpunt u bent het oplossen van problemen.  In het resulterende Hallo **eindpunt** blade, klikt u op Hallo oorsprong.  

![De blade een eindpunt met oorsprong gemarkeerd](./media/cdn-troubleshoot-endpoint/cdn-endpoint.png)

Hallo **oorsprong** blade wordt weergegeven. 

![Oorsprong-blade](./media/cdn-troubleshoot-endpoint/cdn-origin-settings.png)

#### <a name="origin-type-and-hostname"></a>Oorsprongtype en hostnaam
Controleren of Hallo **oorsprongtype** juist is, en controleer of Hallo **hostnaam van oorsprong**.  In mijn voorbeeld `https://cdndocdemo.blob.core.windows.net/publicblob/lorem.txt`, Hallo hostname-deel van Hallo-URL is `cdndocdemo.blob.core.windows.net`.  Zoals u in de schermafbeelding hello ziet, dit klopt.  Hallo voor Azure Storage, Web-App en Cloud Service oorsprongen, **de hostnaam van oorsprong** veld is een vervolgkeuzelijst, dus we er geen tooworry moeten over correct spelling.  Als u een aangepaste oorsprong, het is echter *absoluut essentieel* uw hostnaam juist is gespeld.

#### <a name="http-and-https-ports"></a>HTTP en HTTPS-poorten
Hallo andere ding toocheck hier is uw **HTTP** en **HTTPS-poorten**.  In de meeste gevallen 80 en 443 juist zijn en u geen wijzigingen nodig hebt.  Als de bronserver Hallo op een andere poort luistert, wordt die hier voorgesteld toobe nodig.  Als u niet zeker weet, kijk dan eens Hallo-URL voor uw bronbestand.  Hallo HTTP en HTTPS-specificaties Geef poorten 80 en 443 als Hallo standaardwaarden. In mijn URL `https://cdndocdemo.blob.core.windows.net/publicblob/lorem.txt`, een poort niet is opgegeven, zodat Hallo standaard 443 wordt uitgegaan en Mijn instellingen correct zijn.  

Hallo-URL voor uw oorsprong-bestand dat u eerder hebt getest, is echter aannemen dat `http://www.contoso.com:8080/file.txt`.  Opmerking Hallo `:8080` achter Hallo Hallo hostnaam segment.  Hallo browser toouse poort weet `8080` tooconnect toohello webserver op `www.contoso.com`, dus u tooenter 8080 in Hallo moet **HTTP-poort** veld.  Het is belangrijk toonote dat deze poortinstellingen alleen van invloed op welke poort Hallo-eindpunt maakt gebruik van informatie van de oorsprong Hallo tooretrieve.

> [!NOTE]
> **Azure CDN van Akamai** eindpunten Hallo volledige TCP-poortbereik voor oorsprongen niet toestaan.  Zie [Azure CDN from Akamai Allowed Origin Ports](https://msdn.microsoft.com/library/mt757337.aspx) (Door Azure CDN van Akamai toegestane poorten van oorsprong) voor een lijst met poorten van oorsprong die niet zijn toegestaan.  
> 
> 

### <a name="check-hello-endpoint-settings"></a>Controleer de instellingen van de Hallo-eindpunt
Terug op Hallo **eindpunt** blade, klikt u op Hallo **configureren** knop.

![De blade een eindpunt met de knop configureren gemarkeerd](./media/cdn-troubleshoot-endpoint/cdn-endpoint-configure-button.png)

Hallo-eindpunt **configureren** blade wordt weergegeven.

![Blade configureren](./media/cdn-troubleshoot-endpoint/cdn-configure.png)

#### <a name="protocols"></a>Protocollen
Voor **protocollen**, Controleer of Hallo-protocol wordt gebruikt door clients Hallo is geselecteerd.  Hallo hetzelfde protocol dat wordt gebruikt door de client hello worden gebruikt tooaccess Hallo oorsprong, dus is het belangrijk toohave Hallo oorsprongspoorten juist geconfigureerd in de vorige sectie Hallo Hallo.  Hallo-eindpunt luistert alleen op Hallo standaard HTTP en HTTPS-poorten (80 en 443), ongeacht de Hallo oorsprongspoorten.

Laten we als resultaat tooour hypothetische met `http://www.contoso.com:8080/file.txt`.  Als u onthouden wilt, Contoso opgegeven `8080` als hun HTTP-poort, maar we ook wordt ervan uitgegaan dat ze opgegeven `44300` als hun HTTPS-poort.  Als ze een eindpunt met de naam gemaakt `contoso`, de hostnaam van het CDN-eindpunt zou worden `contoso.azureedge.net`.  Een aanvraag voor `http://contoso.azureedge.net/file.txt` een HTTP-aanvraag is dus Hallo-eindpunt op poort 8080 tooretrieve HTTP gebruikt via Hallo oorsprong.  Beveiligde aanvragen via HTTPS, `https://contoso.azureedge.net/file.txt`, zou leiden tot Hallo eindpunt toouse HTTPS op poort 44300 wanneer op te halen bestand vanuit de oorsprong Hallo Hallo.

#### <a name="origin-host-header"></a>Host-header van oorsprong
Hallo **host-header van oorsprong** Hallo host-headerwaarde toohello oorsprong met elke aanvraag verzonden.  In de meeste gevallen dit moet worden Hallo dezelfde als Hallo **de hostnaam van oorsprong** we eerder gecontroleerd.  Een onjuiste waarde in dit veld niet in het algemeen toe leiden dat 404-statusberichten, maar is waarschijnlijk toocause andere statussen 4xx, afhankelijk van welke oorsprong Hallo verwacht.

#### <a name="origin-path"></a>Pad voor de oorsprong
Ten slotte moet controleren we onze **oorsprongpad**.  Dit is standaard leeg.  U moet dit veld alleen gebruiken als u wilt dat toonarrow Hallo bereik Hallo oorsprong gehost resources dat u wilt dat beschikbaar is op Hallo CDN toomake.  

Bijvoorbeeld in mijn eindpunt gewenste alle bronnen op mijn storage-account toobe die beschikbaar is, zodat ik links **oorsprongpad** leeg.  Dit betekent dat een aanvraag te`https://cdndocdemo.azureedge.net/publicblob/lorem.txt` resulteert in een verbinding van mijn eindpunt te`cdndocdemo.core.windows.net` die aanvragen `/publicblob/lorem.txt`.  Ook kan een aanvraag voor `https://cdndocdemo.azureedge.net/donotcache/status.png` resulteert in het Hallo-eindpunt aanvragen `/donotcache/status.png` vanuit Hallo oorsprong.

Maar wat gebeurt er als ik wil niet toouse Hallo CDN voor elk pad op mijn oorsprong?  Zeg I wilde slechts tooexpose hello `publicblob` pad.  Als ik invoert */publicblob* in mijn **oorsprongpad** veld waardoor Hallo eindpunt tooinsert */publicblob* vóór elk verzoek wordt toohello oorsprong.  Dit betekent dat Hallo-aanvraag voor `https://cdndocdemo.azureedge.net/publicblob/lorem.txt` nu daadwerkelijk duurt Hallo aanvraag deel van Hallo-URL, `/publicblob/lorem.txt`, en toevoeg- `/publicblob` toohello begin. Dit resulteert in een aanvraag voor `/publicblob/publicblob/lorem.txt` vanuit Hallo oorsprong.  Als dat het pad kan niet worden omgezet tooan Werkelijke bestand, worden Hallo oorsprong 404 status geretourneerd.  Hallo juiste URL tooretrieve lorem.txt in dit voorbeeld zou daadwerkelijk worden `https://cdndocdemo.azureedge.net/lorem.txt`.  Opmerking dat we Hallo niet opnemen */publicblob* pad, omdat Hallo aanvraag deel van Hallo URL is `/lorem.txt` en Hallo-eindpunt toegevoegd `/publicblob`, wat resulteert in `/publicblob/lorem.txt` Hallo aanvraag doorgegeven toohello oorsprong .

