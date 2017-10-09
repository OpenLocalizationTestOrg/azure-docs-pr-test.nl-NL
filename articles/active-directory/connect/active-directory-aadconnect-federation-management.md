---
title: aaaActive Directory Federation Services management en aanpassingen met Azure AD Connect | Microsoft Docs
description: AD FS-beheer met Azure AD Connect en aanpassen van AD FS-aanmeldingspagina gebruikerservaring met Azure AD Connect en PowerShell.
keywords: AD FS, ADFS, AD FS-beheer zijn AAD Connect, Connect, aanmelden, AD FS aanpassing, trust, O365, Federatie, relying party herstellen
services: active-directory
documentationcenter: 
author: anandyadavmsft
manager: femila
editor: 
ms.assetid: 2593b6c6-dc3f-46ef-8e02-a8e2dc4e9fb9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 361a2bfd6d7a6993dbe773d6ea039ad1afc6346a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-and-customize-active-directory-federation-services-by-using-azure-ad-connect"></a>Beheren en aanpassen van Active Directory Federation Services met behulp van Azure AD Connect
Dit artikel wordt beschreven hoe toomanage en aanpassen van Active Directory Federation Services (AD FS) met behulp van Azure Active Directory (Azure AD) verbinding maken. Dit omvat ook andere taken van de AD FS dat u toodo mogelijk nodig heeft voor een volledige configuratie van een AD FS-farm.

| Onderwerp | Er wordt aangegeven |
|:--- |:--- |
| **Beheren van AD FS** | |
| [Hallo-vertrouwensrelatie repareren](#repairthetrust) |Hoe toorepair Hallo federatieve vertrouwensrelatie met Office 365. |
| [Gefedereerd met Azure AD met behulp van alternatieve aanmeldings-ID](#alternateid) | Federatie met behulp van alternatieve aanmeldings-ID configureren  |
| [Een AD FS-server toevoegen](#addadfsserver) |Hoe tooexpand een AD FS-farm met een extra AD FS-server. |
| [Een AD FS Web Application Proxy-server toevoegen](#addwapserver) |Hoe tooexpand een AD FS-farm met een extra Webtoepassingsproxy (WAP)-server. |
| [Een federatieve domein toevoegen](#addfeddomain) |Hoe tooadd een federatief domein. |
| [Hallo SSL-certificaat bijwerken](active-directory-aadconnectfed-ssl-update.md)| Hoe tooupdate Hallo SSL-certificaat voor een AD FS-farm. |
| **Aanpassen van AD FS** | |
| [Een aangepast bedrijfslogo of afbeelding toevoegen](#customlogo) |Hoe toocustomize een AD FS-aanmeldingspagina pagina met een bedrijfslogo en afbeelding. |
| [Een beschrijving van de aanmeldingspagina toevoegen](#addsignindescription) |Hoe pagina tooadd een aanmeldingspagina beschrijving. |
| [Wijzigen van de claimregels van AD FS](#modclaims) |Hoe toomodify AD FS-claims voor verschillende scenario's met Federatie. |

## <a name="manage-ad-fs"></a>Beheren van AD FS
U kunt verschillende AD FS-gerelateerde taken in Azure AD Connect met minimale tussenkomst uitvoeren met behulp van hello Azure AD Connect-wizard. Wanneer u klaar bent met het Azure AD Connect door actieve Hallo wizard installeert, kunt u Hallo wizard uitvoeren opnieuw tooperform aanvullende taken.

## Hallo-vertrouwensrelatie repareren<a name=repairthetrust></a>
U kunt Azure AD Connect toocheck Hallo huidige status van Hallo AD FS en Azure AD-vertrouwensrelatie gebruiken en nemen de nodige acties toorepair Hallo vertrouwen. Volg deze stappen toorepair uw Azure AD en AD FS vertrouwen.

1. Selecteer **reparatie AAD en ADFS-vertrouwen** uit Hallo lijst met aanvullende taken.
   ![Herstellen van AAD- en AD FS vertrouwen](media/active-directory-aadconnect-federation-management/RepairADTrust1.PNG)

2. Op Hallo **verbinding tooAzure AD** pagina, Geef uw referenties voor de globale beheerder voor Azure AD en klikt u op **volgende**.
   ![Verbinding maken met tooAzure AD](media/active-directory-aadconnect-federation-management/RepairADTrust2.PNG)

3. Op Hallo **RAS-referenties** pagina, voert u Hallo-referenties in voor de domeinbeheerder Hallo.

   ![Referenties voor externe toegang](media/active-directory-aadconnect-federation-management/RepairADTrust3.PNG)

    Nadat u op **volgende**, Azure AD Connect health certificaat controleert en ziet u eventuele problemen.

    ![Status van certificaten](media/active-directory-aadconnect-federation-management/RepairADTrust4.PNG)

    Hallo **gereed tooconfigure** pagina toont Hallo lijst van acties die worden uitgevoerd toorepair Hallo vertrouwen.

    ![Gereed tooconfigure](media/active-directory-aadconnect-federation-management/RepairADTrust5.PNG)

4. Klik op **installeren** toorepair Hallo vertrouwen.

> [!NOTE]
> Azure AD Connect kan alleen herstellen of act op certificaten die zelf-ondertekend zijn. Azure AD Connect-certificaten van derden niet worden hersteld.

## Gefedereerd met Azure AD dat gebruikmaakt van AlternateID<a name=alternateid></a>
Het verdient aanbeveling dat Hallo on-premises User Principal Name(UPN) en Hallo cloud principalnaam van gebruiker worden gehouden Hallo dezelfde. Als Hallo lokale UPN gebruikmaakt van een niet-routeerbare domein (bijvoorbeeld) Contoso.local) of kan niet worden gewijzigd vanwege toolocal toepassingsafhankelijkheden, wordt aangeraden instellen van de alternatieve aanmeldings-ID. Alternatieve aanmeldings-ID kunt u een aanmelden waar gebruikers zich kunnen aanmelden met een kenmerk dan de UPN, zoals mail tooconfigure. Hallo de keuze voor principalnaam van gebruiker in Azure AD Connect standaardwaarden toohello userPrincipalName kenmerk in Active Directory. Als u een ander kenmerk voor de principalnaam van gebruiker kiezen en zijn Federatie met AD FS, vervolgens Azure AD Connect AD FS wilt configureren voor alternatieve aanmeldings-ID. Een voorbeeld van het kiezen van een ander kenmerk voor User Principal Name wordt hieronder weergegeven:

![Selectie van alternatieve ID-kenmerk](media/active-directory-aadconnect-federation-management/attributeselection.png)

Alternatieve aanmeldings-ID configureren voor AD FS bestaat uit twee belangrijke stappen:
1. **De juiste set Hallo van uitgifte claims configureren**: claimregels Hallo uitgifte van de relying party hello Azure AD vertrouwen gewijzigde toouse Hallo geselecteerd UserPrincipalName kenmerk zijn zoals alternatieve ID van gebruiker Hallo Hallo.
2. **Schakel alternatieve aanmeldings-ID in Hallo AD FS-configuratie**: Hallo AD FS-configuratie is bijgewerkt, zodat AD FS kunt opzoeken van de gebruikers in de juiste forests Hallo Hallo alternatieve-id. Deze configuratie wordt ondersteund voor AD FS in Windows Server 2012 R2 (met KB2919355) of hoger. Als Hallo AD FS-servers 2012 R2 zijn, vereist Azure AD Connect-controles voor Hallo aanwezigheid van Hallo KB. Als hello KB niet wordt gedetecteerd, wordt een waarschuwing weergegeven nadat de configuratie is voltooid, zoals hieronder wordt weergegeven:

    ![Waarschuwing voor KB op 2012R2 ontbreekt](media/active-directory-aadconnect-federation-management/kbwarning.png)

    toorectify hello configuratie in geval van een ontbrekende KB installeren Hallo vereist [KB2919355](http://go.microsoft.com/fwlink/?LinkID=396590) en herstel daarna de vertrouwensrelatie met behulp van Hallo [AAD herstellen en AD FS-vertrouwensrelatie](#repairthetrust).

> [!NOTE]
> Voor meer informatie over alternateID en stappen toomanually configureren, lezen [Configuring Alternate Login ID](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/configuring-alternate-login-id)

## Een AD FS-server toevoegen<a name=addadfsserver></a>

> [!NOTE]
> tooadd een AD FS-server, Azure AD Connect vereist Hallo PFX-certificaat. Daarom kunt u deze bewerking uitvoeren als u Hallo AD FS-farm met behulp van Azure AD Connect geconfigureerd.

1. Selecteer **een extra federatieserver implementeren**, en klik op **volgende**.

   ![Extra federatieserver](media/active-directory-aadconnect-federation-management/AddNewADFSServer1.PNG)

2. Op Hallo **verbinding tooAzure AD** pagina, Geef uw referenties hoofdbeheerder voor Azure AD en klikt u op **volgende**.

   ![Verbinding maken met tooAzure AD](media/active-directory-aadconnect-federation-management/AddNewADFSServer2.PNG)

3. Geef beheerdersreferenties Hallo-domein.

   ![Referenties voor de domeinbeheerder](media/active-directory-aadconnect-federation-management/AddNewADFSServer3.PNG)

4. Azure AD Connect vraagt om wachtwoord op Hallo van Hallo PFX-bestand dat u hebt opgegeven tijdens het configureren van uw nieuwe AD FS-farm met Azure AD Connect. Klik op **wachtwoord invoeren** tooprovide Hallo wachtwoord voor Hallo PFX-bestand.

   ![Certificaatwachtwoord](media/active-directory-aadconnect-federation-management/AddNewADFSServer4.PNG)

    ![SSL-certificaat opgeven](media/active-directory-aadconnect-federation-management/AddNewADFSServer5.PNG)

5. Op Hallo **AD FS-Servers** pagina, voert u Hallo-servernaam of IP-adres toobe toegevoegd toohello AD FS-farm.

   ![AD FS-servers](media/active-directory-aadconnect-federation-management/AddNewADFSServer6.PNG)

6. Klik op **volgende**, en Ga via de uiteindelijke Hallo **configureren** pagina. Nadat Azure AD Connect is voltooid met het toevoegen van Hallo servers toohello AD FS-farm, krijgt u Hallo optie tooverify Hallo connectiviteit.

   ![Gereed tooconfigure](media/active-directory-aadconnect-federation-management/AddNewADFSServer7.PNG)

    ![Installatie voltooid](media/active-directory-aadconnect-federation-management/AddNewADFSServer8.PNG)

## Een AD FS WAP-server toevoegen<a name=addwapserver></a>

> [!NOTE]
> tooadd een WAP-server, in de Azure AD Connect is Hallo PFX-certificaat vereist. Daarom kunt u deze bewerking alleen uitvoeren als u Hallo AD FS-farm met behulp van Azure AD Connect geconfigureerd.

1. Selecteer **Web Application Proxy implementeren** uit Hallo lijst met beschikbare taken.

   ![Webtoepassingsproxy implementeren](media/active-directory-aadconnect-federation-management/WapServer1.PNG)

2. Geef referenties op Hallo Azure globale beheerder.

   ![Verbinding maken met tooAzure AD](media/active-directory-aadconnect-federation-management/wapserver2.PNG)

3. Op Hallo **Geef SSL-certificaat** pagina, Hallo wachtwoord opgeven voor Hallo PFX-bestand dat u hebt opgegeven toen u Hallo AD FS-farm met Azure AD Connect geconfigureerd.
   ![Certificaatwachtwoord](media/active-directory-aadconnect-federation-management/WapServer3.PNG)

    ![SSL-certificaat opgeven](media/active-directory-aadconnect-federation-management/WapServer4.PNG)

4. Hallo server toobe toegevoegd als een WAP-server toevoegen. Omdat Hallo WAP-server mogelijk niet lid toohello domein, Hallo wordt gevraagd voor beheerdersreferenties toohello server die wordt toegevoegd.

   ![Referenties van de beheerserver](media/active-directory-aadconnect-federation-management/WapServer5.PNG)

5. Op Hallo **vertrouwensrelatie proxyreferenties** pagina, Geef beheerdersreferenties tooconfigure Hallo proxyserveradres vertrouwen en toegang Hallo primaire server in Hallo AD FS-farm.

   ![Vertrouwensrelatie proxyreferenties](media/active-directory-aadconnect-federation-management/WapServer6.PNG)

6. Op Hallo **gereed tooconfigure** pagina Hallo wizard geeft Hallo-lijst van acties die worden uitgevoerd.

   ![Gereed tooconfigure](media/active-directory-aadconnect-federation-management/WapServer7.PNG)

7. Klik op **installeren** toofinish Hallo configuratie. Nadat het Hallo-configuratie is voltooid, Hallo Hallo wizard geeft u de optie tooverify Hallo connectiviteit toohello servers. Klik op **controleren** toocheck connectiviteit.

   ![Installatie voltooid](media/active-directory-aadconnect-federation-management/WapServer8.PNG)

## Een federatieve domein toevoegen<a name=addfeddomain></a>

Het is gemakkelijk tooadd een domein toobe gefedereerd met Azure AD met behulp van Azure AD Connect. Azure AD Connect Hallo domein voor Federatie toegevoegd en Hallo claim regels toocorrectly Hallo verlener weer wanneer u meerdere domeinen die zijn gefedereerd met Azure AD hebt gewijzigd.

1. tooadd een federatieve domein, selecteer Hallo taak **toevoegen van een extra Azure AD-domein**.

   ![Extra Azure AD-domein](media/active-directory-aadconnect-federation-management/AdditionalDomain1.PNG)

2. Klik op volgende pagina van wizard Hallo Hallo referenties Hallo hoofdbeheerder voor Azure AD.

   ![Verbinding maken met tooAzure AD](media/active-directory-aadconnect-federation-management/AdditionalDomain2.PNG)

3. Op Hallo **RAS-referenties** pagina, Hallo domein-beheerdersreferenties opgeven.

   ![Referenties voor externe toegang](media/active-directory-aadconnect-federation-management/additionaldomain3.PNG)

4. Op de volgende pagina Hallo overzicht Hallo wizard van Azure AD-domeinen die u kunt uw on-premises directory met federeren. Hallo domein uit Hallo lijst kiezen.

   ![Azure AD-domein](media/active-directory-aadconnect-federation-management/AdditionalDomain4.PNG)

    Nadat u ervoor Hallo domein kiest, wordt Hallo wizard biedt u met de juiste informatie over verdere acties die wizard Hallo nemen en Hallo gevolgen van het Hallo-configuratie. In sommige gevallen, als u een domein dat nog niet is geverifieerd in Azure AD Hallo wizard biedt u informatie toohelp selecteert verifiëren u Hallo domein. Zie [toevoegen van uw aangepaste domein naam tooAzure Active Directory](../active-directory-add-domain.md) voor meer informatie.

5. Klik op **Volgende**. Hallo **gereed tooconfigure** pagina bevat Hallo-lijst van acties die door Azure AD Connect worden uitgevoerd. Klik op **installeren** toofinish Hallo configuratie.

   ![Gereed tooconfigure](media/active-directory-aadconnect-federation-management/AdditionalDomain5.PNG)

> [!NOTE]
> Gebruikers van Hallo toegevoegd federatieve domein moet worden gesynchroniseerd voordat ze kunnen toologin tooAzure AD.

## <a name="ad-fs-customization"></a>AD FS-aanpassing
Hallo volgende secties bevatten informatie over een aantal algemene taken Hallo tooperform hebt wanneer u uw AD FS-aanmeldingspagina aanpassen.

## Een aangepast bedrijfslogo of afbeelding toevoegen<a name=customlogo></a>
toochange hello logo van Hallo-bedrijf dat wordt weergegeven op Hallo **aanmelden** pagina, gebruikt u Hallo na de Windows PowerShell-cmdlet en syntaxis.

> [!NOTE]
> Hallo aanbevolen dimensies voor Hallo logo 260 x 35 96 dpi-waarde met een bestandsgrootte van niet meer dan 10 KB zijn.

    Set-AdfsWebTheme -TargetName default -Logo @{path="c:\Contoso\logo.PNG"}

> [!NOTE]
> Hallo *TargetName* parameter is vereist. Hallo standaardthema dat wordt geleverd met AD FS heet standaard.

## Een beschrijving van de aanmeldingspagina toevoegen<a name=addsignindescription></a>
een aanmeldingspagina beschrijving toohello tooadd **aanmeldingspagina**, Hallo na de Windows PowerShell-cmdlet en syntaxis gebruiken.

    Set-AdfsGlobalWebContent -SignInPageDescriptionText "<p>Sign-in tooContoso requires device registration. Click <A href='http://fs1.contoso.com/deviceregistration/'>here</A> for more information.</p>"

## Wijzigen van de claimregels van AD FS<a name=modclaims></a>
AD FS ondersteunt een taal die u kunt gebruiken voor uitgebreide claim toocreate aangepaste claimregels. Zie voor meer informatie [rol van de Claimregeltaal Hallo Hallo](https://technet.microsoft.com/library/dd807118.aspx).

Hallo volgende secties wordt beschreven hoe u aangepaste regels voor enkele scenario's die betrekking tooAzure AD en AD FS-federatie hebben kan schrijven.

### <a name="immutable-id-conditional-on-a-value-being-present-in-hello-attribute"></a>Niet-wijzigbaar voorwaardelijke op een waarde in het Hallo-kenmerk-ID
Azure AD Connect kunt u een kenmerk toobe gebruikt als een bronanker wanneer objecten zijn gesynchroniseerd tooAzure AD opgeven. Als de waarde in het aangepaste kenmerk Hallo Hallo niet leeg is, kunt u een niet-wijzigbaar ID claim tooissue.

Bijvoorbeeld, kunt u selecteren **ms-ds-consistencyguid** als Hallo-kenmerk voor het bronanker hello en probleem **onveranderbare id genoemd** als **ms-ds-consistencyguid** in case Hallo het kenmerk heeft de waarde tegen. Als er geen waarde tegen Hallo kenmerk is, geven **objectGuid** zoals Hallo onveranderbare ID. U kunt Hallo set aangepaste claimregels kunt opstellen, zoals beschreven in de volgende sectie Hallo.

**Regel 1: Querykenmerken**

    c:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname"]
    => add(store = "Active Directory", types = ("http://contoso.com/ws/2016/02/identity/claims/objectguid", "http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid"), query = "; objectGuid,ms-ds-consistencyguid;{0}", param = c.Value);

In deze regel, waaruit u gegevens ophaalt Hallo waarden van **ms-ds-consistencyguid** en **objectGuid** voor Hallo gebruiker uit Active Directory. Hallo store naam tooan betreffende winkelnaam wijzigen in uw AD FS-implementatie. Hallo claims type tooa juiste claims type voor uw federatieserver ook wijzigen zoals is gedefinieerd voor **objectGuid** en **ms-ds-consistencyguid**.

Ook met behulp van **toevoegen** en niet **probleem**, u te voorkomen dat een uitgaande probleem voor Hallo entiteit toe te voegen en Hallo waarden kunt gebruiken als tussenliggende waarden. Verleent u Hallo claim in een latere regel nadat u hebt vastgesteld welke waarde toouse zoals Hallo onveranderbare ID.

**Regel 2: Controleer of de ds-ms-consistencyguid voor Hallo-gebruiker bestaat**

    NOT EXISTS([Type == "http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid"])
    => add(Type = "urn:anandmsft:tmp/idflag", Value = "useguid");

Deze regel definieert een tijdelijke vlag aangeroepen **idflag** ingestelde te**useguid** als er geen **ms-ds-consistencyguid** ingevuld voor Hallo-gebruiker. Hallo logica achter is Hallo-feit dat AD FS leeg claims niet toegestaan. Dus als u claims http://contoso.com/ws/2016/02/identity/claims/objectguid en http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid in regel 1 toevoegt, u uiteindelijk met eindigen een **msdsconsistencyguid** alleen als claim Hallo-waarde wordt voor de gebruiker hello gevuld. Als deze niet is ingevuld, wordt AD FS ziet dat het een lege waarde hebben en onmiddellijk verwijderd. Alle objecten hebben **objectGuid**, zodat deze claim wordt altijd er nadat regel 1 wordt uitgevoerd.

**Regel 3: Ms-ds-consistencyguid verlenen als niet-wijzigbaar ID indien aanwezig**

    c:[Type == "http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid"]
    => issue(Type = "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier", Value = c.Value);

Dit is een impliciete **Exist** controleren. Als het Hallo-waarde voor Hallo claim bestaat, geven vervolgens dat als niet-wijzigbaar Hallo-id. Hallo maakt gebruik van het vorige voorbeeld Hallo **nameidentifier** claim. Hebt u toochange deze toohello juiste claimtype voor Hallo onveranderbare ID in uw omgeving.

**Regel 4: ObjectGuid verlenen als niet-wijzigbaar-ID als ms-ds-consistencyGuid niet aanwezig is**

    c1:[Type == "urn:anandmsft:tmp/idflag", Value =~ "useguid"]
    && c2:[Type == "http://contoso.com/ws/2016/02/identity/claims/objectguid"]
    => issue(Type = "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier", Value = c2.Value);

In deze regel, bent u gewoon Hallo tijdelijke vlag controleren **idflag**. U bepalen of tooissue Hallo claim is gebaseerd op de waarde ervan.

> [!NOTE]
> Hallo-volgorde van deze regels is belangrijk.

### <a name="sso-with-a-subdomain-upn"></a>Eenmalige aanmelding met een subdomein UPN
U kunt meer dan één domein toobe gefedereerd met behulp van Azure AD Connect, zoals beschreven in toevoegen [toevoegen van een nieuwe federatieve domein](active-directory-aadconnect-federation-management.md#addfeddomain). U moet Hallo UPN (User Principal Name) Gebruikersclaim zodanig aanpassen dat hello uitgever-ID komt toohello hoofddomein en niet Hallo subdomein overeen omdat Hallo federatieve hoofddomein ook Hallo onderliggende vallen.

Standaard Hallo claimregelsjablonen voor uitgevers-ID is ingesteld als:

    c:[Type
    == “http://schemas.xmlsoap.org/claims/UPN“]

    => issue(Type = “http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid“, Value = regexreplace(c.Value, “.+@(?<domain>.+)“, “http://${domain}/adfs/services/trust/“));

![Standaard uitgever-ID claim](media/active-directory-aadconnect-federation-management/issuer_id_default.png)

Standaardregel Hallo gewoon duurt Hallo UPN-achtervoegsel en wordt gebruikt in Hallo uitgever-ID claim. Bijvoorbeeld: John is een gebruiker in sub.contoso.com en contoso.com is gefedereerd met Azure AD. John voert john@sub.contoso.com zoals Hallo gebruikersnaam tijdens het aanmelden tooAzure AD. Hallo standaard uitgever-ID claimregel in AD FS verwerkt op Hallo volgende wijze:

    c:[Type
    == “http://schemas.xmlsoap.org/claims/UPN“]

    => issue(Type = “http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid“, Value = regexreplace(john@sub.contoso.com, “.+@(?<domain>.+)“, “http://${domain}/adfs/services/trust/“));

**Claimwaarde:** http://sub.contoso.com/adfs/services/trust/

toohave alleen Hallo hoofddomein in Hallo verlener claimwaarde, wijzig Hallo claim regel toomatch Hallo volgende:

    c:[Type == “http://schemas.xmlsoap.org/claims/UPN“]

    => issue(Type = “http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid“, Value = regexreplace(c.Value, “^((.*)([.|@]))?(?<domain>[^.]*[.].*)$”, “http://${domain}/adfs/services/trust/“));

## <a name="next-steps"></a>Volgende stappen
Meer informatie over [opties aanmelden gebruiker](active-directory-aadconnect-user-signin.md).
