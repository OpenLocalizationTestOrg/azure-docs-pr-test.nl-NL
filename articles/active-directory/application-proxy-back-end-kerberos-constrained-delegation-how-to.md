---
title: aaaHow tooconfigure een toepassingsproxy toepassing toouse Kerberos-beperkte overdracht | Microsoft Docs
description: Hoe tooconfigure Kerberos-beperkte overdracht voor een Azure AD-toepassingsproxy-toepassing.
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 93dac264ff1d3b99dead1d9c759c37c59373cbd4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-an-application-proxy-application-toouse-kerberos-constrained-delegation"></a>Hoe tooconfigure een toepassingsproxy toepassing toouse Kerberos-beperkte overdracht

Hallo methoden die beschikbaar zijn voor het bereiken van toepassingen enigszins van de toepassing tooapplication en een van de Hallo-opties afwijken kunnen die Azure-toepassingsproxy rechts out of box hello, biedt eenmalige aanmelding-toopublished is Kerberos-beperkt delegatie (KCD). Dit is waarbij een host connector geconfigureerde tooperform beperkte kerberos-verificatie toobackend toepassingen, namens gebruikers.

Hallo werkelijke procedure voor het inschakelen van KCD is betrekkelijk eenvoudig en is doorgaans niet meer dan een algemeen begrip van Hallo verschillende onderdelen en authenticatiestroom voor eenmalige aanmelding. Zoeken goede bronnen van informatie toohelp oplossen scenario's waarbij KCD SSO niet werkt zoals verwacht, kunnen worden verspreid.

In dit artikel probeert als zodanig tooprovide één punt van verwijzing die u helpen kan oplossen en zelf herstelt mogelijk enkele Hallo meest voorkomende problemen die we zien. Op Hallo dezelfde tijd bieden aanvullende richtlijnen bij het vaststellen van Hallo complexer en moeilijkheden van implementatie.

Houd er rekening mee dat dit artikel wordt Hallo veronderstellingen te volgen:

-   Azure-toepassingsproxy is geïmplementeerd als per onze [documentatie](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-enable) en algemene toegang toonon KCD toepassingen werkt zoals verwacht.

-   Hallo is gepubliceerde doeltoepassing gebaseerd op IIS en Microsoft implementatie van kerberos.

-   Hallo-hosts voor servers en toepassingen zich in één Active Directory-domein bevinden. Gedetailleerde informatie over cross-domein en forest-scenario's vindt u in onze [KCD technisch document](http://aka.ms/KCDPaper).

-   Hallo onderwerp toepassing is gepubliceerd in een Azure-tenant met vooraf-verificatie ingeschakeld en gebruikers verwacht tooauthenticate tooAzure via formulieren gebaseerde verificatie. Rich client verificatie scenario's worden niet behandeld in dit artikel wordt beschreven, maar op een bepaald moment in toekomstige Hallo worden toegevoegd.

## <a name="prerequisites"></a>Vereisten

Azure Application Proxy kan worden geïmplementeerd in vrijwel elk type infrastructuur of organisatie tooorganization omgeving en Hallo architecturen geen twijfel bestaat afwijken. Een van de meest voorkomende oorzaken Hallo van KCD met betrekking tot problemen zijn niet Hallo omgevingen zelf, maar in plaats daarvan eenvoudige onjuiste configuraties of algemene toezicht.

Om deze reden onze advies is altijd toostart door ervoor te zorgen dat aan wordt voldaan aan vereisten van alle Hallo lay-out in onze main [KCD-SSO met Hallo toepassingsproxy artikel met behulp van](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd) starten voor het oplossen van problemen.

Met name Hallo sectie over het configureren van KCD op 2012R2, omdat dit een fundamenteel andere benadering tooconfiguring KCD in eerdere versies van Windows, maar houd ook rekening met verschillende andere overwegingen terwijl de veiligheidsmaatregelen:

-   Het is niet ongewoon is voor een domein lid server tooopen een beveiligd kanaal-dialoogvenster met een specifieke domeincontroller. Verplaats tooanother dialoogvenster op elk gewenst connector hosts moeten dus over het algemeen niet beperkt toobeing kunnen toocommunicate met lokale site alleen specifieke DC's.

-   Vergelijkbare toohello boven punt tussen domeinen scenario's zijn afhankelijk van verwijzingen die rechtstreeks van een connector host tooDCs die zich buiten de lokale netwerkverbinding Hallo mogelijk bevinden. In dit scenario is even belangrijk toomake zeker dat u toestaat dat verkeer en hoger ook tooDCs waarbij andere domeinen, anders overdracht mislukken.

-   Waar mogelijk, moet u niet alle actieve apparaten in de IP-Adressen/id's tussen connector hosts en de DC's, plaatsen wanneer deze soms via Tussenkomende worden en core RPC-verkeer verstoren

Zoveel willen we graag tooresolve problemen snel en efficiënt, enige tijd kan duren, dus waar mogelijk te probeer en delegering te testen in Hallo eenvoudigste scenario's. Hallo meer variabelen die u introduceren, hello meer wellicht hebt u toocontend met. Bijvoorbeeld: beperken van uw test tooa één connector bespaart kostbare tijd en aanvullende connectors kunnen worden toegevoegd nadat Hallo problemen zijn opgelost.

Sommige omgevingsfactoren kunnen ook een bijdrage leveren tooan probleem, dus opnieuw als mogelijk probeert en Hallo architectuur tooa bare minimum voor het testen minimaliseren. Bijvoorbeeld, onjuist geconfigureerde interne firewall ACL's zijn niet ongewoon, dus indien mogelijk hebt u al het verkeer van een connector die rechtstreeks via toohello DC's en back-end-toepassing toegestaan. 

Daadwerkelijk is Hallo absolute beste plaats tooposition connectors zo dicht tootheir doelen omdat kan zijn. Met een firewall zat inline wordt aangeroepen terwijl er gewoon testen onnodige complexiteit toegevoegd en kan alleen verlengen van uw onderzoek.

Ja, wat wordt verstaan onder een probleem KCD toch? Er verschillende klassieke aanduidingen van KCD SSO mislukken en Hallo eerste tekenen van een probleem wordt meestal manifest zelf in Hallo browser.

   ![Onjuiste KCD configuratiefout](./media/application-proxy-back-end-kerberos-constrained-delegation-how-to/graphic1.png)

   ![Autorisatie is mislukt vanwege toomissing machtigingen](./media/application-proxy-back-end-kerberos-constrained-delegation-how-to/graphic2.png)

alle die voorzien zijn dezelfde symptoom van tooperform SSO mislukt en als gevolg daarvan weigeren Hallo Hallo toohello toepassing van de gebruiker toegang.

## <a name="troubleshooting"></a>Problemen oplossen

Hoe u vervolgens oplossen, afhankelijk van Hallo probleem en symptomen waargenomen. Voordat u gaat verdere zou het is raadzaam Hallo koppelingen volgen als ze nuttige informatie die u niet nog afkomstig bevatten via zijn mogelijk:

-   [Oplossen van problemen met toepassingsproxy en foutberichten](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-troubleshoot)

-   [Kerberos-fouten en problemen](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-troubleshoot#kerberos-errors)

-   [Werken met eenmalige aanmelding bij het on-premises en cloud identiteiten zijn niet identiek](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd#working-with-sso-when-on-premises-and-cloud-identities-are-not-identical)

Als u dit tot nu toe, en vervolgens hello belangrijkste hebt bestaat probleem definitief. U moet toodig diepere, dus starten door te scheiden Hallo stroom in drie verschillende fasen die u kunt oplossen.

**Clientverificatie vooraf van** -Hallo externe gebruiker verifiëren tooAzure via een browser.

Wordt kunnen toopre-verifiëren tooAzure is van cruciaal belang voor KCD SSO toofunction. Dit moet worden getest en eerst opgelost als er problemen zijn. Hallo verificatie vooraf fase heeft geen relatie tooKCD of Hallo gepubliceerde toepassing. Deze moet relatief eenvoudig toocorrect afwijkingen door sanity controleren Hallo onderwerp account bestaat in Azure, en dat het niet is uitgeschakeld/geblokkeerd. fout antwoord Hallo in browser Hallo is meestal beschrijvende toounderstand Hallo oorzaak. Als u niet weet, kunt u ook onze andere problemen met docs tooverify controleren.

**Overdracht service** -connector voor toepassingsproxy van Azure ophalen van een kerberos-serviceticket uit een KDC (Kerberos Distribution Center) Hallo namens gebruikers.

externe communicatie tussen client hello en hello Azure-front-end Hallo moet geen gevolgen hebben voor KCD dan ook, andere dan ervoor zorgen dat deze werkt. Dit is zodat hello Azure Proxy-service worden kan opgegeven met een geldige gebruikersnaam op die de gebruikte tooobtain een kerberos-ticket worden. Zonder deze KCD niet mogelijk is en mislukken.

Zoals eerder vermeld, leveren Hallo browser foutberichten sommige goede aanwijzingen gewoonlijk op waarom de dingen zijn mislukt. Zorg ervoor toonote Hallo activiteits-ID en de tijdstempel in antwoord Hallo als u dit kunt u toocorrelate Hallo gedrag tooactual gebeurtenissen in logboek hello Azure-Proxy.

   ![Onjuiste KCD configuratiefout](./media/application-proxy-back-end-kerberos-constrained-delegation-how-to/graphic3.png)

En Hallo overeenkomstige vermeldingen gebeurtenislogboek waargenomen Hallo zou worden gezien als gebeurtenissen 13019 of 12027. U vindt Hallo connector gebeurtenislogboeken in **logboeken toepassingen en Services** &gt; **Microsoft** &gt; **AadApplicationProxy** &gt; **Connector**&gt;**Admin**.

   ![Gebeurtenis 13019 uit Application Proxy-gebeurtenislogboek](./media/application-proxy-back-end-kerberos-constrained-delegation-how-to/graphic4.png)

   ![Gebeurtenis 12027 uit Application Proxy-gebeurtenislogboek](./media/application-proxy-back-end-kerberos-constrained-delegation-how-to/graphic5.png)

-   Een A-record in uw interne DNS gebruiken voor het adres van de toepassing hello en niet een CName

-   Opnieuw controleren die Hallo-connector host Hallo rechten toodelegate toohello aangewezen doelaccount van SPN en dat is verleend **elk verificatieprotocol voor gebruiken** is geselecteerd. Deze procedure wordt besproken in onze main [SSO configuratie artikel](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd)

-   Controleer of er slechts één exemplaar van Hallo SPN-naam bestaat in AD door uitgifte van een **setspn - x** vanaf een opdrachtprompt op de host van een domein lid

-   Controleer toosee als een domeinbeleid wordt afgedwongen toolimit hello [de maximale grootte van kerberos-uitgegeven tokens](https://blogs.technet.microsoft.com/askds/2012/09/12/maxtokensize-and-windows-8-and-windows-server-2012/), zoals deze connector verhinderen Hallo van een token verkrijgen als toobe overmatige gevonden

Een nieuwe netwerktracering vastleggen Hallo kunnen worden uitgewisseld tussen Hallo-connector host en een domein KDC worden dan Hallo volgende aanbevolen stap bij het verkrijgen van meer laag niveau detail op Hallo problemen. U vindt dit in [diepgaand oplossen papier](https://aka.ms/proxytshootpaper).

Als tickets er goed uitziet, ziet u een gebeurtenis in het Hallo-logboeken met de mededeling dat de verificatie is mislukt vanwege een 401 retourneren toohello-toepassing. Dit geeft doorgaans aan dat uw ticket weigeren Hallo-doeltoepassing, dus doorgaan met de Hallo na de volgende fase.

**Doeltoepassing** -Hallo consument van kerberos-ticket Hallo geleverd door het Hallo-connector

In deze fase Hallo connector verwachte toohave verzonden een kerberos-serviceticket toohello back-end, als een koptekst binnen de eerste toepassingsaanvraag Hallo.

-   Met behulp van de toepassing hello interne URL die is gedefinieerd in de portal Hallo valideren dat Hallo toepassing rechtstreeks vanuit de browser Hallo op Hallo-connector host toegankelijk is. Vervolgens kunt u aanmelden met succes. Meer informatie hierover vindt u op de pagina Hallo connector oplossen.

-   Nog steeds op Hallo-connector host, bevestig dat Hallo-verificatie tussen de browser Hallo en toepassing hello gebruik van kerberos, op een van de volgende Hallo:

1.  Dev-hulpprogramma's uitvoeren (**F12**) in Internet Explorer of gebruik [Fiddler](https://blogs.msdn.microsoft.com/crminthefield/2012/10/10/using-fiddler-to-check-for-kerberos-auth/) van Hallo-connector host. Ga toohello toepassing met behulp van de interne URL Hallo, en inspecteren Hallo www-autorisatie-header geretourneerd in antwoord van de toepassing hello Hallo aangeboden, tooensure die ofwel onderhandelen of kerberos aanwezig is. Een blob daaropvolgende kerberos geretourneerd in antwoord Hallo van Hallo browser toohello toepassing doorgaans begint met **YII**, zodat dit is een goede indicatie van kerberos in play. NTLM op Hallo daarentegen altijd beginnen met **TlRMTVNTUAAB**, welke luidt NTLMSSP bij het decoderen van Base64. Als u ziet **TlRMTVNTUAAB** aan het begin Hallo van Hallo blob, betekent dit dat Kerberos **niet** beschikbaar. Als u dit niet ziet, is het Kerberos waarschijnlijk beschikbaar.

  * Houd er rekening mee als Fiddler, met deze methode vereist een uitgebreide beveiliging op de configuratie van de toepassing hello in IIS tijdelijk uit te schakelen.

     ![Venster van de controle van de browser](./media/application-proxy-back-end-kerberos-constrained-delegation-how-to/graphic6.png)

    *Afbeelding:* omdat deze niet met TIRMTVNTUAAB begint, dit is een voorbeeld is dat Kerberos beschikbaar is. Dit is een voorbeeld van een Kerberos-Blob die niet met YII begint.

2.  Tijdelijk NTLM uit de lijst met providers Hallo op IIS site en toegang tot app rechtstreeks van Internet Explorer op de host van de connector verwijderen. Met NTLM niet langer in de lijst met providers van hello moet u kunnen tooaccess Hallo toepassing alleen Kerberos gebruiken. Als dit niet lukt, vervolgens die wijst erop dat er een probleem met de configuratie van de toepassing hello en Kerberos-verificatie niet werkt.

Als Kerberos niet beschikbaar is, is controle Hallo toepassing verificatie-instellingen in IIS toomake zeker te onderhandelen over bovenste met NTLM onder het vermeld. (Geen Negotiate: kerberos of Negotiate: PKU2U). Alleen doorgaan als Kerberos functioneel is.

   ![Windows-verificatieproviders](./media/application-proxy-back-end-kerberos-constrained-delegation-how-to/graphic7.png)
   
-   Met Kerberos en NTLM in plaats, kunt vooraf-verificatie voor de toepassing in de portal Hallo Hallo nu tijdelijk uitschakelen. Als u deze vanaf Hallo openen kunt Zie internet met behulp van de externe URL Hallo. U moet na vragen aan gebruiker tooauthenticate en kunnen toodo moet dus Hello die dezelfde die wordt gebruikt in Hallo account vorige stap. Als dat niet het geval is, wordt dit duidt op een probleem met de back-end-toepassing hello en niet KCD helemaal.

-   Nu opnieuw inschakelen van vooraf-verificatie in Hallo-portal en zich verifiëren via Azure door te proberen tooconnect toohello toepassing via de externe URL. Als u eenmalige aanmelding is mislukt, ziet u een niet-toegestane foutbericht weergegeven in de browser hello, plus gebeurtenis 13022 in Hallo logboek:

    *Microsoft AAD Application Proxy Connector kan geen Hallo gebruiker niet verifiëren omdat het back-endserver Hallo reageert tooKerberos verificatiepogingen met een 401 HTTP-fout.*

    ![HTTTP 401 fout is niet toegestaan](./media/application-proxy-back-end-kerberos-constrained-delegation-how-to/graphic8.png)

-   Controleer Hallo IIS application tooensure Hallo geconfigureerd groep van toepassingen is geconfigureerd toouse Hallo hetzelfde account dat Hallo SPN is geconfigureerd op basis van AD, door te navigeren in IIS, zoals hieronder weergegeven

    ![Venster voor configuratie van IIS-toepassing](./media/application-proxy-back-end-kerberos-constrained-delegation-how-to/graphic9.png)

    Zodra u Hallo identiteit weet, uitgeven Hallo volgende vanaf een cmd vragen toomake of dat dit account definitief is geconfigureerd met Hallo SPN betrokken. Bijvoorbeeld: **setspn – q http/spn.wacketywack.com**

    ![SetSPN-opdrachtvenster](./media/application-proxy-back-end-kerberos-constrained-delegation-how-to/graphic10.png)

-   Controleer dat SPN gedefinieerd aan de hand van de toepassing hello-instellingen in de portal Hallo is dezelfde SPN-naam die is geconfigureerd tegen Hallo doel AD-account wordt gebruikt door de groep van toepassingen van de toepassing hello Hallo Hallo

   ![SPN-configuratie in Azure Portal](./media/application-proxy-back-end-kerberos-constrained-delegation-how-to/graphic11.png)
   
-   Ga naar de IIS- en selecteer Hallo **configuratie-Editor** optie voor de toepassing hello en te navigeren**system.webServer/security/authentication/windowsAuthentication** toomake ervoor dat **UseAppPoolCredentials** tootrue is ingesteld

   ![App-groepen van IIS-configuratie referentie-optie](./media/application-proxy-back-end-kerberos-constrained-delegation-how-to/graphic12.png)

Terwijl nuttig zijn bij het verbeteren van de prestaties van Kerberos-bewerkingen hello, verlaten kernelmodus ingeschakeld veroorzaakt ook Hallo ticket voor Hallo service toobe ontsleuteld met behulp van computeraccount aangevraagd. Dit is een afkorting Hallo lokaal systeem, dus met deze set tootrue onderbreking KCD wanneer de toepassing hello wordt gehost op meerdere servers in een farm.

-   Als een aanvullende controle wilt u wellicht ook toodisable hello **Extended** beveiliging te. Er zijn aangetroffen scenario's waar dit is gebleken dat toobreak KCD wanneer ingeschakeld in zeer specifieke configuraties waarin een toepassing is gepubliceerd als een submap van Hallo standaardwebsite. Deze zelf is geconfigureerd voor anonieme verificatie alleen gehele Hallo-dialoogvensters voorstellen onderliggende objecten wordt niet overgenomen actieve instellingen grijs verlaten. Maar waar mogelijk zou altijd aan te raden dit ingeschakeld, dus in alle geval test, maar vergeet niet toorestore deze tooenabled.

Deze extra controles moeten hebben plaats in bijhouden toostart met behulp van de gepubliceerde toepassing. Gaat u door en spin van aanvullende connectors die ook toodelegate geconfigureerd, maar als er dingen zijn niet verder vervolgens zou het is raadzaam het lezen van onze uitgebreidere technische scenario [Hallo volledige handleiding voor het oplossen van Azure AD-toepassing Proxy](https://aka.ms/proxytshootpaper)

Als u bent nog tooprogress uw probleem, ondersteuning zou niet langer zijn dan tevreden tooassist en gaan. Maak een ondersteuningsticket rechtstreeks vanuit de portal Hallo en onze technici tooyou zal bereiken.

## <a name="other-scenarios"></a>Andere scenario's

-   Een Kerberos-ticket aanvragen Azure toepassingsproxy voordat de aanvraag tooan toepassing worden verzonden. Sommige 3e toepassingen van derden zoals Tableau Server niet tevreden bent met deze methode te verifiëren en in plaats daarvan verwacht Hallo meer conventionele onderhandelingen tootake plaatsen. de eerste aanvraag Hallo is anonieme, zodat Hallo toepassing toorespond met Hallo verificatietypen dat het via een 401 ondersteunt.

-   Dubbele hop verificatie - meestal gebruikt in scenario's waarbij lagen van een toepassing, met een back-end als front-end, beide verificatie te vereisen, zoals SQL Reporting Services.

## <a name="next-steps"></a>Volgende stappen
[Kerberos-beperkte delegatie (KCD) configureren op een beheerd domein](https://docs.microsoft.com/azure/active-directory-domain-services/active-directory-ds-enable-kcd)
