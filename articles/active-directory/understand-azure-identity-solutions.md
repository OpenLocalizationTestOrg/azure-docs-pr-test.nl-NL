---
title: aaaUnderstand Azure Identity | Microsoft Docs
description: Haal een basiskennis van Microsoft Azure identiteit oplossing voorwaarden, concepten en aanbevelingen voor u toomake Hallo beste identiteit governance beslissing voor uw organisatie.
keywords: 
author: jeffgilb
manager: femila
ms.reviewer: jsnow
ms.author: jeffgilb
ms.date: 7/17/2017
ms.topic: article
ms.prod: 
ms.service: azure
ms.technology: 
ms.assetid: 
ms.custom: it-pro
ms.openlocfilehash: 4d9c90bd7a6bcc9637be3107998f9da5bd4cbdae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="understand-azure-identity-solutions"></a>Azure-identiteitsoplossingen begrijpen
Microsoft Azure Active Directory (Azure AD) is een identiteits- en toegangsbeheer cloud beheeroplossing die directoryservices en identiteit governance Toepassingsbeheer toegang biedt. Azure AD snel [kunt van eenmalige aanmelding (SSO)](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-manage-sso) too1, 000's met vooraf geïntegreerde commerciële en aangepaste apps in Hallo [Azure AD-toepassingsgalerie](https://azure.microsoft.com/marketplace/active-directory/all/). Veel van deze apps die u waarschijnlijk al, zoals Office 365, Salesforce.com vak, ServiceNow en Workday gebruikt.

Eén Azure AD-directory is automatisch gekoppeld aan een Azure-abonnement wanneer deze wordt gemaakt. Hallo identity-service in Azure biedt vervolgens Azure AD alle identiteits- en controlefuncties voor toegang voor cloud-gebaseerde bronnen. Deze resources kunnen gebruikers, apps en groepen voor een afzonderlijke tenant (organisatie) bevatten zoals weergegeven in het volgende diagram Hallo:

![Azure Active Directory](./media/understand-azure-identity-solutions/azure-ad.png)

Microsoft Azure biedt verschillende manieren tooleverage identiteit als een service (IDaaS) met verschillende bevoegdheidsniveaus complexiteit toomeet behoeften van uw afzonderlijke organisatie. Hallo rest van dit artikel helpt u begrijpen basic Azure identity-terminologie en -concepten, evenals aanbevelingen voor u toomake Hallo beste keuze uit de beschikbare opties Hallo.

## <a name="terms-tooknow"></a>Voorwaarden tooknow

Voordat u op een Azure identity-oplossing voor uw organisatie kunt, moet u een basiskennis van Hallo termen die vaak worden gebruikt bij het bespreken van de identiteit van de Azure-services.

|Term tooknow| Beschrijving|
|-----|-----|
|Azure-abonnement |Abonnementen zijn gebruikte toopay voor Azure-cloudservices en meestal gekoppelde tooa creditcard. U kunt meerdere abonnementen hebt, maar het kan lastig tooshare resources tussen abonnementen zijn.|
|Azure-tenant | Een Azure AD-tenant is representatief is voor één organisatie. Er is een toegewijde, vertrouwde instantie van Azure AD dat automatisch wordt gemaakt wanneer een organisatie zich registreert voor een Microsoft cloud service-abonnement zoals Azure, Intune of Office 365. Tenants kunnen krijgen toegang tooservices in een specifieke omgeving (één tenant) of in een gedeelde omgeving met andere organisaties (multitenant).|
|Azure AD-map | Elke Azure-tenant is een toegewijde, vertrouwde Azure AD-adreslijst met gebruikers, groepen en toepassingen van Hallo-tenant. Het is gebruikte tooperform identiteits- en beheerfuncties voor tenantbronnen. Omdat een unieke Azure AD-directory wordt automatisch ingerichte toorepresent uw organisatie wanneer u zich aanmeldt voor een Microsoft-cloudservice zoals Azure, Microsoft Intune of Office 365, soms ziet u Hallo voorwaarden *tenant*, *Azure AD*, en *Azure AD-directory* door elkaar gebruikt. |
|Aangepast domein | Wanneer u eerst zich aanmeldt voor een Microsoft cloud service-abonnement, uw tenant (organisatie) gebruikt een *. onmicrosoft.com* domeinnaam. De meeste organisaties hebben echter een of meer domeinnamen die gebruikte toodo business en dat eindgebruikers tooaccess bedrijfsbronnen gebruiken. U kunt uw aangepaste domein naam tooAzure AD toevoegen zodat hello domeinnaam bekend tooyour gebruikers, zoals is  *alice@contoso.com*  in plaats van  *alice@contoso.onmicrosoft.com* . |
|Azure AD-account | Dit zijn de identiteiten die zijn gemaakt met behulp van Azure AD of een andere Microsoft-cloudservice, zoals Office 365. Ze worden opgeslagen in Azure AD en toegankelijk tooany van van Hallo organisatie cloud service-abonnementen. |
|Azure-abonnementbeheerder| de accountbeheerder Hallo is Hallo persoon die zich heeft aangemeld of hello Azure-abonnement hebt aangeschaft. Ze kunnen hello gebruiken [Accountcentrum](https://account.windowsazure.com/Home/Index) tooperform verschillende beheertaken, zoals abonnementen maken, abonnementen annuleren, Hallo facturering voor een abonnement te wijzigen of wijzig Hallo servicebeheerder. |
|Globale beheerder van Azure AD | Azure AD globale beheerders hebben volledige toegang tooall Azure AD-beheerfuncties. Hallo persoon die zich voor een Microsoft cloud service-abonnement automatisch aanmeldt wordt een globale beheerder standaard. U kunt meer dan één globale beheerder hebben, maar alleen globale beheerders kunnen toewijzen van [andere beheerdersrollen Hallo](https://docs.microsoft.com/azure/active-directory/active-directory-assign-admin-roles-azure-portal) toousers. |
|Microsoft-account | Microsoft-accounts (gemaakt door u voor persoonlijk gebruik) bieden toegang tooconsumer gerichte Microsoft-producten en cloudservices, zoals Outlook (Hotmail), OneDrive, Xbox LIVE of Office 365. Deze identiteiten worden gemaakt en opgeslagen in Hallo Microsoft-account klantidentiteitssysteem uitgevoerd door Microsoft.|
|Werk-of schoolaccounts | Werk- of schoolaccount accounts (uitgegeven door een beheerder voor gebruik van zakelijke/academic) bieden toegang tooenterprise zakelijke Microsoft cloudservices, zoals Azure, Intune of Office 365.|


## <a name="concepts-toounderstand"></a>Concepten toounderstand

Nu dat u Hallo basic Azure identity voorwaarden weet, moet u meer informatie over deze Azure identity-concepten die u helpen een gefundeerde Azure identity-service-beslissing nemen.

|Concept toounderstand |Beschrijving|
|-----|-----|
|[Hoe Azure-abonnementen worden gekoppeld aan Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-how-subscriptions-associated-directory) |Elke Azure-abonnement heeft een vertrouwensrelatie met een Azure AD-directory tooauthenticate gebruikers, services en apparaten. *Meerdere abonnementen kunnen Hallo dezelfde Azure AD-directory vertrouwen, maar een abonnement vertrouwt slechts één Azure AD-directory*. Deze vertrouwensrelatie is in tegenstelling tot Hallo-relatie die een abonnement heeft met andere Azure-resources (websites, databases, enzovoort), die meer op onderliggende resources van een abonnement lijken. Als u een abonnement is verlopen, klikt u vervolgens toegang tooresources die zijn gekoppeld aan Hallo abonnement dan Azure AD ook geblokkeerd. Hello Azure AD-directory blijft echter in Azure, zodat u kunt een ander abonnement aan die directory koppelen en toomanage tenantbronnen blijven.|
|[Hoe Azure AD werkt licentieverlening](https://docs.microsoft.com/azure/active-directory/active-directory-licensing-get-started-azure-portal) | Wanneer u kopen of Enterprise Mobility Suite, Azure AD Premium of Azure AD Basic, uw directory activeren is bijgewerkt met Hallo abonnement, met inbegrip van de geldigheidsperiode en vooruitbetaald licenties. Zodra het Hallo-abonnement actief is, kunt u Hallo-service worden beheerd door globale beheerders van Azure AD en gebruikt door gebruikers met een licentie. Uw abonnementsgegevens, waaronder het aantal licenties toegewezen of beschikbaar Hallo is beschikbaar in Hallo hello Azure-portal **Azure Active Directory** > **licenties** blade. Dit wordt aanbevolen plaats toomanage ook Hallo uw toewijzen van licenties.|
|[Toegangsbeheer op basis van rollen in hello Azure-portal](https://docs.microsoft.com/azure/active-directory/role-based-access-control-what-is)|Azure op rollen gebaseerde toegangsbeheer (RBAC) biedt Geavanceerd toegangsbeheer voor Azure-resources. Te veel machtigingen kunnen weergeven en tooattackers-account. Te weinig machtigingen betekent dat werknemers hun werk efficiënt kunnen niet ophalen. Met RBAC kunt u kunt werknemers Hallo exacte machtigingen geven ze nodig hebben op basis van drie basic rollen die van toepassing tooall resourcegroepen: eigenaar, bijdrager, reader. U kunt er ook voor maken van too2, 000 van uw eigen [aangepaste RBAC-rollen](https://docs.microsoft.com/azure/active-directory/role-based-access-control-custom-roles) toomeet uw specifieke behoeften. |
|[Hybride identiteit](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect)|Hybride identiteit wordt bereikt door uw lokale Windows Server Active Directory (AD DS) te integreren met Azure AD via [Azure AD Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect). Hiermee kunt u een algemene identiteit voor uw gebruikers voor Office 365, Azure, en lokale apps of SaaS-toepassingen die zijn geïntegreerd met Azure AD tooprovide. Met hybride identiteit uitbreiden u effectief uw on-premises omgeving toohello cloud voor identiteits- en toegangsbeheer.|

### <a name="hello-difference-between-windows-server-ad-ds-and-azure-ad"></a>Hallo verschil tussen Windows Server AD DS en Azure AD
Zowel de Azure Active Directory (Azure AD) en de lokale Active Directory (Active Directory Domain Services of AD DS) zijn systemen die Active directory-gegevens opslaan en beheren van communicatie tussen gebruikers en bronnen, met inbegrip van gebruikersprocessen aanmelden, verificatie en zoekacties in Active directory.

Als u al bekend bent met lokale Windows Server Active Directory Domain Services (AD DS), het eerst geïntroduceerd in Windows 2000 Server en vervolgens u waarschijnlijk Hallo basisconcept een identity-service kent. Het is echter ook belangrijk toounderstand Azure AD is niet een domeincontroller in het Hallo-cloud. Het is een geheel nieuwe manier van het bieden van identiteit als een service (IDaaS) in Azure die u moet een geheel nieuwe manier om na te denken toofully integreren cloud-gebaseerde mogelijkheden en uw organisatie te beschermen tegen moderne bedreigingen. 

AD DS is een serverfunctie in Windows Server, wat betekent dat deze kan worden geïmplementeerd op fysieke of virtuele machines. Er is een hiërarchische structuur op basis van X.500. DNS wordt gebruikt voor het zoeken naar objecten, kunnen worden gecommuniceerd met het gebruik van LDAP en voornamelijk gebruikt Kerberos voor authenticatie. Active Directory kunnen organisatie-eenheden (OE's) en groepsbeleidsobjecten (GPO's) bovendien toojoining machines toohello domein en vertrouwensrelaties worden gemaakt tussen domeinen.

IT hun perimeter beveiliging voor het jaar met AD DS, maar moderne, perimeter minder ondernemingen ondersteunende identiteiten voor werknemers, klanten en partners, een nieuw besturingselement vlak moet heeft beveiligd. Azure AD is dit vlak identity-besturingselement. Beveiliging is gegaan dan Hallo bedrijfsfirewall toohello cloud waar Azure AD bedrijfsbronnen en -toegang beveiligt door een algemene identiteit bieden voor gebruikers (on-premises of in de cloud Hallo). Hiermee geeft u uw gebruikers Hallo flexibiliteit toosecurely toegang Hallo apps moeten tooget hun werk vanaf vrijwel elk apparaat. Naadloze risico gebaseerde beveiliging Gegevensbesturingselementen, ondersteund door de mogelijkheden van machine learning en gedetailleerde rapporten worden ook gegeven dat IT behoeften tookeep bedrijf gegevens veilig zijn.

Azure AD is een klant meerdere openbare adreslijstservice, wat betekent dat een tenant voor uw cloud-servers en toepassingen zoals Office 365 in Azure AD kunt maken. Gebruikers en groepen worden gemaakt in een platte structuur zonder OE's of GPO's. Verificatie wordt uitgevoerd via protocollen, zoals SAML, WS-Federation en OAuth. Het is mogelijk tooquery Azure AD, maar in plaats van LDAP moet u een REST-API aangeroepen AD Graph API. Deze werkt met alle via HTTP en HTTPS.

### <a name="extend-office-365-management-and-security-capabilities"></a>Mogelijkheden voor het beheer en beveiliging van Office 365 uitbreiden
Al gebruikmaakt van Office 365? U kunt uw digitale transformatie versnellen door uit te breiden ingebouwde mogelijkheden voor Office 365 met Azure AD-toosecure al uw resources beveiligde productiviteit inschakelen voor uw hele werknemers. Wanneer u Azure AD gebruikt, naast tooOffice 365 mogelijkheden, u kunt uw gehele toepassing portfolio beveiligen met één identiteit waarmee eenmalige aanmelding voor alle apps. U kunt de mogelijkheden van de voorwaardelijke toegang op basis niet alleen op de locatie van de status, maar de gebruiker, apparaat, toepassing en risico ook uitbreiden. Multi-factor authentication (MFA) mogelijkheden bieden nog meer beveiliging wanneer u deze nodig. U moet extra toezicht van de gebruiker heeft bevoegdheden krijgen en geef beheerderstoegang op aanvraag, just in time. Uw gebruikers productiever zijn en minder helpdesk-tickets maken, wordt met vriendelijke groet toohello selfservice mogelijkheden Azure AD biedt zoals opnieuw instellen van vergeten wachtwoorden, toegangsaanvragen van toepassingen, en groepen maken en beheren.

> [!TIP]
> Wilt u meer over het gebruik van Azure AD-identiteitsbeheer met Office 365 toolearn? [Hallo e-book ophalen](https://info.microsoft.com/Extend-Office-365-security-with-EMS.html).

## <a name="microsoft-azure-identity-solutions"></a>Microsoft Azure-identiteitsoplossingen

Microsoft Azure biedt verschillende manieren toomanage identiteit van uw gebruikers of ze worden bijgehouden volledig on-premises alleen Hallo cloud, of zelfs ergens ertussen. Deze opties zijn onder andere: doe (DIY) AD DS in Azure, Azure Active Directory (Azure AD), hybride identiteit en Azure AD Domain Services.

### <a name="do-it-yourself-diy-ad-ds"></a>Doe (ZELFOPLOSSING) AD DS
Voor bedrijven die slechts een kleine footprint in Hallo-cloud nodig **Doe (DIY) AD DS** kan worden gebruikt in Azure. Deze optie ondersteunt vele Windows Server AD DS-scenario's die geschikt zijn voor de implementatie van virtuele machines (VM's) in Azure zijn. U kunt bijvoorbeeld een virtuele machine van Azure maken als een domeincontroller in een veel datacenter dat extern netwerk verbonden toohello. Van daaruit zou Hallo VM kunnen toosupport worden verificatieaanvragen van externe gebruikers en verbeterde verificatieprestaties. Deze optie is ook geschikt als een relatief goedkope substitute toootherwise kostbare noodherstelsites die als host fungeert voor een klein aantal domeincontrollers en één virtueel netwerk in Azure. Ten slotte of u kunt mogelijk toodeploy een toepassing in Azure, zoals SharePoint, die Windows Server AD DS vereist, maar heeft geen afhankelijkheid op Hallo on-premises netwerk Hallo zakelijke Windows Server Active Directory. U kunt een geïsoleerd forest op Azure toomeet Hallo SharePoint-serverfarm van vereisten in dit geval kan implementeren. Het is ook ondersteund toodeploy netwerktoepassingen waarvoor verbinding toohello on-premises netwerk en Hallo on-premises Active Directory.

### <a name="azure-active-directory-azure-ad"></a>Azure Active Directory (Azure AD)
**Azure AD-zelfstandige** is een volledig cloud-gebaseerde identiteit en toegang te beheren als een Service (IDaaS). Azure AD biedt u een set krachtige mogelijkheden toomanage gebruikers en groepen. Het helpt beveiligde toegang tot tooon-premises en cloudtoepassingen, met inbegrip van Microsoft web-services zoals Office 365 en veel niet-Microsoft-software als een dienst (SaaS)-toepassingen. Azure AD wordt geleverd in drie versies: gratis, basis- en Premium. Azure AD verhoogt de efficiëntie en breidt beveiliging buiten Hallo perimeter firewall tooa nieuw besturingselement vlak die zijn beveiligd door Azure machine learning en andere geavanceerde beveiligingsfuncties.

### <a name="hybrid-identity"></a>Hybride identiteit
In plaats van kiezen tussen on-premises of cloud-gebaseerde identiteitsoplossingen, uitbreidt veel forward denken CIO's en bedrijven die anticiperen op lange termijn richting van hun bedrijf begonnen, hun on-premises mappen toohello cloud via **hybride identiteit** oplossingen. Met hybride identiteit, krijgt u een documentatieklanten werken wereldwijd, identiteit en toegang beheeroplossing die biedt veilige en productieve toegang toohello toepassingen gebruikers moet toodo hun werk.

> [!TIP]
> toolearn informatie over hoe CIO's Azure Active Directory hebt gemaakt centrale onderdeel van hun IT-strategieën downloaden Hallo [van CIO handleiding tooAzure Active Directory](https://aka.ms/AzureADCIOGuide).

### <a name="azure-ad-domain-services"></a>Azure AD Domain Services
**Azure AD Domain Services** voorziet in een cloud-gebaseerde optie toouse AD DS voor controle van lightweight Azure VM-configuratie en een toomeet manier identiteitsvereisten lokale netwerk toepassing ontwikkelen en testen. Azure AD Domain Services is niet bedoeld voor toolift en verplaatsen van uw on-premises AD DS-infrastructuur tooAzure virtuele machines worden beheerd door Azure AD Domain Services. In plaats daarvan moet hello Azure VM's in de beheerde domeinen gebruikte toosupport Hallo ontwikkelen, testen en verkeer van on-premises toepassingen die AD DS-verificatie methoden toohello cloud vereisen.

## <a name="common-scenarios-and-recommendations"></a>Algemene scenario's en aanbevelingen

Hier volgen enkele algemene identiteit en toegang scenario's met aanbevelingen toowhich Azure identiteitsoptie mogelijk meest geschikt is voor elk.

|Identiteitsscenario| Aanbeveling|
|-----|-----|
|Mijn organisatie grote investeringen in de lokale Windows Server Active Directory heeft gemaakt, maar we willen tooextend identiteit toohello cloud.| het meest gebruikt Hello Azure identiteitsoplossing is [hybride identiteit](https://docs.microsoft.com/azure/active-directory/active-directory-hybrid-identity-design-considerations-overview). Als u al investeringen in de lokale AD DS genomen hebt, kunt u eenvoudig de identiteit toohello cloud met Azure AD Connect uitbreiden.|
|Mijn bedrijf is in de cloud Hallo geboren en we hebben geen investeringen in oplossingen voor on-premises-identiteit.| [Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-whatis) is de beste keuze hello voor bedrijven cloudconfiguratie zonder lokale investeringen.|
|Ik heb nodig lightweight Azure VM-configuratie en controle toomeet lokale identiteitsvereisten voor app ontwikkelen en testen.|[Azure AD Domain Services](https://docs.microsoft.com/azure/active-directory-domain-services/active-directory-ds-overview) is een goede keuze als toouse AD DS voor lightweight Azure VM-configuratie-besturingselement moet of toodevelop zoekt of verouderd, van directory-bewuste lokale toepassingen toohello cloud migreren.|  
|Ik heb toosupport enkele virtuele machines in Azure nodig, maar mijn bedrijf is nog steeds sterk geïnvesteerd in de lokale Active Directory (AD DS).|Gebruik [ZELFOPLOSSING AD DS](https://msdn.microsoft.com/library/azure/jj156090.aspx) toouse Azure VM's wanneer u een paar virtuele machines voor toosupport nodig hebt en beschikt over grote AD DS-investeringen on-premises. |

## <a name="where-can-i-learn-more"></a>Waar vind ik meer informatie?
We hebben een berg geweldige bronnen online toohelp die u meer informatie over Azure AD. Hier volgt een lijst met artikelen geweldige tooget die u gestart:

* [De map voor het beheer van hybride met Azure AD Connect inschakelen](active-directory-aadconnect.md)
* [Extra beveiliging voor een ooit verbonden wereld](../multi-factor-authentication/multi-factor-authentication.md)
* [Automatisch gebruikers inrichten en Deprovisioning tooSaaS toepassingen met Azure Active Directory](active-directory-saas-app-provisioning.md)
* [Aan de slag met Azure AD-rapportage](active-directory-reporting-getting-started.md)
* [De wachtwoorden beheren vanaf elke locatie](active-directory-passwords.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)
* [Automatisch gebruikers inrichten en Deprovisioning tooSaaS toepassingen met Azure Active Directory](active-directory-saas-app-provisioning.md)
* [Hoe tooprovide veilige externe toegang tot het tooon-premises toepassingen](active-directory-application-proxy-get-started.md)
* [Tooresources toegang beheren met Azure Active Directory-groepen](active-directory-manage-groups.md)
* [Wat is Microsoft Azure Active Directory-licentieverlening?](active-directory-licensing-what-is.md)
* [Hoe kan ik cloudapps die worden gebruikt in mijn organisatie detecteren](active-directory-cloudappdiscovery-whatis.md)

## <a name="next-steps"></a>Volgende stappen

Nu dat u Azure identity-concepten en Hallo opties beschikbaar tooyou begrijpt, kunt u Hallo resources tooget gestart geïmplementeerd Hallo optie die u hebt gekozen te volgen:

[Meer informatie over hybride Azure-identiteitsoplossingen](https://docs.microsoft.com/azure/active-directory/choose-hybrid-identity-solution)

[Meer informatie in een omgeving met Azure Proof-of-Concept](https://aka.ms/aad-poc)

[Azure AD in de productieomgeving implementeren](https://aka.ms/aad-onboard)
