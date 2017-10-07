---
title: aaa "heeft geen toegang tot deze zakelijke toepassing een fout bij het gebruik van een toepassing toepassingsproxy | Microsoft Docs'
description: Hoe algemene toegang tooresolve problemen met toepassingen voor Azure AD-toepassingsproxy.
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
ms.openlocfilehash: 490b106b7d774ee43fc076cc5d082997a1df85e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="cant-access-this-corporate-application-error-when-using-an-application-proxy-application"></a>"Geen toegang tot deze zakelijke toepassing" Fout bij het gebruik van een toepassing toepassingsproxy

In dit artikel kunt u tootroubleshoot veelvoorkomende problemen wanneer er een fout 'deze zakelijke app kan niet worden geopend' op een Azure AD-toepassingsproxy-toepassing.

## <a name="overview"></a>Overzicht
Wanneer u deze fout ziet, worden de statuscode Hallo pagina ook delen. Deze code is waarschijnlijk een van de volgende Hallo:

-   **Time-out van gateway**: Hallo Application Proxy-service kan geen tooreach Hallo-connector is. Dit geeft doorgaans aan een probleem met Hallo connector toewijzing, connector zelf of Hallo networking regels rond Hallo-connector.

-   **Ongeldige Gateway**: Hallo-connector niet kan tooreach Hallo back-end-toepassing is. Dit kan duiden op een onjuiste configuratie van de toepassing hello.

-   **Verboden**: Hallo gebruiker is geen geautoriseerde tooaccess Hallo-toepassing. Dit kan gebeuren wanneer Hallo gebruiker toohello toepassing in Azure Active Directory niet is toegewezen of als op Hallo backend Hallo gebruiker heeft geen machtiging tooaccess Hallo toepassing.

toofind hello code bekijkt hello tekst in de linkerbenedenhoek Hallo van voor het veld 'Statuscode' Hallo Hallo foutbericht weergegeven. Ook eventuele notities op Hallo onder aan de pagina met extra tips Hallo zoeken.

   ![De time-outfout gateway](./media/application-proxy/connection-problem.png)

Zie voor meer informatie over hoe tootroubleshoot hoofdoorzaak van deze fouten en meer informatie over de voorgestelde oplossingen Hallo Hallo overeenkomstige sectie hieronder.

## <a name="gateway-timeout-errors"></a>De time-outfouten gateway

Er is een time-out van gateway treedt op wanneer Hallo service tooreach Hallo connector probeert en kan geen toowithin Hallo time-out venster. Dit wordt meestal veroorzaakt door een toepassing die is toegewezen tooa Connector groep met geen connectors werken of niet sommige door Hallo Connector vereiste poorten zijn geopend.


## <a name="bad-gateway-errors"></a>Ongeldige Gateway-fouten

Een ongeldige gateway-fout geeft aan die Hallo-connector kan geen tooreach Hallo back-end-toepassing. Zorg ervoor dat u de juiste toepassing hello hebt gepubliceerd. Veelvoorkomende fouten die ervoor zorgen deze fout dat:

-   Een typefout gemaakt of een fout in een interne URL Hallo

-   Hallo-hoofdmap van de toepassing hello publiceren niet. Bijvoorbeeld, publiceren <http://expenses/reimbursement> maar probeert tooaccess <http://expenses>

-   Problemen met Hallo Kerberos-beperkt delegatie (KCD)-configuratie

-   Problemen met de back-end-toepassing hello

## <a name="forbidden-errors"></a>Niet-toegestane fouten

Als u een niet-toegestane fout ziet, is Hallo gebruiker niet toegewezen toohello toepassing. Dit kan zijn in Azure Active Directory of op Hallo back-end-toepassing.

toolearn hoe tooassign gebruikers toohello toepassing in Azure, Zie Hallo [configuratiedocumentatie](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal#add-a-test-user).

Als u Hallo gebruiker toohello toepassing in Azure is toegewezen bevestigt, controleert u Hallo Gebruikersconfiguratie in Hallo back-end-toepassing. Als u Kerberos-beperkte overdracht/geïntegreerde Windows-verificatie gebruikt, ziet u enkele richtlijnen voor onze pagina met KCD oplossen.

## <a name="check-hello-applications-internal-url"></a>Interne URL van de toepassing hello controleren

Als een eerste stap van de snelle Controleer controleren en interne URL Hallo herstellen door het openen van de toepassing hello via **bedrijfstoepassingen**, en vervolgens selecteren Hallo **toepassingsproxy** menu. Controleer of dat dit Hallo juiste interne URL, Hallo gebruikt vanuit uw on-premises netwerk tooaccess Hallo toepassing is.

## <a name="check-hello-application-is-assigned-tooa-working-connector-group"></a>Controleer toepassing hello tooa werkgroep van de Connector is toegewezen

tooverify hello toepassing wordt toegewezen tooa werkgroep-Connector:

1.  Hallo-toepassing in Hallo portal openen door te gaan**Azure Active Directory**, te klikken op **bedrijfstoepassingen**, klikt u vervolgens **alle toepassingen.** Hallo toepassing openen en selecteer vervolgens **toepassingsproxy** in het linkermenu Hallo.

2.  Hallo Connector groepsveld kijken. Als er geen actieve connectors in de groep hello, ziet u een waarschuwing. Als u eventuele waarschuwingen niet ziet, gaat u verder te 'controleren of alle vereiste poorten zijn goedgekeurde lijst'.

3.  Als dit Hallo verkeerde Connector groep gebruik Hallo vervolgkeuzelijst tooselect Hallo juiste groep en Controleer eventuele waarschuwingen niet meer weergegeven. Als dit Hallo bedoeld Connector groep, klikt u op Hallo-bericht tooopen Hallo waarschuwingspagina met Connector management.

4.  Hier zijn enkele manieren toodrill in meer:

  * Een actieve Connector verplaatsen in de groep Hallo: als er een actieve Connector die moet deel uitmaken van de groep toothis en onbelemmerd zicht toohello doeltoepassing back-end heeft, kunt u Hallo Connector naar Hallo toegewezen groep verplaatsen. toodo is dus, klikt u op Hallo Connector. Hallo vervolgkeuzelijst tooselect Hallo juiste groep gebruiken in Hallo ' Connector ' groepsveld, en klik op opslaan.

  * Download een nieuwe Connector voor de groep: op deze pagina kunt u Hallo koppeling te krijgen[downloaden van een nieuwe Connector](https://download.msappproxy.net/Subscription/d3c8b69d-6bf7-42be-a529-3fe9c2e70c90/Connector/Download). Hallo-Connector moet toobe geïnstalleerd op een computer met rechtstreeks toohello back-end-toepassing en meestal wordt geplaatst op dezelfde server als de toepassing hello Hallo. Gebruik Hallo Connector koppeling toodownload een connector op de doelmachine Hallo downloaden. Vervolgens klikt u op Hallo Connector en gebruik Hallo 'Connector groep' vervolgkeuzelijst toomake ervoor dat het juiste toohello-groep behoort.

  * Een inactieve Connector onderzoeken: als een verbindingslijn als inactief toont, is het Hallo-service kan geen tooreach. Dit is meestal vanwege toosome vereist poorten wordt geblokkeerd. toosolve dit probleem, op te 'controleren of alle vereiste poorten zijn goedgekeurde lijst' verplaatsen.

Nadat u deze stappen is tooensure Hallo toepassing toegewezen tooa groep met Connectors, Hallo testtoepassing opnieuw werkt. Als deze nog steeds niet werkt, blijven de volgende sectie toohello.

## <a name="check-all-required-ports-are-whitelisted"></a>Controleer alle vereiste poorten zijn goedgekeurde lijst

tooverify dat alle vereiste poorten zijn geopend, Zie onze documentatie over het openen van poorten. Als alle Hallo vereist poorten geopend zijn, verplaatst u de volgende sectie toohello.

## <a name="check-for-other-connector-errors"></a>Controleer ook op andere fouten Connector

Als geen van bovenstaande Hallo Hallo probleem hebt opgelost, is de volgende stap Hallo toolook voor problemen of fouten Hello Connector zelf. Ziet u een aantal veelvoorkomende fouten in Hallo [oplossen document](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-troubleshoot#connector-errors). 

U kunt ook zoeken rechtstreeks op Hallo Connector logboeken tooidentify eventuele fouten. Veel van de foutberichten kunnen tooshare worden meer specifieke aanbevelingen voor oplossingen. hoe tooview Hallo Logboeken, Zie toolearn [onze documentatie connectors](https://docs.microsoft.com/azure/active-directory/application-proxy-understand-connectors#under-the-hood).

## <a name="additional-resolutions"></a>Aanvullende oplossingen

Als bovenstaande Hallo niet Hallo probleem is verholpen, zijn er enkele verschillende mogelijke oorzaken. probleem met de Hallo tooidentify:

Als de toepassing geconfigureerd toouse is geïntegreerde Windows-verificatie (IWA), Hallo testtoepassing zonder eenmalige aanmelding. Als dat niet het geval is, moet u de volgende alinea toohello verplaatsen. toocheck hello toepassing zonder eenmalige aanmelding, opent u uw toepassing via **bedrijfstoepassingen,** en ga toohello **Single Sign-On** menu. Wijziging Hallo vervolgkeuzelijst van geïntegreerde Windows-verificatie' te "Azure AD single sign-on uitgeschakeld". 

Nu open een browser en probeer het opnieuw tooaccess Hallo-toepassing. U moet worden gevraagd om verificatie en toegang tot de toepassing hello. Als dit werkt, wordt Hallo probleem is met Hallo Kerberos-beperkt delegatie (KCD) configuratie waarmee Hallo eenmalige aanmelding. Zie Hallo KCD oplossen pagina.

Als u toosee Hallo fout doorgaat, gaat u toohello machine waar Hallo Connector is geïnstalleerd, opent u een browser en probeert tooreach Hallo interne URL die wordt gebruikt voor de toepassing hello. Hallo Connector fungeert als een andere client Hallo dezelfde machine. Als u de toepassing hello niet kan bereiken, onderzoeken waarom dat de computer kan geen tooreach Hallo toepassing is of gebruik een connector op een server die is kunnen tooaccess Hallo-toepassing.

Als u de toepassing hello van deze machine toolook voor problemen of fouten Hello Connector zelf bereiken kunt. Ziet u een aantal veelvoorkomende fouten in Hallo [oplossen document](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-troubleshoot#connector-errors). U kunt ook zoeken rechtstreeks op Hallo Connector logboeken tooidentify eventuele fouten. Veel van de foutberichten kunnen tooshare worden meer specifieke aanbevelingen voor oplossingen. hoe tooview Hallo Logboeken, Zie toolearn [onze documentatie connectors](https://docs.microsoft.com/azure/active-directory/application-proxy-understand-connectors#under-the-hood).

## <a name="next-steps"></a>Volgende stappen
[Azure AD-toepassingsproxy connectors begrijpen](application-proxy-understand-connectors.md)
