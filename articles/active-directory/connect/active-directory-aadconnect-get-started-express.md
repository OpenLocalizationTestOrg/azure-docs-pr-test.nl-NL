---
title: 'Azure AD Connect: aan de slag met expresinstellingen | Microsoft Docs'
description: Ontdek hoe toodownload, installeren en voer de installatiewizard Hallo voor Azure AD Connect.
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: curtand
ms.assetid: b6ce45fd-554d-4f4d-95d1-47996d561c9f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 79f796fa7738b85e9236e856bddb529379f60390
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-ad-connect-using-express-settings"></a>Aan de slag met Azure AD Connect met expresinstellingen
**Expresinstellingen** van Azure AD Connect worden gebruikt wanneer u een singleforesttopologie hebt en [wachtwoordsynchronisatie](active-directory-aadconnectsync-implement-password-synchronization.md) voor verificatie. **Snelle instellingen** is de standaardoptie Hallo en wordt gebruikt voor Hallo meest geïmplementeerde scenario. U bent slechts enkele snelle klikken opslag tooextend uw lokale directory toohello cloud.

Zorg voordat u begint met de installatie van Azure AD Connect te[Azure AD Connect downloadt](http://go.microsoft.com/fwlink/?LinkId=615771) en volledige Hallo vereiste stappen in [Azure AD Connect: Hardware en vereisten](active-directory-aadconnect-prerequisites.md).

Zie [verwante documentatie](#related-documentation) voor andere scenario's als de expresinstellingen niet met uw topologie overeenkomen.

## <a name="express-installation-of-azure-ad-connect"></a>Snelle installatie van Azure AD Connect
Ziet u deze stappen in de actie in Hallo [video's](#videos) sectie.

1. Meld u aan als een lokale beheerder toohello-server die u wilt dat Azure AD Connect tooinstall op. U moet dit doen op Hallo server desgewenst toobe Hallo synchronisatieserver.
2. Navigeer tooand Dubbelklik **AzureADConnect.msi**.
3. Welkomstscherm Hallo Hallo vak ermee akkoord toohello licentievoorwaarden en klik op **doorgaan**.  
4. Klik op het scherm Expresinstellingen hello **expresinstellingen gebruiken**.  
   ![Welkom tooAzure AD Connect](./media/active-directory-aadconnect-get-started-express/express.png)
5. Voer op Hallo Connect tooAzure AD scherm Hallo gebruikersnaam en wachtwoord van een globale beheerder voor uw Azure AD. Klik op **Volgende**.  
   ![Verbinding maken met tooAzure AD](./media/active-directory-aadconnect-get-started-express/connectaad.png) als u een foutbericht ontvangt en problemen met de connectiviteit hebt, Zie [connectiviteitsproblemen oplossen](active-directory-aadconnect-troubleshoot-connectivity.md).
6. Voer op Hallo Connect tooAD DS scherm Hallo gebruikersnaam en wachtwoord voor een enterprise-beheerdersaccount. U kunt Hallo domeingedeelte in NetBios- of FQDN-indeling, dat wil zeggen FABRIKAM\administrator of fabrikam.com\administrator. Klik op **Volgende**.  
   ![Verbinding maken met tooAD DS](./media/active-directory-aadconnect-get-started-express/connectad.png)
7. Hallo [ **configuratie van aanmelding bij Azure AD** ](active-directory-aadconnect-user-signin.md#azure-ad-sign-in-configuration) pagina wordt alleen weergegeven als u niet hebt [controleren of uw domeinen](../active-directory-add-domain.md) in Hallo [vereisten](active-directory-aadconnect-prerequisites.md).
   ![Niet-geverifieerde domeinen](./media/active-directory-aadconnect-get-started-express/unverifieddomain.png)  
   Als deze pagina wordt weergegeven, controleert u elk domein dat is gemarkeerd met **Niet toegevoegd** en **Niet geverifieerd**. Zorg ervoor dat de domeinen die u gebruikt in Azure AD zijn geverifieerd. Klik op de symbool vernieuwen Hallo wanneer u uw domeinen hebt geverifieerd.
8. Klik op het welkomstscherm gereed tooconfigure, **installeren**.
   * Optioneel op Hallo gereed tooconfigure pagina kunt u Hallo vakje **Start Hallo-synchronisatieproces zodra de configuratie is voltooid** selectievakje. Schakel dit selectievakje uit als u wilt dat toodo aanvullende configuratiestappen, zoals [filteren](active-directory-aadconnectsync-configure-filtering.md). Als u deze optie uitschakelt, Hallo wizard synchronisatie geconfigureerd, maar laat de Hallo planner uitgeschakeld. Kan niet worden uitgevoerd totdat u deze handmatig inschakelt door [opnieuw uit te voeren Hallo-installatiewizard](active-directory-aadconnectsync-installation-wizard.md).
   * Als u Exchange hebt ingeschakeld in uw lokale Active Directory, hebt u ook een optie tooenable [ **hybride implementatie voor Exchange**](https://technet.microsoft.com/library/jj200581.aspx). Schakel deze optie als u plan toohave Exchange-postbussen beide in Hallo cloud en on-premises op Hallo dezelfde tijd.
     ![Gereed tooconfigure Azure AD Connect](./media/active-directory-aadconnect-get-started-express/readytoconfigure.png)
9. Wanneer het Hallo-installatie is voltooid, klikt u op **afsluiten**.
10. Nadat het Hallo-installatie is voltooid, afmelden en opnieuw aanmelden voordat u Synchronization Service Manager of Synchronization Rule Editor gebruiken.

## <a name="videos"></a>Video's
Zie voor een video over het gebruik van de snelle installatie Hallo:

> [!VIDEO https://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Azure-Active-Directory-Connect-Express-Settings/player]
> 
> 

## <a name="next-steps"></a>Volgende stappen
Nu u Azure AD Connect geïnstalleerd hebt kunt u [Hallo installatie verifiëren en licenties toewijzen](active-directory-aadconnect-whats-next.md).

Meer informatie over deze functies, die Hallo-installatie zijn ingeschakeld: [Automatische upgrade](active-directory-aadconnect-feature-automatic-upgrade.md), [onopzettelijk verwijderen voorkomen](active-directory-aadconnectsync-feature-prevent-accidental-deletes.md), en [Azure AD Connect Health](../connect-health/active-directory-aadconnect-health-sync.md).

Meer informatie over deze veelvoorkomende onderwerpen: [scheduler en hoe tootrigger synchronisatie](active-directory-aadconnectsync-feature-scheduler.md).

Lees meer over het [integreren van uw on-premises identiteiten met Azure Active Directory ](active-directory-aadconnect.md).

## <a name="related-documentation"></a>Verwante documentatie
| Onderwerp |
| --- | --- |
| Overzicht Azure AD Connect |
| Installeren met behulp van aangepaste instellingen |
| Upgraden van DirSync |
| Accounts die worden gebruikt voor installatie |

