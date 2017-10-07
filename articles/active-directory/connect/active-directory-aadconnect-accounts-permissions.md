---
title: 'Azure AD Connect: Accounts en machtigingen | Microsoft Docs'
description: Dit onderwerp beschrijft Hallo accounts gebruikt en gemaakt en de vereiste machtigingen.
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.reviewer: cychua
ms.assetid: b93e595b-354a-479d-85ec-a95553dd9cc2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: billmath
ms.openlocfilehash: 70a7013e0353d74714ec8a3ff54b3e811789a0b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-accounts-and-permissions"></a>Azure AD Connect: De Accounts en machtigingen
Hello Azure AD Connect-installatiewizard biedt twee verschillende paden:

* In de Express-instellingen vereist Hallo wizard meer bevoegdheden.  Dit is zodat deze kan van uw configuratie eenvoudig, instellen zonder dat u toocreate gebruikers of machtigingen configureren.
* In de aangepaste instellingen Hallo wizard biedt u meer mogelijkheden en opties. Er zijn echter situaties waarin u tooensure die u hebt de juiste machtigingen Hallo zelf moet.

## <a name="related-documentation"></a>Verwante documentatie
Als u hebt geen Hallo documentatie te lezen op [uw on-premises identiteiten integreren met Azure Active Directory](../active-directory-aadconnect.md), hello volgende tabel bevat koppelingen toorelated onderwerpen.

|Onderwerp |Koppeling|  
| --- | --- |
|Azure AD Connect downloaden | [Azure AD Connect downloaden](http://go.microsoft.com/fwlink/?LinkId=615771)|
|Installeren met behulp van snelle instellingen | [Snelle installatie van Azure AD Connect](./active-directory-aadconnect-get-started-express.md)|
|Installeren met behulp van aangepaste instellingen | [Aangepaste installatie van Azure AD Connect](./active-directory-aadconnect-get-started-custom.md)|
|Upgraden van DirSync | [Upgraden van Azure AD-synchronisatiehulpprogramma (DirSync)](./active-directory-aadconnect-dirsync-upgrade-get-started.md)|
|Na installatie | [Hallo-installatie verifiëren en licenties toewijzen](active-directory-aadconnect-whats-next.md)|

## <a name="express-settings-installation"></a>Snelle instellingen voor installatie
In de snelle instellingen Hallo installatie wordt gevraagd om AD DS-ondernemingsadministrator referenties.  Dit is uw lokale Active Directory kunnen worden geconfigureerd met de vereiste machtigingen voor Azure AD Connect. Als u een van DirSync upgrade, zijn Hallo AD DS-ondernemingsadministrators referenties gebruikte tooreset Hallo wachtwoord voor Hallo account dat wordt gebruikt door DirSync. U moet ook een globale beheerder van Azure AD-referenties.

| Pagina van wizard | Referenties die worden verzameld | Machtigingen die vereist zijn | Gebruikt voor |
| --- | --- | --- | --- |
| N.v.t. |Gebruiker actief Hallo-installatiewizard |De beheerder van de lokale server Hallo |<li>Hallo lokale account dat wordt gebruikt als Hallo maakt [sync engine-serviceaccount](#azure-ad-connect-sync-service-account). |
| Verbinding maken met tooAzure AD |Azure AD-directory-referenties |De rol globale beheerder in Azure AD |<li>In hello Azure AD-directory-synchronisatie inschakelen.</li>  <li>Het maken van Hallo [Azure AD-account](#azure-ad-service-account) die wordt gebruikt voor continu synchronisatiebewerkingen in Azure AD.</li> |
| Verbinding maken met tooAD DS |On-premises Active Directory-referenties |Lid van groep van Hallo Ondernemingsadministrators (EA) in Active Directory |<li>Maakt een [account](#active-directory-account) in Active Directory en verleent machtigingen tooit. Dit account gemaakt is gebruikte tooread en write directorygegevens tijdens de synchronisatie.</li> |

### <a name="enterprise-admin-credentials"></a>Enterprise-referenties
Deze referenties worden alleen gebruikt tijdens de installatie van Hallo en worden niet gebruikt nadat Hallo-installatie is voltooid. Hallo ondernemingsadministrator, niet Hallo domeinbeheerder moet ervoor zorgen Hallo machtigingen in Active Directory kunnen worden ingesteld in alle domeinen.

### <a name="global-admin-credentials"></a>Referenties van de globale beheerder
Deze referenties worden alleen gebruikt tijdens de installatie van Hallo en worden niet gebruikt nadat Hallo-installatie is voltooid. Het gebruikte toocreate Hallo is [Azure AD-account](#azure-ad-service-account) gebruikt voor het synchroniseren van wijzigingen tooAzure AD. Hallo-account kunt synchronisatie ook als een functie in Azure AD.

### <a name="permissions-for-hello-created-ad-ds-account-for-express-settings"></a>Machtigingen voor Hallo gemaakt in AD DS-account voor snelle instellingen
Hallo [account](#active-directory-account) voor lezen en schrijven tooAD DS Hallo volgende machtigingen wanneer gemaakt door expresinstellingen hebt gemaakt:

| Machtiging | Gebruikt voor |
| --- | --- |
| <li>Directorywijzigingen repliceren</li><li>Alle repliceren Directory gewijzigd |Wachtwoordsynchronisatie |
| Lezen/schrijven alle eigenschappen van gebruiker |Importeren en Exchange hybrid |
| Lezen/schrijven alle eigenschappen iNetOrgPerson |Importeren en Exchange hybrid |
| Lezen/schrijven-groep voor alle eigenschappen |Importeren en Exchange hybrid |
| Neem contact op met lees-/ schrijffout alle eigenschappen |Importeren en Exchange hybrid |
| Wachtwoord opnieuw instellen |Voorbereiding voor het wachtwoord terugschrijven inschakelen |

## <a name="custom-settings-installation"></a>Instellingen voor aangepaste installatie
Azure AD Connect versie 1.1.524.0 en later heeft Hallo optie toolet hello Azure AD Connect-wizard Hallo account gebruikt tooconnect tooActive Directory maken.  Eerdere versies is vereist dat Hallo-account is gemaakt voordat Hallo-installatie. Hallo-machtigingen die u moet dit account de machtigingen kunnen worden gevonden in [Hallo AD DS-account maken](#create-the-ad-ds-account). 

| Pagina van wizard | Referenties die worden verzameld | Machtigingen die vereist zijn | Gebruikt voor |
| --- | --- | --- | --- |
| N.v.t. |Gebruiker actief Hallo-installatiewizard |<li>De beheerder van de lokale server Hallo</li><li>Als een volledige SQL Server wordt gebruikt, moet de gebruiker Hallo System Administrator (SA) in SQL</li> |Maakt standaard Hallo lokale account dat wordt gebruikt als Hallo [sync engine-serviceaccount](#azure-ad-connect-sync-service-account). Hallo-account wordt alleen gemaakt wanneer Hallo beheerder geen een bepaalde account geeft. |
| Installeren van de Synchronisatieservices, optie voor Service-account |AD of lokale gebruikersaccountreferenties |Gebruiker met machtigingen worden verleend Hallo-installatiewizard |Als Hallo beheerder een account opgeeft, wordt dit account gebruikt als Hallo-serviceaccount voor de synchronisatieservice Hallo. |
| Verbinding maken met tooAzure AD |Azure AD-directory-referenties |De rol globale beheerder in Azure AD |<li>In hello Azure AD-directory-synchronisatie inschakelen.</li>  <li>Het maken van Hallo [Azure AD-account](#azure-ad-service-account) die wordt gebruikt voor continu synchronisatiebewerkingen in Azure AD.</li> |
| Verbinding maken met uw directory’s |On-premises Active Directory-referenties voor elke forest dat is verbonden tooAzure AD |Hallo machtigingen zijn afhankelijk van welke functies u inschakelen en kunt u vinden in [Hallo AD DS-account maken](#create-the-ad-ds-account) |Dit account is gebruikte tooread en write directorygegevens tijdens de synchronisatie. |
| AD FS-Servers |Voor elke server in de lijst Hallo verzamelt Hallo wizard referenties wanneer Hallo-aanmeldingsreferenties van Hallo-gebruiker die de wizard Hallo onvoldoende tooconnect zijn |Domeinbeheerder |Installatie en configuratie van Hallo AD FS-serverfunctie. |
| Web application proxy-servers |Voor elke server in de lijst Hallo verzamelt Hallo wizard referenties wanneer Hallo-aanmeldingsreferenties van Hallo-gebruiker die de wizard Hallo onvoldoende tooconnect zijn |Lokale beheerder op de doelmachine Hallo |Installatie en configuratie van WAP-serverfunctie. |
| Vertrouwensrelatie proxyreferenties |Federation service vertrouwen referenties (Hallo referenties Hallo proxy wordt gebruikt tooenroll voor een certificaat van de vertrouwensrelatie van Hallo FS |Domeinaccount die een lokale beheerder van Hallo AD FS-server |Initiële inschrijving van FS WAP vertrouwensrelatie certificaat. |
| AD FS-serviceaccount pagina "Gebruiken een optie gebruiker account" |AD-gebruikersaccountreferenties |Domeingebruiker |Hallo AD-gebruikersaccount met de referenties die zijn opgegeven wordt als aanmeldingsaccount Hallo van Hallo AD FS-service gebruikt. |

### <a name="create-hello-ad-ds-account"></a>Hallo AD DS-account maken
account dat u op Hallo opgeeft Hallo **verbinding maken met uw adreslijsten** pagina moet aanwezig zijn in de voorgaande tooinstallation Active Directory.  Ook moet het Hallo vereist machtigingen verleend. Hallo-installatiewizard wordt niet gecontroleerd Hallo machtigingen en eventuele problemen zijn alleen gevonden tijdens de synchronisatie.

Machtigingen die u nodig hebt, is afhankelijk van Hallo optionele functies inschakelen. Als u meerdere domeinen hebt, moeten Hallo machtigingen worden verleend voor alle domeinen in het Hallo-forest. Als u deze functies niet inschakelt, Hallo standaard **domeingebruiker** machtigingen voldoende zijn.

| Functie | Machtigingen |
| --- | --- |
| de functie msDS-ConsistencyGuid |Schrijfmachtigingen toohello msDS-ConsistencyGuid kenmerk gedocumenteerd in [ontwerpconcepten - msDS-ConsistencyGuid met als sourceAnchor](active-directory-aadconnect-design-concepts.md#using-msds-consistencyguid-as-sourceanchor). | 
| Wachtwoordsynchronisatie |<li>Directorywijzigingen repliceren</li>  <li>Alle repliceren Directory gewijzigd |
| Hybride implementatie voor Exchange |Schrijven machtigingen toohello kenmerken beschreven in [Exchange hybride terugschrijven](active-directory-aadconnectsync-attributes-synchronized.md#exchange-hybrid-writeback) voor gebruikers, groepen en contactpersonen. |
| Exchange Mail openbare map |Kenmerken voor lezen machtigingen toohello gedocumenteerd in [Exchange Mail openbare map](active-directory-aadconnectsync-attributes-synchronized.md#exchange-mail-public-folder) voor openbare mappen. | 
| Wachtwoord terugschrijven |Schrijven machtigingen toohello kenmerken beschreven in [aan de slag met wachtwoordbeheer](../active-directory-passwords-writeback.md) voor gebruikers. |
| Apparaat terugschrijven |Machtigingen verleend met een PowerShell-script, zoals beschreven in [apparaat terugschrijven](active-directory-aadconnect-feature-device-writeback.md). |
| Groep terugschrijven |Lezen, maken, bijwerken en verwijderen van groep objecten voor gesynchroniseerd **Office 365-groepen**.  Zie voor meer informatie [Write-back van groep](active-directory-aadconnect-feature-preview.md#group-writeback).|

## <a name="upgrade"></a>Upgraden
Wanneer u een van één versie van Azure AD Connect tooa nieuwe release upgrade, moet u Hallo volgende machtigingen:

| Principal | Machtigingen die vereist zijn | Gebruikt voor |
| --- | --- | --- |
| Gebruiker actief Hallo-installatiewizard |De beheerder van de lokale server Hallo |Binaire bestanden worden bijgewerkt. |
| Gebruiker actief Hallo-installatiewizard |Lid van ADSyncAdmins |De wijzigingen aanbrengen tooSync regels en andere configuratie. |
| Gebruiker actief Hallo-installatiewizard |Als u een volledige SQL server gebruikt: DBO (of vergelijkbaar) van de synchronisatiedatabase engine Hallo |Database niveau wijzigingen aanbrengen, zoals het bijwerken van tabellen met nieuwe kolommen. |

## <a name="more-about-hello-created-accounts"></a>Meer informatie over Hallo accounts gemaakt
### <a name="active-directory-account"></a>Active Directory-account
Als u snelle instellingen gebruikt, wordt een account gemaakt in Active Directory dat wordt gebruikt voor synchronisatie. Hallo gemaakt account zich bevindt in het foresthoofddomein in de container gebruikers Hallo Hallo en heeft de naam ervan voorafgegaan door **MSOL_**. Hallo-account is gemaakt met een lange complex wachtwoord dat niet verloopt. Als u een wachtwoordbeleid in uw domein hebt, zorg ervoor dat lange en complexe wachtwoorden zou worden toegestaan voor dit account.

![AD-account](./media/active-directory-aadconnect-accounts-permissions/adsyncserviceaccount.png)

Als u aangepaste instellingen gebruikt, vervolgens bent u verantwoordelijk voor het Hallo-account maken voordat u Hallo-installatie begint.

### <a name="azure-ad-connect-sync-service-account"></a>Azure AD Connect sync-serviceaccount
Hallo sync-service kan worden uitgevoerd onder verschillende accounts. Kunnen worden uitgevoerd binnen een **virtuele serviceaccount** (leverancierspecifiek Kenmerk), een **groep beheerd serviceaccount gebruiken** (gMSA/sMSA), of een normaal gebruikersaccount. Hallo ondersteund opties zijn gewijzigd door hello 2017 April versie van Connect wanneer u een nieuwe installatie doen. Als u een van een oudere versie van Azure AD Connect upgrade, zijn deze extra opties niet beschikbaar.

| Type account | Installatie-optie | Beschrijving |
| --- | --- | --- |
| [Virtuele-serviceaccount](#virtual-service-account) | Snelle en aangepaste, 2017 April en hoger | Dit is Hallo-optie gebruikt voor alle installaties van snelle, met uitzondering van installaties op een domeincontroller. Voor aangepaste is de standaardoptie Hallo tenzij een andere optie wordt gebruikt. |
| [Groep beheerd serviceaccount](#group-managed-service-account) | Aangepaste, 2017 April en hoger | Als u een externe SQL server gebruikt, wordt aangeraden toouse een groep beheerd serviceaccount. |
| [Gebruikersaccount](#user-account) | Snelle en aangepaste, 2017 April en hoger | Een gebruikersaccount dat wordt voorafgegaan door AAD_ wordt alleen gemaakt tijdens de installatie, indien geïnstalleerd op Windows Server 2008 en wanneer geïnstalleerd op een domeincontroller. |
| [Gebruikersaccount](#user-account) | Snelle en aangepaste, 2017 maart en eerdere versies | Een lokaal account voorafgegaan door AAD_ is gemaakt tijdens de installatie. Wanneer u aangepaste installatie, kan een ander account worden opgegeven. |

Als u verbinding maken met een build van maart 2017 gebruiken of lager is, dan wordt het Hallo-wachtwoord op Hallo-serviceaccount moet niet worden ingesteld sinds Windows hello coderingssleutels uit veiligheidsoverwegingen vernietigd. U niet op andere account Hallo account tooany wijzigen zonder Azure AD Connect opnieuw te installeren. Als u een tooa build van 2017 April upgrade of hoger, vervolgens het wachtwoord van de ondersteunde toochange Hallo op Hallo-serviceaccount is, maar niet Hallo account dat wordt gebruikt.

> [!Important]
> U kunt alleen Hallo-serviceaccount instellen op de eerste installatie. Het is niet ondersteund toochange Hallo-serviceaccount nadat Hallo-installatie is voltooid.

Dit is een tabel met Hallo standaard aanbevolen, en ondersteunde opties voor Hallo synchronisatie-serviceaccount.

Legenda:

- **Vet** geeft standaardoptie hello en in de meeste gevallen Hallo aanbevolen optie.
- *Cursief* geeft aan de aanbevolen optie wanneer deze niet de standaardoptie Hallo Hallo.
- 2008 - standaard optie indien geïnstalleerd op Windows Server 2008
- Niet-vette - ondersteunde optie
- Lokaal account - lokale gebruikersaccount op Hallo-server
- Domeinaccount - domeingebruikersaccount
- sMSA - [zelfstandig beheerd serviceaccount](https://technet.microsoft.com/library/dd548356.aspx)
- gMSA - [beheerd serviceaccount gebruiken](https://technet.microsoft.com/library/hh831782.aspx)

| | LocalDB</br>Express | LocalDB/LocalSQL</br>Aangepast telefoonnummer | Externe SQL</br>Aangepast telefoonnummer |
| --- | --- | --- | --- |
| **zelfstandige/werkgroep-machine** | Niet ondersteund | **LEVERANCIERSPECIFIEK KENMERK**</br>Lokale account (2008)</br>Lokaal account |  Niet ondersteund |
| **domein-machine** | **LEVERANCIERSPECIFIEK KENMERK**</br>Lokale account (2008) | **LEVERANCIERSPECIFIEK KENMERK**</br>Lokale account (2008)</br>Lokaal account</br>Domeinaccount</br>sMSA, gMSA | **gMSA**</br>Domeinaccount |
| **Domeincontroller** | **Domeinaccount** | *gMSA*</br>**Domeinaccount**</br>sMSA| *gMSA*</br>**Domeinaccount**|

#### <a name="virtual-service-account"></a>Virtuele-serviceaccount
Een virtuele-serviceaccount is een speciaal type account dat u hebt geen wachtwoord en wordt beheerd door Windows.

![LEVERANCIERSPECIFIEK KENMERK](./media/active-directory-aadconnect-accounts-permissions/aadsyncvsa.png)

Hallo leverancierspecifiek Kenmerk is bedoeld toobe gebruikt met scenario's waarin Hallo synchronisatie-engine en SQL zijn op Hallo dezelfde server. Als u een externe SQL, wordt aangeraden toouse een [groep beheerd serviceaccount gebruiken](#managed-service-account) in plaats daarvan.

Deze functie moet Windows Server 2008 R2 of hoger. Als u Azure AD Connect op Windows Server 2008 installeren, wordt de installatie van de Hallo toousing terugvalt een [gebruikersaccount](#user-account) in plaats daarvan.

#### <a name="group-managed-service-account"></a>Groep beheerd serviceaccount
Als u een externe SQL server gebruikt, wordt aangeraden toousing een **groep beheerd serviceaccount**. Voor meer informatie over het tooprepare uw Active Directory voor groep beheerd serviceaccount, Zie [Group Managed Service Accounts Overview](https://technet.microsoft.com/library/hh831782.aspx).

Deze optie op Hallo toouse [vereiste onderdelen installeren](active-directory-aadconnect-get-started-custom.md#install-required-components) pagina **een bestaand serviceaccount gebruiken**, en selecteer **beheerd serviceaccount**.  
![LEVERANCIERSPECIFIEK KENMERK](./media/active-directory-aadconnect-accounts-permissions/serviceaccount.png)  
Het is ook ondersteunde toouse een [zelfstandig beheerd serviceaccount](https://technet.microsoft.com/library/dd548356.aspx). Echter deze kunnen alleen worden gebruikt op de lokale machine Hallo en er is geen voordeel toouse ze via Hallo standaard virtuele-serviceaccount.

Deze functie moet WindowsServer 2012 of later. Als u een ouder besturingssysteem toouse nodig hebt en gebruik van externe SQL, dan moet u een [gebruikersaccount](#user-account).

#### <a name="user-account"></a>Gebruikersaccount
Een lokale service-account wordt gemaakt door de installatiewizard Hallo (tenzij u Hallo account toouse in de aangepaste instellingen opgeeft). Hallo-account wordt voorafgegaan **AAD_** en gebruikt voor Hallo werkelijke sync-service toorun als. Als u Azure AD Connect op een domeincontroller installeert, wordt in Hallo domein Hallo account gemaakt. Hallo **AAD_** -serviceaccount moet zich bevinden in Hallo domein als:
   - gebruik van een externe server met SQL server
   - gebruik van een proxy die verificatie vereist

![Serviceaccount voor synchronisatie](./media/active-directory-aadconnect-accounts-permissions/syncserviceaccount.png)

Hallo-account is gemaakt met een lange complex wachtwoord dat niet verloopt.

Dit account wordt gebruikt toostore Hallo wachtwoorden voor Hallo andere accounts in een veilige manier. Deze andere accounts wachtwoorden zijn versleuteld in Hallo-database opgeslagen. Hallo persoonlijke sleutels voor Hallo versleutelingssleutels worden beveiligd met Hallo cryptografische services geheime sleutel versleuteling met behulp van Windows Data Protection API (DPAPI).

Als u een volledige SQL Server gebruikt, is Hallo-serviceaccount Hallo DBO van database voor de synchronisatie-engine Hallo Hallo gemaakt. Hallo-service werkt niet zoals bedoeld met andere machtigingen. Een SQL-aanmelding wordt ook gemaakt.

Hallo account krijgt ook machtigingen toofiles, registersleutels en andere gerelateerde toohello synchronisatie-Engine van objecten.

### <a name="azure-ad-service-account"></a>Azure AD-serviceaccount
Een account in Azure AD is voor Hallo synchronisatie van de service gemaakt. Dit account kan worden geïdentificeerd door de weergavenaam.

![AD-account](./media/active-directory-aadconnect-accounts-permissions/aadsyncserviceaccount.png)

Hallo-naam van Hallo server Hallo account wordt gebruikt op kunnen worden geïdentificeerd in de tweede deel Hallo van Hallo-gebruikersnaam. In afbeelding hello is het Hallo-servernaam FABRIKAMCON. Als u staging-servers hebt, heeft elke server een eigen account.

Hallo-serviceaccount wordt gemaakt met een lange complex wachtwoord dat niet verloopt. Een speciale functie zijn toegekend **Directory-synchronisatie Accounts** die alleen machtigingen tooperform directory synchronisatietaken heeft. Deze speciale ingebouwde rol kan niet worden toegekend buiten hello Azure AD Connect-wizard. Hello Azure-portal ziet u dit account met de rol Hallo **gebruiker**.

Er is een limiet van 20 sync-service-accounts in Azure AD. tooget hello lijst met bestaande Azure AD-serviceaccounts in uw Azure AD Hallo volgende Azure AD PowerShell-cmdlet uitvoeren:`Get-AzureADDirectoryRole | where {$_.DisplayName -eq "Directory Synchronization Accounts"} | Get-AzureADDirectoryRoleMember`

ongebruikte tooremove Azure AD-serviceaccounts Hallo volgende Azure AD PowerShell-cmdlet uitvoeren:`Remove-AzureADUser -ObjectId <ObjectId-of-the-account-you-wish-to-remove>`

## <a name="next-steps"></a>Volgende stappen
Lees meer over het [integreren van uw on-premises identiteiten met Azure Active Directory](../active-directory-aadconnect.md).
