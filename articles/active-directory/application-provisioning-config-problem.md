---
title: configureren van gebruikers inrichten tooan Azure AD-galerie toepassing aaaProblem | Microsoft Docs
description: Hoe tootroubleshoot veelvoorkomende problemen bij het configureren van gebruikers inrichten tooan toepassing al wordt vermeld in hello Azure AD-Toepassingsgalerie managementoverhead
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
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 19b12be019b05faecef74c6f92a9de03b52a5ef9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="problem-configuring-user-provisioning-tooan-azure-ad-gallery-application"></a>Probleem gebruikers inrichten tooan Azure AD-galerie toepassing configureren

Configureren van [automatisch gebruikers inrichten](https://docs.microsoft.com/azure/active-directory/active-directory-saas-app-provisioning) voor een app (indien ondersteund), vereist dat specifieke instructies gevolgd tooprepare Hallo-toepassing voor het automatisch inrichten. Vervolgens kunt u hello Azure portal tooconfigure hello toosynchronize gebruiker accounts toohello servicetoepassing wordt ingericht.

U moet altijd eerst Hallo setup zelfstudie specifieke toosetting up inrichting voor uw toepassing te zoeken. Volg deze stappen tooconfigure beide Hallo-app en Azure AD toocreate Hallo inrichting verbinding. Een lijst met app-zelfstudies kan worden gevonden op [lijst zelfstudies over het SaaS-Apps met Azure Active Directory tooIntegrate](https://docs.microsoft.com/azure/active-directory/active-directory-saas-tutorial-list).

## <a name="how-toosee-if-provisioning-is-working"></a>Hoe toosee als inrichting werkt 

Zodra Hallo-service is geconfigureerd, kunnen de meeste inzichten in Hallo werking van Hallo-service worden getekend vanaf twee locaties:

-   **Controlelogboeken** – hello inrichting logboeken controlerecord alle Hallo bewerkingen uitgevoerd door Hallo-service inricht, waaronder het uitvoeren van query's Azure AD voor toegewezen gebruikers die binnen het bereik van de inrichting. Query Hallo doel app Hallo bestaan van de gebruikers, vergelijken Hallo gebruikersobjecten tussen Hallo-systeem. Vervolgens toevoegen, bijwerken of Hallo-gebruikersaccount in Hallo doelsysteem op basis van de vergelijking Hallo uitschakelen. Hallo inrichting controlelogboeken kan worden geopend in hello Azure-portal, op Hallo **Azure Active Directory &gt; zakelijke Apps &gt; \[toepassingsnaam\] &gt; Audit logboeken**tabblad. Filter Hallo Hallo aanmeldt **Account inrichten** categorie tooonly Zie Hallo gebeurtenissen voor die app-inrichting.

-   **Inrichtingsstatus –** voor een bepaalde app kan worden bekeken in Hallo worden uitgevoerd, een overzicht van de laatste inrichting Hallo **Azure Active Directory &gt; zakelijke Apps &gt; \[toepassingsnaam\] &gt; Inrichting** sectie aan de onderkant Hallo van welkomstscherm onder Hallo service-instellingen. Deze sectie bevat een overzicht van hoeveel gebruikers (en/of groepen) momenteel worden gesynchroniseerd tussen Hallo twee systemen en als er fouten zijn. Details van fouten worden in Hallo controlelogboeken. Let op Hallo van inrichting status niet worden gevuld totdat een volledige initiële synchronisatie is voltooid tussen Azure AD en Hallo-app.

## <a name="general-problem-areas-with-provisioning-tooconsider"></a>Algemene probleemgebieden met het leveren van tooconsider

Hieronder volgt een lijst van Hallo algemene probleemgebieden die u inzoomen kunt in als u een idee van de locatie waar toostart.

* [-Service inricht toostart niet wordt weergegeven](#provisioning-service-does-not-appear-to-start)
* [Kan geen configuratie vanwege tooapp referenties werkt niet op te slaan](#can’t-save-configuration-due-to-app-credentials-not-working)
* [Controlelogboeken spreken gebruikers zijn 'overgeslagen' en niet is ingericht, zelfs als ze zijn toegewezen](#audit-logs-say-users-are-skipped-and-not-provisioned-even-though-they-are-assigned)

## <a name="provisioning-service-does-not-appear-toostart"></a>-Service inricht toostart niet wordt weergegeven

Als u Hallo instelt **inrichting Status** toobe **op** in Hallo **Azure Active Directory &gt; zakelijke Apps &gt; \[toepassingsnaam\] &gt;Inrichten** sectie Hallo Azure-portal. Er zijn geen andere statusgegevens zijn echter op die pagina weergegeven nadat daaropvolgende wordt opnieuw geladen. Is het waarschijnlijk dat Hallo-service wordt uitgevoerd, maar niet nog een initiële synchronisatie is voltooid. Controleer Hallo **controlelogboeken** hierboven toodetermine beschreven welke bewerkingen Hallo-service wordt uitgevoerd en als er fouten zijn.

>[!NOTE]
>Een initiële synchronisatie kan van 20 minuten tooseveral uren, afhankelijk van de grootte Hallo van hello Azure AD-directory en het aantal gebruikers in het bereik voor het inrichten van Hallo duren. Volgende synchronisaties na de initiële synchronisatie Hallo niet sneller als Hallo-service inricht watermerken waarbij Hallo status van beide systemen na de initiële synchronisatie hello, verbeterde prestaties van de volgende synchronisatie worden opgeslagen.
>
>

## <a name="cant-save-configuration-due-tooapp-credentials-not-working"></a>Kan geen configuratie vanwege tooapp referenties werkt niet op te slaan

Azure AD vereist in de volgorde voor inrichting toowork, geldige referenties op waarmee het tooconnect tooa Gebruikersbeheer API geleverd door de app. Als deze referenties niet werkt, of u niet weet wat die ze zijn, raadpleegt u Hallo-zelfstudie voor het instellen van deze app, die eerder zijn beschreven.

## <a name="audit-logs-say-users-are-skipped-and-not-provisioned-even-though-they-are-assigned"></a>Controlelogboeken dat gebruikers worden overgeslagen en niet is ingericht, hoewel ze zijn toegewezen

Wanneer een gebruiker wordt weergegeven als 'overgeslagen' in de controlelogboeken hello, is erg belangrijk tooread Hallo details in het vak Hallo logboek bericht toodetermine Hallo reden uitgebreid. Hieronder vindt u veelvoorkomende oorzaken en oplossingen:

-   **Een filter scope is geconfigureerd** **die wordt uitgefilterd Hallo gebruiker op basis van een kenmerkwaarde**. Zie voor meer informatie over het bereikfilters <https://docs.microsoft.com/azure/active-directory/active-directory-saas-scoping-filters>.

-   **Hallo-gebruiker is 'niet effectief heeft het recht'.** Als u dit specifieke foutbericht ziet, is dit omdat er een probleem met de Hallo toewijzing gebruikersrecord opgeslagen in Azure AD. toofix dit probleem toewijzing gebruiker (of groep) uit de app Hallo Hallo en opnieuw opnieuw toe te wijzen. Zie voor meer informatie over toewijzing <https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal>.

-   **Een vereist kenmerk is ontbreekt of niet ingevuld voor een gebruiker.** Een tooconsider wat belangrijk is bij het instellen van de inrichting tooreview Hallo kenmerktoewijzingen en werkstromen die welke gebruiker (of groep) eigenschappen stroom van Azure AD-toepassing voor toohello definiëren en configureren. Dit omvat Hallo 'overeenkomende eigenschap' instelt met gebruikte toouniquely worden geïdentificeerd en overeen met gebruikers/groepen tussen Hallo twee systemen. Zie voor meer informatie over dit proces belangrijk <https://docs.microsoft.com/azure/active-directory/active-directory-saas-customizing-attribute-mappings>.

   * **Kenmerktoewijzingen voor groepen:** inrichten Hallo naam en details in toevoeging toohello leden, groeperen als ondersteund op bepaalde toepassingen. U kunt inschakelen of uitschakelen van deze functionaliteit met in- of uitschakelen van Hallo **toewijzing** voor een groepsobjecten worden weergegeven in Hallo **inrichten** tabblad. Als inrichting groepen is ingeschakeld, moet u tooreview Hallo kenmerk toewijzingen tooensure een juiste veld wordt gebruikt voor Hallo 'die overeenkomt met de ID'. Kan dit Hallo weergegeven naam of e-mailalias), zoals het Hallo-groep en de bijbehorende leden niet worden ingericht als hello die overeenkomt met de eigenschap is leeg of niet ingevuld voor een groep in Azure AD.

#<a name="next-steps"></a>Volgende stappen
[Automatisch gebruikers inrichten en Deprovisioning tooSaaS toepassingen met Azure Active Directory](active-directory-saas-app-provisioning.md)
