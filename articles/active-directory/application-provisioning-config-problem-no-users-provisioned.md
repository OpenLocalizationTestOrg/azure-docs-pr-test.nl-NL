---
title: aaaNo gebruikers worden ingericht tooan Azure AD-galerie toepassing | Microsoft Docs
description: Hoe tootroubleshoot veelvoorkomende problemen geconfronteerd wanneer er geen gebruikers die voorkomen een an Azure AD-galerie-toepassing die u hebt geconfigureerd voor gebruikers inrichten met Azure AD
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: asteen
ms.openlocfilehash: 4d9693a202ed657e1de5571b50e5d499bef1bb3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="no-users-are-being-provisioned-tooan-azure-ad-gallery-application"></a>Er zijn geen gebruikers worden ingericht tooan Azure AD-galerie toepassing

Eenmaal automatische inrichting is geconfigureerd voor een toepassing (inclusief verifiëren dat het Hallo app referenties verstrekt tooAzure AD tooconnect toohello app zijn geldig). Vervolgens gebruikers en/of groepen ingerichte toohello app zijn en wordt bepaald door de volgende dingen Hallo:

-   Die gebruikers en groepen zijn **toegewezen** toohello toepassing. Zie voor meer informatie over toewijzing [toewijzen van een gebruiker of groep tooan enterprise-app in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal).

-   Wel of niet **kenmerktoewijzingen** zijn geldige kenmerken vanuit Azure AD toohello app toosync ingeschakeld en geconfigureerd. Zie voor meer informatie over kenmerktoewijzingen [aanpassen gebruiker inrichting kenmerktoewijzingen voor SaaS-toepassingen in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-customizing-attribute-mappings).

-   Of er is al dan niet een **bereik filter** aanwezig die gebruikers wordt gefilterd op basis van specifieke kenmerkwaarden. Zie voor meer informatie over het bereikfilters [inrichten van toepassing op basis van kenmerken met bereikfilters](https://docs.microsoft.com/azure/active-directory/active-directory-saas-scoping-filters).

Wanneer observeren gebruikers niet worden ingericht, Raadpleeg de controlelogboeken Hallo in Azure AD en zoek naar logboekvermeldingen voor een specifieke gebruiker.

Hallo inrichting controlelogboeken kan worden geopend in hello Azure-portal, op Hallo **Azure Active Directory &gt; zakelijke Apps &gt; \[toepassingsnaam\] &gt; Audit logboeken**tabblad. Filter Hallo Hallo aanmeldt **Account inrichten** categorie tooonly Zie Hallo gebeurtenissen voor die app-inrichting. U kunt zoeken naar gebruikers op basis van Hallo 'overeenkomende ID' die is geconfigureerd voor deze in Hallo kenmerktoewijzingen. Bijvoorbeeld, als u Hallo 'user principal name' of 'e-mailadres' als Hallo die overeenkomt met het kenmerk hello Azure AD-zijde geconfigureerd en Hallo gebruiker niet inrichten heeft de waarde 'audrey@contoso.com'. Zoek vervolgens Hallo controlelogboeken voor 'audrey@contoso.com' en bekijk vervolgens vermeldingen geretourneerd.

Hallo inrichting audit logboek vastgelegd die alle bewerkingen die worden uitgevoerd door Hallo inrichting service, inclusief uitvoeren van query's Azure AD voor toegewezen gebruikers die zich binnen het bereik van de inrichting, Hallo doel app Hallo aanwezigheid van deze gebruikers opvragen, vergelijken Hallo Hallo gebruikersobjecten tussen Hallo-systeem. Vervolgens toevoegen, bijwerken of Hallo-gebruikersaccount in Hallo doelsysteem op basis van de vergelijking Hallo uitschakelen.

## <a name="general-problem-areas-with-provisioning-tooconsider"></a>Algemene probleemgebieden met het leveren van tooconsider

Hieronder volgt een lijst van Hallo algemene probleemgebieden die u inzoomen kunt in als u een idee van de locatie waar toostart.

* [-Service inricht toostart niet wordt weergegeven](#provisioning-service-does-not-appear-to-start)
* [Controlelogboeken dat gebruikers worden overgeslagen en niet is ingericht, zelfs als ze worden toegewezen](#audit-logs-say-users-are-skipped-and-not-provisioned-even-though-they-are-assigned)

## <a name="provisioning-service-does-not-appear-toostart"></a>-Service inricht toostart niet wordt weergegeven

Als u Hallo instelt **inrichting Status** toobe **op** in Hallo **Azure Active Directory &gt; zakelijke Apps &gt; \[toepassingsnaam\] &gt;Inrichten** sectie Hallo Azure-portal. Echter geen andere statusgegevens worden weergegeven op deze pagina nadat het volgende wordt opnieuw geladen, is het waarschijnlijk dat Hallo-service wordt uitgevoerd, maar niet nog een initiële synchronisatie is voltooid. Controleer Hallo **controlelogboeken** hierboven toodetermine beschreven welke bewerkingen Hallo-service wordt uitgevoerd en als er fouten zijn.

>[!NOTE]
>Een initiële synchronisatie kan van 20 minuten tooseveral uren, afhankelijk van de grootte Hallo van hello Azure AD-directory en het aantal gebruikers in het bereik voor het inrichten van Hallo duren. Volgende synchronisaties na de initiële synchronisatie Hallo sneller zijn, als Hallo watermerken waarbij Hallo status van beide systemen na de initiële synchronisatie Hallo-service inricht opslaat. Dit verbetert de prestaties van de volgende synchronisatie.
>
>

## <a name="audit-logs-say-users-are-skipped-and-not-provisioned-even-though-they-are-assigned"></a>Controlelogboeken dat gebruikers worden overgeslagen en niet is ingericht, hoewel ze zijn toegewezen

Wanneer een gebruiker wordt weergegeven als 'overgeslagen' in de controlelogboeken hello, is erg belangrijk tooread Hallo details in het vak Hallo logboek bericht toodetermine Hallo reden uitgebreid. Hieronder vindt u veelvoorkomende oorzaken en oplossingen:

-   **Een filter scope is geconfigureerd** **die wordt uitgefilterd Hallo gebruiker op basis van een kenmerkwaarde**. Zie voor meer informatie over het bereikfilters <https://docs.microsoft.com/azure/active-directory/active-directory-saas-scoping-filters>.

-   **Hallo-gebruiker is 'niet effectief heeft het recht'.** Als u dit specifieke foutbericht ziet, is dit omdat er een probleem met de Hallo toewijzing gebruikersrecord opgeslagen in Azure AD. toofix dit probleem toewijzing gebruiker (of groep) uit de app Hallo Hallo en opnieuw opnieuw toe te wijzen. Zie voor meer informatie over toewijzing <https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal>.

-   **Een vereist kenmerk is ontbreekt of niet ingevuld voor een gebruiker.** Een tooconsider wat belangrijk is bij het instellen van de inrichting tooreview Hallo kenmerktoewijzingen en werkstromen die welke gebruiker (of groep) eigenschappen stroom van Azure AD-toepassing voor toohello definiëren en configureren. Dit omvat Hallo 'overeenkomende eigenschap' instelt met gebruikte toouniquely worden geïdentificeerd en overeen met gebruikers/groepen tussen Hallo twee systemen. Zie voor meer informatie over dit proces belangrijk [aanpassen gebruiker inrichting kenmerktoewijzingen voor SaaS-toepassingen in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-customizing-attribute-mappings).

  * **Kenmerktoewijzingen voor groepen:** inrichten Hallo naam en details in toevoeging toohello leden, groeperen als ondersteund op bepaalde toepassingen. U kunt inschakelen of uitschakelen van deze functionaliteit met in- of uitschakelen van Hallo **toewijzing** voor een groepsobjecten worden weergegeven in Hallo **inrichten** tabblad. Als inrichting groepen is ingeschakeld, moet u tooreview Hallo kenmerk toewijzingen tooensure een juiste veld wordt gebruikt voor Hallo 'die overeenkomt met de ID'. Kan dit Hallo weergegeven naam of e-mailalias), zoals het Hallo-groep en de bijbehorende leden niet worden ingericht als hello die overeenkomt met de eigenschap is leeg of niet ingevuld voor een groep in Azure AD.

## <a name="next-steps"></a>Volgende stappen
[Azure AD Connect-synchronisatie: inzicht declaratieve inrichting](active-directory-aadconnectsync-understanding-declarative-provisioning.md)

