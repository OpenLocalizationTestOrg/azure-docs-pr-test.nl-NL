---
title: aaaWhat is Selfserviceregistratie voor Azure? | Microsoft Docs
description: Een overzicht van toepassing met selfserviceregistratie voor Azure, hoe toomanage Hallo aanmeldproces en hoe tootake via een DNS-domeinnaam.
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: b9f01876-29d1-4ab8-8b74-04d43d532f4b
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/08/2017
ms.author: curtand
ms.openlocfilehash: dbf3b59e3807e98f7bf39f3d5591fcde01667323
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-self-service-signup-for-azure"></a>Wat is Selfserviceregistratie voor Azure?
Dit onderwerp wordt uitgelegd Hallo selfservice aanmeldproces en hoe tootake via een DNS-domeinnaam.  

## <a name="why-use-self-service-signup"></a>Waarom toepassing met selfserviceregistratie gebruiken?
* Get klanten tooservices die ze sneller willen.
* Maak aanbiedingen voor een service op basis van e-mail.
* Aanmelding op basis van e-stromen die snel kunnen gebruikers met hun werk gemakkelijk te onthouden e-aliassen toocreate-identiteiten maken.
* Niet-beheerde Azure mappen kunnen later in beheerde mappen worden gemaakt en opnieuw worden gebruikt voor andere services.

## <a name="terms-and-definitions"></a>Termen en definities
* **Selfserviceaanmelding**: dit Hallo methode waarmee een gebruiker zich aanmeldt voor een cloudservice en heeft een identiteit voor ze in Azure Active Directory (Azure AD) automatisch gemaakt op basis van hun e-maildomein is.
* **Niet-beheerde Azure-map**: dit is Hallo directory waar die identiteit is gemaakt. Een niet-beheerde map is een map die geen globale beheerder heeft.
* **E-mailbericht geverifieerde gebruiker**: dit is een type gebruikersaccount in Azure AD. Een gebruiker met een automatisch gemaakt na het aanmelden voor een aanbieding selfservice identiteit staat bekend als een gebruiker met e-mailadres gecontroleerd. Een e-mailbericht geverifieerde gebruiker reguliere lid is van een map die is gemarkeerd met creationmethod = EmailVerified.

## <a name="user-experience"></a>Gebruikerservaring
Bijvoorbeeld, Stel dat een gebruiker waarvan e-mail is Dan@BellowsCollege.com vertrouwelijke bestanden via e-mail ontvangt. Hallo-bestanden zijn beveiligd door Azure Rights Management (Azure RMS). Maar Dan de organisatie, balg universiteit bent, is niet aangemeld voor Azure RMS of heeft deze Active Directory RMS geïmplementeerd. In dit geval, kunt Dan aanmelden voor een gratis abonnement tooRMS voor personen in volgorde tooread Hallo beveiligde bestanden.

Als Dan de eerste gebruiker Hallo met een e-mailadres van BellowsCollege.com toosign voor deze aanbieding self-service is, klikt u vervolgens een niet-beheerde map wordt gemaakt voor BellowsCollege.com in Azure AD. Als andere gebruikers van Hallo BellowsCollege.com domein zich registreert voor deze aanbieding of een vergelijkbare selfservice aanbieding, e-mailadres gecontroleerd gebruikersaccounts die zijn gemaakt in Hallo dezelfde zonder begeleiding ook hebben map in Azure.

## <a name="admin-experience"></a>Ervaring beheerder
Een beheerder die eigenaar is van Hallo DNS-domeinnaam van een niet-beheerde Azure-map kan overnemen of samenvoegen Hallo directory na het eigendom aan te tonen. Hallo volgende secties wordt de ervaring Hallo beheerder in meer detail uitgelegd, maar hier volgt een samenvatting:

* Wanneer u een niet-beheerde Azure-map overneemt, zijn u simpelweg Hallo globale beheerder van de niet-beheerde map Hallo. Dit wordt soms een interne overname genoemd.
* Wanneer u een niet-beheerde Azure-map samenvoegt, u Hallo DNS-domeinnaam van Hallo onbeheerde directory tooyour beheerde Azure-map toevoegen en een toewijzing van gebruikers voor resources is gemaakt zodat gebruikers kunnen blijven tooaccess services zonder onderbreking. Dit wordt soms een externe overname genoemd.

## <a name="what-gets-created-in-azure-active-directory"></a>Wat wordt gemaakt in Azure Active Directory?
#### <a name="directory"></a>Directory
* Een Azure Active Directory-map voor Hallo domein wordt gemaakt, één map per domein.
* Hello Azure AD-directory heeft geen globale beheerder.

#### <a name="users"></a>Gebruikers
* Voor elke gebruiker die zich aanmeldt, wordt een gebruikersobject gemaakt in hello Azure AD-directory.
* Elk gebruikersobject is gemarkeerd als extern.
* Elke gebruiker krijgt toegang tot toohello service die zij zich heeft aangemeld.

### <a name="how-do-i-claim-a-self-service-azure-ad-directory-for-a-domain-i-own"></a>Hoe claim een selfservice Azure AD voor een domein dat ik eigen map?
U kunt een Azure AD met selfservice claim map door het valideren van het domein. Domeinvalidatie bewijst eigen Hallo domein door het maken van DNS-records.

Er zijn twee manieren toodo een DNS-overname van een Azure Active directory:

* interne overname (Admin detecteert een niet-beheerde Azure-map, en wil tooturn in een beheerde map)
* externe overname (Admin probeert tooadd een nieuw domein tootheir beheerde Azure-map)

U mogelijk geïnteresseerd in het valideren van een domein te eigenaar, omdat u via een niet-beheerde directory onderneemt nadat een gebruiker de toepassing met selfserviceregistratie uitgevoerd, of u wilt een nieuw domein tooan bestaande beheerde map toevoegen. Bijvoorbeeld, hebt u een domein met de naam contoso.com en u wilt dat een nieuw domein met de naam contoso.co.uk of contoso.uk tooadd.

## <a name="what-is-domain-takeover"></a>Wat is de overname van domein?
Deze sectie bevat informatie over hoe toovalidate eigenaar van een domein

### <a name="what-is-domain-validation-and-why-is-it-used"></a>Wat is de domeinvalidatie van het en waarom is het gebruikt?
In de volgorde tooperform bewerkingen op een map vereist Azure AD dat u het eigendom van Hallo DNS-domein valideren.  Validatie van Hallo domein kunt u tooclaim Hallo directory en een promoveren Hallo selfservice directory tooa beheerde map of merge Hallo selfservice directory naar een bestaande directory beheerd.

## <a name="examples-of-domain-validation"></a>Voorbeelden validatie van het domein
Er zijn twee manieren toodo een DNS-overname van een map:

* interne overname (bijvoorbeeld een beheerder een selfservice, niet-beheerde adreslijst detecteert, en wil tooturn in beheerde map)
* externe overname (bijvoorbeeld een beheerder een nieuwe beheerde map van de domein-tooa tooadd probeert)

### <a name="internal-takeover---promote-a-self-service-unmanaged-directory-toobe-a-managed-directory"></a>Interne overname - promoveren van een selfservice, niet-beheerde directory toobe beheerde map
Als u interne overname doet, opgehaald uit een niet-beheerde directory tooa beheerde directory Hallo directory geconverteerd. U moet toocomplete DNS-domeinvalidatie van de naam, waarin u een MX-record of een TXT-record in Hallo DNS-zone maken. Deze actie:

* Valideert dat u Hallo-domein bezit
* Hallo directory beheerd maakt
* Zorgt ervoor dat u een globale beheerder van de map Hallo Hallo

Stel dat een IT-beheerder van balg school detecteert dat gebruikers van Hallo school hebt aangemeld voor self-service aanbiedingen. Hallo geregistreerde eigenaar van Hallo DNS-naam BellowsCollege.com, Hallo IT-beheerder kunt valideren van de eigenaar van Hallo DNS-naam in Azure en vervolgens overnemen Hallo onbeheerde directory. Hallo directory wordt vervolgens een beheerde map en hello IT-beheerder is toegewezen Hallo globale beheerdersrol voor Hallo BellowsCollege.com directory.

### <a name="external-takeover---merge-a-self-service-directory-into-an-existing-managed-directory"></a>Externe overname - een map Self-service samenvoegen met een bestaande beheerde map
In een externe overname, hebt u al een beheerde map en u wilt dat alle gebruikers en groepen van een niet-beheerde directory toojoin die directory worden beheerd, in plaats eigen twee afzonderlijke mappen.

Als een beheerder van een beheerde map toevoegen van een domein en dat domein gebeurt toohave een niet-beheerde directory gekoppeld.

Stel dat bijvoorbeeld u een IT-beheerder bent en u hebt al een beheerde map voor Contoso.com, een domeinnaam die is geregistreerd tooyour organisatie. U ontdekt die gebruikers van uw organisatie hebt uitgevoerd selfservice sign up voor een aanbieding met behulp van e-domeinnaam user@contoso.co.uk, dit is een andere domeinnaam die uw organisatie eigenaar is. Deze gebruikers hebben momenteel accounts in een niet-beheerde map voor contoso.co.uk.

U wilt niet toomanage twee afzonderlijke mappen, zodat u de niet-beheerde map Hallo voor contoso.co.uk in uw bestaande directory IT beheerd voor contoso.com samenvoegen.

Externe overname volgt Hallo dezelfde DNS-validatieproces als interne overname.  Om het verschil: gebruikers en services zijn opnieuw toegewezen toohello IT beheerde map.

#### <a name="whats-hello-impact-of-performing-an-external-takeover"></a>Wat is de invloed van de uitvoering van een externe overname Hallo?
Met een externe overname een toewijzing van gebruikers naar resources gemaakt zodat gebruikers tooaccess services zonder onderbreking kunnen doorgaan. Veel toepassingen, waaronder RMS voor personen, verwerken Hallo toewijzing van gebruikers aan bronnen goed en kunnen gebruikers blijven tooaccess die services zonder wijzigingen. Als een toepassing hello toewijzing van gebruikers aan bronnen niet effectief verwerkt, is externe overname mogelijk expliciet geblokkeerde tooprevent gebruikers van een slechte ervaring.

#### <a name="directory-takeover-support-by-service"></a>Directory overname ondersteuning door service
Momenteel Hallo services ondersteuning overname te volgen:

* RMS

Hallo na services wordt binnenkort overname ondersteund:

* PowerBI

Hallo hieronder niet en vereisen aanvullende admin actie toomigrate gebruikersgegevens na een externe overname.

* SharePoint/OneDrive

## <a name="how-tooperform-a-dns-domain-name-takeover"></a>Hoe een DNS-domein tooperform overname naam
U hebt een aantal opties voor het tooperform de domeinvalidatie van een (en een overname doen als u wenst):

1. Azure Management Portal

   Een overname wordt geactiveerd als volgt de toevoeging van een domein.  Als er al een map voor Hallo domein bestaat, hebt u Hallo optie tooperform een externe overname.

   Meld u aan toohello Azure-portal met uw referenties.  Tooyour bestaande map te navigeren en vervolgens te**domein toevoegen**.
2. Office 365

   U kunt Hallo-opties op Hallo [domeinen beheren](https://support.office.com/article/Navigate-to-the-Office-365-Manage-domains-page-026af1f2-0e6d-4f2d-9b33-fd147420fac2/) pagina in Office 365 toowork met uw domeinen en DNS-records. Zie [Verifieer uw domein in Office 365](https://support.office.com/article/Verify-your-domain-in-Office-365-6383f56d-3d09-4dcb-9b41-b5f5a5efd611/).
3. Windows Powershell

   Hallo stappen zijn vereist tooperform een validatie met behulp van Windows PowerShell.

   | Stap | Cmdlet toouse |
   | --- | --- |
   | Een referentieobject maken |Get-Credential |
   | Verbinding maken met tooAzure AD |Connect-MsolService |
   | een lijst met domeinen |Get-MsolDomain |
   | Een vraag maken |Get-MsolDomainVerificationDns |
   | DNS-record maken |Dit doen op de DNS-server |
   | Hallo uitdaging controleren |Confirm-MsolEmailVerifiedDomain |

Bijvoorbeeld:

1. Verbinding maken met tooAzure AD met Hallo-referenties die gebruikt toorespond toohello selfservice aanbieding werden:

        import-module MSOnline
        $msolcred = get-credential
        connect-msolservice -credential $msolcred
2. Haal een lijst met domeinen:

    Get-MsolDomain
3. Voer Hallo Get MsolDomainVerificationDns cmdlet toocreate een challenge:

    Get-MsolDomainVerificationDns – DomainName *your_domain_name* – modus DnsTxtRecord

    Bijvoorbeeld:

    Get-MsolDomainVerificationDns – domeinnaam contoso.com – modus DnsTxtRecord
4. Kopieer Hallo-waarde (Hallo challenge) die wordt geretourneerd door deze opdracht.

    Bijvoorbeeld:

    MS 32DD01B82C05D27151EA9AE93C5890787F0E65D9 =
5. Maak een DNS txt-record met Hallo-waarde die u in de vorige stap Hallo gekopieerd in uw openbare DNS-naamruimte.

    Hallo naam voor deze record is Hallo naam van Hallo bovenliggende domein, dus als u deze bronrecord maakt met behulp van DNS-serverfunctie Hallo van Windows Server, de recordnaam Hallo leeg laten en alleen Hallo-waarde in het tekstvak Hallo plakken
6. Hallo bevestigen MsolDomain cmdlet tooverify Hallo uitdaging uitvoeren:

    Bevestig MsolEmailVerifiedDomain - DomainName *your_domain_name*

    Bijvoorbeeld:

    Bevestig MsolEmailVerifiedDomain - domeinnaam contoso.com

Een geslaagde uitdaging retourneert toohello prompt zonder fouten.

## <a name="how-do-i-control-self-service-settings"></a>Hoe bepaal ik selfservice-instellingen
Beheerders hebben twee selfservice besturingselementen vandaag. Ze kunnen bepalen:

* Of gebruikers lid worden Hallo directory via e-mail.
* Gebruikers kunnen de zelf of licentie voor toepassingen en services.

### <a name="how-can-i-control-these-capabilities"></a>Hoe kan ik deze mogelijkheden bepalen?
Een beheerder kan deze mogelijkheden gebruik van deze parameters van de cmdlet Set-MsolCompanySettings Azure AD configureren:

* **AllowEmailVerifiedUsers** bepaalt of een gebruiker kunt maken of koppelen van een niet-beheerde directory. Als u deze parameter instelt te$ false, niet door de e-mailadres gecontroleerd kunnen gebruikers lid worden Hallo-directory.
* **AllowAdHocSubscriptions** regelt Hallo mogelijkheid voor gebruikers die Self-service tooperform aanmelden. Als u deze parameter te instelt $ONWAAR is, er zijn geen gebruikers kunnen uitvoeren toepassing met selfserviceregistratie.

### <a name="how-do-hello-controls-work-together"></a>Hoe werken Hallo besturingselementen samen?
Deze twee parameters kunnen worden gebruikt in combinatie toodefine meer controle over self-service aanmelden. Bijvoorbeeld, Hallo na de opdracht kan gebruikers tooperform selfserviceaanmelding, maar alleen als deze gebruikers al een account in Azure AD hebben (met andere woorden, gebruikers hoeven een e-mailadres gecontroleerd account toobe gemaakt kunnen niet worden uitgevoerd selfservice sign up):

    Set-MsolCompanySettings -AllowEmailVerifiedUsers $false -AllowAdHocSubscriptions $true

Hallo volgende stroomdiagram wordt uitgelegd alle Hallo verschillende combinaties voor deze parameters en de resulterende voorwaarden Hallo voor Hallo directory en de selfserviceaanmelding.

![][1]

Voor meer informatie en voorbeelden van hoe toouse deze parameters zien [Set-MsolCompanySettings](/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0).

## <a name="see-also"></a>Zie ook
* [Hoe tooinstall Azure PowerShell en configureren](/powershell/azure/overview)
* [Azure PowerShell](/powershell/azure/overview)
* [Azure-cmdlet-naslaginformatie](/powershell/azure/get-started-azureps)
* [Set-MsolCompanySettings](/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0)

<!--Image references-->
[1]: ./media/active-directory-self-service-signup/SelfServiceSignUpControls.png
