---
title: 'Azure Active Directory Connect: Veelgestelde vragen - | Microsoft Docs'
description: Deze pagina is Veelgestelde vragen over Azure AD Connect.
services: active-directory
documentationcenter: 
author: billmath
manager: femila
ms.assetid: 4e47a087-ebcd-4b63-9574-0c31907a39a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 39c0b127d3dcf6f45607ad8b4647a9ad79dfc732
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-for-azure-active-directory-connect"></a>Veelgestelde vragen over Azure Active Directory Connect

## <a name="general-installation"></a>Algemene installatie
**V: installatie werkt als hello Azure AD met globale beheerder 2FA ingeschakeld heeft?**  
Met de Hallo builds van februari 2016, wordt dit ondersteund.

**V: is er een manier tooinstall Azure AD Connect zonder toezicht?**  
Alleen ondersteunde tooinstall Azure AD Connect is Hallo-installatiewizard gebruiken. Een installatie zonder toezicht en de achtergrond wordt niet ondersteund.

**V: ik heb een forest waar één domein is niet bereikbaar. Hoe kan ik Azure AD Connect installeren?**  
Met de Hallo builds van februari 2016, wordt dit ondersteund.

**V: Hallo AD DS health agent werkt op server core?**  
Ja. Nadat Hallo-agent is geïnstalleerd, kunt u Hallo registratieproces met behulp van de volgende PowerShell-cmdlet Hallo voltooien: 

`Register-AzureADConnectHealthADDSAgent -Credentials $cred`

## <a name="network"></a>Netwerk
**V: ik heb een firewall, netwerkapparaat of iets anders dat Hallo maximumtijd verbindingen beperkt geopend op mijn netwerk kunt blijven. Hoe lang mijn client side time-out drempelwaarde moet bij gebruik van Azure AD Connect?**  
Alle netwerksoftware, fysieke apparaten of iets anders dat limieten Hallo maximumtijd verbindingen kunnen open blijven een drempel van minstens 5 minuten (300 seconden) voor de verbinding tussen gebruiken moet Hallo server waarop hello Azure AD Connect-client is geïnstalleerd en Azure Active Directory. Dit geldt ook hulpprogramma's voor eerder uitgebrachte tooall Microsoft Identity synchronisatie.

**V: zijn niveaudomeinen (één Label domeinen) ondersteund?**  
Nee, Azure AD Connect biedt geen ondersteuning voor lokale forests/domeinen met behulp van niveaudomeinen.

**V: zijn 'scheidingspunten' NetBios-naam ondersteund?**  
Nee, Azure AD Connect biedt geen ondersteuning voor lokale forests/domeinen waar Hallo NetBIOS-naam een punt bevat '. ' Hallo-naam.

## <a name="federation"></a>Federation
**V: wat moet ik doen als ik een e-mailbericht ontvangen die vragen toorenew mijn Office 365-certificaat**  
Gebruik Hallo richtlijnen die wordt beschreven in Hallo [certificaten vernieuwen](active-directory-aadconnect-o365-certs.md) onderwerp op hoe toorenew Hallo certificaat.

**V: ik heb 'Automatisch bijwerken relying party' instellen voor de relying party O365. Heb ik tootake geen acties als mijn voor token-ondertekening certificaat automatisch boven?**  
Gebruik Hallo richtlijnen die wordt beschreven in artikel Hallo [certificaten vernieuwen](active-directory-aadconnect-o365-certs.md).

## <a name="environment"></a>Omgeving
**V: is it ondersteund toorename Hallo server nadat Azure AD Connect is geïnstalleerd?**  
Nee. Hallo-servernaam wijzigen oorzaak Hallo sync engine toonot worden kunnen tooconnect toohello SQL-database en Hallo service toostart kunnen niet worden.

## <a name="identity-data"></a>Id-gegevens
**V: Hallo UPN (userPrincipalName)-kenmerk in Azure AD komt niet overeen met on-premises UPN - waarom Hallo?**  
Zie de volgende artikelen:

* [Gebruikersnamen in Office 365, Azure of Intune komen niet overeen Hallo lokale UPN of alternatieve aanmeldings-ID](https://support.microsoft.com/en-us/kb/2523192)
* [Wijzigingen zijn niet gesynchroniseerd door hello Azure Active Directory-synchronisatie nadat u Hallo UPN van een gebruiker account toouse een ander federatieve domein wijzigen](https://support.microsoft.com/en-us/kb/2669550)

U kunt ook Azure AD tooallow Hallo sync engine tooupdate Hallo userPrincipalName configureren zoals beschreven in [functies van de service Azure AD Connect-synchronisatie](active-directory-aadconnectsyncservice-features.md).

**V: is it ondersteund toosoft overeen lokale AD-groep/Contact-objecten met bestaande Azure AD-groep/Contact objecten?**  
Nee, dit wordt momenteel niet ondersteund.

**V: is it ondersteund toomanually onveranderbare id genoemd-kenmerk ingesteld op bestaande Azure AD-groep/contactpersoon objecten toohard hieraan tooon-premises AD-groep/Contact objecten?**  
Nee, dit wordt momenteel niet ondersteund.



## <a name="custom-configuration"></a>Aangepaste configuratie
**V: waar zijn Hallo PowerShell-cmdlets voor Azure AD Connect beschreven?**  
Hallo, met uitzondering van Hallo-cmdlets beschreven op deze site worden andere gevonden in Azure AD Connect PowerShell-cmdlets niet ondersteund voor gebruik van de klant.

**V: kan ik gebruiken 'Server exportserver/importeren' gevonden in *Synchronization Service Manager* toomove configuratie tussen servers?**  
Nee. Deze optie worden alle configuratie-instellingen niet ophalen en mag niet worden gebruikt. U moet in plaats daarvan Hallo wizard toocreate Hallo basisconfiguratie op Hallo tweede server gebruiken en Hallo sync regel editor toogenerate PowerShell-scripts toomove een aangepaste regel tussen servers. Zie [migratie bewegen](active-directory-aadconnect-upgrade-previous-version.md#swing-migration).

**V: kunnen wachtwoorden worden opgeslagen in de cache voor de pagina hello Azure aanmelden en kan dit worden voorkomen omdat het een wachtwoord invoerelement met Hallo automatisch aanvullen bevat = 'false' kenmerk?**</br>
Wordt momenteel niet ondersteund wijzigen Hallo HTML-kenmerken van het Hallo wachtwoord invoerveld, met inbegrip van Hallo automatisch aanvullen label. We zijn momenteel gewerkt aan een functie die wordt toegestaan voor aangepaste Javascript waarmee u tooadd elk kenmerkveld toohello-wachtwoord. Dit moet deel uitmaken beschikbaar hoger van 2017.

**V: op Hallo Azure-aanmeldingspagina, worden gebruikersnamen voor gebruikers die zich eerder hebt geregistreerd in met succes weergegeven.  U kunt dit gedrag uitschakelen?**</br>
Wordt momenteel niet ondersteund wijzigen Hallo HTML-kenmerken van de aanmeldingspagina Hallo. We zijn momenteel gewerkt aan een functie die wordt toegestaan voor aangepaste Javascript waarmee u tooadd elk kenmerkveld toohello-wachtwoord. Dit moet deel uitmaken beschikbaar hoger van 2017.

**V: is er een manier tooprevent gelijktijdige sessies?**</br>
Nee.



## <a name="troubleshooting"></a>Problemen oplossen
**V: hoe vind ik meer informatie over Azure AD Connect?**

[Zoek Hallo Microsoft Knowledge Base (KB)](https://www.microsoft.com/en-us/Search/result.aspx?q=azure%20active%20directory%20connect&form=mssupport)

* Zoek Hallo Microsoft Knowledge Base (KB) voor technische oplossingen toocommon schadevergoedings problemen over ondersteuning voor Azure AD Connect.

[Microsoft Azure Active Directory-Forums](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=WindowsAzureAD)

* U kunt zoeken en bladeren voor technische vragen en uit Hallo community antwoorden of uw eigen vraag door te klikken op [hier](https://social.msdn.microsoft.com/Forums/azure/en-US/newthread?category=windowsazureplatform&forum=WindowsAzureAD&prof=required).

[Ondersteuning van de klant Azure AD Connect](https://manage.windowsazure.com/?getsupport=true)

* Gebruik deze koppeling tooget ondersteuning via hello Azure-portal.

