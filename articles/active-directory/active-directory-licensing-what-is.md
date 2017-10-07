---
title: aaaLicense Azure Active Directory-gebruikers in de klassieke Azure-portal Hallo | Microsoft Docs
description: Beschrijving van Microsoft Azure Active Directory-licentieverlening, hoe het werkt, hoe tooget gestart en beste praktijken, zoals Office 365, Microsoft Intune en Azure Active Directory Premium en Basic-edities
services: active-directory
keywords: Azure AD-licentieverlening
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: d769e8c6-7581-43f5-a3b4-de4b1dca2344
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/24/2017
ms.author: curtand
ms.custom: oldportal;it-pro;H1Hack27Feb2017
ms.openlocfilehash: 4d5f244cbee2ae37a30976f70b5d4f21c3516d90
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-microsoft-azure-active-directory-licensing-in-hello-azure-classic-portal"></a>Wat is Microsoft Azure Active Directory-licentieverlening in Hallo klassieke Azure-portal?

> [!div class="op_single_selector"]
> * [Instructies voor Azure portal](active-directory-licensing-get-started-azure-portal.md)
> * [Azure classic portal info](active-directory-licensing-what-is.md)
>
>

Azure Active Directory (Azure AD) van Microsoft Identity is als een Service (IDaaS)-oplossing en platform. Azure AD wordt aangeboden in een aantal technische en functionele versies, variërend van Azure AD-vrij, zodat de is beschikbaar bij alle Microsoft-services zoals Office 365, Dynamics, Microsoft Intune en Azure (Azure AD genereert geen eventuele kosten verbruik in deze modus), tooAzure AD betaald versies zoals Enterprise Mobility Suite (EMS), Azure AD Premium en Basic, evenals Azure multi-factor Authentication (MFA). De meeste Azure AD betaald versies worden geleverd via een per gebruiker rechten net als veel van Microsoft online services, zoals in Office 365, Microsoft Intune en Azure AD. In dergelijke gevallen Hallo service aankoop wordt aangegeven door een of meer abonnementen en elk abonnement bevat een vooraf aankoop aantal licenties in uw tenant. Rechten per gebruiker worden bereikt via de licentietoewijzing, het maken van een koppeling tussen Hallo gebruiker en Hallo-product, Hallo serviceonderdelen voor Hallo gebruiker inschakelen en gebruiken van een van de Hallo vooruitbetaald licenties.

> [!IMPORTANT]
> Microsoft raadt aan dat u Azure AD beheren met Hallo [Azure AD-beheercentrum](https://aad.portal.azure.com) in Hallo hello Azure-portal in plaats van de klassieke Azure-portal waarnaar wordt verwezen in dit artikel. Zie voor hoe tooassign beheerdersrollen in Azure AD Hallo beheerder centreren, [licentie uzelf en uw gebruikers in Azure AD](active-directory-licensing-get-started-azure-portal.md).

[Probeer Azure AD premium nu.](https://portal.office.com/Signup/Signup.aspx?OfferId=01824d11-5ad8-447f-8523-666b0848b381&ali=1#0)

> [!NOTE]
> Azure AD-beheerportal is een onderdeel van Hallo klassieke Azure-portal. Terwijl u met behulp van Azure AD, hoeft niet alle Azure aankopen, toegang tot deze portal moet een actief Azure-abonnement of een [Azure-proefabonnement](https://azure.microsoft.com/pricing/free-trial/).
>
>

Zie voor een breed overzicht van Azure AD-servicefuncties [wat is Azure AD](active-directory-whatis.md).
[Meer informatie over Azure AD-serviceniveaus](https://azure.microsoft.com/support/legal/sla/)

> [!NOTE]
> Azure omslagstelsel abonnementen zijn verschillend:, terwijl ook weergegeven in uw directory, deze abonnementen maken van een Azure-resources en deze betalingsmethode tooyour toewijzen. In dit geval zijn er geen licentieaantallen Hallo-abonnement gekoppeld. Koppeling van de gebruikers met Hallo abonnement, Hallo gebruikers toegang tot toomanaging abonnement bronnen wordt bereikt door het verlenen van machtigingen toooperate op Azure-resources toegewezen toohello abonnement.
>
>

## <a name="how-does-azure-ad-licensing-work"></a>Hoe Azure AD werkt licentieverlening?
Azure AD (recht gebaseerd) op basis van een licentie services werk door een abonnement in uw Azure AD-directory-service-tenant activeren. Zodra het Hallo-abonnement actief is worden Hallo servicefuncties beheerd door beheerders van directory-service en die wordt gebruikt door gebruikers met een licentie.

Wanneer u kopen of Enterprise Mobility Suite, Azure AD Premium of Azure AD Basic, uw directory activeren is bijgewerkt met Hallo abonnement, met inbegrip van de geldigheidsperiode en vooruitbetaald licenties. Uw abonnementsgegevens waaronder status, volgende lifecycle gebeurtenis en Hallo aantal licenties toegewezen of beschikbaar is beschikbaar via de klassieke Azure-portal op Hallo licenties tabblad voor de specifieke map Hallo Hallo. Dit is ook toobest plaats toomanage uw toewijzen van licenties.

Elk abonnement bestaat uit een of meer service-abonnementen, elke toewijzing Hallo opgenomen functionaliteitsniveau van het type van de service Hallo; bijvoorbeeld: Azure AD, Azure MFA, Microsoft Intune, Exchange Online of SharePoint Online. Azure AD-Licentiebeheer vereist geen serviceniveaubeheer plan. Dit wijkt af van Office 365 die afhankelijk van deze geavanceerde configuratie modus toomanage toegang tooincluded services is. Azure AD is afhankelijk van in de serviceconfiguratie, tooenable functies en afzonderlijke machtigingen beheren.

In het algemeen wordt Azure AD-abonnementsgegevens beheerd via de klassieke Azure-portal op Hallo licenties tabblad voor de specifieke map Hallo Hallo. Azure AD-abonnementen, met uitzondering van Azure AD Premium Hallo worden niet weergegeven in Hallo Office-portal.

> [!IMPORTANT]
> Azure AD Premium en Basic zijn beperkt tootheir ingericht directory/tenant-en Enterprise Mobility Suite-abonnementen. Abonnementen kunnen niet worden gesplitst tussen voltooiing mappen of gebruikte tooentitle gebruikers in andere directory's. Een abonnement verplaatsen tussen mappen is mogelijk, maar vereist het verzenden van een ondersteuningsticket of annuleren en opnieuw in geval van directe aankopen Hallo kopen.
>
> Bij de aanschaf van Azure AD of Enterprise Mobility Suite via Volume Licensing abonnement activering gebeurt automatisch wanneer Hallo overeenkomst bevat andere Microsoft Online services, zoals Office 365.
>
>

Azure AD-functies betaald span Hallo breedte van de directory Hallo. Voorbeelden zijn:

* Toewijzing op basis van een groep tooapplications, die is ingeschakeld onder Hallo specifieke toepassing die u beheert.
* Geavanceerde en mogelijkheden voor groepsbeheer met Self-service zijn beschikbaar binnen Hallo specifieke groep of onder Hallo directory-configuratie.
* Premium-beveiligingsrapporten zijn op het tabblad Hallo-rapportage
* Detectie van cloud-toepassing wordt weergegeven in hello Azure-portal onder identiteit.

### <a name="assigning-licenses"></a>Licenties toewijzen
Tijdens het verkrijgen van een abonnement dat alle moeten tooconfigure betaald mogelijkheden is, vereist met behulp van uw Azure AD betaalde functies voor het distribueren van licenties toohello juiste personen. In het algemeen moet dat elke gebruiker die toegang tooor die wordt beheerd via een Azure AD betaald functie moet een licentie worden toegewezen. De licentietoewijzing van een is geen toewijzing tussen een gebruiker en een gekochte service, zoals Azure AD Premium of Basic of Enterprise Mobility Suite.

Beheren welke gebruikers in uw directory moeten beschikken over een licentie is eenvoudig. Worden kan bereikt door toe te wijzen tooa groep toocreate toewijzingsregels via hello Azure AD-beheerportal of door het toewijzen van licenties rechtstreeks toohello juiste personen via een portal, PowerShell of API's. Bij het toewijzen van licenties tooa groep, wordt alle groepsleden een licentie toegewezen. Als gebruikers worden toegevoegd of verwijderd uit groep Hallo worden ze de juiste licentie Hallo toegewezen of verwijderd. Groepstoewijzing kan gebruikmaken van elke groep management beschikbaar tooyou en consistent is met toewijzing op basis van een groep tooapplications. Met deze benadering kunt u instellen van regels zodanig dat alle gebruikers in uw directory worden automatisch toegewezen of zelfs delegeren Hallo besluit tooother managers in Hallo organisatie, zorg ervoor dat iedereen met de juiste functie Hallo een licentie heeft.

Bij licentietoewijzing op basis van een groep neemt elke gebruiker ontbreekt een gebruikslocatie Hallo maplocatie tijdens de toewijzing. Deze locatie kan worden gewijzigd door Hallo beheerder op elk gewenst moment. In gevallen waarbij Hallo automatische toewijzing is mislukt vanwege het tooerror, Hallo gebruikersgegevens onder licentietype geeft die status.

## <a name="getting-started-with-azure-ad-licensing"></a>Aan de slag met Azure AD-licentieverlening
Aan de slag met Azure AD is eenvoudig; u kunt altijd uw directory als onderdeel van het aanmelden tooa gratis proefversie van Azure maken. [Meer informatie over het aanmelden als een organisatie](sign-up-organization.md). de volgende Hallo kunt u ervoor zorgen dat uw directory beste wordt uitgelijnd met andere Microsoft-services kan worden verbruikt of u van plan bent tooconsume en uw doelstellingen te verkrijgen Hallo-service.

Hier volgen enkele aanbevolen procedures:

* Als u al van een van de organisatie-services van Microsoft gebruikmaakt, hebt u al een Azure Active directory. In dit geval moet u blijven toouse Hallo dezelfde directory voor andere services, zodat de identiteitsbeheer core, zoals inrichting en hybride SSO, kan worden gebruikt op Hallo-services. Uw gebruikers een ervaring voor eenmalige aanmelding zijn, en profiteert van mogelijkheden op Hallo-services. Als gevolg hiervan, als u toobuy een Azure AD-service voor uw werknemers betaald besluit, raden wij aan dat u dezelfde directory toodo Hallo dit.
* Als u van plan bent toouse Azure AD voor een andere set gebruikers (partners, klanten, enzovoort), of als u wilt dat tooevaluate Azure AD-services en toodo wilt die in de isolatie van uw productieservice, of als u op zoek bent toosetup een sandbox-omgeving voor uw services, wordt u aangeraden eerst een nieuwe map via de klassieke Azure-Azure-portal hello te maken. [Meer informatie over het maken van een nieuwe Azure AD-directory in de klassieke Azure-portal Hallo](active-directory-licensing-directory-independence.md). Hallo nieuwe map wordt gemaakt met uw account als een externe gebruiker met globale beheerdersmachtigingen. Wanneer u zich aanmeldt toohello klassieke Azure portal met dit account u toosee kunnen deze map en toegang tot alle directorybeheertaken. U wordt aangeraden dat u een lokaal account maken met de juiste bevoegdheden toomanage andere Microsoft-services (die niet toegankelijk via de klassieke Azure-portal Hallo). [Meer informatie over het maken van gebruikersaccounts in Azure AD](active-directory-create-users.md).

> [!NOTE]
> Azure AD biedt ondersteuning voor 'externe gebruikers', wat gebruikersaccounts zijn in een exemplaar van Azure AD die zijn gemaakt met een Microsoft-Account (MSA) of een Azure AD-identiteit van een andere map. Terwijl we bezig zijn worden uitbreiden deze mogelijkheid in alle van de organisatie-services van Microsoft, nu deze accounts niet ondersteund in een aantal Hallo services ervaringen; bijvoorbeeld, ondersteunt Hallo Office 365-beheerportal momenteel geen deze gebruikers. Als gevolg hiervan externe gebruikers met een Microsoft-accounts worden niet kunnen tooaccess Hallo Office 365-beheerportal, terwijl externe gebruikers van andere Azure AD-directory's worden genegeerd. In het laatste geval hello, enige Hallo-gebruiker-lokale account, hello Azure AD of Office 365 zou de directory waarin de gebruiker Hallo oorspronkelijk is gemaakt, zijn toegankelijk via deze.
>
>

Zoals wordt aangegeven, heeft Azure AD een verschillende betaald versies. Deze versies hebben een aantal kleine verschillen in hun beschikbaarheid aankoop:

| Product | EA/VOLUMELICENTIES | Open | CSP | MPN gebruiksrechten | Rechtstreekse aankoop | Proefversie |
| --- | --- | --- | --- | --- | --- | --- |
| Enterprise Mobility Suite |X |X |X |X | |X |
| Azure AD Premium |X |X |X | |X |X |
| Azure AD Basic |X |X |X |X |<br /> |<br /> |

### <a name="select-one-or-more-license-trials"></a>Selecteer een of meer licentie-experimenten
 In alle gevallen kunt u een Azure AD Premium of Enterprise Mobility Suite-proefabonnement activeren door het selecteren van specifieke Hallo-proefversie die op het gewenste tab Hallo-licenties in uw directory. De evaluatieversie bevat een 30-daagse abonnement met 100 licenties.

![Azure Active Directory proeflicentie plannen](./media/active-directory-licensing-what-is/trial_plans.png)

![Enterprise Mobility Suite proeflicentie plannen](./media/active-directory-licensing-what-is/EMS_trial_plan.png)

![Actieve proeflicentie plannen](./media/active-directory-licensing-what-is/active_license_trials.png)

### <a name="assign-licenses"></a>Licenties toewijzen
Zodra het Hallo-abonnement actief is, moet u een tooyourself licentie toewijzen en vernieuw Hallo browser tooensure ziet u alle functies. Hallo volgende stap is tooassign licenties toohello gebruikers die tooaccess moet of worden opgenomen in betaalde Azure AD-functies. Zoals we hierboven vermeld in "toewijzen licenties,' Hallo aanbevolen manier toodo dit is tooidentify Hallo groep Hallo gewenst doelgroep die vertegenwoordigt en toe te wijzen toohello licentie; op deze manier kunnen gebruikers die zijn toegevoegd of verwijderd uit groep Hallo gedurende de levenscyclus tooor verwijderd uit het Hallo-licentie toegewezen.

een licentiegroep tooa tooassign of individuele gebruikers, selecteer licentieabonnement u wilt tooassign en klikt u op Hallo **toewijzen** op Hallo opdrachtbalk klikken.

![Actieve proeflicentie plannen](./media/active-directory-licensing-what-is/assign_licenses.png)

Wanneer in Hallo toewijzing dialoogvenster voor het geselecteerde abonnement hello, kunt u gebruikers en ze toe te voegen toohello **toewijzen** kolom op Hallo rechts. U kunt via de gebruikerslijst Hallo pagina of zoeken naar specifieke personen met Hallo opzoeken glas op Hallo top rechts van Hallo gebruiker raster. tooassign-groepen selecteren 'Groepen' hello **weergeven** menu en klik vervolgens op het selectievakje Hallo op Hallo rechts toorefresh Hallo toewijzingen die worden weergegeven.

![Toewijzen van licenties toogroups](./media/active-directory-licensing-what-is/assign_licenses_to_groups.png)

U kunt nu zoeken of pagina via groepen en toevoegen toohello **toewijzen** kolom in Hallo dezelfde manier. U kunt deze tooassign een combinatie van gebruikers en groepen in één bewerking. toocomplete toewijzingsproces hello, klikt u op Hallo selectievakje in Hallo rechterbenedenhoek van Hallo pagina.

![Licentie toewijzing voortgangsbericht](./media/active-directory-licensing-what-is/license_assignment_progress_message.png)

Wanneer een groep wordt toegewezen, overgenomen leden Hallo licenties binnen 30 minuten, maar meestal binnen 1-2 minuten.

Toewijzingsfouten kunnen optreden tijdens de licentietoewijzing van Azure AD, maar zijn relatief zeldzame. Mogelijke toewijzingsfouten zijn beperkt tot:

* Toewijzing conflict - wanneer een gebruiker een licentie die niet compatibel is met de huidige licentie Hallo was toegewezen. In dit geval moeten Hallo nieuwe licentie toewijzen Hallo vorige verwijderen.
* Beschikbare licenties overschreden - wanneer het aantal gebruikers in de toegewezen groepen Hallo beschikbare licenties overschrijden toewijzingsstatus Hallo gebruikers bevatten een tooassign is mislukt vanwege toomissing licenties.

### <a name="view-assigned-licenses"></a>Weergave toegewezen licenties
Een samenvatting weergegeven van de toegewezen licenties beschikbaar, toegewezen en volgende abonnement lifecycle gebeurtenis inclusief worden weergegeven op Hallo **licenties** tabblad.

![Weergave Hallo aantal toegewezen licenties](./media/active-directory-licensing-what-is/view_assigned_licenses.png)

Een gedetailleerde lijst met toegewezen gebruikers en groepen, inclusief de status van toewijzing en het pad (direct of overgenomen uit een of meer groepen) is beschikbaar bij het navigeren naar de planning van een licentie.

![Gegevens weergeven van licenties voor een licentieabonnement worden toegewezen](./media/active-directory-licensing-what-is/assigned_licenses_detail.png)

Het is net zo eenvoudig als het eraan toe te wijzen om licenties te verwijderen. Als gebruiker Hallo direct wordt toegewezen of voor een toegewezen groep, u Hallo-licentie verwijderen kunt door Hallo licentietype, selecteer **verwijderen**Hallo gebruiker of groep toohello verwijderen lijst toe te voegen en Hallo actie te bevestigen. U kunt ook kunt u openen een licentietype, selecteer Hallo specifieke gebruiker of groep, en tik op **verwijderen** op Hallo opdrachtbalk klikken. tooend hello gebruiker van een gebruiker overnemen van een licentie uit een groep gewoon verwijderen uit Hallo-groep.

### <a name="extending-trials"></a>Proefversies uitbreiden
Evaluatieversie uitbreidingen voor klanten zijn beschikbaar als selfservice via Hallo Office 365-portal. Een beheerder van de klant kunt navigeren toohello [Office-portal](https://portal.office.com/#Billing) (toegang is afhankelijk van de machtigingen voor de Office-portal Hallo) en selecteer de Azure AD Premium-proefversie. Klik op Hallo **proefversie uitbreiden** koppeling en Hallo instructies volgen. U moet een creditcard tooenter, maar deze wordt niet in rekening gebracht.

![Uitbreiden van een licentie proefversie in Hallo Office-portal](./media/active-directory-licensing-what-is/extend_license_trial.png)

Proefperiode verlengen kunnen ook worden aangevraagd door het indienen van een aanvraag voor ondersteuning. Een beheerder van de klant toohello Office 365-portal kunt navigeren [ondersteuningspagina](http://aka.ms/extendAADtrial) (toegang is afhankelijk van de machtigingen voor Hallo Office ondersteuningspagina). Selecteer op deze pagina 'Abonnementen en Proefabonnementen' onder de functies en 'Proefversie vragen' onder symptoom. Voer ten slotte op Hallo omstandigheden gegevens

![Een licentie proefversie met behulp van een ondersteuningsverzoek uitbreiden](./media/active-directory-licensing-what-is/alternate_office_aad_trial_extension.png)

## <a name="next-steps"></a>Volgende stappen
U kunt nu klaar tooconfigure worden en sommige Azure AD Premium-functies gebruiken.

* [Selfservice voor wachtwoordherstel](active-directory-manage-passwords.md)
* [Self-service groepsbeheer](active-directory-accessmanagement-self-service-group-management.md)
* [Azure AD Connect Health](active-directory-aadconnect-health.md)
* [Groep toewijzing tooapplications](active-directory-manage-groups.md)
* [Azure multi-factor Authentication](../multi-factor-authentication/multi-factor-authentication.md)
* [Directe aankoop van Azure AD Premium-licenties](http://aka.ms/buyaadp)
