---
title: aaaTroubleshoot toepassingsproxy | Microsoft Docs
description: Dekt hoe tootroubleshoot fouten in Azure AD-toepassingsproxy.
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 970caafb-40b8-483c-bb46-c8b032a4fb74
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: H1Hack27Feb2017; it-pro
ms.openlocfilehash: d426708a2ee32da6674987b5794602ed984b06b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-application-proxy-problems-and-error-messages"></a>Oplossen van problemen met toepassingsproxy en foutberichten
Als er fouten optreden bij het openen van een gepubliceerde toepassing of in de publicatie van toepassingen, controleert u Hallo opties toosee volgen als Microsoft Azure AD-toepassingsproxy correct werkt:

* Open Hallo Windows Services console en controleer of deze Hallo **Microsoft AAD Application Proxy Connector** -service is ingeschakeld en worden uitgevoerd. U kunt ook toolook op de pagina voor Hallo Application Proxy-service-eigenschappen, zoals wordt weergegeven in Hallo installatiekopie te volgen:  
  ![Eigenschappen van Microsoft AAD Application Proxy Connector venster-schermafbeelding](./media/active-directory-application-proxy-troubleshoot/connectorproperties.png)
* Open Logboeken en zoekt u naar Application Proxy connector-gebeurtenissen in **logboeken toepassingen en Services** > **Microsoft** > **AadApplicationProxy** > **Connector** > **Admin**.
* Indien nodig, meer gedetailleerde logboeken kunnen worden [logboeken van de sessie connector voor toepassingsproxy inschakelen Hallo](application-proxy-understand-connectors.md#under-the-hood).

Zie voor meer informatie over het hulpprogramma voor probleemoplossing hello Azure AD [probleemoplossing hulpprogramma toovalidate connector netwerken vereisten](https://blogs.technet.microsoft.com/applicationproxyblog/2015/09/03/troubleshooting-tool-to-validate-connector-networking-prerequisites).

## <a name="hello-page-is-not-rendered-correctly"></a>Hallo-pagina is niet correct weergegeven
Mogelijk hebt u problemen met uw toepassing rendering of werkt niet goed zonder specifieke foutberichten worden weergegeven. Dit kan gebeuren als u Hallo artikel pad gepubliceerd, maar de toepassing hello inhoud buiten dat pad vereist.

Bijvoorbeeld, als u Hallo pad https://yourapp/app publiceren, maar toepassing hello afbeeldingen in https://yourapp/media aanroept, won't ze worden weergegeven. Zorg ervoor dat u Hallo toepassingen publiceren met Hallo hoogste niveau pad u tooinclude moet alle relevante inhoud. In dit voorbeeld zou worden http://yourapp/.

Als u de inhoud van uw pad tooinclude waarnaar wordt verwezen wijzigen, maar nog steeds gebruikers tooland in op een dieper koppeling Hallo pad moet, raadpleegt u Hallo blogbericht [instelling Hallo juiste koppeling voor toepassingsproxy-toepassingen in het toegangsvenster hello Azure AD en Office 365-app linksboven](https://blogs.technet.microsoft.com/applicationproxyblog/2016/04/06/setting-the-right-link-for-application-proxy-applications-in-the-azure-ad-access-panel-and-office-365-app-launcher/).

## <a name="connector-errors"></a>Connector-fouten

Gebruik Hallo [Azure AD Application Proxy Connector poorten hulpprogramma Test](https://aadap-portcheck.connectorporttest.msappproxy.net/) tooverify dat uw connector Hallo-service voor toepassingsproxy kunt bereiken. Ten minste Zorg ervoor dat de regio VS-midden Hallo en Hallo regio dichtstbijzijnde tooyou alle een groen vinkje. Daarna betekent meer een groen vinkje groter tolerantie. 

Als de registratie is mislukt tijdens de installatie van de Connector-wizard hello, zijn er twee manieren tooview Hallo reden voor Hallo mislukken. Een zoeken in het gebeurtenislogboek Hallo onder **toepassingen en Services Logs\Microsoft\AadApplicationProxy\Connector\Admin**, of Voer Hallo de volgende Windows PowerShell-opdracht:

    Get-EventLog application –source “Microsoft AAD Application Proxy Connector” –EntryType “Error” –Newest 1

Zodra u Hallo Connector fout van het gebeurtenislogboek Hallo vinden, gebruikt u deze tabel van veelvoorkomende fouten tooresolve Hallo probleem:

| Fout | Aanbevolen stappen |
| ----- | ----------------- |
| Registratie van de connector is mislukt: Zorg ervoor dat u toepassingsproxy in hello Azure-beheerportal en dat u uw Active Directory-gebruikersnaam en wachtwoord correct ingevoerd ingeschakeld. Fout: 'een of meer fouten opgetreden." | Als u Hallo registratie venster gesloten zonder tooAzure AD aanmelden, Hallo Connector-wizard opnieuw uitvoeren en Hallo Connector registreren. <br><br> Als Hallo registratie venster wordt geopend en wordt onmiddellijk afgesloten zonder dat u toolog in, krijgt u waarschijnlijk deze fout. Deze fout treedt op wanneer er een netwerkfout op uw systeem. Zorg ervoor dat het is mogelijk tooconnect vanuit een browser tooa openbare website en dat de Hallo poorten zijn geopend zoals opgegeven in [toepassingsproxy vereisten](active-directory-application-proxy-enable.md). |
| Schakel fout is opgenomen in het venster Hallo-registratie. Kan niet worden voortgezet | Als u deze fout te zien en vervolgens Hallo-venster wordt gesloten, u hebt ingevoerd Hallo onjuiste gebruikersnaam of wachtwoord. &Opnieuw. |
| Registratie van de connector is mislukt: Zorg ervoor dat u toepassingsproxy in hello Azure-beheerportal en dat u uw Active Directory-gebruikersnaam en wachtwoord correct ingevoerd ingeschakeld. Fout: ' AADSTS50059: Er is geen tenant-identificatiegegevens gevonden in de aanvraag Hallo of impliciet door een opgegeven referenties en zoeken door de service principal URI is mislukt. | U probeert toosign aan met een Microsoft-Account en niet van een domein dat deel uitmaakt van Hallo organisatie-ID van de map Hallo u tooaccess probeert. Zorg ervoor dat Hallo beheerder maakt deel uit van Hallo dezelfde domeinnaam als Hallo tenant domein, bijvoorbeeld als hello Azure AD-domein contoso.com, Hallo beheerder moet admin@contoso.com. |
| Kan geen tooretrieve Hallo huidige-uitvoeringsbeleid voor het uitvoeren van PowerShell-scripts. | Als Hallo connectorinstallatie mislukt, controleert u toomake zorgen dat er geen PowerShell-uitvoeringsbeleid is uitgeschakeld. <br><br>1. Open Hallo Groepsbeleidsobjecteditor.<br>2. Ga te**Computerconfiguratie** > **Beheersjablonen** > **Windows-onderdelen**  >   **Windows PowerShell** en dubbelklikt u op **uitvoering van Script inschakelen**.<br>3. Hallo uitvoeringsbeleid kan worden ingesteld op tooeither **niet geconfigureerd** of **ingeschakeld**. Als instellen te**ingeschakeld**, zorg ervoor dat onder Opties, Hallo uitvoeringsbeleid ingesteld tooeither **scripts lokale en externe ondertekende scripts toestaan** of te**alle scripts toestaan**. |
| Connector is mislukt toodownload Hallo configuratie. | Hallo-Connector clientcertificaat dat wordt gebruikt voor verificatie, is verlopen. Dit kan ook gebeuren als er Hallo-Connector geïnstalleerd achter een proxy. In dit geval Hallo Connector heeft geen toegang tot Internet Hallo en worden toepassingen kunnen tooprovide tooremote gebruikers. Vernieuwen van de vertrouwensrelatie handmatig met Hallo `Register-AppProxyConnector` cmdlet in Windows PowerShell. Als de Connector zich achter een proxy, is het nodig toogrant Internet toohello Connector toegangsaccounts 'network services' en 'Lokaal systeem'. Dit kunt u doen door te verlenen die ze toegang toohello Proxy of door in te stellen die ze toobypass Hallo proxy. |
| Registratie van de connector is mislukt: Zorg ervoor dat u een globale beheerder van uw Active Directory tooregister Hallo Connector. Fout: 'hello registratieverzoek is geweigerd.' | Hallo-alias die u toolog met probeert is niet van een beheerder in dit domein. De Connector is altijd geïnstalleerd voor Hallo-directory die eigenaar is van het domein van de gebruiker Hallo. Zorg ervoor dat Hallo-beheeraccount die u toosign met probeert algemene machtigingen toohello Azure AD-tenant heeft. |

## <a name="kerberos-errors"></a>Kerberos-fouten

Deze tabel bevat informatie over Hallo veelvoorkomende fouten die afkomstig zijn van het Kerberos-installatie en configuratie en bevat suggesties voor naamomzetting.

| Fout | Aanbevolen stappen |
| ----- | ----------------- |
| Kan geen tooretrieve Hallo huidige-uitvoeringsbeleid voor het uitvoeren van PowerShell-scripts. | Als Hallo connectorinstallatie mislukt, controleert u toomake zorgen dat er geen PowerShell-uitvoeringsbeleid is uitgeschakeld.<br><br>1. Open Hallo Groepsbeleidsobjecteditor.<br>2. Ga te**Computerconfiguratie** > **Beheersjablonen** > **Windows-onderdelen**  >   **Windows PowerShell** en dubbelklikt u op **uitvoering van Script inschakelen**.<br>3. Hallo uitvoeringsbeleid kan worden ingesteld op tooeither **niet geconfigureerd** of **ingeschakeld**. Als instellen te**ingeschakeld**, zorg ervoor dat onder Opties, Hallo uitvoeringsbeleid ingesteld tooeither **scripts lokale en externe ondertekende scripts toestaan** of te**alle scripts toestaan**. |
| 12008 - azure AD overschreden Hallo maximum aantal toegestane Kerberos-verificatie geprobeerd toohello back-endserver. | Deze fout kan wijzen op onjuiste configuratie tussen Azure AD en back-end Hallo toepassingsserver of een probleem in de configuratie van de datum en tijd op beide computers. Hallo back-endserver afgewezen Hallo Kerberos-ticket is gemaakt door Azure AD. Controleer of deze Azure AD en Hallo back-end-toepassingsserver correct zijn geconfigureerd. Controleer of de datum en tijd configuratie Hallo op Hallo Azure AD en Hallo back-end-toepassingsserver gesynchroniseerd. |
| 13016 - azure AD kan een Kerberos-ticket namens Hallo gebruiker niet ophalen omdat er geen UPN in Hallo rand token of in Hallo toegang cookie. | Er is een probleem met de Hallo STS-configuratie. Los de UPN-claim Hallo configuratie in Hallo STS. |
| 13019 - azure AD kan een Kerberos-ticket namens Hallo gebruiker niet ophalen vanwege Hallo volgende algemene API-fout. | Deze gebeurtenis mogelijk een onjuiste configuratie tussen Azure AD en domeincontrollerserver hello of een probleem in de configuratie van de datum en tijd op beide computers. Hallo-domeincontroller afgewezen Hallo Kerberos-ticket is gemaakt door Azure AD. Controleer of dat Azure AD en Hallo back-end-toepassingsserver correct zijn geconfigureerd, met name Hallo SPN configuratie. Zorg ervoor dat hello Azure AD is verbonden met het domein toohello hetzelfde domein als domain controller tooensure die domeincontroller Hallo Hallo vertrouwensrelatie te worden ingesteld met Azure AD. Controleer of de datum en tijd configuratie Hallo op Hallo Azure AD en de domeincontroller Hallo gesynchroniseerd. |
| 13020 - azure AD kan een Kerberos-ticket namens Hallo gebruiker niet ophalen omdat Hallo back-endserver SPN niet is gedefinieerd. | Deze gebeurtenis mogelijk een onjuiste configuratie tussen Azure AD en domeincontrollerserver hello of een probleem in de configuratie van de datum en tijd op beide computers. Hallo-domeincontroller afgewezen Hallo Kerberos-ticket is gemaakt door Azure AD. Controleer of dat Azure AD en Hallo back-end-toepassingsserver correct zijn geconfigureerd, met name Hallo SPN configuratie. Zorg ervoor dat hello Azure AD is verbonden met het domein toohello hetzelfde domein als domain controller tooensure die domeincontroller Hallo Hallo vertrouwensrelatie te worden ingesteld met Azure AD. Controleer of de datum en tijd configuratie Hallo op Hallo Azure AD en de domeincontroller Hallo gesynchroniseerd. |
| 13022 - Hallo gebruiker azure AD niet worden geverifieerd omdat de back-endserver Hallo tooKerberos verificatiepogingen met een 401 HTTP-fout reageert. | Deze gebeurtenis kan duiden op onjuiste configuratie tussen Azure AD en back-end Hallo toepassingsserver of een probleem in de configuratie van de datum en tijd op beide computers. Hallo back-endserver afgewezen Hallo Kerberos-ticket is gemaakt door Azure AD. Controleer of deze Azure AD en Hallo back-end-toepassingsserver correct zijn geconfigureerd. Controleer of de datum en tijd configuratie Hallo op Hallo Azure AD en Hallo back-end-toepassingsserver gesynchroniseerd. |

## <a name="end-user-errors"></a>Fouten van de eindgebruiker

Deze lijst bevat informatie over fouten die uw eindgebruikers tegenkomen kunt wanneer ze tooaccess Hallo app proberen en mislukken. 

| Fout | Aanbevolen stappen |
| ----- | ----------------- |
| Hallo-website kan Hallo pagina niet weergeven. | Uw gebruikers foutmelding deze wanneer u probeert tooaccess Hallo app die u als de toepassing hello een IWA is gepubliceerd. Hallo gedefinieerd SPN voor deze toepassing is mogelijk onjuist. Geïntegreerde Windows-apps, zorg ervoor dat Hallo SPN geconfigureerd voor deze toepassing juist is. |
| Hallo-website kan Hallo pagina niet weergeven. | Uw gebruikers foutmelding deze wanneer u probeert tooaccess Hallo app die u als toepassing hello een OWA is gepubliceerd. Dit kan worden veroorzaakt door een van de volgende Hallo:<br><li>Hallo gedefinieerd SPN voor deze toepassing onjuist is. Zorg ervoor dat Hallo SPN geconfigureerd voor deze toepassing juist is.</li><li>Hallo-gebruiker die heeft geprobeerd tooaccess Hallo toepassing gebruikt een Microsoft-account in plaats van Hallo juiste bedrijfsaccount toosign in of Hallo gebruiker is een gastgebruiker. Zorg ervoor dat Hallo gebruiker zich aanmeldt met hun bedrijfsaccount dat overeenkomt met domein Hallo Hallo gepubliceerde toepassing. Gebruikers van Microsoft-Account en Gast geen toegang tot toepassingen IWA.</li><li>Hallo-gebruiker die heeft geprobeerd tooaccess Hallo toepassing is niet correct gedefinieerd voor deze toepassing hello on-premises-zijde. Zorg ervoor dat de gebruiker de juiste machtigingen Hallo is zoals gedefinieerd voor deze back-end-toepassing op Hallo on-premises machine. |
| Deze zakelijke app kan niet worden geopend. U geen geautoriseerde tooaccess deze toepassing zijn. Autorisatie is mislukt. Zorg ervoor dat tooassign Hallo-gebruiker met toegang toothis toepassing. | Uw gebruikers foutmelding deze wanneer u probeert tooaccess Hallo app die u als ze Microsoft-accounts gebruiken in plaats van hun bedrijfsaccount toosign in gepubliceerd. Deze fout kunnen ook ophalen door gastgebruikers. Gebruikers van Microsoft-Account en gasten geen toegang tot toepassingen IWA. Zorg ervoor dat Hallo gebruiker zich aanmeldt met hun bedrijfsaccount dat overeenkomt met domein Hallo Hallo gepubliceerde toepassing.<br><br>U hebt mogelijk Hallo gebruiker voor deze toepassing niet toegewezen. Ga toohello **toepassing** tabblad en klikt u onder **gebruikers en groepen**, deze gebruiker of groep toothis toepassing van de gebruiker toewijzen. |
| Deze zakelijke app kan niet nu worden geopend. Probeer het later opnieuw... Hallo-connector is een time-out. | Uw gebruikers foutmelding deze wanneer u probeert tooaccess Hallo app die u hebt gepubliceerd als ze zijn niet correct gedefinieerd voor deze toepassing hello on-premises-zijde. Zorg ervoor dat uw gebruikers de juiste machtigingen Hallo hebben, zoals is gedefinieerd voor deze back-end-toepassing op Hallo on-premises machine. |
| Deze zakelijke app kan niet worden geopend. U geen geautoriseerde tooaccess deze toepassing zijn. Autorisatie is mislukt. Zorg ervoor dat Hallo-gebruiker een licentie voor Azure Active Directory Premium of Basic heeft. | Uw gebruikers foutmelding deze wanneer u probeert tooaccess Hallo app die u als ze zijn niet expliciet met een Premium en eenvoudige licentie door de beheerder van de abonnee Hallo toegewezen gepubliceerd. Active Directory van de abonnee toohello gaat **licenties** tabblad en zorg ervoor dat deze gebruiker of groep een Premium of Basic-licentie is toegewezen. |

## <a name="my-error-wasnt-listed-here"></a>Mijn fout niet is hier vermeld

Als er een fout of een probleem met Azure AD-toepassingsproxy die niet is vermeld in deze handleiding voor probleemoplossing optreden, graag willen we toohear erover. Verzenden van een e-tooour [feedback team](mailto:aadapfeedback@microsoft.com) met details Hallo Hallo fout dat u is opgetreden.

## <a name="see-also"></a>Zie ook
* [Toepassingsproxy voor Azure Active Directory inschakelen](active-directory-application-proxy-enable.md)
* [Publiceren van toepassingen met toepassingsproxy](active-directory-application-proxy-publish.md)
* [Eenmalige aanmelding inschakelen](active-directory-application-proxy-sso-using-kcd.md)
* [Voorwaardelijke toegang inschakelen](active-directory-application-proxy-conditional-access.md)


<!--Image references-->
[1]: ./media/active-directory-application-proxy-troubleshoot/connectorproperties.png
[2]: ./media/active-directory-application-proxy-troubleshoot/sessionlog.png
