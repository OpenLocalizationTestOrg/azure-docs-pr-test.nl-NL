---
title: 'Azure AD Connect: Gebruiker aanmelden | Microsoft Docs'
description: Azure AD Connect gebruiker aanmelden voor aangepaste instellingen.
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: curtand
ms.assetid: 547b118e-7282-4c7f-be87-c035561001df
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 7848b419f3855b25cfa074a46779d258bd534bae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-user-sign-in-options"></a>Azure AD Connect gebruiker aanmeldingsopties
Verbinden met Azure Active Directory (Azure AD) kunt uw gebruikers toosign in tooboth cloud en lokale bronnen met behulp van dezelfde wachtwoorden Hallo. Dit artikel beschrijft de belangrijkste concepten voor elk model identiteit toohelp Kies van Hallo-identiteit die u wilt toouse tooAzure AD aanmelden.

Als u al bekend met hello Azure AD identiteitsmodel bent en meer informatie over een specifieke methode toolearn, raadpleegt u de desbetreffende koppeling Hallo:

* [Wachtwoordsynchronisatie](#password-synchronization) met [eenmalige aanmelding (SSO)](active-directory-aadconnect-sso.md)
* [Pass through-verificatie](active-directory-aadconnect-pass-through-authentication.md)
* [Federatieve eenmalige aanmelding (met Active Directory Federation Services (AD FS))](#federation-that-uses-a-new-or-existing-farm-with-ad-fs-in-windows-server-2012-r2)

## <a name="choosing-hello-user-sign-in-method-for-your-organization"></a>Hallo gebruiker aanmelden methode voor uw organisatie te kiezen
Voor de meeste organisaties die alleen tooenable gebruiker aanmelden tooOffice 365, SaaS-toepassingen en andere Azure AD gebaseerde bronnen wilt, wordt aangeraden wachtwoord Hallo-synchronisatie standaardoptie. Sommige organisaties hebben echter een bepaalde reden is dat ze niet kunnen toouse deze optie. Ze kunnen beide een federatieve aanmelding opties, zoals AD FS of Pass through-verificatie kiezen. U kunt na de tabel toohelp u bij het maken van de juiste keuze Hallo Hallo gebruiken.

Nodig| PS met eenmalige aanmelding| PA met eenmalige aanmelding| AD FS |
 --- | --- | --- | --- |
Nieuwe gebruikers, contactpersonen en groepsaccounts in de lokale Active Directory toohello cloud automatisch gesynchroniseerd.|x|x|x|
Instellen van mijn tenants voor Office 365 hybride scenario's.|x|x|x|
Mijn gebruikers toosign in services en -toegang cloud inschakelen met behulp van hun on-premises wachtwoord.|x|x|x|
Eenmalige aanmelding implementeren met behulp van zakelijke referenties.|x|x|x|
Zorg ervoor dat er geen wachtwoorden in Hallo cloud worden opgeslagen.||x *|x|
Oplossingen voor on-premises meervoudige verificatie inschakelen.|||x|

* Via een lichtgewicht connector.

>[!NOTE]
> Pass through-verificatie heeft momenteel de enige beperkingen met uitgebreide clients. Zie [Pass through-verificatie](active-directory-aadconnect-pass-through-authentication.md) voor meer informatie.

### <a name="password-synchronization"></a>Wachtwoordsynchronisatie
Met Wachtwoordsynchronisatie worden-hashes van gebruikerswachtwoorden gesynchroniseerd vanaf de lokale Active Directory tooAzure AD. Wanneer wachtwoorden worden gewijzigd of opnieuw instellen van lokale, nieuwe wachtwoorden Hallo gesynchroniseerde tooAzure AD zijn onmiddellijk zodat uw gebruikers kunnen altijd gebruik dezelfde Hallo wachtwoord voor cloud-bronnen en lokale bronnen. Hallo wachtwoorden worden nooit verzonden tooAzure AD of opgeslagen in Azure AD in ongecodeerde tekst. U kunt Wachtwoordsynchronisatie samen met wachtwoord terugschrijven tooenable selfservice wachtwoordherstel in Azure AD.

Bovendien kunt u inschakelen [SSO](active-directory-aadconnect-sso.md) voor gebruikers op domein-machines op Hallo bedrijfsnetwerk. Met eenmalige aanmelding ingeschakeld gebruikers alleen nodig tooenter een gebruikersnaam toohelp ze veilig toegang krijgen tot bronnen.

![Wachtwoordsynchronisatie](./media/active-directory-aadconnect-user-signin/passwordhash.png)

Zie voor meer informatie, Hallo [Wachtwoordsynchronisatie](active-directory-aadconnectsync-implement-password-synchronization.md) artikel.

### <a name="pass-through-authentication"></a>Pass through-verificatie
Met Pass through-verificatie wordt het wachtwoord van gebruiker Hallo gevalideerd met Hallo lokale Active Directory-domeincontroller. Hallo wachtwoord nodig niet aanwezig in Azure AD in een formulier toobe. Hierdoor lokale beleidsregels, zoals aanmelden uur beperkingen, toobe geëvalueerd tijdens toocloud verificatieservices.

Pass through-verificatie gebruikt een eenvoudige-agent op een Windows Server 2012 R2 domein machine Hallo on-premises omgeving. Deze agent luistert naar aanvragen voor wachtwoord-validatie. Alle poorten voor inkomend verkeer toobe open toohello Internet nodig niet is.

Bovendien kunt u ook eenmalige aanmelding voor gebruikers in domein-machines op Hallo bedrijfsnetwerk. Met eenmalige aanmelding ingeschakeld gebruikers alleen nodig tooenter een gebruikersnaam toohelp ze veilig toegang krijgen tot bronnen.
![Pass through-verificatie](./media/active-directory-aadconnect-user-signin/pta.png)

Zie voor meer informatie:
- [Pass through-verificatie](active-directory-aadconnect-pass-through-authentication.md)
- [Eenmalige aanmelding](active-directory-aadconnect-sso.md)

### <a name="federation-that-uses-a-new-or-existing-farm-with-ad-fs-in-windows-server-2012-r2"></a>Federatieve die gebruikmaakt van een nieuwe of bestaande farm met AD FS in Windows Server 2012 R2
Met federatieve aanmelden, kunnen uw gebruikers aanmelden tooAzure AD gebaseerde services met hun on-premises wachtwoorden. Terwijl ze op het bedrijfsnetwerk hello, hebben ze geen zelfs tooenter hun wachtwoorden. Hallo federation optie met AD FS gebruikt, kunt u een nieuwe of bestaande farm met AD FS in Windows Server 2012 R2 kunt implementeren. Als u op een bestaande farm toospecify kiest, configureert Azure AD Connect Hallo vertrouwensrelatie tussen uw farm en Azure AD, zodat uw gebruikers zich kunnen aanmelden.

<center>![Federatie met AD FS in Windows Server 2012 R2](./media/active-directory-aadconnect-user-signin/federatedsignin.png)</center>

#### <a name="deploy-federation-with-ad-fs-in-windows-server-2012-r2"></a>Federatie met AD FS in Windows Server 2012 R2 implementeren

Als u een nieuwe farm implementeert, moet u het volgende nodig:

* Een Windows Server 2012 R2-server voor Hallo federation-server.
* Een Windows Server 2012 R2-server voor Hallo Web Application Proxy.
* Een pfx-bestand met een SSL-certificaat voor de naam van uw beoogde federation-service. Bijvoorbeeld: fs.contoso.com.

Als u een nieuwe farm implementeert of via een bestaande farm, u moet:

* Lokale beheerdersreferenties op uw federatieservers.
* Lokale beheerdersreferenties op de werkgroepservers van een (geen lid van een domein) die u van plan toodeploy bent Hallo Web Application Proxy-rol op.
* Hallo-machine uit te voeren Hallo wizard op toobe kunnen tooconnect tooany andere machines dat u tooinstall AD FS of Web Application Proxy op wilt met behulp van Windows Remote Management.

Zie voor meer informatie [eenmalige aanmelding met AD FS configureren](active-directory-aadconnect-get-started-custom.md#configuring-federation-with-ad-fs).

#### <a name="sign-in-by-using-an-earlier-version-of-ad-fs-or-a-third-party-solution"></a>Aanmelden met een eerdere versie van AD FS of een oplossing van derden
Als u al cloud aanmelden met behulp van een eerdere versie van AD FS (zoals AD FS 2.0) of een derde partij federatieprovider hebt geconfigureerd, kunt u tooskip aanmelden Gebruikersconfiguratie met Azure AD Connect. Hierdoor kunt u tooget Hallo laatste synchronisatie en andere mogelijkheden van Azure AD Connect terwijl u ook uw bestaande oplossing voor aanmelden.

Zie voor meer informatie, Hallo [Azure AD van derden federatiecompatibiliteitslijst](active-directory-aadconnect-federation-compatibility.md).


## <a name="user-sign-in-and-user-principal-name"></a>Gebruiker aanmelden en UPN
### <a name="understanding-user-principal-name"></a>Understanding UPN-naam
In Active Directory is voor het achtervoegsel voor user principal name (UPN) voor Hallo standaard Hallo DNS-naam van het Hallo-domein waarin Hallo-gebruikersaccount is gemaakt. In de meeste gevallen is dit Hallo-domeinnaam die geregistreerd als Hallo enterprise domein op Hallo Internet. U kunt echter meer UPN-achtervoegsels toevoegen met behulp van Active Directory: domeinen en vertrouwensrelaties.

Hallo UPN van de gebruiker Hallo heeft Hallo indeling username@domain. Bijvoorbeeld, een Active Directory-domein 'contoso.com' met de naam van een gebruiker met de naam John wellicht Hallo UPN 'john@contoso.com'. Hallo UPN van de gebruiker Hallo is gebaseerd op RFC 822. Hoewel hello UPN- en e-share hello dezelfde indeling, Hallo-waarde van Hallo UPN voor een gebruiker kunnen wel of niet dezelfde als e-mailadres van de gebruiker Hallo HALLO hallo.

### <a name="user-principal-name-in-azure-ad"></a>UPN-naam in Azure AD
Hello Azure AD Connect-wizard gebruikt de kenmerk userPrincipalName Hallo of kunt die u opgeven Hallo kenmerk (in een aangepaste installatie) toobe als Hallo UPN-naam van on-premises gebruikt in Azure AD. Dit is Hallo-waarde die wordt gebruikt voor het aanmelden tooAzure AD. Als het Hallo-waarde van Hallo userPrincipalName kenmerk komt niet overeen tooa gecontroleerd domein in Azure AD, Azure AD wordt vervangen door een standaard. onmicrosoft.com-waarde.

Elke map in Azure Active Directory wordt geleverd met een ingebouwde domeinnaam Hallo indeling contoso.onmicrosoft.com, waarmee u aan de slag met Azure of andere Microsoft-services. U kunt verbeteren en de aanmeldingservaring Hallo vereenvoudigen met behulp van aangepaste domeinen. Voor informatie over aangepaste domeinnamen in Azure AD en hoe tooverify een domein, Zie [toevoegen van uw aangepaste domein naam tooAzure Active Directory](../add-custom-domain.md#add-your-custom-domain).

## <a name="azure-ad-sign-in-configuration"></a>Aanmeldconfiguratie Azure AD
### <a name="azure-ad-sign-in-configuration-with-azure-ad-connect"></a>Azure AD-in-configuratie met Azure AD Connect
Hello Azure AD-aanmeldingservaring aanpast, is afhankelijk van of in Azure AD kan overeenkomen met Hallo UPN-achtervoegsel van een gebruiker die wordt gesynchroniseerd tooone van Hallo aangepaste domeinen die zijn geverifieerd in hello Azure AD-directory. Azure AD Connect bevat help tijdens het configureren van Azure AD-aanmelden-instellingen, zodat Hallo aanmelden gebruikerservaring in Hallo cloud vergelijkbare toohello lokale ervaring.

Azure AD Connect lijsten Hallo UPN-achtervoegsels die zijn gedefinieerd voor de domeinen en pogingen toomatch Hallo ze met een aangepast domein in Azure AD. Vervolgens kunt u met de Hallo gepaste actie die toobe genomen moet.
Hello Azure AD-aanmeldingspagina bevat Hallo UPN-achtervoegsels die zijn gedefinieerd voor de lokale Active Directory en wordt de bijbehorende status Hallo tegen elk achtervoegsel weergegeven. Hallo statuswaarden kunnen een van de volgende Hallo zijn:

| Status | Beschrijving | Actie vereist |
|:--- |:--- |:--- |
| Geverifieerd |Azure AD Connect gevonden dat een overeenkomende domein in Azure AD geverifieerd. Alle gebruikers voor dit domein kunnen aanmelden met hun on-premises referenties. |Er is geen actie vereist. |
| Niet geverifieerd |Azure AD Connect een overeenkomende aangepast domein in Azure AD gevonden, maar het is niet geverifieerd. Hallo UPN-achtervoegsel van Hallo gebruikers van dit domein worden standaard toohello gewijzigd. het achtervoegsel onmicrosoft.com na synchronisatie als Hallo domein is niet geverifieerd. | [Controleer of het aangepaste domein Hallo in Azure AD.](../add-custom-domain.md#verify-the-domain-name-with-azure-ad) |
| Niet toegevoegd |Azure AD Connect niet een aangepast domein gevonden die overeenkwam toohello UPN-achtervoegsel. Hallo UPN-achtervoegsel van Hallo gebruikers van dit domein worden standaard toohello gewijzigd. achtervoegsel onmicrosoft.com als Hallo domein niet is toegevoegd en geverifieerd in Azure. | [Toevoegen en controleer of u een aangepast domein dat overeenkomt met toohello UPN-achtervoegsel.](../add-custom-domain.md) |

de aanmeldingspagina Hello Azure AD geeft een lijst Hallo UPN-achtervoegsels die zijn gedefinieerd voor de lokale Active Directory en de bijbehorende aangepast domein in Azure AD met de huidige verificatiestatus Hallo Hallo. In een aangepaste installatie kunt u nu Hallo-kenmerk voor Hallo user principal name op Hallo selecteren **Azure AD-aanmeldingspagina** pagina.

![Azure AD-aanmeldingspagina](./media/active-directory-aadconnect-user-signin/custom_azure_sign_in.png)

U kunt klikken op Hallo vernieuwen knop toore ophalen Hallo laatste status van aangepaste domeinen Hallo van Azure AD.

### <a name="selecting-hello-attribute-for-hello-user-principal-name-in-azure-ad"></a>Hallo-kenmerk voor Hallo user principal name in Azure AD selecteren
Hallo kenmerk userPrincipalName is Hallo-kenmerk die gebruikers gebruiken wanneer ze zich tooAzure AD en Office 365 aanmelden. Hallo-domeinen (ook wel bekend als UPN-achtervoegsels) die worden gebruikt in Azure AD voordat Hallo gebruikers worden gesynchroniseerd, moet u controleren.

Het is raadzaam Hallo standaard kenmerk userPrincipalName te houden. Als dit kenmerk nonroutable en kan niet worden geverifieerd, dan is het mogelijk tooselect een ander kenmerk (bijvoorbeeld e-mail) als Hallo-kenmerk van de Hallo aanmeldings-ID. Dit staat bekend als Hallo alternatieve-ID. Hallo alternatieve id-kenmerkwaarde moet Hallo RFC 822 standaard volgen. U kunt een alternatieve ID met wachtwoord SSO en federatieve SSO als oplossing voor aanmelden hello gebruiken.

> [!NOTE]
> Met behulp van een alternatieve ID is niet compatibel met alle Office 365-werkbelastingen. Zie voor meer informatie [Configuring Alternate Login ID](https://technet.microsoft.com/library/dn659436.aspx).
>
>

#### <a name="different-custom-domain-states-and-their-effect-on-hello-azure-sign-in-experience"></a>Ander aangepast domein statussen en hun effect op Hallo Azure aanmelden ervaring
Het is heel belangrijk toounderstand Hallo relatie tussen Hallo aangepast domein statussen in uw Azure AD-directory en hello UPN-achtervoegsels die zijn gedefinieerd op de lokale. We doorlopen Hallo verschillende mogelijke Azure aanmelden ervaringen wanneer u synchronisatie instellen bent met behulp van Azure AD Connect.

Voor Hallo informatie te volgen, gaan we ervan uit dat we betrokken zijn bij Hallo UPN-achtervoegsel contoso.com, die wordt gebruikt in Hallo on-premises adreslijst als onderdeel van de UPN--bijvoorbeeld user@contoso.com.

###### <a name="express-settingspassword-synchronization"></a>Snelle synchronisatie-instellingen en wachtwoord
| Status | Effect op de gebruikerservaring Azure aanmelden |
|:---:|:--- |
| Niet toegevoegd |In dit geval is geen aangepast domein voor contoso.com toegevoegd aan hello Azure AD-directory. Gebruikers die beschikken over UPN met on-premises Hallo achtervoegsel @contoso.com niet kunnen toouse hun lokale UPN toosign in tooAzure. Ze hebt een nieuwe UPN die is opgegeven toothem door Azure AD door toe te voegen Hallo achtervoegsel voor Hallo standaard Azure AD-directory in plaats daarvan toouse. Bijvoorbeeld, als u gebruikers toohello Azure AD-directory azurecontoso.onmicrosoft.com synchroniseert bent, vervolgens Hallo lokale gebruiker user@contoso.com een UPN van krijgt user@azurecontoso.onmicrosoft.com. |
| Niet geverifieerd |In dit geval hebben we een aangepast domein contoso.com die in hello Azure AD-directory wordt toegevoegd. Het echter nog niet geverifieerd. Als u verder gaat met het synchroniseren van gebruikers zonder Hallo domein te verifiëren, wordt vervolgens Hallo gebruikers een nieuwe UPN wordt toegewezen door Azure AD, net als in Hallo 'Wordt niet toegevoegd'-scenario. |
| Geverifieerd |In dit geval hebben we een aangepast domein contoso.com die al is toegevoegd en geverifieerd in Azure AD voor Hallo UPN-achtervoegsel. Gebruikers worden kunnen toouse hun lokale UPN-naam, bijvoorbeeld user@contoso.com, toosign in tooAzure nadat ze zijn gesynchroniseerd tooAzure AD. |

###### <a name="ad-fs-federation"></a>AD FS-federatie
U kunt een federatie met Hallo standaard maken. onmicrosoft.com-domein in Azure AD of een niet-geverifieerde aangepaste in Azure AD. Wanneer u uitvoert hello Azure AD Connect-wizard, als u een niet-geverifieerd domein toocreate selecteert een federatie met vervolgens Azure AD Connect wordt u gevraagd u Hello nodig toobe gemaakt waar uw DNS wordt gehost voor Hallo domein registreert. Zie voor meer informatie [hello Azure AD-domein controleren voor Federatie is geselecteerd](active-directory-aadconnect-get-started-custom.md#verify-the-azure-ad-domain-selected-for-federation).

Als u Hallo gebruiker aanmelden optie geselecteerd **Federatie met AD FS**, en vervolgens moet u een aangepast domein toocontinue maken van een federatieve in Azure AD hebben. Voor onze bespreking betekent dit dat er moet een aangepast domein contoso.com in hello Azure AD-directory toegevoegd.

| Status | Effect op Hallo Azure aanmelden gebruikerservaring |
|:---:|:--- |
| Niet toegevoegd |Azure AD Connect gevonden in dit geval een overeenkomende aangepast domein voor Hallo UPN-achtervoegsel contoso.com in hello Azure AD-directory. Moet u een aangepast domein contoso.com tooadd als u gebruikers toosign in met behulp van AD FS met de UPN van de lokale (zoals user@contoso.com). |
| Niet geverifieerd |In dit geval Azure AD Connect vraagt u om met de juiste informatie over hoe u uw domein in een later stadium kunt controleren. |
| Geverifieerd |In dit geval gaat u door met de Hallo-configuratie zonder verdere actie. |

## <a name="changing-hello-user-sign-in-method"></a>Hallo gebruiker aanmelden methode wijzigen
U kunt Hallo gebruiker aanmelden methode kunt wijzigen van federatieve, Wachtwoordsynchronisatie of Pass through-verificatie met behulp van Hallo-taken die beschikbaar in Azure AD Connect na de initiële configuratie Hallo van Azure AD Connect met Hallo-wizard zijn. Hello Azure AD Connect-wizard opnieuw uitvoeren en ziet u een lijst met taken die u kunt uitvoeren. Selecteer **wijzigen gebruikersaanmelding** uit Hallo lijst met taken.

![Gebruikersaanmelding wijzigen](./media/active-directory-aadconnect-user-signin/changeusersignin.png)

Op de volgende pagina hello, bent u tooprovide Hallo referenties gevraagd voor Azure AD.

![Verbinding maken met tooAzure AD](./media/active-directory-aadconnect-user-signin/changeusersignin2.png)

Op Hallo **gebruikersaanmelding** pagina, selecteert u Hallo gewenst gebruiker aanmelden.

![Verbinding maken met tooAzure AD](./media/active-directory-aadconnect-user-signin/changeusersignin2a.png)

> [!NOTE]
> Als u alleen een tijdelijke switch toopassword synchronisatie maakt, selecteert u Hallo **gebruikersaccounts niet worden geconverteerd** selectievakje. Hallo-optie niet inschakelt, wordt elke gebruiker toofederated converteren en het kan enkele uren duren.
>
>

## <a name="next-steps"></a>Volgende stappen
- Meer informatie over [uw on-premises identiteiten integreren met Azure Active Directory](active-directory-aadconnect.md).
- Meer informatie over [ontwerpconcepten Azure AD Connect](active-directory-aadconnect-design-concepts.md).
