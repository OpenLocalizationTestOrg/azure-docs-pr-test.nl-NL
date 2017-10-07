---
title: aaaImplement Wachtwoordsynchronisatie met Azure AD Connect-synchronisatie | Microsoft Docs
description: Bevat informatie over hoe Wachtwoordsynchronisatie werkt en hoe tooset up.
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 05f16c3e-9d23-45dc-afca-3d0fa9dbf501
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: billmath
ms.openlocfilehash: a0401640f2a4d914419ee4446f923bb3a972389d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="implement-password-synchronization-with-azure-ad-connect-sync"></a>Wachtwoordsynchronisatie met Azure AD Connect-synchronisatie implementeren
Dit artikel bevat informatie die u nodig toosynchronize uw wachtwoorden van een lokale Active Directory-exemplaar tooa cloud-gebaseerde Azure Active Directory (Azure AD)-exemplaar.

## <a name="what-is-password-synchronization"></a>Wat is synchronisatie van wachtwoorden
Hallo kans dat u bent geblokkeerd toegang krijgen tot uw werk vanwege tooa vergeten wachtwoord is gerelateerd toohello nummer van verschillende wachtwoorden moet u tooremember. Hallo meer wachtwoorden moet u tooremember, Hallo hoger Hallo kans tooforget een. Hallo meeste helpdesk bronnen vragen en oproepen over wachtwoorden en andere problemen met de wachtwoord-aanvraag.

Wachtwoordsynchronisatie is dat een functie toosynchronize wachtwoorden van een lokale Active Directory-exemplaar tooa cloud-gebaseerde Azure AD-exemplaar gebruikt.
Gebruik deze functie toosign in tooAzure AD-services zoals Office 365, Microsoft Intune, CRM Online en Azure Active Directory Domain Services (Azure AD DS). U zich aanmeldt toohello service met behulp van Hallo hetzelfde wachtwoord dat u toosign in tooyour lokale Active Directory-exemplaar.

![Wat is Azure AD Connect?](./media/active-directory-aadconnectsync-implement-password-synchronization/arch1.png)

Vermindert het aantal wachtwoorden hello, moeten uw gebruikers toomaintain toojust een. Wachtwoordsynchronisatie helpt u bij:

* Hallo productiviteit van uw gebruikers verbeteren.
* Uw helpdesk kosten te verlagen.  

Ook als u toouse besluit [Federatie met Active Directory Federation Services (AD FS)](https://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Configuring-AD-FS-for-user-sign-in-with-Azure-AD-Connect), kunt u eventueel instellen Wachtwoordsynchronisatie als een back-up als uw AD FS-infrastructuur is mislukt.

Wachtwoordsynchronisatie is een uitbreiding toohello directory-synchronisatiefunctie geïmplementeerd door Azure AD Connect-synchronisatie. Wachtwoordsynchronisatie toouse in uw omgeving, moet u:

* Azure AD Connect installeren.  
* Adreslijstsynchronisatie configureert tussen uw lokale Active Directory-exemplaar en uw Azure Active Directory-exemplaar.
* Wachtwoordsynchronisatie inschakelen.

Zie [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md) (Uw on-premises identiteiten integreren met Azure Active Directory) voor meer informatie.

> [!NOTE]
> Zie voor meer informatie over Azure Active Directory Domain Services geconfigureerd voor FIPS en Wachtwoordsynchronisatie 'Wachtwoordsynchronisatie en FIPS' verderop in dit artikel.
>
>

## <a name="how-password-synchronization-works"></a>Hoe werkt Wachtwoordsynchronisatie
wachtwoorden worden opgeslagen in de vorm van een weergave van de hash-waarde van de werkelijke gebruikerswachtwoord Hallo Hallo van Hallo Active Directory domain Services. Een hash-waarde is een resultaat van een wiskundige eenrichtingsfunctie (Hallo *hash-algoritme*). Er is geen methode toorevert Hallo resultaat van een one-way function toohello tekst zonder opmaak versie van een wachtwoord. U kunt een wachtwoord-hash-toosign in tooyour on-premises netwerk gebruiken.

uw wachtwoord, Azure AD Connect-synchronisatie pakt de wachtwoord-hash van toosynchronize Hallo lokale Active Directory-exemplaar. Verwerking van de extra beveiliging wordt toegepast toohello wachtwoordhash voordat deze wordt gesynchroniseerd toohello Azure Active Directory authentication-service. Wachtwoorden worden gesynchroniseerd, op basis van een gebruiker en in chronologische volgorde.

Hallo werkelijke gegevensstroom van Hallo wachtwoord-synchronisatieproces is vergelijkbaar toohello synchronisatie van gebruikersgegevens, zoals DisplayName of e-mailadressen. Wachtwoorden worden echter vaker dan Hallo standaard directory-synchronisatievenster voor andere kenmerken gesynchroniseerd. Hallo wachtwoord synchronisatieproces wordt elke twee minuten uitgevoerd. U kunt Hallo frequentie van dit proces niet wijzigen. Wanneer u een wachtwoord synchroniseert, overschrijft het Hallo bestaande cloud wachtwoord.

Hallo eerst die Hallo wachtwoord synchronisatie functie is ingeschakeld, wordt uitgevoerd een initiële synchronisatie van wachtwoorden Hallo van alle gebruikers die in het bereik. U kunt geen expliciet een subset van wachtwoorden van gebruikers die u wilt dat toosynchronize definiëren.

Wanneer u een on-premises wachtwoord wijzigt, is Hallo bijgewerkt wachtwoord gesynchroniseerd, meestal binnen een paar minuten.
Hallo wachtwoord synchronisatiefunctie mislukte synchronisatiepogingen wordt automatisch opnieuw geprobeerd. Als er een fout optreedt tijdens een poging toosynchronize een wachtwoord, wordt er een fout vastgelegd in de logboeken.

Hallo synchronisatie van een wachtwoord heeft geen invloed op Hallo-gebruiker die momenteel is aangemeld.
De huidige sessie van de cloud-service wordt niet direct beïnvloed door een gesynchroniseerde wachtwoordwijziging die optreedt terwijl u bent aangemeld met tooa-cloudservice. Echter, wanneer Hallo-cloudservice, u tooauthenticate opnieuw moet moet u tooprovide uw nieuwe wachtwoord.

Een gebruiker moet hun bedrijfsreferenties invoeren een tweede keer tooauthenticate tooAzure AD, ongeacht of ze tootheir bedrijfsnetwerk bent aangemeld. Deze patroon kan echter worden geminimaliseerd als Hallo gebruiker selecteert Hallo behouden mij ondertekend (KMSI) selectievakje apenstaartje in. Deze selectie stelt een sessiecookie dat verificatie voor een korte periode omzeilt. KMSI gedrag kan worden ingeschakeld of uitgeschakeld door hello Azure AD-beheerder.

> [!NOTE]
> Wachtwoordsynchronisatie wordt alleen ondersteund voor Hallo object type gebruiker in Active Directory. Dit wordt niet ondersteund voor Hallo iNetOrgPerson-objecttype.

### <a name="detailed-description-of-how-password-synchronization-works"></a>Gedetailleerde beschrijving van hoe Wachtwoordsynchronisatie werkt
Hallo hieronder wordt beschreven diepgaande hoe werkt Wachtwoordsynchronisatie tussen Active Directory en Azure AD.

![Gedetailleerde wachtwoord stroom](./media/active-directory-aadconnectsync-implement-password-synchronization/arch3.png)


1. Elke twee minuten Hallo agent voor Wachtwoordsynchronisatie op Hallo AD Connect-server aanvragen opgeslagen wachtwoord-hashes (Hallo unicodePwd kenmerk) van een DC via Hallo standaard [MS DRSR](https://msdn.microsoft.com/library/cc228086.aspx) replicatie-protocol gebruikt toosynchronize gegevens tussen domeincontrollers. Hallo-serviceaccount moet directorywijzigingen repliceren en repliceren Directory alle wijzigingen AD machtigingen (standaard op de installatie) tooobtain Hallo wachtwoord-hashes hebben.
2. Voordat u verzendt, Hallo DC versleuteld Hallo MD4 wachtwoord-hash met een sleutel die is een [MD5](http://www.rfc-editor.org/rfc/rfc1321.txt) hash van de sessiesleutel van Hallo RPC en een salt. Vervolgens stuurt Hallo resultaat toohello agent voor Wachtwoordsynchronisatie via RPC. Hallo geeft DC ook Hallo salt toohello synchronisatie-agent met behulp van Hallo DC replicatie-protocol, dus Hallo agent kunnen toodecrypt Hallo envelop.
3.  Nadat de agent voor Wachtwoordsynchronisatie Hallo Hallo versleutelde envelop heeft, gebruikt [MD5CryptoServiceProvider](https://msdn.microsoft.com/library/System.Security.Cryptography.MD5CryptoServiceProvider.aspx) en Hallo salt toogenerate een sleutel toodecrypt Hallo ontvangen back tooits oorspronkelijke MD4 gegevensindeling. Op geen enkel heeft agent voor Wachtwoordsynchronisatie Hallo toegang toohello wachtwoord met ongecodeerde tekst. Hallo agent voor Wachtwoordsynchronisatie van gebruik van MD5 geldt uitsluitend voor replicatie protocol compatibiliteit met Hallo DC en wordt alleen gebruikt on-premises tussen Hallo DC en Hallo agent voor Wachtwoordsynchronisatie.
4.  agent voor Wachtwoordsynchronisatie Hallo breidt Hallo 16 bytes binary-wachtwoord-hash too64 bytes door de eerste converteren Hallo hash tooa 32 byte hexadecimale tekenreeks, en vervolgens back-deze tekenreeks converteren naar binair met UTF-16-codering.
5.  agent voor Wachtwoordsynchronisatie Hello wordt toegevoegd een salt die bestaan uit een lengte in 10 bytes salt, toohello 64-bytes binary toofurther beveiligen Hallo oorspronkelijke-hash.
6.  agent voor Wachtwoordsynchronisatie Hallo Hallo MD4-hash plus salt combineert en de bestelling op Hallo [PBKDF2](https://www.ietf.org/rfc/rfc2898.txt) functie. 1000 herhalingen van Hallo [HMAC SHA256](https://msdn.microsoft.com/library/system.security.cryptography.hmacsha256.aspx) sleutelhash hash-algoritme wordt gebruikt. 
7.  agent voor Wachtwoordsynchronisatie Hallo Hallo resulterende 32-byte-hash heeft, worden aaneengeschakeld beide salt Hallo en Hallo aantal SHA256 iteraties tooit (voor gebruik door Azure AD) en verzendt Hallo tekenreeks van Azure AD Connect tooAzure AD via SSL.</br> 
8.  Wanneer een gebruiker probeert toosign in tooAzure AD en hun wachtwoord, hello wachtwoord invoert, wordt uitgevoerd via Hallo dezelfde MD4 + salt + PBKDF2 + HMAC SHA256-proces. Als de resulterende hash Hallo overeenkomt met Hallo hash opgeslagen in Azure AD, wordt Hallo gebruiker Hallo juiste wachtwoord heeft ingevoerd en is geverifieerd. 

>[!Note] 
>Hallo oorspronkelijke MD4-hash is niet verzonden tooAzure AD. In plaats daarvan wordt Hallo SHA256-hash van de oorspronkelijke MD4-hash hello verzonden. Worden als gevolg hiervan als Hallo hash opgeslagen in Azure AD wordt verkregen, deze kan niet gebruikt in een lokale pass-the-hash-aanval.

### <a name="how-password-synchronization-works-with-azure-active-directory-domain-services"></a>Hoe werkt Wachtwoordsynchronisatie met Azure Active Directory Domain Services
U kunt ook Hallo wachtwoord synchronisatie functie toosynchronize uw on-premises wachtwoorden te[Azure Active Directory Domain Services](../../active-directory-domain-services/active-directory-ds-overview.md). In dit scenario verifieert hello Azure Active Directory Domain Services-exemplaar uw gebruikers in de cloud Hallo met alle Hallo-methoden die beschikbaar zijn in uw lokale Active Directory-exemplaar. Hallo-ervaring van dit scenario is vergelijkbaar toousing Hallo Active Directory Migration Tool (ADMT) in een on-premises omgeving.

### <a name="security-considerations"></a>Beveiligingsoverwegingen
Bij het synchroniseren van wachtwoorden, Hallo tekst zonder opmaak versie van uw wachtwoord is niet blootgestelde toohello wachtwoordfunctie voor synchronisatie, tooAzure AD of een van de services Hallo die zijn gekoppeld.

Gebruikersverificatie vindt plaats met Azure AD in plaats van op Hallo van organisatie Active Directory-exemplaar. Als uw organisatie opmerkingen over de wachtwoordgegevens in een formulier verlaten premises Hallo, houd dan rekening Hallo feit die Hallo SHA256 wachtwoord opgeslagen gegevens in Azure AD--is een hash van de oorspronkelijke MD4-hash Hallo--veel veiliger is dan wat wordt opgeslagen in Active Directory. Verder, omdat deze SHA256-hash kan niet worden ontsleuteld, het niet kan worden teruggebracht van toohello organisatie Active Directory-omgeving en weergegeven als een geldige gebruiker-wachtwoord in een pass-the-hash-aanval.





### <a name="password-policy-considerations"></a>Overwegingen bij het beleid van wachtwoord
Er zijn twee soorten beleid voor wachtwoorden die worden beïnvloed door Wachtwoordsynchronisatie inschakelen:

* Beleid voor wachtwoordcomplexiteit
* Vervalbeleid voor wachtwoorden

#### <a name="password-complexity-policy"></a>Beleid voor wachtwoordcomplexiteit  
Als Wachtwoordsynchronisatie is ingeschakeld, overschrijven Hallo wachtwoordbeleid complexiteit in uw lokale Active Directory-exemplaar complexiteit beleid in de cloud Hallo voor gesynchroniseerde gebruikers. U kunt alle Hallo geldige wachtwoorden van uw lokale Active Directory-exemplaar tooaccess Azure AD-services.

> [!NOTE]
> Wachtwoorden voor gebruikers die zijn gemaakt, rechtstreeks in de cloud Hallo zijn nog steeds onderwerp toopassword beleidsregels zoals gedefinieerd in de cloud Hallo.

#### <a name="password-expiration-policy"></a>Vervalbeleid voor wachtwoorden  
Als een gebruiker in het bereik van Wachtwoordsynchronisatie hello, Hallo cloud accountwachtwoord te is ingesteld*nooit verlopen*.

U kunt toosign blijven in tooyour cloudservices met behulp van een gesynchroniseerde wachtwoord dat is verlopen in uw on-premises omgeving. Uw wachtwoord cloud wordt bijgewerkt zodra u Hallo wachtwoord in Hallo on-premises omgeving wijzigen Hallo.

#### <a name="account-expiration"></a>Account verloopt
Als uw organisatie gebruikmaakt van Hallo accountExpires kenmerk als onderdeel van Gebruikersaccountbeheer, let er dan voor dat dit kenmerk is niet gesynchroniseerd tooAzure AD. Als gevolg hiervan wordt verlopen Active Directory-account in een omgeving die is geconfigureerd voor Wachtwoordsynchronisatie nog steeds actief zijn in Azure AD. We raden aan dat als Hallo-account is verlopen, een werkstroomactie moet worden geactiveerd door een PowerShell-script waarmee Hallo van Azure AD-gebruikersaccount worden uitgeschakeld. Als u daarentegen wanneer Hallo-account is ingeschakeld, moet hello Azure AD-exemplaar worden ingeschakeld.

### <a name="overwrite-synchronized-passwords"></a>Gesynchroniseerde wachtwoorden overschrijven
Een beheerder kan handmatig uw wachtwoord opnieuw instellen met behulp van Windows PowerShell.

In dit geval Hallo nieuw wachtwoord overschrijft uw gesynchroniseerde wachtwoord en alle wachtwoordbeleidsregels gedefinieerd in de cloud Hallo zijn toegepaste toohello nieuwe wachtwoord.

Als u uw on-premises-wachtwoord opnieuw wijzigt, Hallo nieuwe wachtwoord is gesynchroniseerd toohello cloud en heeft deze voorrang op wachtwoord Hallo handmatig worden bijgewerkt.

Hallo synchronisatie van een wachtwoord heeft geen invloed op Hallo Azure gebruiker die is aangemeld. De huidige sessie van de cloud-service is niet direct beïnvloed door gesynchroniseerde wachtwoord wijzigen die wordt uitgevoerd terwijl u bent aangemeld in tooa-cloudservice. KMSI breidt Hallo duur van dit verschil. Wanneer het Hallo-cloudservice, moet u tooauthenticate opnieuw moet u tooprovide uw nieuwe wachtwoord.

### <a name="additional-advantages"></a>Extra voordelen

- Wachtwoordsynchronisatie is over het algemeen eenvoudiger tooimplement dan een federation-service. Deze geen extra servers vereist en elimineert de afhankelijkheid van een maximaal beschikbare federation service tooauthenticate gebruikers. 
- Wachtwoordsynchronisatie kan ook worden ingeschakeld in toevoeging toofederation. Worden kan gebruikt als terugval als een storing optreedt in uw federatieservice.












## <a name="enable-password-synchronization"></a>Wachtwoordsynchronisatie inschakelen
Wanneer u Azure AD Connect installeert met behulp van Hallo **Expresinstellingen** , Wachtwoordsynchronisatie is automatisch ingeschakeld. Zie voor meer informatie [aan de slag met Azure AD Connect met expresinstellingen](active-directory-aadconnect-get-started-express.md).

Als u aangepaste instellingen wanneer u Azure AD Connect installeert, is Wachtwoordsynchronisatie beschikbaar op Hallo aanmelden op de gebruikerspagina. Zie voor meer informatie [aangepaste installatie van Azure AD Connect](active-directory-aadconnect-get-started-custom.md).

![Wachtwoordsynchronisatie inschakelen](./media/active-directory-aadconnectsync-implement-password-synchronization/usersignin.png)

### <a name="password-synchronization-and-fips"></a>Wachtwoordsynchronisatie en FIPS
Als uw server is vergrendeld op basis van tooFederal Information Processing Standard (FIPS), wordt MD5 uitgeschakeld.

**tooenable MD5 voor Wachtwoordsynchronisatie Hallo stappen uitvoeren:**

1. Ga too%programfiles%\Azure AD Sync\Bin.
2. Open miiserver.exe.config.
3. Ga naar toohello configuration/runtime knooppunt achter Hallo Hallo-bestand.
4. Hallo knooppunt volgt toevoegen:`<enforceFIPSPolicy enabled="false"/>`
5. Sla uw wijzigingen op.

Voor een verwijzing naar is dit fragment wat er moet eruitzien als:

```
    <configuration>
        <runtime>
            <enforceFIPSPolicy enabled="false"/>
        </runtime>
    </configuration>
```

Zie voor meer informatie over beveiliging en FIPS [AAD Password Sync, versleuteling en FIPS-naleving](https://blogs.technet.microsoft.com/enterprisemobility/2014/06/28/aad-password-sync-encryption-and-fips-compliance/).

## <a name="troubleshoot-password-synchronization"></a>Probleem met Wachtwoordsynchronisatie oplossen
Als u problemen met synchronisatie van wachtwoorden hebt, raadpleegt u [Wachtwoordsynchronisatie oplossen](active-directory-aadconnectsync-troubleshoot-password-synchronization.md).

## <a name="next-steps"></a>Volgende stappen
* [Azure AD Connect-synchronisatie: Synchronisatieopties voor aanpassen](active-directory-aadconnectsync-whatis.md)
* [Uw on-premises identiteiten integreren met Azure Active Directory](active-directory-aadconnect.md)
