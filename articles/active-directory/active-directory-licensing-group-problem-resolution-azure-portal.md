---
title: Oplossen van licentieproblemen voor een groep in Azure Active Directory | Microsoft Docs
description: Het identificeren en oplossen van toewijzing licentieproblemen wanneer u Azure Active Directory-groepen gebaseerde licentieverlening
services: active-directory
keywords: Azure AD-licentieverlening
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/05/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: bfa951a897c9b383072c0d29c9a4266c163fe753
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="identify-and-resolve-license-assignment-problems-for-a-group-in-azure-active-directory"></a>Het identificeren en oplossen van problemen met licentie-toewijzing voor een groep in Azure Active Directory

Op basis van een groep licentieverlening in Azure Active Directory (Azure AD), wordt het concept van gebruikers in een foutstatus licentieverlening geïntroduceerd. In dit artikel leggen we de redenen waarom de gebruikers in deze status terechtkomen mogelijk.

Als u licenties rechtstreeks naar afzonderlijke gebruikers zonder gebruik te maken op basis van een groep licentieverlening toewijst, mislukken de toewijzingsbewerking. Bijvoorbeeld bij het uitvoeren van de PowerShell-cmdlet `Set-MsolUserLicense` op een gebruiker, de cmdlet voor een aantal redenen die gerelateerd zijn aan de zakelijke logica kan mislukken. Bijvoorbeeld, kunnen er onvoldoende licenties of een conflict tussen twee serviceniveaus die op hetzelfde moment kan niet worden toegewezen. Het probleem onmiddellijk gerapporteerd terug.

Wanneer u op basis van een groep-licentieverlening, wordt de dezelfde fouten kunnen optreden, maar wordt voorkomen op de achtergrond wanneer u de Azure AD-service is licenties toewijzen. Daarom moet kunnen niet de fouten worden gecommuniceerd naar u onmiddellijk. Ze zijn in plaats daarvan geregistreerd op het gebruikersobject en vervolgens via de portal beheerdersrechten gerapporteerd. Houd er rekening mee dat de oorspronkelijke bedoeling licentie voor de gebruiker nooit verloren is, maar deze wordt vastgelegd in een foutstatus voor toekomstig onderzoek en omzetten.

## <a name="how-to-find-license-assignment-errors"></a>Licentie toewijzingsfouten zoeken

1. Open de blade voor de groep gebruikers in een foutstatus van een specifieke groep vindt. Onder **licenties**, zal er een melding weergegeven als er geen gebruikers in een foutstatus.

![Groep foutmeldingen](media/active-directory-licensing-group-problem-resolution-azure-portal/group-error-notification.png)

2. Klik op de melding om een lijst van alle betrokken gebruikers te openen. U kunt klikken op elke gebruiker afzonderlijk voor meer informatie.

![Groep lijst met gebruikers in de foutstatus](media/active-directory-licensing-group-problem-resolution-azure-portal/list-of-users-with-errors.png)

3. Alle groepen met ten minste één fout op de **Azure Active Directory** blade Selecteer **licenties** en vervolgens **overzicht**. Een info wordt weergegeven wanneer u een aantal groepen uw aandacht vereisen.

![Overzicht van informatie over groepen in de foutstatus](media/active-directory-licensing-group-problem-resolution-azure-portal/group-errors-widget.png)

4. Klik op het vak om een lijst weer van alle groepen met fouten. U kunt klikken op elke groep voor meer informatie.

![Overzicht van lijst met groepen met fouten](media/active-directory-licensing-group-problem-resolution-azure-portal/list-of-groups-with-errors.png)


Hieronder volgt een beschrijving van elke potentieel probleem en de manier te verhelpen.

## <a name="not-enough-licenses"></a>Niet voldoende licenties

**Probleem:** er niet voldoende beschikbare licenties voor een van de producten die is opgegeven in de groep. Moet u meer licenties voor het product kopen of niet-gebruikte licenties van andere gebruikers of groepen vrijmaken.

Hoeveel licenties beschikbaar zijn, Ga naar **Azure Active Directory** > **licenties** > **alle producten**.

Als u wilt zien welke gebruikers en groepen licenties verbruiken, klikt u op een product. Onder **gelicentieerde gebruikers**, ziet u alle gebruikers die direct of via een of meer groepen toegewezen licenties hebt. Onder **groepen in licentie gegeven**, ziet u alle groepen met dat product dat is toegewezen.

**PowerShell:** PowerShell-cmdlets rapporteer deze fout als _CountViolation_.

## <a name="conflicting-service-plans"></a>Conflicterende service-abonnementen

**Probleem:** een van de producten die is opgegeven in de groep bevat een service-abonnement dat conflicteert met een andere service-abonnement al aan de gebruiker via een ander product toegewezen is. Sommige service-abonnementen zijn geconfigureerd op een manier die ze kunnen niet worden toegewezen aan dezelfde gebruiker die een andere gerelateerde service-abonnement.

Bekijk het volgende voorbeeld. Een gebruiker een licentie voor Office 365 Enterprise heeft **E1** toegewezen rechtstreeks met de abonnementen die zijn ingeschakeld. De gebruiker is toegevoegd aan een groep met de Office 365 Enterprise **E3** product toegewezen. Dit product bevat service-abonnementen die elkaar niet overlappen met de abonnementen die zijn opgenomen in E1, zodat de licentietoewijzing van de groep met de fout 'Serviceplannen conflicterende' mislukt. In dit voorbeeld zijn de conflicterende serviceplannen:

-   SharePoint Online (2 plannen) veroorzaakt een conflict met SharePoint Online (1 plannen).
-   Exchange Online (2 plannen) veroorzaakt een conflict met Exchange Online (1 plannen).

U lost dit conflict, moet u die uitschakelen twee abonnementen op de E1 licentie die rechtstreeks aan de gebruiker toegewezen. Of u moet de licentietoewijzing van de hele groep wijzigen en de plannen in de E3-licentie uitschakelen. U kunt ook moet u besluiten de licentie E1 van de gebruiker wordt verwijderd als deze in de context van de licentie E3 redundant.

De beslissing over het oplossen van conflicterende productlicenties altijd hoort bij de beheerder. Azure AD oplossen niet automatisch licentie conflicten.

**PowerShell:** PowerShell-cmdlets rapporteer deze fout als _MutuallyExclusiveViolation_.

## <a name="other-products-depend-on-this-license"></a>Andere producten zijn afhankelijk van deze licentie

**Probleem:** een van de producten die is opgegeven in de groep bevat een serviceplan dat moet worden ingeschakeld voor een andere service-abonnement in een ander product, te laten functioneren. Deze fout treedt op wanneer Azure AD probeert te verwijderen van de onderliggende service-abonnement. Dit kan bijvoorbeeld gebeuren als gevolg van de gebruiker wordt verwijderd uit de groep.

U lost dit probleem, moet u ervoor zorgen dat het vereiste plan nog is toegewezen aan gebruikers via een andere methode, of dat de afhankelijke services zijn uitgeschakeld voor deze gebruikers. Na dat doet, kunt u de groepslicentie goed verwijderen van deze gebruikers.

**PowerShell:** PowerShell-cmdlets rapporteer deze fout als _DependencyViolation_.

## <a name="usage-location-isnt-allowed"></a>Gebruikslocatie is niet toegestaan

**Probleem:** sommige Microsoft-services zijn niet beschikbaar op alle locaties vanwege lokale wet- en regelgeving. Voordat u een licentie aan een gebruiker toewijzen kunt, die u moet de eigenschap 'Gebruikslocatie' voor de gebruiker opgeven. U kunt dit onder doen de **gebruiker** > **profiel** > **instellingen** sectie in de Azure-portal.

Wanneer Azure AD probeert een groepslicentie toewijzen aan een gebruiker waarvan gebruikslocatie wordt niet ondersteund, wordt deze mislukt en noteer deze fout op de gebruiker.

U lost dit probleem, gebruikers van de ondersteunde locaties van de gelicentieerde groep te verwijderen. U kunt ook als de huidige locatie waarden voor informatie over het gebruik niet de locatie van de werkelijke gebruiker vertegenwoordigen, kunt u ze aanpassen zodat de licenties correct volgende keer zijn toegewezen (als de nieuwe locatie wordt ondersteund).

**PowerShell:** PowerShell-cmdlets rapporteer deze fout als _ProhibitedInUsageLocationViolation_.

> [!NOTE]
> Als Azure AD groep licenties toewijst, nemen alle gebruikers zonder een gebruikslocatie opgegeven de locatie van de map. Het is raadzaam dat beheerders het juiste gebruik locatie waarden instellen voor gebruikers voordat u op basis van een groep licensing om te voldoen aan de lokale wet- en regelgeving.

## <a name="what-happens-when-theres-more-than-one-product-license-on-a-group"></a>Wat gebeurt er wanneer er meer dan één productlicentie op een groep?

U kunt meer dan één productlicentie toewijzen aan een groep. U kunt bijvoorbeeld Office 365 Enterprise E3 en Enterprise Mobility + Security toewijzen aan een groep voor alle inbegrepen services voor gebruikers eenvoudig in te schakelen.

Azure AD probeert toe te wijzen alle licenties die zijn opgegeven in de groep aan elke gebruiker. Als Azure AD kan niet toewijzen een van de producten vanwege zakelijke logica problemen (bijvoorbeeld, als er niet voldoende licenties voor alle, of als er conflicten met andere services die zijn ingeschakeld op de gebruiker zijn), het won't ofwel de andere licenties in de groep toewijzen.

U zult kunnen zien welke gebruikers kunnen niet worden toegewezen, is mislukt en controleer welke producten zijn beïnvloed door deze.

## <a name="license-assignment-fails-silently-for-a-user-due-to-duplicate-proxy-addresses-in-exchange-online"></a>De licentietoewijzing niet achtergrond voor een gebruiker vanwege dubbele proxyadressen in Exchange Online

Als u Exchange Online gebruikt, zijn sommige gebruikers in uw tenant mogelijk verkeerd geconfigureerd met dezelfde waarde voor het proxyadres. Wanneer een licentie toewijzen aan een gebruiker op basis van een groep licentieverlening probeert, deze mislukt en wordt een fout niet opgenomen (in tegenstelling tot in de andere foutgevallen die hierboven worden beschreven): dit is een beperking in de preview-versie van deze functie en gaan we deze oplossen voordat *</c0>Algemenebeschikbaarheid<spanclass="notranslate">*.</span>

> [!TIP]
> Als u merkt dat sommige gebruikers geen licentie is ontvangen en er geen fout vastgelegd op die gebruikers is, moet u eerst controleren als er dubbele proxyadres.
> Dit kan worden gedaan door het uitvoeren van de volgende PowerShell-cmdlet op basis van Exchange Online:
```
Run Get-Recipient | where {$_.EmailAddresses -match "user@contoso.onmicrosoft.com"} | fL Name, RecipientType,emailaddresses
```
> [In dit artikel](https://support.microsoft.com/help/3042584/-proxy-address-address-is-already-being-used-error-message-in-exchange-online) bevat meer informatie over dit probleem op door met informatie over [verbinding maken met Exchange Online met externe PowerShell](https://technet.microsoft.com/library/jj984289.aspx).

Nadat de proxy-adres problemen zijn opgelost voor de betreffende gebruikers, zorg er dan voor dat forceren licentie-verwerking op de groep om te controleren of licenties nu opnieuw kunnen worden toegepast.

## <a name="how-do-you-force-license-processing-in-a-group-to-resolve-errors"></a>Hoe u de verwerking van de licentie in een groep fouten op te lossen afdwingen?

Afhankelijk van welke stappen u fouten op te lossen hebt gemaakt, kan het nodig zijn voor het verwerken van een groep bijwerken van de gebruikersstatus handmatig te activeren.

Bijvoorbeeld, als u een aantal licenties vrijgemaakt door het verwijderen van directe licentietoewijzingen van gebruikers, hebt u nodig voor het activeren van de verwerking van groepen die eerder volledig licentie voor alle leden van de gebruiker is mislukt. Zoeken naar de groep blade open hiertoe **licenties**, en selecteer de **opnieuw verwerken** knop op de werkbalk.

## <a name="next-steps"></a>Volgende stappen

Zie de volgende onderwerpen voor meer informatie over andere scenario's voor Licentiebeheer via groepen:

* [Licenties toewijzen aan een groep in Azure Active Directory](active-directory-licensing-group-assignment-azure-portal.md)
* [Wat is licentieverlening in Azure Active Directory op basis van groep?](active-directory-licensing-whatis-azure-portal.md)
* [Het migreren van afzonderlijke gebruikers met een licentie aan op basis van een groep licentieverlening in Azure Active Directory](active-directory-licensing-group-migration-azure-portal.md)
* [Azure Active Directory-licentieverlening voor aanvullende scenario's op basis van groep](active-directory-licensing-group-advanced.md)
