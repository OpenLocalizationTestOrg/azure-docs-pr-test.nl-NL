---
title: aan de slag aaaAzure AD-App-Proxy - connector installeren | Microsoft Docs
description: Toepassingsproxy inschakelen in hello Azure-portal en installeer Hallo Connectors voor Hallo omgekeerde proxy.
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: c7186f98-dd80-4910-92a4-a7b8ff6272b9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: ea79ffa92fa223584be04f49019fd31a0bfd8358
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-application-proxy-and-install-hello-connector"></a>Aan de slag met Application Proxy en het Hallo-connector installeren
Dit artikel begeleidt u bij Hallo stappen tooenable Microsoft Azure AD-toepassingsproxy voor uw clouddirectory in Azure AD.

Als u niet bent nog op de hoogte van de beveiliging en productiviteit voordelen Hallo toepassingsproxy tooyour organisatie biedt meer informatie over [hoe tooprovide veilige externe toegang tot het tooon-premises toepassingen](active-directory-application-proxy-get-started.md).

## <a name="application-proxy-prerequisites"></a>Vereisten voor toepassingsproxy
Voordat u kunt inschakelen en gebruiken van services voor toepassingsproxy, moet u toohave:

* Een [basis- of premiumabonnement op Microsoft Azure AD](active-directory-editions.md) en een Azure AD-directory waarvan u een globale beheerder bent.
* Een server met Windows Server 2012 R2 of 2016, waarbij u Hallo Connector voor toepassingsproxy kunt installeren. Hallo-server moet toobe kunnen tooconnect toohello toepassingsproxy services in de cloud hello, en Hallo on-premises toepassingen die u wilt publiceren.
  * Voor één aanmelding tooyour moet gepubliceerde toepassingen met een Kerberos-beperkte overdracht deze machine worden domein in Hallo dezelfde AD-domein als Hallo-toepassingen die u wilt publiceren. Zie voor informatie [KCD voor eenmalige aanmelding met toepassingsproxy](active-directory-application-proxy-sso-using-kcd.md).

Als uw organisatie gebruikmaakt van proxy servers tooconnect toohello internet, lezen [werken met bestaande lokale proxyservers](application-proxy-working-with-proxy-servers.md) voor meer informatie over hoe tooconfigure ze voordat u ervoor zorgen dat de slag met Application Proxy.

## <a name="open-your-ports"></a>De poorten openen

tooprepare uw omgeving voor Azure AD-toepassingsproxy, moet u eerst de tooenable communicatie tooAzure datacenters. Als er een firewall in Hallo pad, zorg ervoor dat deze geopend is zodat die Connector HTTPS (TCP) kunt maken Hallo toohello Application Proxy aanvragen.

1. Open Hallo hierna genoemde poorten te**uitgaande** verkeer:

   | Poortnummer | Hoe deze wordt gebruikt |
   | --- | --- |
   | 80 | Downloaden van certificaatintrekking (CRL's) worden tijdens het valideren van Hallo SSL-certificaat |
   | 443 | Alle uitgaande communicatie met de Hallo service voor toepassingsproxy |

   Als uw firewall verkeer volgens toooriginating gebruikers wordt afgedwongen, opent u deze poorten voor verkeer van Windows-services die worden uitgevoerd als een netwerkservice.

   > [!IMPORTANT]
   > Hallo tabel weerspiegelt Hallo Poortvereisten voor connector-versies 1.5.132.0 en nieuwer. Als u nog steeds een oudere versie van de connector hebt, moet u ook tooenable Hallo na poorten in toevoeging too80 en 443:5671, 8080, 9090-9091 9350, 9352, 10100 – 10120.
   >
   >Zie voor meer informatie over het bijwerken van de nieuwste versie van connectors toohello [inzicht in Azure AD-toepassingsproxy connectors](application-proxy-understand-connectors.md#automatic-updates).

2. Als uw firewall of proxyserver kunt DNS-whitelisting, kunt u geaccepteerde verbindingen toomsappproxy.net en servicebus.windows.net. Als u niet het geval is, moet u tooallow toegang toohello [Azure DataCenter IP ranges](https://www.microsoft.com/download/details.aspx?id=41653), dat elke week worden bijgewerkt.

3. Microsoft maakt gebruik van vier adressen tooverify certificaten. Toegang toohello volgende URL's als u dit nog niet hebt gedaan voor andere producten toestaan:
   * mscrl.Microsoft.com:80
   * CRL.Microsoft.com:80
   * OCSP.msocsp.com:80
   * www.Microsoft.com:80

4. De connector moet toegang toologin.windows.net en login.microsoftonline.net voor Hallo registratieproces.

5. Gebruik Hallo [Azure AD Application Proxy Connector poorten hulpprogramma Test](https://aadap-portcheck.connectorporttest.msappproxy.net/) tooverify dat uw connector Hallo-service voor toepassingsproxy kunt bereiken. Ten minste Zorg ervoor dat de regio VS-midden Hallo en Hallo regio dichtstbijzijnde tooyou alle een groen vinkje. Daarna betekent meer een groen vinkje groter tolerantie.

## <a name="install-and-register-a-connector"></a>Installeren en registreren van een connector
1. Meld u aan als een beheerder in Hallo [Azure-portal](https://portal.azure.com/).
2. De huidige map wordt weergegeven onder uw gebruikersnaam in de rechterbovenhoek Hallo. Als u toochange mappen nodig hebt, selecteert u dit pictogram.
3. Ga te**Azure Active Directory** > **toepassingsproxy**.

   ![Navigeer tooApplication Proxy](./media/active-directory-application-proxy-enable/app_proxy_navigate.png)

4. Selecteer **Connector downloaden**.

   ![Connector downloaden](./media/active-directory-application-proxy-enable/download_connector.png)

5. Voer **AADApplicationProxyConnectorInstaller.exe** op Hallo-server die u hebt voorbereid volgens toohello vereisten.
6. Volg de instructies Hallo in Hallo wizard tooinstall. Tijdens de installatie bent u na vragen aan gebruiker tooregister Hallo connector met Hallo toepassingsproxy van uw Azure AD-tenant.

   * Geef de globale-beheerdersreferentie voor Azure AD op. De referenties van uw globale beheerderstenant kunnen afwijken van uw Microsoft Azure-referenties.
   * Zorg ervoor dat Hallo beheerder die registers Hallo connector bevindt zich in dezelfde map waarin u ingeschakeld Hallo Hallo service voor toepassingsproxy. Bijvoorbeeld, als Hallo tenant domein contoso.com is, Hallo beheerder moet admin@contoso.com of een ander alias in dat domein.
   * Als **verbeterde beveiliging van Internet Explorer** te is ingesteld,**op** op Hallo-server waarop u Hallo-connector installeert, kan er geen Hallo registratiescherm. tooget toegang, volg de instructies in Hallo in Hallo-bericht. Zorg ervoor dat de verbeterde beveiliging van Internet Explorer is uitgeschakeld.

Voor maximale beschikbaarheid dient u minstens nog twee extra connectoren te implementeren. Elke connector moet afzonderlijk worden geregistreerd.

## <a name="test-that-hello-connector-installed-correctly"></a>Testen die Hallo-connector correct is geïnstalleerd

U kunt bevestigen dat een nieuwe connector goed door te controleren op het in beide hello Azure-portal of op uw server geïnstalleerd. 

In Azure-portal hello, tooyour tenant aanmelden en te navigeren**Azure Active Directory** > **toepassingsproxy**. Alle connectors en groepen van de connector weergegeven op deze pagina. Selecteer een connector toosee de details ervan of verplaatsen naar een andere connector-groep. 

Controleer Hallo lijst met actieve services voor het Hallo-connector en Hallo connector updater op uw server. Hallo twee services moeten onmiddellijk worden gestart, maar zo niet, ze inschakelen: 

   * Met **Microsoft AAD Application Proxy Connector** wordt de connectiviteit mogelijk gemaakt

   * **Microsoft AAD Application Proxy Connector Updater** is een automatische updateservice. Hallo updater controleert op nieuwe versies van het Hallo-connector en updates Hallo connector indien nodig.

   ![Connectorservices voor toepassingsproxy - schermafbeelding](./media/active-directory-application-proxy-enable/app_proxy_services.png)

Zie voor meer informatie over connectors en hoe ze blijven toodate [inzicht in Azure AD-toepassingsproxy connectors](application-proxy-understand-connectors.md).


## <a name="next-steps"></a>Volgende stappen
U bent gereed te[publiceren van toepassingen met toepassingsproxy](application-proxy-publish-azure-portal.md).

Als u toepassingen die op afzonderlijke netwerken of verschillende locaties hebt, gebruikt u connector groepen tooorganize Hallo verschillende connectors in logische eenheden. Meer informatie over [Working with Application Proxy connectors](active-directory-application-proxy-connectors-azure-portal.md) (Werken met connectoren voor toepassingsproxy).
