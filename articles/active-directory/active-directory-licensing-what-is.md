---
title: Licentie voor Azure Active Directory-gebruikers in de klassieke Azure portal | Microsoft Docs
description: Beschrijving van Microsoft Azure Active Directory-licentieverlening, hoe het werkt, hoe u aan de slag en beste praktijken, zoals Office 365, Microsoft Intune en Azure Active Directory Premium en Basic-edities
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
ms.openlocfilehash: 9da5bb6987a9eb3398abe0d6066f1945620df9a4
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="what-is-microsoft-azure-active-directory-licensing-in-the-azure-classic-portal"></a>Wat is Microsoft Azure Active Directory-licentieverlening in de klassieke Azure portal?

> [!div class="op_single_selector"]
> * [Instructies voor Azure portal](active-directory-licensing-get-started-azure-portal.md)
> * [Azure classic portal info](active-directory-licensing-what-is.md)
>
>

Azure Active Directory (Azure AD) van Microsoft Identity is als een Service (IDaaS)-oplossing en platform. Azure AD wordt aangeboden in een aantal technische en functionele versies, variërend van Azure AD-vrij, zodat de is beschikbaar bij alle Microsoft-services zoals Office 365, Dynamics, Microsoft Intune en Azure (Azure AD genereert geen eventuele kosten verbruik in deze modus), naar Betaalde Azure AD-versies zoals Enterprise Mobility Suite (EMS), Azure AD Premium en Basic, evenals Azure multi-factor Authentication (MFA). De meeste Azure AD betaald versies worden geleverd via een per gebruiker rechten net als veel van Microsoft online services, zoals in Office 365, Microsoft Intune en Azure AD. In dergelijke gevallen de aankoop van de service wordt weergegeven met een of meer abonnementen en elk abonnement bevat een vooraf aankoop aantal licenties in uw tenant. Rechten per gebruiker worden bereikt via de licentietoewijzing, het maken van een koppeling tussen de gebruiker en het product, de onderdelen van de service voor de gebruiker inschakelen en gebruiken van een van de vooruitbetaalde licenties.

> [!IMPORTANT]
> Microsoft raadt u aan Azure AD te beheren met het [Azure AD-beheercentrum](https://aad.portal.azure.com) in Azure Portal in plaats van de klassieke Azure portal waarnaar in dit artikel wordt verwezen. Voor informatie over het toewijzen van beheerdersrollen in het Azure AD-beheercentrum, Zie [licentie uzelf en uw gebruikers in Azure AD](active-directory-licensing-get-started-azure-portal.md).

[Probeer Azure AD premium nu.](https://portal.office.com/Signup/Signup.aspx?OfferId=01824d11-5ad8-447f-8523-666b0848b381&ali=1#0)

> [!NOTE]
> Azure AD-beheerportal is een onderdeel van de klassieke Azure portal. Terwijl u met behulp van Azure AD, hoeft niet alle Azure aankopen, toegang tot deze portal moet een actief Azure-abonnement of een [Azure-proefabonnement](https://azure.microsoft.com/pricing/free-trial/).
>
>

Zie voor een breed overzicht van Azure AD-servicefuncties [wat is Azure AD](active-directory-whatis.md).
[Meer informatie over Azure AD-serviceniveaus](https://azure.microsoft.com/support/legal/sla/)

> [!NOTE]
> Azure omslagstelsel abonnementen zijn verschillend:, terwijl ook weergegeven in uw directory, deze abonnementen maken van een Azure-resources en toe te wijzen aan uw betalingswijze. In dit geval zijn er geen licentieaantallen gekoppeld aan het abonnement. Koppeling van de gebruikers met het abonnement, de gebruikers toegang tot het beheren van abonnementresources, wordt bereikt door het verlenen van machtigingen voor het Azure-resources toegewezen aan het abonnement niet bewerken.
>
>

## <a name="how-does-azure-ad-licensing-work"></a>Hoe Azure AD werkt licentieverlening?
Azure AD (recht gebaseerd) op basis van een licentie services werk door een abonnement in uw Azure AD-directory-service-tenant activeren. Zodra het abonnement actief is kunnen u de servicemogelijkheden worden beheerd door beheerders van directory-service en die wordt gebruikt door gebruikers met een licentie.

Wanneer u kopen of Enterprise Mobility Suite, Azure AD Premium of Azure AD Basic activeren, wordt uw directory bijgewerkt met het abonnement, met inbegrip van de geldigheidsperiode en vooruitbetaalde licenties. Uw abonnementsgegevens waaronder status, volgende lifecycle gebeurtenis en het aantal licenties toegewezen of beschikbaar is beschikbaar via de klassieke Azure portal op het tabblad licenties voor de specifieke map. Dit is ook naar de beste plaats voor het beheren van uw licentietoewijzingen.

Elk abonnement bestaat uit een of meer service-abonnementen, elke toewijzing van het opgenomen functionaliteitsniveau van het type van de service; bijvoorbeeld: Azure AD, Azure MFA, Microsoft Intune, Exchange Online of SharePoint Online. Azure AD-Licentiebeheer vereist geen serviceniveaubeheer plan. Dit wijkt af van Office 365 die afhankelijk van deze modus geavanceerde configuratie is voor het beheren van toegang tot services opgenomen. In de serviceconfiguratie, functies inschakelen en beheren van afzonderlijke machtigingen, is afhankelijk van Azure AD.

In het algemeen wordt Azure AD-abonnementsgegevens beheerd via de klassieke Azure-portal op het tabblad licenties voor de specifieke map. Azure AD-abonnementen, met uitzondering van Azure AD Premium, worden niet weergegeven in de Office-portal.

> [!IMPORTANT]
> Azure AD Premium en Basic, evenals de Enterprise Mobility Suite-abonnementen zijn beperkt tot hun ingerichte directory/tenant. Abonnementen kunnen niet worden gesplitst tussen voltooiing van mappen of gebruikt voor het machtigen van gebruikers in andere directory's. Een abonnement verplaatsen tussen mappen is mogelijk, maar vereist het verzenden van een ondersteuningsticket of annuleren en opnieuw in het geval van een directe aankopen kopen.
>
> Bij de aanschaf van Azure AD of Enterprise Mobility Suite via Volume Licensing abonnement activering gebeurt automatisch wanneer de overeenkomst bevat andere Microsoft Online services, zoals Office 365.
>
>

Betaalde Azure AD-functies omvatten de breedte van de map. Voorbeelden zijn:

* Groep toewijzing op basis van toepassingen, die is ingeschakeld in de specifieke toepassing die u beheert.
* Geavanceerde en mogelijkheden voor groepsbeheer met Self-service zijn beschikbaar binnen de specifieke groep of onder de directory-configuratie.
* Premium-beveiligingsrapporten zijn op het tabblad Rapportage
* Detectie van cloud-toepassing wordt weergegeven in de Azure-portal onder identiteit.

### <a name="assigning-licenses"></a>Licenties toewijzen
Hoewel het verkrijgen van een abonnement hoeft u alleen betaald mogelijkheden configureren, vereist met behulp van uw Azure AD betaalde functies voor het distribueren van licenties aan de juiste personen. Elke gebruiker die toegang moeten hebben tot of die wordt beheerd via een Azure AD betaald functie moet in het algemeen een licentie toegewezen. De licentietoewijzing van een is geen toewijzing tussen een gebruiker en een gekochte service, zoals Azure AD Premium of Basic of Enterprise Mobility Suite.

Beheren welke gebruikers in uw directory moeten beschikken over een licentie is eenvoudig. Worden kan bereikt door toe te wijzen aan een groep te maken van toewijzingsregels voor via de Azure AD-beheerportal of door het toewijzen van licenties rechtstreeks aan de juiste personen via een portal, PowerShell of API's. Bij het toewijzen van licenties aan een groep, wordt alle groepsleden een licentie toegewezen. Als gebruikers worden toegevoegd of verwijderd uit de groep ze worden toegewezen of de juiste licentie verwijderd. Groepstoewijzing kan gebruikmaken van een groep management voor u beschikbaar is en consistent is met toewijzing op basis van een groep van toepassingen. Met deze benadering kunt u regels instellen dat alle gebruikers in uw directory worden automatisch toegewezen of zelfs delegeren de beslissing aan andere beheerders in de organisatie, zorg ervoor dat iedereen met de juiste functie een licentie heeft.

Bij licentietoewijzing op basis van een groep neemt elke gebruiker een gebruikslocatie ontbreekt de maplocatie tijdens de toewijzing. Deze locatie kan worden gewijzigd door de beheerder op elk gewenst moment. In gevallen waar de automatische toewijzing is mislukt vanwege fout weerspiegelt de gebruikersinformatie onder die licentietype die status.

## <a name="getting-started-with-azure-ad-licensing"></a>Aan de slag met Azure AD-licentieverlening
Aan de slag met Azure AD is eenvoudig; u kunt altijd uw directory als onderdeel van zich registreren voor een gratis proefversie van Azure maken. [Meer informatie over het aanmelden als een organisatie](sign-up-organization.md). Het volgende kunt u ervoor zorgen dat uw directory beste wordt uitgelijnd met andere Microsoft-services u mogelijk worden verbruikt of van plan bent te gebruiken en uw doelstellingen bij het verkrijgen van de service.

Hier volgen enkele aanbevolen procedures:

* Als u al van een van de organisatie-services van Microsoft gebruikmaakt, hebt u al een Azure Active directory. In dit geval moet u blijven gebruiken dezelfde directory voor andere services, zodat de identiteitsbeheer core, zoals inrichting en hybride SSO, kan worden gebruikt in services. Uw gebruikers een ervaring voor eenmalige aanmelding zijn, en profiteert van mogelijkheden in services. Als gevolg hiervan, als u besluit een Azure AD-service voor uw werknemers betaald aanschaffen, raden wij u dezelfde map gebruiken om dit te doen.
* Als u van plan bent met Azure AD voor een andere set van gebruikers (partners, klanten, enzovoort), of als u wilt evalueren, Azure AD-services en wilt dat doen in de isolatie van uw productieservice, of als u op zoek bent voor het instellen van een sandbox-omgeving voor y onze services, wordt aangeraden dat u eerst een nieuwe map via de klassieke Azure-Azure-portal maakt. [Meer informatie over het maken van een nieuwe Azure AD-directory in de klassieke Azure portal](active-directory-licensing-directory-independence.md). De nieuwe map wordt gemaakt met uw account als een externe gebruiker met globale beheerdersmachtigingen. Wanneer u zich aanmeldt bij de klassieke Azure portal met dit account, kunt u zich zien van deze map en alle directorybeheertaken openen. U wordt aangeraden dat u een lokaal account met de juiste toegangsrechten maken voor het beheren van andere Microsoft-services (die niet toegankelijk via de klassieke Azure portal). [Meer informatie over het maken van gebruikersaccounts in Azure AD](active-directory-create-users.md).

> [!NOTE]
> Azure AD biedt ondersteuning voor 'externe gebruikers', wat gebruikersaccounts zijn in een exemplaar van Azure AD die zijn gemaakt met een Microsoft-Account (MSA) of een Azure AD-identiteit van een andere map. Terwijl we bezig zijn worden uitbreiden deze mogelijkheid in alle van de organisatie-services van Microsoft, nu deze accounts niet ondersteund in een aantal ervaringen van de services; bijvoorbeeld, ondersteunt de Office 365-beheerportal momenteel geen deze gebruikers. Als gevolg hiervan is externe gebruikers met een Microsoft-account niet mogelijk tot de Office 365-beheerportal, terwijl externe gebruikers van andere Azure AD-directory's worden genegeerd. In dat geval wordt alleen het lokale gebruikersaccount, de Azure AD of Office 365-directory waar de gebruiker oorspronkelijk is gemaakt, toegankelijk via deze zou zijn.
>
>

Zoals wordt aangegeven, heeft Azure AD een verschillende betaald versies. Deze versies hebben een aantal kleine verschillen in hun beschikbaarheid aankoop:

| Product | EA/VOLUMELICENTIES | Open | CSP | MPN gebruiksrechten | Rechtstreekse aankoop | Proefversie |
| --- | --- | --- | --- | --- | --- | --- |
| Enterprise Mobility Suite |X |X |X |X | |X |
| Azure AD Premium |X |X |X | |X |X |
| Azure AD Basic |X |X |X |X |<br /> |<br /> |

### <a name="select-one-or-more-license-trials"></a>Selecteer een of meer licentie-experimenten
 In alle gevallen kunt u een Azure AD Premium of Enterprise Mobility Suite-proefabonnement activeren door het selecteren van de specifieke evaluatieversie die u wilt dat op het tabblad licenties in uw directory. De evaluatieversie bevat een 30-daagse abonnement met 100 licenties.

![Azure Active Directory proeflicentie plannen](./media/active-directory-licensing-what-is/trial_plans.png)

![Enterprise Mobility Suite proeflicentie plannen](./media/active-directory-licensing-what-is/EMS_trial_plan.png)

![Actieve proeflicentie plannen](./media/active-directory-licensing-what-is/active_license_trials.png)

### <a name="assign-licenses"></a>Licenties toewijzen
Zodra het abonnement actief is, moet u een licentie toewijzen aan uzelf en vernieuw de browser om te controleren of dat u alle functies in uw ziet. De volgende stap is om licenties te wijzen aan de gebruikers die toegang tot of worden opgenomen in moet betaalde Azure AD-functies. Zoals we eerder vermeld bij 'Licenties toewijzen', is de beste manier om dit te doen om te bepalen van de groep die de gewenste doelgroep en deze toewijzen aan de licentie; op deze manier kunnen worden gebruikers die zijn toegevoegd of verwijderd uit de groep gedurende de levenscyclus toegewezen aan of verwijderd uit de licentie.

Als u wilt een licentie toewijzen aan een groep of individuele gebruikers, selecteert u het licentie-plan dat u wilt toewijzen en klik op **toewijzen** op de opdrachtbalk.

![Actieve proeflicentie plannen](./media/active-directory-licensing-what-is/assign_licenses.png)

Als in het dialoogvenster toewijzing voor het geselecteerde abonnement kunt u gebruikers en toevoegen aan de **toewijzen** kolom aan de rechterkant. U kunt de pagina via de lijst met gebruikers of zoeken naar specifieke personen met behulp van het zoeken op de bovenste glas rechts van het raster voor de gebruiker. Als u groepen toewijzen, selecteert u 'Groepen' in de **weergeven** menu en klik vervolgens op de controle van de knop aan de rechterkant vernieuwen van de toewijzingen die worden weergegeven.

![Licenties toewijzen aan groepen](./media/active-directory-licensing-what-is/assign_licenses_to_groups.png)

U kunt nu zoeken of pagina via groepen en voeg deze toe aan de **toewijzen** kolom op dezelfde manier. U kunt deze gebruiken voor het toewijzen van een combinatie van gebruikers en groepen in één bewerking. Klik op de knop controleren in de rechterbenedenhoek van de pagina om het toewijzingsproces.

![Licentie toewijzing voortgangsbericht](./media/active-directory-licensing-what-is/license_assignment_progress_message.png)

Wanneer een groep wordt toegewezen, neemt de leden ervan de licenties binnen 30 minuten, maar meestal binnen 1-2 minuten.

Toewijzingsfouten kunnen optreden tijdens de licentietoewijzing van Azure AD, maar zijn relatief zeldzame. Mogelijke toewijzingsfouten zijn beperkt tot:

* Toewijzing conflict - wanneer een gebruiker een licentie die niet compatibel is met de huidige licentie was toegewezen. In dit geval wordt moet de nieuwe licentie toewijzen de vorige verwijdert.
* Beschikbare licenties overschreden - wanneer het aantal gebruikers in de toegewezen groepen overschrijdt de beschikbare licenties toewijzingsstatus van de gebruikers bevatten een mislukt als gevolg van ontbrekende licenties toewijzen.

### <a name="view-assigned-licenses"></a>Weergave toegewezen licenties
Een samenvatting weergegeven van de toegewezen licenties beschikbaar, toegewezen en volgende abonnement lifecycle gebeurtenis inclusief worden weergegeven op de **licenties** tabblad.

![Het aantal toegewezen licenties weergeven](./media/active-directory-licensing-what-is/view_assigned_licenses.png)

Een gedetailleerde lijst met toegewezen gebruikers en groepen, inclusief de status van toewijzing en het pad (direct of overgenomen uit een of meer groepen) is beschikbaar bij het navigeren naar de planning van een licentie.

![Gegevens weergeven van licenties voor een licentieabonnement worden toegewezen](./media/active-directory-licensing-what-is/assigned_licenses_detail.png)

Het is net zo eenvoudig als het eraan toe te wijzen om licenties te verwijderen. Als de gebruiker rechtstreeks is toegewezen of voor een toegewezen groep, u de licentie verwijderen kunt door het selecteren van het licentietype, selecteer **verwijderen**, de gebruiker of groep toe te voegen aan de lijst verwijderen en de actie te bevestigen. U kunt ook u kunt een licentietype openen, selecteer de specifieke gebruiker of groep en tik op **verwijderen** op de opdrachtbalk. Als u wilt beëindigen van een gebruiker overnemen van een licentie uit een groep, hoeft de gebruiker van de groep te verwijderen.

### <a name="extending-trials"></a>Proefversies uitbreiden
Evaluatieversie uitbreidingen voor klanten zijn beschikbaar als selfservice via de Office 365-portal. Een beheerder van de klant kunt navigeren naar de [Office-portal](https://portal.office.com/#Billing) (toegang is afhankelijk van de machtigingen voor de Office-portal) en selecteer de Azure AD Premium-proefversie. Klik op de **uitbreiden proefversie** koppelen en volg de instructies. U moet een creditcard invoeren, maar deze wordt niet in rekening gebracht.

![Uitbreiden van een licentie proefversie in de Office-portal](./media/active-directory-licensing-what-is/extend_license_trial.png)

Proefperiode verlengen kunnen ook worden aangevraagd door het indienen van een aanvraag voor ondersteuning. Een beheerder van de klant kunt navigeren naar de Office 365-portal [ondersteuningspagina](http://aka.ms/extendAADtrial) (toegang is afhankelijk van de machtigingen voor de ondersteuningspagina van Office). Selecteer op deze pagina 'Abonnementen en Proefabonnementen' onder de functies en 'Proefversie vragen' onder symptoom. Voer ten slotte informatie over de omstandigheden

![Een licentie proefversie met behulp van een ondersteuningsverzoek uitbreiden](./media/active-directory-licensing-what-is/alternate_office_aad_trial_extension.png)

## <a name="next-steps"></a>Volgende stappen
Nu u mogelijk klaar om te configureren en bepaalde Azure AD Premium-functies gebruikt.

* [Selfservice voor wachtwoordherstel](active-directory-manage-passwords.md)
* [Self-service groepsbeheer](active-directory-accessmanagement-self-service-group-management.md)
* [Azure AD Connect Health](active-directory-aadconnect-health.md)
* [Groepstoewijzing van toepassingen](active-directory-manage-groups.md)
* [Azure multi-factor Authentication](../multi-factor-authentication/multi-factor-authentication.md)
* [Directe aankoop van Azure AD Premium-licenties](http://aka.ms/buyaadp)
