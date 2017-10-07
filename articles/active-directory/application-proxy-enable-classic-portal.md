---
title: Azure AD-toepassingsproxy in de klassieke portal Hallo aaaEnable | Microsoft Docs
description: Toepassingsproxy inschakelen in de klassieke Azure-portal Hallo en installeer Hallo Connectors voor Hallo omgekeerde proxy.
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
ms.date: 07/02/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro; oldportal
ms.openlocfilehash: 8be9416a61993e1b46a20152e172c5133e54c0a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-application-proxy-in-hello-classic-portal-and-download-connectors"></a>Toepassingsproxy inschakelen in de klassieke portal Hallo en connectors downloaden
Dit artikel begeleidt u bij Hallo stappen tooenable Microsoft Azure AD-toepassingsproxy voor uw clouddirectory in Azure AD.

Als u niet bekend bent met wat toepassingsproxy kunt u doen, meer informatie over [hoe tooprovide veilige externe toegang tot het tooon-premises toepassingen](active-directory-application-proxy-get-started.md).

## <a name="application-proxy-prerequisites"></a>Vereisten voor toepassingsproxy
Voordat u kunt inschakelen en gebruiken van services voor toepassingsproxy, moet u toohave:

* Een [basis- of premiumabonnement op Microsoft Azure AD](active-directory-editions.md) en een Azure AD-directory waarvan u een globale beheerder bent.
* Een server met Windows Server 2012 R2 of 2016, waarbij u Hallo Connector voor toepassingsproxy kunt installeren. Hallo-server verzendt aanvragen toohello-services voor toepassingsproxy in de cloud Hallo en moet een HTTP of HTTPS-verbinding toohello toepassingen die u wilt publiceren.
  * Voor één aanmelding tooyour gepubliceerde toepassingen, deze machine moet worden domein in Hallo dezelfde AD-domein als Hallo-toepassingen die u wilt publiceren. Zie voor informatie [eenmalige aanmelding met toepassingsproxy](active-directory-application-proxy-sso-using-kcd.md)
* Als uw organisatie gebruikmaakt van proxy servers tooconnect toohello internet, lezen [werken met bestaande lokale proxyservers](application-proxy-working-with-proxy-servers.md) voor meer informatie over het tooconfigure ze.

## <a name="open-your-ports"></a>De poorten openen

tooprepare uw omgeving voor Azure AD-toepassingsproxy, moet u eerst de tooenable communicatie tooAzure datacenters. Als er een firewall in Hallo pad, zorg ervoor dat deze geopend is zodat die Connector HTTPS (TCP) kunt maken Hallo toohello Application Proxy aanvragen.

1. Open Hallo hierna genoemde poorten te**uitgaande** verkeer:

   | Poortnummer | Hoe deze wordt gebruikt |
   | --- | --- |
   | 80 | Downloaden van certificaatintrekking (CRL's) worden tijdens het valideren van Hallo SSL-certificaat |
   | 443 | Alle uitgaande communicatie met de Hallo service voor toepassingsproxy |

   Als uw firewall verkeer volgens toooriginating gebruikers wordt afgedwongen, opent u deze poorten voor verkeer dat afkomstig is van Windows-services uitgevoerd als netwerkservice.

   > [!IMPORTANT]
   > Hallo tabel weerspiegelt Hallo Poortvereisten voor connector-versies 1.5.132.0 en nieuwer. Als u nog steeds een oudere versie van de connector hebt, moet u ook tooenable Hallo volgende poorten: 5671, 8080 9090, 9091, 9350, 9352 en 10100 – 10120.
   >
   >Zie voor meer informatie over het bijwerken van de nieuwste versie van connectors toohello [inzicht in Azure AD-toepassingsproxy connectors](application-proxy-understand-connectors.md#automatic-updates).

2. Als uw firewall of proxyserver kunt DNS-whitelisting, kunt u geaccepteerde verbindingen toomsappproxy.net en servicebus.windows.net. Als u niet het geval is, moet u tooallow toegang toohello [Azure DataCenter IP ranges](https://www.microsoft.com/download/details.aspx?id=41653), dat elke week worden bijgewerkt.

3. Gebruik Hallo [Azure AD Application Proxy Connector poorten hulpprogramma Test](https://aadap-portcheck.connectorporttest.msappproxy.net/) tooverify dat uw connector Hallo-service voor toepassingsproxy kunt bereiken. Ten minste Zorg ervoor dat de regio VS-midden Hallo en Hallo regio dichtstbijzijnde tooyou alle een groen vinkje. Daarna betekent meer een groen vinkje groter tolerantie.

## <a name="enable-application-proxy-in-azure-ad"></a>Toepassingsproxy inschakelen in Azure AD
1. Meld u aan als een beheerder in Hallo [klassieke Azure-portal](https://manage.windowsazure.com/).
2. Ga tooActive Directory en Hallo directory waarin u toepassingsproxy tooenable wilt selecteren.

    ![Active Directory - pictogram](./media/active-directory-application-proxy-enable/ad_icon.png)
3. Selecteer **configureren** Hallo directory pagina en schuif naar beneden te**toepassingsproxy**.
4. Wisselknop **Application Proxy-Services inschakelen voor deze Directory** te**ingeschakeld**.

    ![Toepassingsproxy inschakelen](./media/active-directory-application-proxy-enable/app_proxy_enable.png)
5. Selecteer **Nu downloaden**. Hallo **Azure AD Application Proxy Connector downloaden** wordt geopend. Lees en accepteer de licentievoorwaarden Hallo en klikt u op **downloaden** toosave Hallo Windows Installer-bestand (.exe) voor Hallo-connector.

## <a name="install-and-register-hello-connector"></a>Installeren en registreren Hallo Connector
1. Voer **AADApplicationProxyConnectorInstaller.exe** op Hallo-server die u hebt voorbereid volgens toohello vereisten.
2. Volg de instructies Hallo in Hallo wizard tooinstall.
3. Tijdens de installatie bent u na vragen aan gebruiker tooregister Hallo connector met Hallo toepassingsproxy van uw Azure AD-tenant.

   * Geef de globale-beheerdersreferentie voor Azure AD op. De referenties van uw globale beheerderstenant kunnen afwijken van uw Microsoft Azure-referenties.
   * Zorg ervoor dat Hallo beheerder die registers Hallo connector bevindt zich in dezelfde map waarin u ingeschakeld Hallo Hallo service voor toepassingsproxy. Bijvoorbeeld, als Hallo tenant domein contoso.com is, Hallo beheerder moet admin@contoso.com of een ander alias in dat domein.
   * Als **verbeterde beveiliging van Internet Explorer** te is ingesteld,**op** op Hallo van server, Hallo registratiescherm mogelijk geblokkeerd. tooallow toegang, volg de instructies in Hallo in Hallo-bericht. Zorg ervoor dat de verbeterde beveiliging van Internet Explorer is uitgeschakeld.
   * Zie [Troubleshoot Application Proxy](active-directory-application-proxy-troubleshoot.md) (Engelstalig) als de registratie van de connector niet lukt.  
4. Wanneer het Hallo-installatie is voltooid, worden twee nieuwe services tooyour server toegevoegd:

   * Met **Microsoft AAD Application Proxy Connector** wordt de connectiviteit mogelijk gemaakt

     * **Microsoft AAD Application Proxy Connector Updater** is een automatische updateservice. Regelmatig gecontroleerd op nieuwe versies van Hallo-connector en updates Hallo-connector, indien nodig.

     ![Connectorservices voor toepassingsproxy - schermafbeelding](./media/active-directory-application-proxy-enable/app_proxy_services.png)
5. Klik op **voltooien** in het venster Hallo-installatie.

Zie [Informatie over connectors voor de Azure AD-toepassingsproxy](application-proxy-understand-connectors.md) voor meer informatie over connectors.

Voor maximale beschikbaarheid dient u minstens nog twee extra connectoren te implementeren. toodeploy meer connectoren Herhaal stappen 2 en 3. Elke connector moet afzonderlijk worden geregistreerd.

Als u toouninstall Hallo Connector wilt, zowel Hallo Connector-service en Hallo Updater service verwijderen. Start uw computer toofully verwijderen Hallo-service opnieuw.

## <a name="next-steps"></a>Volgende stappen
U bent gereed te[publiceren van toepassingen met toepassingsproxy](active-directory-application-proxy-publish.md).

Als u toepassingen die op afzonderlijke netwerken of verschillende locaties hebt, kunt u connector groepen tooorganize Hallo verschillende connectors in logische eenheden. Meer informatie over [Working with Application Proxy connectors](active-directory-application-proxy-connectors.md) (Werken met connectoren voor toepassingsproxy).
