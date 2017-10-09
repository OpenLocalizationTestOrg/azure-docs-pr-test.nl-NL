---
title: aaaHow beheren van gebruikersaccounts in Azure API Management | Microsoft Docs
description: Meer informatie over hoe toocreate of uitnodiging gebruikers in Azure API Management
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 078abfa5-1e4f-4c9d-b9c7-a172bd19c1a2
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 3966f4454e29621d7c615beefee352ec91b48b2e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-user-accounts-in-azure-api-management"></a>Hoe toomanage gebruikersaccounts in Azure API Management
In API Management zijn ontwikkelaars Hallo gebruikers Hallo API's die u met behulp van API Management. Deze handleiding bevat toohow toocreate en uitnodiging ontwikkelaars toouse Hallo API's en producten toothem beschikbaar te maken met uw API Management-exemplaar. Zie voor informatie over het beheren van gebruikersaccounts programmatisch Hallo [entiteit gebruiker](https://msdn.microsoft.com/library/azure/dn776330.aspx) documentatie in Hallo [API Management REST](https://msdn.microsoft.com/library/azure/dn776326.aspx) verwijzing.

## <a name="create-developer"></a>Maken van een nieuwe ontwikkelaar
een nieuwe ontwikkelaar toocreate klikt u op **publicatieportal** in hello Azure-Portal voor uw API Management-service. Hiermee gaat u toohello API Management-publicatieportal. Als u nog geen exemplaar van API Management-service hebt gemaakt, raadpleegt u [API Management service-exemplaar maken] [ Create an API Management service instance] in Hallo [aan de slag met Azure API Management] [ Get started with Azure API Management] zelfstudie.

![Publicatieportal][api-management-management-console]

Klik op **gebruikers** van Hallo **API Management** menu op Hallo links en klik vervolgens op **gebruiker toevoegen**.

![Ontwikkelaars maken][api-management-create-developer]

Voer Hallo **e**, **wachtwoord**, en **naam** voor nieuwe developer Hallo en klik op **opslaan**.

![Ontwikkelaars maken][api-management-add-new-user]

De van de zojuist gemaakte ontwikkelaarsaccounts zijn standaard **Active**, en die zijn gekoppeld aan Hallo **ontwikkelaars** groep.

![Nieuwe ontwikkelaars][api-management-new-developer]

Ontwikkelaarsaccounts die zich in een **active** status gebruikte tooaccess kan worden alle Hallo-API's waarvoor ze abonnementen hebben. Zie tooassociate Hallo nieuw gemaakte developer met extra groepen [hoe tooassociate groepen met ontwikkelaars][How tooassociate groups with developers].

## <a name="invite-developer"></a>Een ontwikkelaar uitnodigen
tooinvite een ontwikkelaar, klikt u op **gebruikers** van Hallo **API Management** menu op Hallo links en klik vervolgens op **gebruiker uit te nodigen**.

![Developer uit te nodigen][api-management-invite-developer]

Voer Hallo naam en e-mailadres van de ontwikkelaar Hallo van, en klik op **uitnodigen**.

![Developer uit te nodigen][api-management-invite-developer-window]

Een bevestigingsbericht wordt weergegeven, maar Hallo zojuist uitgenodigd developer niet wordt weergegeven in lijst Hallo pas nadat ze Hallo uitnodiging accepteren. 

![Bevestiging uitnodigen][api-management-invite-developer-confirmation]

Als een ontwikkelaar uitgenodigd is, wordt een e-mailbericht toohello developer verzonden. Dit e-mailbericht met een sjabloon wordt gegenereerd en kan worden aangepast. Zie voor meer informatie [e-mailsjablonen configureren][Configure email templates].

Zodra het Hallo-uitnodiging is geaccepteerd, actief Hallo account.

## <a name="block-developer"></a> Deactiveren of opnieuw activeren een ontwikkelaarsaccount
Gemaakte of uitgenodigde ontwikkelaarsaccounts zijn standaard **Active**. een ontwikkelaarsaccount toodeactivate klikt u op **blok**. tooreactivate een geblokkeerde ontwikkelaarsaccount, klikt u op **activeren**. Een geblokkeerde ontwikkelaarsaccount kan geen toegang tot de ontwikkelaarsportal Hallo of alle API's aanroepen. toodelete een gebruikersaccount, klik op **verwijderen**.

![Blok-ontwikkelaars][api-management-new-developer]

## <a name="reset-a-user-password"></a>Een gebruikerswachtwoord opnieuw instellen
tooreset hello wachtwoord voor een gebruikersaccount, klik op Hallo-naam van het Hallo-account.

![Wachtwoord opnieuw instellen][api-management-view-developer]

Klik op **wachtwoord opnieuw instellen** toosend een koppeling toohello gebruiker tooreset hun wachtwoord.

![Wachtwoord opnieuw instellen][api-management-reset-password]

tooprogrammatically werken met gebruikersaccounts, Zie Hallo [entiteit gebruiker](https://msdn.microsoft.com/library/azure/dn776330.aspx) documentatie in Hallo [API Management REST](https://msdn.microsoft.com/library/azure/dn776326.aspx) verwijzing. een gebruiker account wachtwoord tooa specifieke waarde tooreset, kunt u Hallo [bijwerken van een gebruiker](https://msdn.microsoft.com/library/azure/dn776330.aspx#UpdateUser) bewerking en geef de gewenste wachtwoord Hallo.

## <a name="pending-verification"></a>Verificatie van in behandeling
![Verificatie van in behandeling][api-management-pending-verification]

## <a name="next-steps"> </a>Volgende stappen
Zodra een ontwikkelaarsaccount is gemaakt, kunt u aan functies koppelen en het abonneren tooproducts en API's. Zie voor meer informatie [hoe toocreate en gebruik groepen][How toocreate and use groups].

[api-management-management-console]: ./media/api-management-howto-create-or-invite-developers/api-management-management-console.png
[api-management-add-new-user]: ./media/api-management-howto-create-or-invite-developers/api-management-add-new-user.png
[api-management-create-developer]: ./media/api-management-howto-create-or-invite-developers/api-management-create-developer.png
[api-management-invite-developer]: ./media/api-management-howto-create-or-invite-developers/api-management-invite-developer.png
[api-management-new-developer]: ./media/api-management-howto-create-or-invite-developers/api-management-new-developer.png
[api-management-invite-developer-window]: ./media/api-management-howto-create-or-invite-developers/api-management-invite-developer-window.png
[api-management-invite-developer-confirmation]: ./media/api-management-howto-create-or-invite-developers/api-management-invite-developer-confirmation.png
[api-management-pending-verification]: ./media/api-management-howto-create-or-invite-developers/api-management-pending-verification.png
[api-management-view-developer]: ./media/api-management-howto-create-or-invite-developers/api-management-view-developer.png
[api-management-reset-password]: ./media/api-management-howto-create-or-invite-developers/api-management-reset-password.png


[Create a new developer]: #create-developer
[Invite a developer]: #invite-developer
[Deactivate or reactivate a developer account]: #block-developer
[Next steps]: #next-steps
[How toocreate and use groups]: api-management-howto-create-groups.md
[How tooassociate groups with developers]: api-management-howto-create-groups.md#associate-group-developer

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Configure email templates]: api-management-howto-configure-notifications.md#email-templates
