---
title: "Azure AD Connect: Ondersteunde topologieën | Microsoft Docs"
description: "In dit onderwerp beschrijft de ondersteunde en niet-ondersteunde topologieën voor Azure AD Connect"
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 1034c000-59f2-4fc8-8137-2416fa5e4bfe
ms.service: active-directory
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: identity
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 41632a54e8e85492fbf1a751ef4e618c8870abe0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="topologies-for-azure-ad-connect"></a>Topologieën voor Azure AD Connect
In dit artikel beschrijft de verschillende on-premises en Azure Active Directory (Azure AD)-topologieën die Azure AD Connect-synchronisatie als belangrijkste Hallo-integratieoplossing gebruiken. Dit artikel bevat de ondersteunde en niet-ondersteunde configuraties.

Hier volgt Hallo legenda voor afbeeldingen in Hallo artikel:

| Beschrijving | Symbool |
| --- | --- |
| On-premises Active Directory-forest |![On-premises Active Directory-forest](./media/active-directory-aadconnect-topologies/LegendAD1.png) |
| On-premises Active Directory met gefilterde importeren |![Active Directory met gefilterde importeren](./media/active-directory-aadconnect-topologies/LegendAD2.png) |
| Azure AD Connect sync-server |![Azure AD Connect sync-server](./media/active-directory-aadconnect-topologies/LegendSync1.png) |
| Azure AD Connect sync-server 'fasering modus' |![Azure AD Connect sync-server 'fasering modus'](./media/active-directory-aadconnect-topologies/LegendSync2.png) |
| GALSync met Forefront Identity Manager (FIM) 2010 of Microsoft Identity Manager (MIM) 2016 |![GALSync met FIM 2010 of MIM 2016](./media/active-directory-aadconnect-topologies/LegendSync3.png) |
| Azure AD Connect sync-server, gedetailleerde |![Azure AD Connect sync-server, gedetailleerde](./media/active-directory-aadconnect-topologies/LegendSync4.png) |
| Azure AD |![Azure Active Directory](./media/active-directory-aadconnect-topologies/LegendAAD.png) |
| Niet-ondersteund scenario |![Niet-ondersteund scenario](./media/active-directory-aadconnect-topologies/LegendUnsupported.png) |

## <a name="single-forest-single-azure-ad-tenant"></a>Eén forest, één Azure AD-tenant
![Topologie voor één forest en een enkele tenant](./media/active-directory-aadconnect-topologies/SingleForestSingleDirectory.png)

meest voorkomende Hallo-topologie is één lokale forest, met een of meerdere domeinen en een enkele Azure AD-tenant. Wachtwoordsynchronisatie is voor Azure AD-verificatie gebruikt. Hallo snelle installatie van Azure AD Connect ondersteunt alleen deze topologie.

### <a name="single-forest-multiple-sync-servers-tooone-azure-ad-tenant"></a>Eén forest, meerdere synchronisatie-servers tooone Azure AD-tenant
![Niet-ondersteunde, gefilterde topologie voor één forest](./media/active-directory-aadconnect-topologies/SingleForestFilteredUnsupported.png)

Met meerdere servers met Azure AD Connect-synchronisatie verbonden toohello dezelfde Azure AD-tenant wordt niet ondersteund, met uitzondering van een [testserver](#staging-server). Het bevat niet-ondersteunde zelfs als deze servers geconfigureerd toosynchronize met een sluiten elkaar wederzijds uit set van objecten zijn. U kunt hebben beschouwd als deze topologie als u alle domeinen in de forest Hallo van één server niet kan bereiken, of als u wilt laden toodistribute over verschillende servers.

## <a name="multiple-forests-single-azure-ad-tenant"></a>Meerdere forests, enkel Azure AD-tenant
![Topologie voor meerdere forests en een enkele tenant](./media/active-directory-aadconnect-topologies/MultiForestSingleDirectory.png)

Veel organisaties hebben omgevingen met meerdere lokale Active Directory-forests. Er zijn diverse redenen voor het hebben van meer dan een lokale Active Directory-forest. Typische voorbeelden zijn ontwerpen met account-bron-forests en Hallo resultaat van een fusie of overname.

Wanneer u meerdere forests, alle forests hebt moet bereikbaar is op één server van Azure AD Connect-synchronisatie. U hebt geen toojoin Hallo server tooa-domein. Indien nodig tooreach alle forests kunt u Hallo server plaatsen in een perimeternetwerk (ook wel DMZ, gedemilitariseerde zone en gescreend subnet).

Hello Azure AD Connect-installatiewizard biedt verschillende opties tooconsolidate gebruikers worden weergegeven in meerdere forests. Hallo-doel is dat een gebruiker slechts één keer wordt weergegeven in Azure AD. Er zijn algemene topologieën die u in de aangepaste installatiepad Hallo in de installatiewizard Hallo kunt configureren. Op Hallo **een unieke id van uw gebruikers** pagina, selecteer Hallo corresponderende optie waarmee uw topologie. Hallo consolidatie is alleen geconfigureerd voor gebruikers. Dubbele groepen zijn niet geconsolideerd met standaardconfiguratie Hallo.

Algemene topologieën worden besproken in Hallo secties over [scheiden topologieën](#multiple-forests-separate-topologies), [full mesh](#multiple-forests-full-mesh-with-optional-galsync), en [account resource topologie Hallo](#multiple-forests-account-resource-forest).

Hallo standaardconfiguratie in Azure AD Connect-synchronisatie wordt ervan uitgegaan dat:

* Elke gebruiker heeft slechts één ingeschakeld-account en Hallo-forest waar dit account bevindt gebruikte tooauthenticate Hallo gebruiker. Deze aanname is voor zowel Wachtwoordsynchronisatie en Federatie. UserPrincipalName en sourceAnchor/onveranderbare id genoemd, is afkomstig van dit forest.
* Elke gebruiker heeft slechts één postvak.
* Hallo-forest die als host fungeert voor Hallo postvak voor een gebruiker heeft Hallo aanbevolen kwaliteit van de gegevens voor kenmerken die zichtbaar zijn in Hallo Exchange globale adreslijst (GAL). Als er geen postvak voor de gebruiker hello, elk forest gebruikte toocontribute kan worden deze kenmerkwaarden die.
* Als u een gekoppeld postvak hebt, is er ook een account in een ander forest dat is gebruikt voor aanmelden.

Als uw omgeving komt niet overeen met deze veronderstellingen, hello volgende gebeuren:

* Als u meer dan één actieve account of meer dan één postvak hebt, wordt Hallo synchronisatie-engine haalt een en Hallo andere worden genegeerd.
* Een gekoppeld postvak met geen andere actieve account is geen geëxporteerde tooAzure AD. Hallo-gebruikersaccount is niet weergegeven als een lid in een groep. Een gekoppeld postvak in DirSync wordt altijd weergegeven als een normale postvak. Deze wijziging is opzettelijk een scenario's verschillend gedrag toobetter ondersteuning voor meerdere forests.

U vindt meer informatie in [Understanding Hallo standaardconfiguratie](active-directory-aadconnectsync-understanding-default-configuration.md).

### <a name="multiple-forests-multiple-sync-servers-tooone-azure-ad-tenant"></a>Meerdere forests, meerdere synchronisatie-servers tooone Azure AD-tenant
![Niet-ondersteunde topologie voor meerdere forests en meerdere synchronisatieservers](./media/active-directory-aadconnect-topologies/MultiForestMultiSyncUnsupported.png)

Met meer dan één Azure AD Connect sync-server verbonden tooa eenmalige Azure AD-tenant wordt niet ondersteund. Hallo uitzondering is Hallo gebruik van een [testserver](#staging-server).

### <a name="multiple-forests-separate-topologies"></a>Afzonderlijke topologieën met meerdere forests
![Optie voor het voorstellen van gebruikers slechts één keer op alle mappen](./media/active-directory-aadconnect-topologies/MultiForestUsersOnce.png)

![Weergave van meerdere forests en afzonderlijke topologieën](./media/active-directory-aadconnect-topologies/MultiForestSeperateTopologies.png)

In deze omgeving worden alle on-premises-forests behandeld als afzonderlijke entiteiten. Er is geen gebruiker is aanwezig in een andere forest. Elk forest heeft een eigen Exchange-organisatie en er is geen GALSync tussen forests Hallo. Deze topologie mogelijk Hallo situatie na een fusie/aanschaf of in een organisatie waar elk bedrijfsonderdeel onafhankelijk optreedt. Deze forests zijn dezelfde organisatie in Azure AD Hallo en worden weergegeven met een geïntegreerde GAL. Elk object in elk forest is in Hallo voorgaande afbeelding, één keer weergegeven in de metaverse Hallo en geaggregeerd in Hallo doel Azure AD-tenant.

### <a name="multiple-forests-match-users"></a>Meerdere forests: overeenkomst met gebruikers
Algemene tooall is die verdeling van deze scenario's en beveiligingsgroepen kunnen een combinatie van gebruikers, contactpersonen en afwijkende beveiligings-Principals (FSP's) bevatten. FSP's worden gebruikt in Active Directory Domain Services (AD DS) toorepresent leden uit andere forests in een beveiligingsgroep. Alle FSP's zijn opgelost toohello echte object in Azure AD.

### <a name="multiple-forests-full-mesh-with-optional-galsync"></a>Meerdere forests: full mesh met optionele GALSync
![Optie voor het gebruik van e-mailkenmerk Hallo voor overeenkomende wanneer gebruikers-id's aanwezig zijn op meerdere mappen](./media/active-directory-aadconnect-topologies/MultiForestUsersMail.png)

![Full mesh-topologie voor meerdere forests](./media/active-directory-aadconnect-topologies/MultiForestFullMesh.png)

Full mesh-topologie kan gebruikers en bronnen toobe zich in een forest. Er zijn doorgaans vertrouwensrelaties in twee richtingen tussen de forests Hallo.

Als Exchange in meer dan één forest aanwezig is, kan er (optioneel) een GALSync on-premises oplossing. Elke gebruiker wordt vervolgens weergegeven als een contactpersoon in alle andere forests. GALSync wordt meestal geïmplementeerd via de FIM 2010 of MIM 2016. Azure AD Connect kan niet worden gebruikt voor lokale GALSync.

In dit scenario identiteitsobjecten die via het e-mailkenmerk Hallo lid zijn. Een gebruiker met een postvak in één forest wordt samengevoegd met de Hallo contactpersonen in Hallo andere forests.

### <a name="multiple-forests-account-resource-forest"></a>Meerdere forests: account-bron-forest
![Optie voor het gebruik van Hallo ObjectSID en msExchMasterAccountSID kenmerken voor het overeenkomende wanneer bestaan-id's op meerdere mappen](./media/active-directory-aadconnect-topologies/MultiForestUsersObjectSID.png)

![Account-resource foresttopologie voor meerdere forests](./media/active-directory-aadconnect-topologies/MultiForestAccountResource.png)

In een topologie met account-resource forest, hebt u een of meer *account* forests met actieve gebruikersaccounts. U hebt ook een of meer *resource* forests met uitgeschakelde accounts.

In dit scenario wordt forestvertrouwensrelaties een (of meer) resource alle accountforests. Hallo bronforest heeft doorgaans een uitgebreid Active Directory-schema in Exchange en Lync. Alle Exchange en Lync services, samen met andere gedeelde services, bevinden zich in dit forest. Gebruikers hebben een uitgeschakelde gebruikersaccount in dit forest en Hallo postvak is gekoppeld toohello account-forest.

## <a name="office-365-and-topology-considerations"></a>Office 365 en aandachtspunten voor topologie
Sommige Office 365-werkbelastingen hebben bepaalde beperkingen op ondersteunde topologieën:

| Workload | Beperkingen |
--------- | ---------
| Exchange Online | Als er meer dan een on-premises Exchange-organisatie (dat wil zeggen, Exchange is geïmplementeerde toomore dan één forest), moet u Exchange 2013 SP1 of hoger. Zie voor meer informatie [hybride implementaties met meerdere Active Directory-forests](https://technet.microsoft.com/library/jj873754.aspx). |
| Skype voor bedrijven | Wanneer u meerdere on-premises-forests, worden alleen Hallo account-resource foresttopologie wordt ondersteund. Zie voor meer informatie [omgevingsvereisten voor Skype voor bedrijven Server 2015](https://technet.microsoft.com/library/dn933910.aspx). |


## <a name="staging-server"></a>Tijdelijke server
![Tijdelijke server in een topologie](./media/active-directory-aadconnect-topologies/MultiForestStaging.png)

Azure AD Connect ondersteunt het installeren van een tweede server in *faseringsmodus*. Een server in deze modus leest de gegevens uit alle gekoppelde mappen, maar schrijft niet iets tooconnected mappen. Hallo normale synchronisatiecyclus wordt gebruikt en daarom is een bijgewerkte kopie van identiteitsgegevens Hallo.

In een noodgeval waar Hallo primaire server mislukt, kunt u failover-overschakeling toohello staging-server. Hiervoor kunt u hello Azure AD Connect-wizard. Deze tweede server kan zich bevinden in een ander datacenter, omdat er geen infrastructuur wordt gedeeld met Hallo primaire server. Elke configuratiewijziging op Hallo primaire server toohello tweede server gemaakt, moet u handmatig kopiëren.

U kunt een tijdelijke server tootest een nieuwe aangepaste configuratie en Hallo effect dat er op uw gegevens. U kunt wijzigingen Hallo bekijken en Hallo-configuratie aanpassen. Wanneer u tevreden met de nieuwe configuratie hello bent, kunt u Hallo staging-server Hallo actieve server maken en Hallo oude active toostaging servermodus instellen.

Ook kunt u deze methode tooreplace Hallo ActiveSync-server. Bereid de nieuwe server Hallo en stel deze toostaging-modus. Zorg ervoor dat deze zich in goede staat verkeren, faseringsmodus (waardoor dit active), uitschakelen en de momenteel actieve server Hallo afsluiten.

Het is mogelijk toohave meer dan één server met tijdelijke bestanden wanneer u meerdere back-ups in verschillende datacenters toohave wilt.

## <a name="multiple-azure-ad-tenants"></a>Meerdere Azure AD-tenants
Het is raadzaam dat een één tenant in Azure AD voor een organisatie.
Voordat u van plan toouse meerdere Azure AD-tenants bent, Zie het artikel Hallo [beheer van beheereenheden in Azure AD](../active-directory-administrative-units-management.md). Deze heeft algemene scenario's waarin u een één tenant kunt.

![Topologie voor meerdere forests en meerdere tenants](./media/active-directory-aadconnect-topologies/MultiForestMultiDirectory.png)

Er is een 1:1-relatie tussen een Azure AD Connect sync-server en een Azure AD-tenant. Voor elke Azure AD-tenant moet u één serverinstallatie van de Azure AD Connect-synchronisatie. exemplaren van Hello Azure AD-tenant zijn geïsoleerd standaard. Dat wil zeggen, gebruikers in een tenant kunnen geen gebruikers wilt weergeven in Hallo andere tenant. Als u wilt dat deze scheiding, is dit een ondersteunde configuratie. Anders moet u Hallo één model van Azure AD-tenant.

### <a name="each-object-only-once-in-an-azure-ad-tenant"></a>Elk object slechts eenmaal in een Azure AD-tenant
![Gefilterde topologie voor één forest](./media/active-directory-aadconnect-topologies/SingleForestFiltered.png)

In deze topologie is een Azure AD Connect-synchronisatie-server verbonden tooeach Azure AD-tenant. Hello Azure AD Connect sync-servers moeten worden geconfigureerd voor het filteren zodat elk heeft een sluiten elkaar wederzijds uit set objecten toooperate op. U kunt bijvoorbeeld het bereik van elke server tooa bepaald domein of organisatie-eenheid.

Een DNS-domein kan worden geregistreerd in slechts één Azure AD-tenant. Hallo UPN's Hallo gebruikers in Hallo lokale Active Directory-exemplaar moet ook afzonderlijke naamruimten gebruiken. Bijvoorbeeld drie afzonderlijke UPN-achtervoegsels in Hallo voorgaande afbeelding, zijn geregistreerd in de lokale Active Directory-exemplaar Hallo: contoso.com en fabrikam.com wingtiptoys.com. Hallo-gebruikers in elk lokale Active Directory-domein gebruiken een andere naamruimte.

Er is geen GALSync tussen exemplaren van hello Azure AD-tenant. Hallo-adresboek in Exchange Online en Skype voor bedrijven toont alleen gebruikers in Hallo dezelfde tenant.

Deze topologie heeft Hallo beperkingen op andere wijze ondersteund scenario's:

* Slechts één van hello Azure AD-tenants, kunt een hybride Exchange inschakelen met Hallo lokale Active Directory-exemplaar.
* Windows 10-apparaten kunnen worden gekoppeld aan slechts één Azure AD-tenant.
* Hallo eenmalige aanmelding (SSO) optie voor wachtwoord synchronisatie en Pass through-verificatie kan worden gebruikt met slechts één Azure AD-tenant.

Hallo vereiste voor een sluiten elkaar wederzijds uit verzameling objecten geldt ook toowriteback. Sommige Write-back-functies worden niet ondersteund met deze topologie omdat ze wordt ervan uitgegaan een configuratie met één on-premises dat. Deze functies:

* Groep terugschrijven met standaardconfiguratie.
* Write-back van apparaat.

### <a name="each-object-multiple-times-in-an-azure-ad-tenant"></a>Elk object meerdere keren in een Azure AD-tenant
![Niet-ondersteunde topologie voor één forest en meerdere tenants](./media/active-directory-aadconnect-topologies/SingleForestMultiDirectoryUnsupported.png) ![Niet-ondersteunde topologie voor één forest en meerdere connectors](./media/active-directory-aadconnect-topologies/SingleForestMultiConnectorsUnsupported.png)

Deze taken worden niet ondersteund:

* Synchronisatie Hallo dezelfde gebruiker toomultiple Azure AD-tenants.
* Maak een configuratie wijzigen, zodat gebruikers in een Azure AD-tenant worden weergegeven als contactpersonen in een andere Azure AD-tenant.
* Azure AD Connect-synchronisatie tooconnect toomultiple Azure AD-tenants wijzigen.

### <a name="galsync-by-using-writeback"></a>GALSync via Write-back
![Niet-ondersteunde topologie voor meerdere forests en meerdere mappen, met GALSync gericht op Azure AD](./media/active-directory-aadconnect-topologies/MultiForestMultiDirectoryGALSync1Unsupported.png) ![Niet-ondersteunde topologie voor meerdere forests en meerdere mappen, met GALSync te focussen op lokale Active Directory](./media/active-directory-aadconnect-topologies/MultiForestMultiDirectoryGALSync2Unsupported.png)

Azure AD-tenants worden geïsoleerd met opzet. Deze taken worden niet ondersteund:

* Hallo-configuratie voor het wijzigen van Azure AD Connect-synchronisatie tooread gegevens uit een andere Azure AD-tenant.
* Exporteer gebruikers als contactpersonen tooanother lokale Active Directory-exemplaar met behulp van Azure AD Connect-synchronisatie.

### <a name="galsync-with-on-premises-sync-server"></a>GALSync met lokale synchronisatieserver
![GALSync in een topologie voor meerdere forests en meerdere mappen](./media/active-directory-aadconnect-topologies/MultiForestMultiDirectoryGALSync.png)

U kunt FIM 2010 of MIM 2016 on-premises toosync gebruikers (via GALSync) tussen twee organisaties met Exchange. Hallo-gebruikers in een organisatie worden weergegeven als externe gebruikers/contacts in Hallo andere organisatie. Deze verschillende on-premises Active Directory exemplaren kunnen vervolgens worden gesynchroniseerd met hun eigen Azure AD-tenants.

## <a name="next-steps"></a>Volgende stappen
hoe tooinstall Azure AD Connect voor deze scenario's, Zie toolearn [aangepaste installatie van Azure AD Connect](active-directory-aadconnect-get-started-custom.md).

Meer informatie over Hallo [Azure AD Connect-synchronisatie](active-directory-aadconnectsync-whatis.md) configuratie.

Meer informatie over [uw on-premises identiteiten integreren met Azure Active Directory](active-directory-aadconnect.md).
