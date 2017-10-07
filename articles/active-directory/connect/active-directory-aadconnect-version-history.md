---
title: 'Azure AD Connect: Versiegeschiedenis van release | Microsoft Docs'
description: Dit artikel vindt u alle versies van Azure AD Connect en Azure AD Sync
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: ef2797d7-d440-4a9a-a648-db32ad137494
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: b55e0f2d426e34ceef9869d5a6d1b0956d8bd076
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-version-release-history"></a>Azure AD Connect: Versiegeschiedenis van release
Azure AD Connect Hello Azure Active Directory (Azure AD) team regelmatig bijgewerkt met nieuwe functies en functionaliteit. Niet alle toevoegingen zijn van toepassing tooall doelgroepen.

Dit artikel is ontworpen toohelp u van bijhouden Hallo-versies die zijn uitgebracht en toounderstand of u de nieuwste versie van tooupdate toohello moet of niet.

Dit is een lijst met verwante onderwerpen:


Onderwerp |  Details
--------- | --------- |
Stappen tooupgrade van Azure AD Connect | Verschillende methoden te[upgrade van een vorige versie-toohello recente](active-directory-aadconnect-upgrade-previous-version.md) Azure AD Connect-release.
Vereiste machtigingen | Zie voor machtigingen tooapply een update vereist, [accounts en machtigingen](./active-directory-aadconnect-accounts-permissions.md#upgrade).
Downloaden| [Azure AD Connect downloaden](http://go.microsoft.com/fwlink/?LinkId=615771).

## <a name="115610"></a>1.1.561.0
Status: Juli 23 2017

### <a name="azure-ad-connect"></a>Azure AD Connect

#### <a name="fixed-issue"></a>Opgelost probleem

* Een probleem waardoor Hallo out of box synchronisatieregel vaste 'Out tooAD - gebruiker onveranderbare id genoemd' toobe verwijderd:

  * Hallo probleem treedt op wanneer de upgrade van Azure AD Connect is voltooid, of wanneer Hallo taakoptie *Update synchronisatieconfiguratie* in hello Azure AD Connect-wizard volledig is gebruikte tooupdate Azure AD Connect-synchronisatie.
  
  * Deze synchronisatieregel is van toepassing toocustomers die hebben ingeschakeld Hallo [msDS-ConsistencyGuid als Bronanker functie](active-directory-aadconnect-design-concepts.md#using-msds-consistencyguid-as-sourceanchor). Deze functie is geïntroduceerd in versie 1.1.524.0 en na. Als u Hallo synchronisatieregel is verwijderd, Azure AD Connect niet langer lokale kunt vullen AD DS-ms-ConsistencyGuid kenmerk met de Hallo waarde van het kenmerk ObjectGuid. Dit voorkomt dat nieuwe gebruikers niet worden ingericht in Azure AD.
  
  * Hallo fix zorgt ervoor dat synchronisatieregel Hallo wordt niet meer verwijderd tijdens de upgrade, of wijziging in de configuratie, zolang het Hallo-functie is ingeschakeld. Voor bestaande klanten die zijn beïnvloed door dit probleem, zorgt Hallo fix er ook voor dat synchronisatieregel Hallo terug na de upgrade van versie van Azure AD Connect toothis wordt toegevoegd.

* Een probleem dat ervoor zorgt dat out-of-box-synchronisatieregels toohave prioriteit die lager is dan 100 opgelost:

  * In het algemeen zijn voorrang waarden 0 - 99 gereserveerd voor aangepaste synchronisatieregels. Tijdens de upgrade zijn Hallo voorrang waarden voor out-of-box-synchronisatieregels bijgewerkte tooaccommodate sync regel wijzigingen. Vervaldatum toothis probleem, worden out-of-box-synchronisatieregels toegewezen prioriteit die lager is dan 100.
  
  * Hallo fix voorkomt u dat Hallo probleem plaatsvindt tijdens de upgrade. Echter, worden niet hersteld Hallo voorrang waarden voor bestaande klanten die zijn beïnvloed door Hallo probleem. Een afzonderlijke oplossing worden vermeld in toekomstige toohelp Hallo met Hallo herstelbewerking.

* Een probleem opgelost waarbij hello [domein en OE filteren scherm](active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering) in hello Azure AD Connect wizard wordt weergegeven *synchroniseren van alle domeinen en OE* optie geselecteerd is, zelfs als filteren op basis van organisatie-eenheid is ingeschakeld.

*   Een probleem opgelost dat veroorzaakt Hallo [mappartities configureren scherm](active-directory-aadconnectsync-configure-filtering.md#organizational-unitbased-filtering) in Hallo Synchronization Service Manager tooreturn een fout als hello *vernieuwen* knop wordt geklikt. Fout bij het Hallo-bericht is *' is een fout opgetreden tijdens het vernieuwen van domeinen: kan geen toocast object van het type 'System.Collections.ArrayList' tootype ' Microsoft.DirectoryServices.MetadirectoryServices.UI.PropertySheetBase.MaPropertyPages.PartitionObject."* Hallo fout treedt op wanneer een nieuw AD-domein is toegevoegd tooan bestaande AD-forest en probeert u tooupdate Azure AD Connect met behulp van de knop Vernieuwen Hallo.

#### <a name="new-features-and-improvements"></a>Nieuwe functies en verbeteringen

* [De functie voor automatisch bijwerken](active-directory-aadconnect-feature-automatic-upgrade.md) is uitgevouwen toosupport klanten met Hallo volgende configuraties:
  * U kunt Hallo apparaat terugschrijven functie hebt ingeschakeld.
  * U kunt Hallo groep Write-back-functie hebt ingeschakeld.
  * Hallo-installatie is niet een snelle instellingen of een upgrade van DirSync.
  * U hebt meer dan 100.000 objecten in Hallo metaverse.
  * U verbinding maakt toomore dan één forest. Snelle installatie verbinding alleen tooone forest.
  * Hallo AD Connector-account is niet-standaardaccount MSOL_ Hallo meer.
  * Hallo-server is toobe ingesteld in de faseringsmodus.
  * U kunt Hallo gebruiker Write-back-functie hebt ingeschakeld.
  
  >[!NOTE]
  >Hallo bereik uitbreiding van de functie voor automatische Upgrade van Hallo heeft betrekking op klanten met Azure AD Connect build 1.1.105.0 en na. Als u niet dat uw Azure AD Connect-server toobe automatisch bijgewerkt wilt, moet u uitvoeren volgende cmdlet op uw Azure AD Connect-server: `Set-ADSyncAutoUpgrade -AutoUpgradeState disabled`. Raadpleeg voor meer informatie over het inschakelen/uitschakelen van automatische Upgrade tooarticle [Azure AD Connect: Automatische upgrade](active-directory-aadconnect-feature-automatic-upgrade.md).

## <a name="115580"></a>1.1.558.0
Status: Wordt niet vrijgegeven. Wijzigingen in deze versie worden opgenomen in versie 1.1.561.0.

### <a name="azure-ad-connect"></a>Azure AD Connect

#### <a name="fixed-issue"></a>Opgelost probleem

* Toobe vast van een probleem waardoor Hallo out of box synchronisatie regel 'Out tooAD - gebruiker onveranderbare id genoemd' verwijderd als configuratie van filteren op basis van organisatie-eenheid is bijgewerkt. Deze synchronisatieregel is vereist voor Hallo [msDS-ConsistencyGuid als Bronanker functie](active-directory-aadconnect-design-concepts.md#using-msds-consistencyguid-as-sourceanchor).

* Een probleem opgelost waarbij hello [domein en OE filteren scherm](active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering) in hello Azure AD Connect wizard wordt weergegeven *synchroniseren van alle domeinen en OE* optie geselecteerd is, zelfs als filteren op basis van organisatie-eenheid is ingeschakeld.

*   Een probleem opgelost dat veroorzaakt Hallo [mappartities configureren scherm](active-directory-aadconnectsync-configure-filtering.md#organizational-unitbased-filtering) in Hallo Synchronization Service Manager tooreturn een fout als hello *vernieuwen* knop wordt geklikt. Fout bij het Hallo-bericht is *' is een fout opgetreden tijdens het vernieuwen van domeinen: kan geen toocast object van het type 'System.Collections.ArrayList' tootype ' Microsoft.DirectoryServices.MetadirectoryServices.UI.PropertySheetBase.MaPropertyPages.PartitionObject."* Hallo fout treedt op wanneer een nieuw AD-domein is toegevoegd tooan bestaande AD-forest en probeert u tooupdate Azure AD Connect met behulp van de knop Vernieuwen Hallo.

#### <a name="new-features-and-improvements"></a>Nieuwe functies en verbeteringen

* [De functie voor automatisch bijwerken](active-directory-aadconnect-feature-automatic-upgrade.md) is uitgevouwen toosupport klanten met Hallo volgende configuraties:
  * U kunt Hallo apparaat terugschrijven functie hebt ingeschakeld.
  * U kunt Hallo groep Write-back-functie hebt ingeschakeld.
  * Hallo-installatie is niet een snelle instellingen of een upgrade van DirSync.
  * U hebt meer dan 100.000 objecten in Hallo metaverse.
  * U verbinding maakt toomore dan één forest. Snelle installatie verbinding alleen tooone forest.
  * Hallo AD Connector-account is niet-standaardaccount MSOL_ Hallo meer.
  * Hallo-server is toobe ingesteld in de faseringsmodus.
  * U kunt Hallo gebruiker Write-back-functie hebt ingeschakeld.
  
  >[!NOTE]
  >Hallo bereik uitbreiding van de functie voor automatische Upgrade van Hallo heeft betrekking op klanten met Azure AD Connect build 1.1.105.0 en na. Als u niet dat uw Azure AD Connect-server toobe automatisch bijgewerkt wilt, moet u uitvoeren volgende cmdlet op uw Azure AD Connect-server: `Set-ADSyncAutoUpgrade -AutoUpgradeState disabled`. Raadpleeg voor meer informatie over het inschakelen/uitschakelen van automatische Upgrade tooarticle [Azure AD Connect: Automatische upgrade](active-directory-aadconnect-feature-automatic-upgrade.md).

## <a name="115570"></a>1.1.557.0
Status: Juli 2017

>[!NOTE]
>Deze versie is niet beschikbaar toocustomers via hello Azure AD Connect automatische Upgrade-functie.

### <a name="azure-ad-connect"></a>Azure AD Connect

#### <a name="fixed-issue"></a>Opgelost probleem
* Een probleem opgelost met Hallo Initialize-ADSyncDomainJoinedComputerSync cmdlet waardoor Hallo geverifieerde domeinnaam op Hallo bestaande service connection point object toobe gewijzigd, zelfs als deze nog steeds een geldig domein geconfigureerd. Dit probleem treedt op wanneer uw Azure AD-tenant meer dan één geverifieerde domeinen die kunnen worden gebruikt heeft voor het serviceverbindingspunt Hallo configureren.

#### <a name="new-features-and-improvements"></a>Nieuwe functies en verbeteringen
* Wachtwoord terugschrijven is nu beschikbaar voor het voorbeeld met Microsoft Azure Government cloud en Microsoft Cloud Duitsland. Raadpleeg voor meer informatie over Azure AD Connect-ondersteuning voor andere service-exemplaren Hallo tooarticle [Azure AD Connect: speciale overwegingen voor exemplaren](active-directory-aadconnect-instances.md).

* Hallo Initialize-ADSyncDomainJoinedComputerSync cmdlet heeft nu een nieuwe optionele parameter met de naam AzureADDomain. Deze parameter kunt u opgeven die domein toobe gebruikt voor het configureren van het serviceverbindingspunt Hallo gecontroleerd.

### <a name="pass-through-authentication"></a>Pass-through-verificatie

#### <a name="new-features-and-improvements"></a>Nieuwe functies en verbeteringen
* Hallo-naam van het Hallo-agent vereist is voor Pass-through-verificatie is gewijzigd van *Microsoft Azure AD Connector voor toepassingsproxy* te*Microsoft Azure AD Connect-verificatie Agent*.

* Inschakelen van Pass-through-verificatie niet langer synchronisatie van wachtwoordhash standaard ingeschakeld.


## <a name="115530"></a>1.1.553.0
Status: Juni 2017

> [!IMPORTANT]
> Er zijn schema en sync regel wijzigingen die zijn geïntroduceerd in deze versie. Azure AD Connect-synchronisatieservice activeren volledige Import en een volledige synchronisatie stappen na de upgrade. Details van Hallo wijzigingen worden hieronder beschreven. tootemporarily volledige Import en een volledige synchronisatie stappen na de upgrade uit te stellen, raadpleeg dan tooarticle [hoe toodefer volledige synchronisatie na de upgrade](active-directory-aadconnect-upgrade-previous-version.md#how-to-defer-full-synchronization-after-upgrade).
>
>

### <a name="azure-ad-connect-sync"></a>Azure AD Connect Sync

#### <a name="known-issue"></a>Bekende problemen
* Er is een probleem dat betrekking heeft op klanten die [filteren op basis van organisatie-eenheid](active-directory-aadconnectsync-configure-filtering.md#organizational-unitbased-filtering) met Azure AD Connect-synchronisatie. Wanneer u toohello navigeert [domein en OE filteren pagina](active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering) in hello Azure AD Connect-wizard, Hallo na gedrag wordt verwacht:
  * Als filteren op basis van organisatie-eenheid is ingeschakeld, Hallo **geselecteerde domeinen en OE's synchroniseren** optie is geselecteerd.
  * Anders Hallo **synchroniseren van alle domeinen en OE** optie is geselecteerd.

Hallo probleem dat zich voordoet is die Hallo **synchroniseren van alle domeinen en organisatie-eenheden optie** is altijd ingeschakeld wanneer u Hallo Wizard uitvoert.  Dit gebeurt zelfs als filteren op basis van organisatie-eenheid is geconfigureerd. Voordat u opslaat configuratiewijzigingen AAD Connect, moet u ervoor dat Hallo **synchroniseren geselecteerde domeinen en organisatie-eenheden-optie is geselecteerd** en controleer of alle OE's die toosynchronize moeten opnieuw worden ingeschakeld. Anders wordt filteren op basis van organisatie-eenheid uitgeschakeld.

#### <a name="fixed-issues"></a>Opgeloste problemen

* Een probleem opgelost met terugschrijven van wachtwoord waarmee een Azure AD-beheerder tooreset Hallo-wachtwoord van een on-premises AD-gebruikersaccount beschermde. Hallo probleem treedt op wanneer het Azure AD Connect is de machtiging Hallo wachtwoord opnieuw instellen via Hallo bevoorrecht account. Hallo wordt besproken in deze versie van Azure AD Connect doordat een Azure AD-beheerder tooreset niet Hallo-wachtwoord van een willekeurige on-premises AD-gebruikersaccount beschermde tenzij Hallo beheerder Hallo eigenaar van dat account. Voor meer informatie raadpleegt u te[Security Advisory 4033453](https://technet.microsoft.com/library/security/4033453).

* Een probleem opgelost toohello [msDS-ConsistencyGuid als Bronanker](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-design-concepts#using-msds-consistencyguid-as-sourceanchor) functie waar Azure AD Connect niet terugschrijven tooon-premises komt AD msDS-ConsistencyGuid kenmerk. Hallo probleem treedt op wanneer er zich meerdere on-premises AD-forests toegevoegd tooAzure AD Connect en Hallo *gebruikersidentiteiten bestaan tussen meerdere mappen optie* is geselecteerd. Wanneer u deze configuratie gebruikt, vullen Hallo resulterende synchronisatieregels Hallo sourceAnchorBinary kenmerk in Hallo Metaverse. Hallo sourceAnchorBinary kenmerk wordt gebruikt als Hallo bronkenmerk voor het kenmerk msDS-ConsistencyGuid. Als gevolg hiervan wordt terugschrijven toohello ms DSConsistencyGuid kenmerk niet uitgevoerd. volgende synchronisatie regels zijn toofix Hallo probleem, bijgewerkte tooensure die sourceAnchorBinary-kenmerk in de Metaverse altijd wordt ingevuld Hallo Hallo:
  * In uit Active Directory - InetOrgPerson AccountEnabled.xml
  * In uit Active Directory - InetOrgPerson Common.xml
  * In uit Active Directory - gebruiker AccountEnabled.xml
  * In uit Active Directory - gebruiker Common.xml
  * In uit Active Directory - gebruiker aanmelden SOAInAAD.xml

* Eerder, zelfs als hello [msDS-ConsistencyGuid als Bronanker](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-design-concepts#using-msds-consistencyguid-as-sourceanchor) functie niet is ingeschakeld, Hallo 'Out tooAD – gebruiker onveranderbare id genoemd' synchronisatieregel wordt nog steeds toegevoegd tooAzure AD Connect. Hallo effect onschadelijk is en niet leidt tot Write-back van msDS-ConsistencyGuid kenmerk toooccur. tooavoid verwarring logica is toegevoegd tooensure die Hallo synchronisatieregel is alleen worden toegevoegd als Hallo-functie is ingeschakeld.

* Een probleem dat de wachtwoord-hash synchronisatie toofail met een foutgebeurtenis 611 veroorzaakt vast. Dit probleem treedt op nadat een of meer domain controllers zijn verwijderd uit on-premises AD. Hallo Hallo na elke synchronisatiecyclus wachtwoord cookie voor adreslijstsynchronisatie van uitgegeven door on-premises AD aanroep-id's bevat van de domeincontrollers Hallo verwijderd met de waarde van 0 USN (Update Sequence Number). Hallo Wachtwoordsynchronisatiebeheer niet kan toopersist synchronisatie cookie met USN-waarde van 0 en mislukt met foutgebeurtenis 611. Tijdens de volgende synchronisatie Hallo cyclus, Hallo Wachtwoordsynchronisatiebeheer gebruikt Hallo laatste permanente cookie voor adreslijstsynchronisatie die USN-waarde van 0 niet bevat. Dit zorgt ervoor dat Hallo dezelfde wachtwoordwijzigingen toobe opnieuw gesynchroniseerd. Met deze oplossing persistente Hallo Wachtwoordsynchronisatiebeheer cookie voor adreslijstsynchronisatie van Hallo correct.

* Eerder, zelfs als de automatische Upgrade is uitgeschakeld met de cmdlet Set-ADSyncAutoUpgrade hello, Hallo automatische Upgrade-proces toocheck voor upgrade regelmatig blijft en is afhankelijk van Hallo gedownload installatieprogramma toohonor deactivering. Met deze oplossing Hallo automatische Upgrade-proces niet langer wordt gecontroleerd voor upgrade regelmatig. Hallo-oplossing wordt automatisch toegepast wanneer de upgrade installatieprogramma voor deze versie van Azure AD Connect eenmaal wordt uitgevoerd.

#### <a name="new-features-and-improvements"></a>Nieuwe functies en verbeteringen

* Voorheen Hallo [msDS-ConsistencyGuid als Bronanker](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-design-concepts#using-msds-consistencyguid-as-sourceanchor) functie is alleen beschikbaar toonew-implementaties. Het is nu beschikbaar tooexisting implementaties. Met name:
  * tooaccess Hallo functie hello Azure AD Connect-wizard start en kies Hallo *Bronanker Update* optie.
  * Deze optie is alleen zichtbaar tooexisting-implementaties die van objectGuid als kenmerk sourceAnchor gebruikmaken.
  * Bij het configureren van de optie Hallo valideert Hallo wizard Hallo status van kenmerk msDS-ConsistencyGuid op Hallo in uw lokale Active Directory. Als het Hallo-kenmerk is niet geconfigureerd op elk gebruikersobject in de map hello, gebruikt Hallo wizard Hallo msDS-ConsistencyGuid als Hallo sourceAnchor kenmerk. Als het Hallo-kenmerk is geconfigureerd op een of meer gebruikersobjecten in Hallo directory, concludeert Hallo wizard Hallo kenmerk wordt gebruikt door andere toepassingen en is niet geschikt is als het kenmerk sourceAnchor en staat niet toe dat Hallo Bronanker wijziging tooproceed. Als u er zeker van bent dat Hallo-kenmerk wordt niet gebruikt door bestaande toepassingen, moet u toocontact ondersteuning voor meer informatie over hoe toosuppress Hallo fout.

* Specifieke te**userCertificate** -kenmerk op apparaatobjecten, Azure AD Connect nu gecontroleerd op waarden van de certificaten die zijn vereist voor [domeinapparaten tooAzure AD voor Windows 10-ervaring verbinden](https://docs.microsoft.com/azure/active-directory/active-directory-azureadjoin-devices-group-policy) en filters Hallo overige voordat tooAzure AD worden gesynchroniseerd. tooenable dit gedrag, Hallo out of box synchronisatieregel 'Out tooAAD - apparaat koppelen SOAInAD' is bijgewerkt.

* Azure AD Connect nu ondersteunt Write-back van Exchange Online **cloudPublicDelegates** kenmerk tooon-premises AD **publicDelegates** kenmerk. Hierdoor Hallo scenario waarbij een Exchange Online-postvak kan worden verleend SendOnBehalfTo rechten toousers met lokale Exchange-postvak. toosupport deze functie, een nieuwe synchronisatieregel out of box 'Out tooAD – Write-back van gebruiker Exchange hybride PublicDelegates' is toegevoegd. Deze synchronisatieregel wordt alleen toegevoegd aan tooAzure AD verbinden wanneer Exchange hybride-functie is ingeschakeld.

*   Azure AD Connect ondersteunt voor de nu synchroniseren Hallo **altRecipient** kenmerk vanuit Azure AD. Deze wijziging, volgens de regels voor out-of-box-synchronisatie is toosupport bijgewerkt tooinclude Hallo vereist kenmerkstroom:
  * In uit Active Directory-gebruiker Exchange
  * Uitgaand tooAAD – gebruiker ExchangeOnline
  
* Hallo **cloudSOAExchMailbox** kenmerk in Hallo Metaverse geeft aan of een bepaalde gebruiker Exchange Online-postvak of niet. De definitie is bijgewerkte tooinclude extra Exchange Online RecipientDisplayTypes als die apparatuur en vergaderzaal postvakken. tooenable deze wijziging, Hallo definitie van Hallo cloudSOAExchMailbox kenmerk vinden onder synchronisatieregel van out of box 'In van AAD – gebruiker Exchange hybride', is bijgewerkt van:

```
CBool(IIF(IsNullOrEmpty([cloudMSExchRecipientDisplayType]),NULL,BitAnd([cloudMSExchRecipientDisplayType],&amp;HFF) = 0))
```

... toohello volgende:

```
CBool(
  IIF(IsPresent([cloudMSExchRecipientDisplayType]),(
    IIF([cloudMSExchRecipientDisplayType]=0,True,(
      IIF([cloudMSExchRecipientDisplayType]=2,True,(
        IIF([cloudMSExchRecipientDisplayType]=7,True,(
          IIF([cloudMSExchRecipientDisplayType]=8,True,(
            IIF([cloudMSExchRecipientDisplayType]=10,True,(
              IIF([cloudMSExchRecipientDisplayType]=16,True,(
                IIF([cloudMSExchRecipientDisplayType]=17,True,(
                  IIF([cloudMSExchRecipientDisplayType]=18,True,(
                    IIF([cloudMSExchRecipientDisplayType]=1073741824,True,(
                       IF([cloudMSExchRecipientDisplayType]=1073741840,True,False)))))))))))))))))))),False))

```

* De volgende toegevoegde Hallo instellen X509Certificate2-compatibele functies voor het maken van synchronisatie expressies toohandle certificaat regelwaarden in Hallo userCertificate kenmerk:

    ||||
    | --- | --- | --- |
    |CertSubject|CertIssuer|CertKeyAlgorithm|
    |CertSubjectNameDN|CertIssuerOid|CertNameInfo|
    |CertSubjectNameOid|CertIssuerDN|IsCert|
    |CertFriendlyName|certThumbprint|CertExtensionOids|
    |CertFormat|CertNotAfter|CertPublicKeyOid|
    |CertSerialNumber|CertNotBefore|CertPublicKeyParametersOid|
    |CertVersion|CertSignatureAlgorithmOid|Selecteer|
    |CertKeyAlgorithmParams|CertHashString|waar|
    |||met|

* Wijzigingen in het schema te volgen zijn geïntroduceerd tooallow klanten toocreate aangepaste synchronisatie regels tooflow sAMAccountName domainNetBios en domainFQDN voor een groepsobjecten worden weergegeven, evenals distinguishedName voor gebruikersobjecten:

  * Volgende kenmerken zijn tooMV schema toegevoegd:
    * Groep: AccountName
    * Groep: domainNetBios
    * Groep: domainFQDN
    * Persoon: distinguishedName

  * Volgende kenmerken zijn tooAzure schema van de AD-Connector toegevoegd:
    * Groep: OnPremisesSamAccountName
    * Groep: NetBiosName
    * Groep: DNS-domeinnaam
    * Gebruiker: OnPremisesDistinguishedName

* Hallo ADSyncDomainJoinedComputerSync cmdlet script heeft nu een nieuwe optionele parameter met de naam AzureEnvironment. Hallo-parameter is gebruikte toospecify welke regio Hallo bijbehorende Azure Active Directory-tenant wordt gehost in. Geldige waarden zijn:
  * AzureCloud (standaard)
  * AzureChinaCloud
  * AzureGermanyCloud
  * USGovernment
 
* Bijgewerkte Sync Rule Editor toouse deelnemen aan (in plaats van ingericht) als de standaardwaarde Hallo van het koppelingstype tijdens het maken van de regel voor synchronisatie.

### <a name="ad-fs-management"></a>AD FS-beheer

#### <a name="issues-fixed"></a>Problemen worden opgelost

* Volgende URL's zijn nieuwe WS-Federation-eindpunten die zijn geïntroduceerd in Azure AD tooimprove tolerantie tegen storing van de verificatie en worden toegevoegd tooon-premises AD FS-configuratie van vertrouwensrelaties van derden beantwoorden:
  * https://Ests.Login.microsoftonline.com/Login.srf
  * https://stamp2.Login.microsoftonline.com/Login.srf
  * https://CCS.Login.microsoftonline.com/Login.srf
  * https://CCS-sdf.Login.microsoftonline.com/Login.srf
  
* Een probleem dat AD FS toogenerate onjuist claimwaarde voor IssuerID heeft opgelost. Hallo probleem doet zich voor als er meerdere geverifieerde domeinen in hello Azure AD-tenant en het domeinachtervoegsel Hallo van Hallo userPrincipalName kenmerk gebruikt toogenerate Hallo IssuerID claim ten minste is 3 niveaus diep (bijvoorbeeld johndoe@us.contoso.com). Hallo-probleem is opgelost door Hallo reguliere expressie die wordt gebruikt door de claimregels Hallo bij te werken.

#### <a name="new-features-and-improvements"></a>Nieuwe functies en verbeteringen
* Voorheen kan Hallo ADFS Certificate Management-functie met Azure AD Connect alleen worden gebruikt met AD FS-farms beheerd via Azure AD Connect. U kunt nu Hallo functie gebruiken met AD FS-farms die niet worden beheerd met Azure AD Connect.

## <a name="115240"></a>1.1.524.0
Uitgebracht: Mei 2017

> [!IMPORTANT]
> Er zijn schema en sync regel wijzigingen die zijn geïntroduceerd in deze versie. Azure AD Connect-synchronisatieservice activeren volledige Import en een volledige synchronisatie stappen na de upgrade. Details van Hallo wijzigingen worden hieronder beschreven.
>
>

**Opgeloste problemen:**

Azure AD Connect-synchronisatie

* Een probleem dat ervoor zorgt automatische Upgrade toooccur op Hallo Azure AD Connect-server dat ook als met Hallo Set ADSyncAutoUpgrade cmdlet Hallo-functie is uitgeschakeld door de klant wordt opgelost. Met deze oplossing Hallo automatische Upgrade-proces op Hallo server nog steeds gecontroleerd op upgrade periodiek, maar hello gedownloade installatieprogramma respecteert Hallo-configuratie automatisch bijwerken.
* Tijdens een upgrade ter plekke van DirSync maakt Azure AD Connect een Azure AD-service-account toobe door hello Azure AD-connector gebruikt voor het synchroniseren met Azure AD. Wanneer het Hallo-account is gemaakt, wordt Azure AD Connect verifieert met Azure AD met Hallo-account. Soms verificatie is mislukt vanwege tijdelijke problemen waardoor DirSync in-place upgrade toofail op zijn beurt met de fout *' uitvoerende configureren AAD Sync-taak is een fout is opgetreden: AADSTS50034: toosign in deze toepassing, Hallo-account moet worden toegevoegd toohello xxx.onmicrosoft.com directory."* tooimprove hello tolerantie van upgrade van DirSync, Azure AD Connect Hallo verificatie stap nu opnieuw.
* Er is een probleem met de build 443 waardoor DirSync in-place upgrade toosucceed maar uitvoeringsprofielen vereist is voor adreslijstsynchronisatie niet worden gemaakt. Herstel van logica is opgenomen in deze versie van Azure AD Connect. Wanneer de klant upgrades toothis build, wordt Azure AD Connect detecteert uitvoeringsprofielen ontbreekt en ze zijn gemaakt.
* Een probleem dat ervoor zorgt Wachtwoordsynchronisatie proces toofail toostart met 6900 van gebeurtenis-ID en de fout dat vast *'Een item met dezelfde sleutel is al toegevoegd Hallo'*. Dit probleem treedt op als u OE filteren configuratiepartitie tooinclude AD configuratie bijwerken. Dit probleem, Wachtwoordsynchronisatie verwerken nu toofix synchroniseert wachtwoordwijzigingen uit domeinpartities alleen AD. Niet-domeinpartities zoals configuratiepartitie worden overgeslagen.
* Tijdens de snelle installatie Azure AD Connect maakt een on-premises AD DS account toobe die wordt gebruikt door Hallo AD connector toocommunicate met on-premises AD. Voorheen Hallo-account is gemaakt met Hallo PASSWD_NOTREQD-vlag ingesteld op Hallo Gebruikersaccountbeheer kenmerk en een willekeurig wachtwoord is ingesteld op Hallo-account. Nu verwijdert Azure AD Connect expliciet Hallo PASSWD_NOTREQD vlag nadat Hallo wachtwoord is ingesteld op Hallo-account.
* Een probleem dat ervoor zorgt de upgrade toofail DirSync met fout dat opgelost *' een impasse opgetreden in sql server die tijdens het tooacquire een toepassingsvergrendeling'* wanneer Hallo mailNickname kenmerk is gevonden in Hallo lokale AD-schema, maar is niet begrensd toohello objectklasse AD-gebruiker.
* Vaste een probleem dat ervoor zorgt apparaat terugschrijven functie tooautomatically dat worden uitgeschakeld wanneer een beheerder met behulp van Azure AD Connect-wizard voor configuratie Azure AD Connect-synchronisatie wordt bijgewerkt. Dit wordt veroorzaakt door het Hallo wizard presterende vereiste controleren voor Hallo bestaande apparaat terugschrijven configuratie in on-premises AD en Hallo controle mislukt. Hallo-oplossing is tooskip Hallo selectievakje als write-back van apparaat al eerder is ingeschakeld.
* tooconfigure OE filteren, kunt u Azure AD Connect-wizard hello gebruiken of Hallo Synchronization Service Manager. Voorheen als u hello Azure AD Connect wizard tooconfigure OE-filters, zijn nieuwe organisatie-eenheden die zijn gemaakt daarna opgenomen voor directory-synchronisatie. Als u niet dat nieuwe OE's toobe opgenomen wilt, moet u de organisatie-eenheid configureren voor het filteren met behulp van Hallo Synchronization Service Manager. U kunt nu bereiken Hallo hetzelfde gedrag met behulp van Azure AD Connect-wizard.
* Een probleem dat ervoor zorgt dat de opgeslagen procedures die zijn vereist voor Azure AD Connect toobe gemaakt onder het Hallo-schema van Hallo beheerder, installeren in plaats van onder Hallo dbo-schema opgelost.
* Een probleem dat ervoor zorgt Hallo TrackingId kenmerk geretourneerd door Azure AD-toobe weggelaten in Hallo gebeurtenislogboeken AAD Connect Server dat opgelost. Hallo probleem treedt op als Azure AD Connect een bericht voor de omleiding van Azure AD ontvangt en Azure AD Connect kan niet tooconnect toohello eindpunt is. Hallo TrackingId wordt gebruikt door ondersteuningsmedewerkers toocorrelate met side-service worden tijdens het oplossen van problemen.
* Wanneer Azure AD Connect LargeObject fout van Azure AD ontvangt, Azure AD Connect wordt een gebeurtenis met gebeurtenis-id 6941 en het bericht gegenereerd *'hello ingerichte object is te groot. Het aantal kenmerkwaarden voor dit object Hallo trim'.* Op Hallo dezelfde tijdstip, Azure AD Connect ook een misleidend gebeurtenis met gebeurtenis-id 6900 en het bericht genereert *' Microsoft.Online.Coexistence.ProvisionRetryException: kan geen toocommunicate Hello Windows Azure Active Directory-service. "* toominimize verwarring, Azure AD Connect niet langer genereert Hallo laatste geval wanneer LargeObject fout wordt ontvangen.
* Een probleem dat ervoor zorgt Hallo Synchronization Service Manager toobecome niet reageert dat wanneer u probeert tooupdate Hallo configuratie voor algemene LDAP-connector opgelost.

**Nieuwe functies/verbeteringen:**

Azure AD Connect-synchronisatie
* Wijzigingen in synchronisatie-regel – Hallo volgende synchronisatie regel wijzigingen zijn uitgevoerd:
  * Synchronisatie van bijgewerkte standaardregel ingesteld toonot export kenmerken **userCertificate** en **userSMIMECertificate** als Hallo kenmerken meer dan 15 waarden hebben.
  * AD-kenmerken **werknemer-id** en **msExchBypassModerationLink** zijn nu opgenomen in de regelset van Hallo standaard synchronisatie.
  * AD-kenmerk **photo** is verwijderd uit de standaard synchronisatie regelset.
  * Toegevoegd **preferredDataLocation** toohello Metaverse planning en planning van de AAD-Connector. Klanten die willen tooupdate die beide kenmerken in Azure AD kunnen implementeren aangepaste regels toodo dus worden gesynchroniseerd. toofind voor meer informatie over het Hallo-kenmerk verwijzen tooarticle sectie [Azure AD Connect-synchronisatie: hoe een wijziging toohello toomake-configuratie - synchronisatie inschakelen van PreferredDataLocation standaard](active-directory-aadconnectsync-change-the-configuration.md#enable-synchronization-of-preferreddatalocation).
  * Toegevoegd **userType** toohello Metaverse planning en planning van de AAD-Connector. Klanten die willen tooupdate die beide kenmerken in Azure AD kunnen implementeren aangepaste regels toodo dus worden gesynchroniseerd.

* Azure AD Connect nu automatisch schakelt Hallo van ConsistencyGuid kenmerk als Hallo Bronanker kenmerk voor on-premises gebruiken AD-objecten. Bovendien kunnen de Azure AD Connect vult Hallo ConsistencyGuid kenmerk met de waarde van het kenmerk objectGuid Hallo als deze leeg is. Deze functie is alleen van toepassing toonew-implementatie. toofind voor meer informatie over deze functie verwijzen tooarticle sectie [Azure AD Connect: concepten - msDS-ConsistencyGuid met als sourceAnchor ontwerpen](active-directory-aadconnect-design-concepts.md#using-msds-consistencyguid-as-sourceanchor).
* Nieuwe cmdlet Invoke-ADSyncDiagnostics is het oplossen van problemen diagnosticeren toegevoegde toohelp synchronisatie van wachtwoordhash problemen met betrekking tot. Raadpleeg voor informatie over het gebruik van de cmdlet Hallo tooarticle [Wachtwoordsynchronisatie met Azure AD Connect-synchronisatie oplossen](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnectsync-troubleshoot-password-synchronization).
* Azure AD Connect nu ondersteunt synchroniseren Mail-Enabled openbare map objecten uit een on-premises AD tooAzure AD. U kunt met behulp van Azure AD Connect-wizard onder optionele functies Hallo-functie inschakelen. toofind voor meer informatie over deze functie verwijzen tooarticle [Office 365 Directory op basis van rand blokkeren ondersteuning voor lokale Mail ingeschakeld openbare mappen](https://blogs.technet.microsoft.com/exchange/2017/05/19/office-365-directory-based-edge-blocking-support-for-on-premises-mail-enabled-public-folders).
* Azure AD Connect is vereist voor een AD DS account toosynchronize on-premises AD. Als u Azure AD Connect geïnstalleerd Hallo Express-modus met eerder u kan Hallo referenties opgeven van een Enterprise-beheerdersaccount en Azure AD Connect maakt Hallo AD DS-account vereist. Voor een aangepaste installatie en het toevoegen van bestaande forests tooan-implementatie, waren u echter vereist tooprovide Hallo AD DS-account in plaats daarvan. Nu hebt u ook Hallo optie tooprovide Hallo referenties van een Enterprise-beheerdersaccount tijdens een aangepaste installatie en laat u Azure AD Connect Hallo AD DS-account vereist maken.
* Azure AD Connect ondersteunt nu SQL AOA. Voordat u Azure AD Connect installeert, moet u SQL AOA inschakelen. Tijdens de installatie van detecteert Azure AD Connect of Hallo opgegeven SQL-exemplaar is ingeschakeld voor SQL AOA. Als SQL AOA is ingeschakeld, wordt Azure AD Connect meer cijfers uit als SQL AOA geconfigureerde toouse synchrone replicatie of asynchrone replicatie is. Bij het instellen van Hallo beschikbaarheidsgroep-Listener, verdient het aanbeveling Hallo RegisterAllProvidersIP eigenschap too0 in te stellen. Dit is omdat Azure AD Connect momenteel SQL Native Client tooconnect tooSQL gebruikt en SQL Native Client biedt geen ondersteuning voor Hallo gebruik van de MultiSubNetFailover-eigenschap.
* Als u LocalDB als Hallo database voor uw Azure AD Connect-server gebruikt en heeft de groottelimiet van 10 GB-bereikt, wordt niet meer Hallo Synchronization Service gestart. Eerder, moet u tooperform ShrinkDatabase-bewerking op Hallo LocalDB tooreclaim voldoende ruimte DB voor Hallo synchronisatieservice toostart. Na waarop, u kunt gebruik Hallo toodelete Synchronization Service Manager uitvoeren geschiedenis tooreclaim meer DB ruimte. U kunt nu starten ADSyncPurgeRunHistory cmdlet toopurge geschiedenisgegevens uitvoering vanuit LocalDB tooreclaim DB ruimte gebruiken. Verder kan deze cmdlet biedt ondersteuning voor de offline modus (door te geven Hallo - parameter offline) die kan worden gebruikt bij Hallo Synchronization-Service wordt niet uitgevoerd. Opmerking: Hallo offlinemodus kan alleen worden gebruikt als hello Synchronization-Service wordt niet uitgevoerd en het Hallo-database die wordt gebruikt LocalDB is.
* tooreduce hello hoeveelheid opslagruimte vereist, Azure AD Connect sync foutdetails nu bij het opslaan in LocalDB/SQL-databases worden gecomprimeerd. Bij het bijwerken van een oudere versie van Azure AD Connect toothis versie, voert Azure AD Connect een eenmalige compressie op bestaande foutdetails voor synchronisatie.
* Voorheen na het bijwerken van de organisatie-eenheid filteren configuratie u moet handmatig uitvoeren volledige import tooensure bestaande objecten zijn correct opgenomen/uitgesloten van directory-synchronisatie. Nu Azure AD Connect volledige import automatisch geactiveerd tijdens de volgende synchronisatie Hallo cyclus. Bovendien kunnen de volledige import is alleen worden toegepast toohello AD connectors Hallo update van invloed op. Opmerking: deze verbetering is van toepassing tooOU voor het filteren van updates die zijn gemaakt met behulp van alleen hello Azure AD Connect-wizard. Het is niet van toepassing tooOU filteren update gemaakt met behulp van Hallo Synchronization Service Manager.
* Voorheen filteren op basis van een groep gebruikers, groepen ondersteunt en neem contact op met alleen objecten. Ondersteunt nu het, filteren op basis van de groep ook computerobjecten.
* U kunt eerder Connectorruimte gegevens verwijderen zonder de Azure AD Connect sync scheduler uit te schakelen. Nu is Hallo Synchronization Service Manager blokken Hallo verwijderen van gegevens van de Connectorruimte als wordt gedetecteerd dat scheduler Hallo ingeschakeld. Bovendien wordt een waarschuwing tooinform klanten over mogelijk gegevensverlies geretourneerd als Hallo adresruimtegegevens Connector is verwijderd.
* Eerder, moet u de schrijffouten PowerShell voor Azure AD Connect-wizard toorun correct uitschakelen. Dit probleem is gedeeltelijk opgelost. Als u Azure AD Connect-wizard toomanage sync-configuratie gebruikt, kunt u PowerShell schrijffouten inschakelen. Als u Azure AD Connect-wizard toomanage AD FS-configuratie gebruikt, moet u PowerShell schrijffouten uitschakelen.



## <a name="114860"></a>1.1.486.0
Uitgebracht: April 2017

**Opgeloste problemen:**
* Hallo-probleem opgelost waarbij Azure AD Connect zal niet goed geïnstalleerd op een gelokaliseerde versie van Windows Server.

## <a name="114840"></a>1.1.484.0
Uitgebracht: April 2017

**Bekende problemen:**

* Deze versie van Azure AD Connect zal niet goed geïnstalleerd als Hallo volgende voorwaarden alle waar zijn:
   1. U kunt beide DirSync in-place upgrade of nieuwe installatie van Azure AD Connect wilt uitvoeren.
   2. U gebruikt een gelokaliseerde versie van Windows Server waarbij de naam van de ingebouwde groep Administrators op de server Hallo Hallo 'Administrators' niet.
   3. U gebruikt Hallo standaard SQL Server 2012 Express LocalDB geïnstalleerd met Azure AD Connect in plaats van uw eigen volledig SQL bieden.

**Opgeloste problemen:**

Azure AD Connect-synchronisatie
* Een probleem opgelost waarbij Hallo sync scheduler Hallo volledige synchronisatie stap overslaan als een of meer connectors uitvoeringsprofiel voor die stap synchronisatie ontbreken. Bijvoorbeeld, u handmatig hebt toegevoegd een verbindingslijn Hallo Synchronization Service Manager met zonder te maken van een Delta-Import profiel voor het uitvoert. Deze oplossing zorgt ervoor dat Hallo sync scheduler toorun Delta-Import voor andere connectors blijft.
* Een probleem opgelost waarbij Hallo Synchronization Service onmiddellijk stopt met de verwerking een uitvoeringsprofiel wanneer het is een probleem optreedt met een van de stappen Hallo uitvoeren. Deze oplossing zorgt ervoor dat Hallo Synchronization Service slaat die stap worden uitgevoerd en blijft tooprocess Hallo rest. U hebt bijvoorbeeld een Delta-Import profiel voor uw AD-connector uitvoert met meerdere uitgevoerde stappen (één voor elk lokale AD-domein). Hallo Synchronization Service wordt uitgevoerd Delta-Import Hello andere AD-domeinen zelfs als een van deze problemen met de netwerkverbinding heeft.
* Een probleem dat ervoor zorgt hello Azure AD-Connector update toobe overgeslagen tijdens de automatische Upgrade dat opgelost.
* Een probleem opgelost dat oorzaken Azure AD Connect tooincorrectly bepalen of Hallo-server een domeincontroller is tijdens de installatie in Schakel oorzaken DirSync toofail upgraden.
* Vaste een probleem waarbij DirSync in-place upgrade toonot maakt een profiel voor hello Azure AD-Connector uitvoert.
* Een probleem opgelost waarbij Hallo Synchronization Service Manager-gebruikersinterface reageert niet meer wanneer u probeert tooconfigure algemene LDAP-Connector.

AD FS-beheer
* Een probleem opgelost waarbij hello Azure AD Connect-wizard als primaire Hallo AD FS-knooppunt verplaatst tooanother server is mislukt.

Bureaublad SSO
* Een probleem opgelost in hello Azure AD Connect-wizard waar hello aanmeldingsscherm kunt u niet bureaublad SSO-functie inschakelen als u synchronisatie van wachtwoorden hebt gekozen als uw aanmeldoptie tijdens de installatie van nieuwe.

**Nieuwe functies/verbeteringen:**

Azure AD Connect-synchronisatie
* Azure AD Connect-synchronisatie ondersteunt nu het Hallo-gebruik van virtuele-serviceaccount, beheerd serviceaccount en beheerd serviceaccount als serviceaccount. Dit geldt toonew installatie van Azure AD Connect. Wanneer u Azure AD Connect installeert:
    * Standaard Azure AD Connect-wizard maakt een virtuele-Account en gebruikt als serviceaccount ervan.
    * Als u op een domeincontroller installeert, terugvalt Azure AD Connect tooprevious gedrag waarbij een domeingebruikersaccount maakt en in plaats daarvan gebruikt als serviceaccount ervan.
    * U kunt het standaardgedrag Hallo negeren door een van de volgende Hallo:
      * Een groep beheerd serviceaccount
      * Een beheerd serviceaccount
      * Een domeingebruikersaccount zijn.
      * Een lokale gebruikersaccount
* Als u een nieuwe build van Azure AD Connect die tooa upgrade voorheen connectors bijwerken of wijzigingen in synchronisatie-regel, Azure AD Connect de cyclus van een volledige synchronisatie wordt geactiveerd. Azure AD Connect activeert nu selectief volledige Import stap alleen voor connectors met update, en volledige synchronisatie alleen voor connectors met wijzigingen in synchronisatie-regel.
* Voorheen Hallo exporteren verwijdering drempelwaarde is alleen van toepassing tooexports die worden geactiveerd via Hallo sync scheduler. Hallo-functie is nu tooinclude uitvoer handmatig geactiveerd door Hallo klant op basis van Hallo Synchronization Service Manager uitgebreid.
* Er is een serviceconfiguratie waarmee wordt aangegeven of Password Synchronization-functie is ingeschakeld voor uw tenant op uw Azure AD-tenant. Eerder, is het eenvoudig hello service configuration toobe onjuist met Azure AD Connect geconfigureerd wanneer u een actief en een server met tijdelijke bestanden. Azure AD Connect probeert nu tookeep Hallo-serviceconfiguratie consistent zijn met uw actieve alleen Azure AD Connect-server.
* Azure AD Connect wizard nu detecteert en een waarschuwing wordt gegeven als lokale AD heeft geen AD Recycle Bin is ingeschakeld.
* Eerder overschrijdt Export tooAzure AD time-out en mislukt als Hallo totale grootte van objecten in een batch Hallo Hallo bepaalde drempelwaarde. Hallo-synchronisatieservice probeert nu tooresend Hallo objecten in afzonderlijke, kleinere batches als Hallo probleem is opgetreden.
* Hallo synchronisatie Service Key Management-toepassing is verwijderd uit de Windows-Menu Start. Beheer van de versleutelingssleutel blijven toobe ondersteund via de opdrachtregelinterface miiskmu.exe gebruiken. Raadpleeg voor informatie over het beheren van de versleutelingssleutel tooarticle [Abandoning hello Azure AD Connect-synchronisatie versleutelingssleutel](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnectsync-change-serviceacct-pass#abandoning-the-azure-ad-connect-sync-encryption-key).
* Voorheen als u een wachtwoord hello Azure AD Connect sync-serviceaccount wijzigt, zich Hallo Synchronization Service niet kunnen starten correct totdat u hebt verlaten Hallo versleutelingssleutel en opnieuw geïnitialiseerd wachtwoord hello Azure AD Connect sync-serviceaccount. Dit is nu niet langer vereist.

Bureaublad SSO

* Azure AD Connect-wizard is niet langer vereist poort 9090 toobe geopend op Hallo netwerk bij het configureren van Pass through-verificatie en SSO-bureaublad. Alleen poort 443 is vereist. 

## <a name="114430"></a>1.1.443.0
Uitgebracht: Maart 2017

**Opgeloste problemen:**

Azure AD Connect-synchronisatie
* Een probleem waardoor Azure AD Connect-wizard toofail als Hallo weergavenaam van hello Azure AD-Connector geen Hallo initiële onmicrosoft.com domein toegewezen toohello Azure AD-tenant opgelost.
* Een probleem waardoor Azure AD Connect-wizard toofail tijdens het maken van verbinding tooSQL database wanneer Hallo wachtwoord Hallo synchronisatieserviceaccount speciale tekens bevatten zoals apostrof, dubbele punt en ruimte bevat opgelost.
* Een probleem waardoor Hallo fout 'hello dimage heeft een anker die verschilt van de installatiekopie van het Hallo' toooccur op een Azure AD Connect-server in de faseringsmodus wordt opgelost, nadat u hebt tijdelijk uitgesloten een on-premises AD worden gesynchroniseerd object en vervolgens deze opnieuw om opgenomen synchroniseren.
* Een probleem waardoor Hallo fout 'Hallo-object gevonden met de DN-naam is een phantomstuklijst' toooccur op een Azure AD Connect-server in de faseringsmodus wordt opgelost, nadat u hebt tijdelijk uitgesloten een on-premises AD-object wordt gesynchroniseerd en opnieuw opgenomen voor het synchroniseren.

AD FS-beheer
* Vaste een probleem waarbij Azure AD Connect-wizard niet bijwerken van de AD FS-configuratie en ingesteld Hallo rechts claims op Hallo vertrouwensrelatie van relying party nadat alternatieve aanmeldings-ID is geconfigureerd.
* Een probleem opgelost waarbij Azure AD Connect-wizard niet kan toocorrectly ingang AD FS-servers waarvan serviceaccounts zijn geconfigureerd met de indeling userPrincipalName in plaats van sAMAccountName indeling is.

Pass-through-verificatie
* Een probleem waardoor Azure AD Connect-wizard toofail als doorgeven via verificatie is geselecteerd, maar de registratie van de connector niet kan worden opgelost.
* Vaste een probleem waardoor Azure AD Connect wizard toobypass validatiecontroles van aanmelden methode geselecteerd als bureaublad SSO-functie is ingeschakeld.

Wachtwoord opnieuw instellen
* Een probleem waardoor hello Azure AAD Connect server toonot poging toore opgelost-verbinding maken als het Hallo-verbinding is afgebroken door een firewall of proxyserver.

**Nieuwe functies/verbeteringen:**

Azure AD Connect-synchronisatie
* De cmdlet Get-ADSyncScheduler retourneert nu een nieuwe Boole-eigenschap met de naam SyncCycleInProgress. Als Hallo waarde geretourneerde is true is, betekent dit dat er een cyclus geplande synchronisatie uitgevoerd is.
* Doelmap voor het opslaan van Azure AD Connect-installatie en installatielogboeken is verplaatst uit %localappdata%\AADConnect too%programdata%\AADConnect tooimprove toegankelijkheid toohello-logboekbestanden.

AD FS-beheer
* Ondersteuning toegevoegd voor het bijwerken van SSL-certificaat voor AD FS-Farm.
* Ondersteuning toegevoegd voor het beheer van AD FS-2016.
* Nu kunt u bestaande gMSA (groep beheerd serviceaccount gebruiken) opgeven tijdens de installatie van AD FS.
* U kunt nu SHA-256 configureren als Hallo handtekening hash-algoritme voor Azure AD-vertrouwensrelatie voor relying party.

Wachtwoord opnieuw instellen
* Verbeteringen tooallow Hallo product toofunction in omgevingen met strengere firewallregels geïntroduceerd.
* Verbinding met verbeterde betrouwbaarheid tooAzure Service Bus.

## <a name="113800"></a>1.1.380.0
Uitgebracht: December 2016

**Opgelost probleem:**

* Vaste Hallo probleem waarbij Hallo issuerid claimregelsjablonen voor Active Directory Federation Services (AD FS) ontbreekt in deze versie.

>[!NOTE]
>Deze versie is niet beschikbaar toocustomers via hello Azure AD Connect automatische Upgrade-functie.

## <a name="113710"></a>1.1.371.0
Uitgebracht: December 2016

**Bekende problemen:**

* Hallo issuerid claimregel voor AD FS ontbreekt in deze versie. Hallo issuerid claimregel is vereist als u bij het federeren van meerdere domeinen met Azure Active Directory (Azure AD). Als u Azure AD Connect toomanage met uw on-premises AD FS-implementatie upgraden toothis build Hallo bestaande issuerid claimregel verwijdert uit uw AD FS-configuratie. U kunt Hallo probleem omzeilen door toe te voegen Hallo issuerid claimregel na Hallo installatie/upgrade. Voor meer informatie over het toevoegen van Hallo issuerid claimregelsjablonen, toothis artikel verwijzen op [ondersteuning voor meerdere domeinen voor federatie met Azure AD](active-directory-aadconnect-multiple-domains.md).

**Opgelost probleem:**

* Als poort 9090 is niet geopend voor de uitgaande verbinding hello, mislukt hello Azure AD Connect-installatie of upgrade.

>[!NOTE]
>Deze versie is niet beschikbaar toocustomers via hello Azure AD Connect automatische Upgrade-functie.

## <a name="113700"></a>1.1.370.0
Uitgebracht: December 2016

**Bekende problemen:**

* Hallo issuerid claimregel voor AD FS ontbreekt in deze versie. Hallo issuerid claimregel is vereist als u meerdere domeinen met Azure AD federeert. Als u Azure AD Connect toomanage met uw on-premises AD FS-implementatie upgraden toothis build Hallo bestaande issuerid claimregel verwijdert uit uw AD FS-configuratie. U kunt Hallo probleem omzeilen door Hallo issuerid claimregel toe te voegen na de installatie/upgrade. Voor meer informatie over het toevoegen van issuerid claimregelsjablonen, toothis artikel verwijzen op [ondersteuning voor meerdere domeinen voor federatie met Azure AD](active-directory-aadconnect-multiple-domains.md).
* Poort 9090 moet open uitgaande toocomplete installatie.

**Nieuwe functies:**

* Pass through-verificatie (Preview).

>[!NOTE]
>Deze versie is niet beschikbaar toocustomers via hello Azure AD Connect automatische Upgrade-functie.

## <a name="113430"></a>1.1.343.0
Uitgebracht: November 2016

**Bekende problemen:**

* Hallo issuerid claimregel voor AD FS ontbreekt in deze versie. Hallo issuerid claimregel is vereist als u meerdere domeinen met Azure AD federeert. Als u Azure AD Connect toomanage met uw on-premises AD FS-implementatie upgraden toothis build Hallo bestaande issuerid claimregel verwijdert uit uw AD FS-configuratie. U kunt Hallo probleem omzeilen door Hallo issuerid claimregel toe te voegen na de installatie/upgrade. Voor meer informatie over het toevoegen van issuerid claimregelsjablonen, toothis artikel verwijzen op [ondersteuning voor meerdere domeinen voor federatie met Azure AD](active-directory-aadconnect-multiple-domains.md).

**Opgeloste problemen:**

* Azure AD Connect installeert mislukt soms, omdat deze toocreate een lokaal serviceaccount waarvan het wachtwoord voldoet aan Hallo-niveau van complexiteit opgegeven door het wachtwoordbeleid van Hallo organisatie.
* Een probleem opgelost waarbij join regels niet opnieuw geëvalueerd wanneer een object in Hallo connectorruimte gelijktijdig buiten het bereik wordt voor een regel toevoegen en worden in het bereik voor een andere. Dit kan gebeuren als er twee of meer join regels waarvan join-voorwaarden sluiten elkaar wederzijds uit.
* Een probleem opgelost waarbij inkomende synchronisatieregels (van Azure AD), die geen join-regels bevatten, worden niet verwerkt als ze hebben lagere prioriteit waarden dan de join-regels met.

**Verbeteringen:**

* Ondersteuning toegevoegd voor de installatie van Azure AD Connect op Windows Server 2016 Standard of hoger.
* Ondersteuning toegevoegd voor het gebruik van SQL Server 2016 als de externe database Hallo voor Azure AD Connect.

## <a name="112810"></a>1.1.281.0
Uitgebracht: Augustus 2016

**Opgeloste problemen:**

* Wijzigingen toosync interval eerst plaatsvinden nadat nadat Hallo volgende synchronisatiecyclus is voltooid.
* Azure AD Connect-wizard wordt niet geaccepteerd voor een Azure AD-account waarvan de gebruikersnaam wordt gestart met een onderstrepingsteken (\_).
* Azure AD Connect-wizard mislukt tooauthenticate hello Azure AD-account als Hallo accountwachtwoord te veel tekens bevat. Foutbericht 'kan geen toovalidate referenties. Een onverwachte fout opgetreden." wordt geretourneerd.
* Verwijderen van testserver schakelt Wachtwoordsynchronisatie in Azure AD-tenant en zorgt ervoor dat wachtwoord synchronisatie toofail met actieve server.
* Wachtwoordsynchronisatie is mislukt in ongewoon gevallen wanneer er geen wachtwoord-hash op Hallo gebruiker opgeslagen.
* Als Azure AD Connect-server van de faseringsmodus is ingeschakeld, is niet tijdelijk wachtwoord terugschrijven uitgeschakeld.
* Azure AD Connect-wizard weergegeven niet Hallo werkelijke Wachtwoordsynchronisatie en wachtwoord terugschrijven configuratie als de server in de faseringsmodus. Altijd wordt deze als uitgeschakeld.
* Synchronisatie van configuratie wijzigingen toopassword en Write-back van wachtwoord zijn niet permanent door Azure AD Connect-wizard als server in de faseringsmodus.

**Verbeteringen:**

* Hallo Start ADSyncSyncCycle cmdlet tooindicate bijgewerkt of kunnen toosuccessfully start een nieuwe synchronisatiecyclus of niet.
* Toegevoegde Hallo Stop ADSyncSyncCycle cmdlet tooterminate synchronisatiecyclus en bewerking, die momenteel uitgevoerd worden.
* Bijgewerkte Hallo Stop ADSyncScheduler cmdlet tooterminate synchronisatiecyclus en bewerking, die momenteel uitgevoerd worden.
* Bij het configureren van [Directory uitbreidingen](active-directory-aadconnectsync-feature-directory-extensions.md) in Azure AD Connect-wizard kenmerk van het type 'Teletex tekenreeks' hello Azure AD kan nu worden geselecteerd.

## <a name="111890"></a>1.1.189.0
Uitgebracht: Juni 2016

**Opgeloste problemen en verbeteringen:**

* Azure AD Connect kan nu worden geïnstalleerd op een server FIPS-compatibel.
  * Zie voor Wachtwoordsynchronisatie [Wachtwoordsynchronisatie en FIPS](active-directory-aadconnectsync-implement-password-synchronization.md#password-synchronization-and-fips).
* Een probleem opgelost waarbij een NetBIOS-naam kan niet omgezet toohello FQDN in Hallo Active Directory-Connector.

## <a name="111800"></a>1.1.180.0
Uitgebracht: Mei 2016

**Nieuwe functies:**

* Waarschuwt en kunt u domeinen verifiëren als u deze voordat u Azure AD Connect niet hebt gedaan.
* Ondersteuning toegevoegd voor [Microsoft Cloud Duitsland](active-directory-aadconnect-instances.md#microsoft-cloud-germany).
* Ondersteuning toegevoegd voor de meest recente Hallo [Microsoft Azure Government cloud](active-directory-aadconnect-instances.md#microsoft-azure-government-cloud) infrastructuur met nieuwe URL-vereisten.

**Opgeloste problemen en verbeteringen:**

* Toegevoegde filteren toohello Sync Rule Editor toomake het eenvoudig toofind sync regels.
* Verbeterde prestaties bij het verwijderen van een connectorruimte.
* Een probleem opgelost wanneer Hallo hetzelfde object is verwijderd en toegevoegd in Hallo dezelfde uitvoeren (aangeroepen verwijderen/toevoegen).
* Een uitgeschakelde synchronisatie regel niet meer wordt opnieuw ingeschakeld opgenomen objecten en kenmerken op upgrade of Active directory-schema vernieuwen.

## <a name="111300"></a>1.1.130.0
Uitgebracht: April 2016

**Nieuwe functies:**

* Ondersteuning toegevoegd voor kenmerken met meerdere waarden te[Directory uitbreidingen](active-directory-aadconnectsync-feature-directory-extensions.md).
* Ondersteuning toegevoegd voor meer configuratie variaties voor [Automatische upgrade](active-directory-aadconnect-feature-automatic-upgrade.md) toobe in aanmerking voor upgrade.
* Sommige cmdlets voor toegevoegd [aangepaste scheduler](active-directory-aadconnectsync-feature-scheduler.md#custom-scheduler).

## <a name="111190"></a>1.1.119.0
Uitgebracht: Maart 2016

**Opgeloste problemen:**

* Aangebracht wordt ervoor Express-installatie kan niet worden gebruikt op Windows Server 2008 (pre-R2), omdat het wachtwoord synchroniseren niet ondersteund op dit besturingssysteem.
* Upgrade van DirSync met een aangepast filterconfiguratie werkt niet zoals verwacht.
* Bij een upgrade van de nieuwere versie tooa en er zijn geen wijzigingen toohello configuratie, een volledige import/synchronisatie moet niet worden gepland.

## <a name="111100"></a>1.1.110.0
Uitgebracht: Februari 2016

**Opgeloste problemen:**

* Upgrade van eerdere versies werkt niet als Hallo-installatie niet in de standaardmap C:\Program Files Hallo is.
* Als u installeert en schakel **Start het synchronisatieproces Hallo** aan Hallo einde van de installatiewizard hello, actieve Hallo-installatiewizard een tweede keer niet mogelijk Hallo scheduler.
* Hallo werkt scheduler niet zoals verwacht op servers waar hello US-en datum/tijd-indeling wordt niet gebruikt. Blokkeert tevens `Get-ADSyncScheduler` tooreturn juiste tijden.
* Als u een eerdere versie van Azure AD Connect geïnstalleerd met AD FS, zoals Hallo aanmeldoptie en upgrade, kan niet u Hallo-installatiewizard opnieuw uitvoeren.

## <a name="111050"></a>1.1.105.0
Uitgebracht: Februari 2016

**Nieuwe functies:**

* [Automatische upgrade](active-directory-aadconnect-feature-automatic-upgrade.md) functie voor snelle instellingen klanten.
* Ondersteuning voor globale beheerder met behulp van Azure multi-factor Authentication en Privileged Identity Management in de installatiewizard Hallo Hallo.
  * U moet tooallow uw proxy-tooalso toohttps://secure.aadcdn.microsoftonline-p.com verkeer toestaan als u multi-factor Authentication gebruikt.
  * U moet tooadd https://secure.aadcdn.microsoftonline-p.com tooyour lijst met vertrouwde websites voor multi-factor Authentication tooproperly werk.
* Hallo-in de methode van gebruiker wijzigen na de eerste installatie toegestaan.
* Toestaan dat [domein en OE filteren](active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering) in Hallo-installatiewizard. Hierdoor kunnen ook verbinding maken met tooforests waar niet alle domeinen beschikbaar zijn.
* [Scheduler](active-directory-aadconnectsync-feature-scheduler.md) is ingebouwd in toohello synchronisatie-engine.

**Promoveren vanuit tooGA preview-functies:**

* [Apparaat terugschrijven](active-directory-aadconnect-feature-device-writeback.md).
* [Directory-uitbreidingen](active-directory-aadconnectsync-feature-directory-extensions.md).

**Nieuwe preview-functies:**

* Hallo nieuwe standaard synchronisatiecyclus interval 30 minuten is. Gebruikt toobe drie uur voor alle eerdere versies. Voegt ondersteuning toochange hello [scheduler](active-directory-aadconnectsync-feature-scheduler.md) gedrag.

**Opgeloste problemen:**

* Hallo Controleer of DNS-domeinen pagina niet altijd Hallo domeinen herkend.
* Als u wordt gevraagd om domeinreferenties van beheerder bij het configureren van AD FS.
* Hallo een on-premises AD-accounts worden niet herkend door de installatiewizard Hallo als zich in een domein met een andere DNS-structuur dan Hallo hoofddomein.

## <a name="1091310"></a>1.0.9131.0
Uitgebracht: December 2015

**Opgeloste problemen:**

* Wachtwoordsynchronisatie werkt mogelijk niet wanneer u wachtwoorden in Active Directory Domain Services (AD DS), maar werkt wijzigen wanneer u een wachtwoord instelt.
* Wanneer u een proxyserver verificatie tooAzure AD tijdens de installatie mislukken hebt of als een upgrade op de configuratiepagina Hallo is geannuleerd.
* Bijwerken van een vorige versie van Azure AD Connect met een volledige SQL Server-instantie mislukt als u niet een SQL Server-systeembeheerder (SA).
* Bijwerken van een vorige versie van Azure AD Connect met een externe SQL Server bevat Hallo "ADSync SQL-database kan niet tooaccess hello" fout.

## <a name="1091250"></a>1.0.9125.0
Uitgebracht: November 2015

**Nieuwe functies:**

* Kunt opnieuw configureren van AD FS tooAzure AD-vertrouwensrelatie.
* Kan Hallo Active Directory-schema vernieuwen en sync-regels genereren.
* Een synchronisatieregel kan worden uitgeschakeld.
* Kan 'AuthoritativeNull' te definiëren als een nieuwe literal in een synchronisatieregel.

**Nieuwe preview-functies:**

* [Azure AD Connect Health voor synchroniseren](../connect-health/active-directory-aadconnect-health-sync.md).
* Ondersteuning voor [Azure AD Domain Services](../active-directory-passwords-update-your-own-password.md) Wachtwoordsynchronisatie.

**Nieuwe ondersteunde scenario:**

* Biedt ondersteuning voor meerdere lokale Exchange-organisaties. Zie voor meer informatie [hybride implementaties met meerdere Active Directory-forests](https://technet.microsoft.com/library/jj873754.aspx).

**Opgeloste problemen:**

* Problemen met synchronisatie van wachtwoord:
  * Een object buiten het bereik tooin-bereik overgeplaatst heeft geen bijbehorende wachtwoord is gesynchroniseerd. Dit omvat de organisatie-eenheid en kenmerkfilters inschakelt.
  * Een volledige Wachtwoordsynchronisatie is niet vereist als u een nieuwe organisatie-eenheid tooinclude synchroon selecteren.
  * Wanneer een uitgeschakelde gebruiker is ingeschakeld wordt Hallo wachtwoord niet synchroniseren.
  * Hallo wachtwoord opnieuw wachtrij is oneindig en Hallo vorige limiet van 5000 objecten toobe buiten gebruik gesteld is verwijderd.
* Er kan geen tooconnect tooActive Directory met Windows Server 2016 forest-functionaliteitsniveau.
* Kan geen toochange Hallo-groep die wordt gebruikt voor het filteren van de groep na de eerste installatie Hallo.
* Maakt een nieuw gebruikersprofiel niet langer op Hallo Azure AD Connect-server voor elke gebruiker een wachtwoordwijziging met wachtwoord terugschrijven ingeschakeld doen.
* Er kan geen toouse Lange Integer waarden synchroon regels scopes.
* selectievakje Hallo 'apparaat terugschrijven' blijft uitgeschakeld als er domeincontrollers niet bereikbaar.

## <a name="1086670"></a>1.0.8667.0
Uitgebracht: Augustus 2015

**Nieuwe functies:**

* Hello Azure AD Connect nu installatiewizard is gelokaliseerd tooall Windows Server-talen.
* Ondersteuning toegevoegd voor het account ontgrendelen wanneer u Azure AD-wachtwoordbeheer.

**Opgeloste problemen:**

* Azure AD Connect-installatiewizard loopt vast als een andere gebruiker heeft nog steeds installatie in plaats van Hallo persoon die het Hallo-installatie eerst wordt gestart.
* Als een eerdere installatie van Azure AD Connect foutloos toouninstall Azure AD Connect-synchronisatie mislukt, maar het is niet mogelijk tooreinstall.
* Kan Azure AD Connect met snelle installatie als Hallo gebruiker niet in het hoofddomein Hallo van Hallo forest of als een niet-Engelse versie van Active Directory wordt gebruikt niet installeren.
* Als Hallo FQDN-naam van Hallo Active Directory-gebruikersaccount kan niet worden omgezet, wordt een foutbericht misleidend 'Mislukt toocommit Hallo schema' weergegeven.
* Als Hallo account dat wordt gebruikt op Hallo Active Directory-Connector is gewijzigd buiten Hallo wizard, mislukt Hallo wizard bij latere wordt uitgevoerd.
* Azure AD Connect mislukt soms tooinstall op een domeincontroller.
* Kan niet in- en 'faseringsmodus' uitschakelen als uitbreidingskenmerken zijn toegevoegd.
* Wachtwoord terugschrijven is mislukt in bepaalde configuraties vanwege een ongeldig wachtwoord op Hallo Active Directory-Connector.
* DirSync kan niet worden bijgewerkt als een DN-naam (Distinguished Name) wordt gebruikt in het kenmerk filteren.
* Buitensporig CPU-gebruik bij gebruik van wachtwoord opnieuw instellen.

**Verwijderde preview-functies:**

* Hallo preview-functie [Write-back van gebruiker](active-directory-aadconnect-feature-preview.md#user-writeback) tijdelijk op basis van feedback van onze klanten preview is verwijderd. Dit wordt later opnieuw worden toegevoegd nadat Hallo feedback gegeven is verholpen.

## <a name="1086410"></a>1.0.8641.0
Uitgebracht: Juni 2015

**Initiële versie van Azure AD Connect.**

Gewijzigde naam van Azure AD Sync tooAzure AD Connect.

**Nieuwe functies:**

* [Snelle instellingen](active-directory-aadconnect-get-started-express.md) installatie
* Kan [AD FS configureren](active-directory-aadconnect-get-started-custom.md#configuring-federation-with-ad-fs)
* Kan [upgraden van DirSync](active-directory-aadconnect-dirsync-upgrade-get-started.md)
* [Onopzettelijke verwijderingen voorkomen](active-directory-aadconnectsync-feature-prevent-accidental-deletes.md)
* Geïntroduceerd [faseringsmodus](active-directory-aadconnectsync-operations.md#staging-mode)

**Nieuwe preview-functies:**

* [Write-back van gebruiker](active-directory-aadconnect-feature-preview.md#user-writeback)
* [Write-back van groep](active-directory-aadconnect-feature-preview.md#group-writeback)
* [Write-back van apparaat](active-directory-aadconnect-feature-device-writeback.md)
* [Uitbreidingen van de directory](active-directory-aadconnect-feature-preview.md)

## <a name="104940501"></a>1.0.494.0501
Uitgebracht: Mei 2015

**Nieuwe vereiste:**

* Azure AD Sync is nu vereist Hallo .NET Framework versie 4.5.1 toobe geïnstalleerd.

**Opgeloste problemen:**

* Wachtwoord terugschrijven van Azure AD is mislukt met een Azure Service Bus-verbindingsfout.

## <a name="104910413"></a>1.0.491.0413
Uitgebracht: April 2015

**Opgeloste problemen en verbeteringen:**

* Hallo Active Directory-Connector verwerkt geen verwijderingen correct als de Prullenbak Hallo is ingeschakeld en er meerdere domeinen in Hallo forest.
* Hallo-prestaties van importbewerkingen is voor hello Azure Active Directory-Connector verbeterd.
* Wanneer een groep Hallo lidmaatschap limiet heeft overschreden (limiet Hallo is standaard too50, 000 objecten), Hallo-groep is verwijderd in Azure Active Directory. Met nieuw gedrag hello, Hallo-groep niet verwijderd, wordt een fout gegenereerd en nieuwe lidmaatschapswijzigingen worden niet geëxporteerd.
* Een nieuw object kan niet worden ingericht als een gefaseerde verwijderen Hello die dezelfde DN-naam al is aanwezig zijn op Hallo connectorgebied overgebracht.
* Sommige objecten zijn gemarkeerd voor synchronisatie tijdens een Deltasynchronisatie, zelfs als er geen wijziging voorgefaseerd op het Hallo-object is.
* Waardoor de Wachtwoordsynchronisatie van een, verwijdert ook Hallo voorkeur DC-lijst.
* CSExportAnalyzer, kent problemen met de statussen van sommige objecten.

**Nieuwe functies:**

* Een join kan nu verbinding maken te '' objecttype in Hallo MV.

## <a name="104850222"></a>1.0.485.0222
Uitgebracht: Februari 2015

**Verbeteringen:**

* Verbeterde import van de prestaties.

**Opgeloste problemen:**

* Wachtwoordsynchronisatie respecteert Hallo cloudFiltered kenmerk dat wordt gebruikt door het kenmerk filteren. Gefilterde objecten zijn niet langer in het bereik voor Wachtwoordsynchronisatie.
* In zeldzame gevallen Hallo topologie waar veel domeincontrollers zijn, werkt Wachtwoordsynchronisatie niet.
* 'Gestopt-server' bij het importeren van hello Azure AD-Connector na het beheer van apparaten is ingeschakeld in Azure AD/Intune.
* Lid worden van afwijkende beveiligings-Principals (FSP's) van meerdere domeinen in hetzelfde forest, veroorzaakt een dubbelzinnige join-fout.

## <a name="104751202"></a>1.0.475.1202
Uitgebracht: December 2014

**Nieuwe functies:**

* Wachtwoordsynchronisatie met filteren op basis van een kenmerk wordt nu ondersteund. Zie voor meer informatie [Wachtwoordsynchronisatie met filtering](active-directory-aadconnectsync-configure-filtering.md).
* Hallo msDS-ExternalDirectoryObjectID kenmerk teruggeschreven tooActive Directory. Deze functie wordt ondersteuning toegevoegd voor Office 365-toepassingen. OAuth2 tooaccess-postvakken in een hybride implementatie voor Exchange Online en On-Premises wordt gebruikt.

**Vaste problemen met de upgrade:**

* Een nieuwere versie van het Hallo-aanmeldhulp is beschikbaar op Hallo-server.
* Het pad van een aangepaste installatie is gebruikte tooinstall Azure AD Sync.
* Een ongeldige aangepaste join criterium blokken Hallo upgrade.

**Andere correcties voor:**

* Vaste Hallo sjablonen voor Office Professional Plus.
* Vaste installatieproblemen veroorzaakt door de gebruikersnamen die met een streepje beginnen.
* Vaste overdragende Hallo sourceAnchor instelling wanneer Hallo-installatiewizard wordt een tweede keer uitgevoerd.
* Vaste ETW-tracering voor Wachtwoordsynchronisatie.

## <a name="104701023"></a>1.0.470.1023
Uitgebracht: Oktober 2014

**Nieuwe functies:**

* Wachtwoordsynchronisatie van meerdere lokale Active Directory tooAzure AD.
* Gelokaliseerde installatie UI tooall Windows Server-talen.

**Een upgrade uitvoert van AADSync 1.0 NH**

Als u al Azure AD Sync geïnstalleerd hebt, is er een extra stap hebt u tootake als u een out-of-box-synchronisatieregels Hallo hebt gewijzigd. Nadat u toohello 1.0.470.1023 versie hebt bijgewerkt, worden Hallo-synchronisatieregels die u hebt gewijzigd gedupliceerd. Elke synchronisatieregel gewijzigde Hallo te volgen:

1.  Zoek Hallo synchronisatieregel u hebt gewijzigd, en noteer Hallo wijzigingen.
* Hallo-sync-regel verwijderen.
* Zoek Hallo nieuwe synchronisatieregel die door Azure AD Sync is gemaakt en vervolgens pas Hallo wijzigingen.

**Machtigingen voor Hallo Active Directory-account**

Hallo Active Directory-account moet beschikken over aanvullende machtigingen toobe kunnen tooread Hallo wachtwoord-hashes van Active Directory. Hallo machtigingen toogrant heten 'Directorywijzigingen repliceren' en "Replicating Directory alle gewijzigd." Beide machtigingen zijn vereist toobe kunnen tooread Hallo wachtwoord-hashes.

## <a name="104190911"></a>1.0.419.0911
Uitgebracht: September 2014

**Initiële versie van Azure AD Sync.**

## <a name="next-steps"></a>Volgende stappen
Lees meer over het [integreren van uw on-premises identiteiten met Azure Active Directory](active-directory-aadconnect.md).
