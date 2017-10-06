---
title: toegang tot bronnen in Azure aaaUnderstanding | Microsoft Docs
description: In dit onderwerp worden enkele concepten uitgelegd over het gebruik van abonnement beheerders toocontrol brontoegang in Hallo volledige Azure-portal
services: active-directory
documentationcenter: 
author: curtand
manager: femila
ms.assetid: 174f1706-b959-4230-9a75-bf651227ebf6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/24/2017
ms.author: curtand
ms.custom: oldportal;it-pro;
ms.openlocfilehash: 06b9c4166bdea849faae67cae3146c6c278deb97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="understanding-resource-access-in-azure"></a>Wat is de toegang tot bronnen in Azure?
> [!IMPORTANT]
> Microsoft raadt aan dat u Azure AD beheren met Hallo [Azure AD-beheercentrum](https://aad.portal.azure.com) in Hallo hello Azure-portal in plaats van de klassieke Azure-portal waarnaar wordt verwezen in dit artikel. Hello Azure portal biedt [toegangsbeheer op basis van rollen](role-based-access-control-configure.md) zodat Azure-resources preciezer kunnen worden beheerd.
> 
> 

In oktober 2013 Hallo klassieke Azure-portal en Service Management-API's zijn geïntegreerd met Azure Active Directory in volgorde toolay Hallo basis voor het verbeteren van de gebruikerservaring Hallo voor het beheren van toegang tot tooAzure bronnen. Azure Active Directory biedt al geweldige mogelijkheden, zoals het beheer van gebruikers, lokale directory-synchronisatie, meervoudige verificatie en toegangsbeheer van toepassing. Natuurlijk, deze moeten ook worden beschikbaar gemaakt voor het beheer van Azure-resources lineaire.

Toegangsbeheer in Azure wordt gestart vanuit het oogpunt van facturering van. Hallo-eigenaar van een Azure-account toegankelijk via Hallo [Azure-Accountcentrum](https://account.windowsazure.com/subscriptions), Hallo Account Administrator (AA) is. Abonnementen zijn een container voor facturering, maar ze ook fungeren als een beveiligingsgrens: elk abonnement heeft een Service Administrator (SA) die u kunt toevoegen, verwijderen en wijzigen van de Azure-resources in het desbetreffende abonnement met behulp van Hallo [klassieke Azure-portal](https://manage.windowsazure.com/). Hallo standaard SA van een nieuw abonnement Hallo AA is, maar Hallo AA Hallo SA in hello Azure Accounts Center kunt wijzigen.

<br><br>![Azure-Accounts][1]

Abonnementen hebben ook een koppeling naar een map. Hallo directory definieert een set van gebruikers. Deze kunnen gebruikers van Hallo werk of school die Hallo directory gemaakt of ze kunnen externe gebruikers (dat wil zeggen, een Microsoft-Accounts). Abonnementen zijn toegankelijk voor een subset van de directorygebruikers die zijn toegewezen als Service-beheerder (SA) of Medebeheerder (CA); Hallo alleen uitzondering is dat, omwille van de oudere Microsoft-Accounts (voorheen Windows Live ID) kan worden toegewezen als SA of CA zonder aanwezig is in het Hallo-directory.

<br><br>![Toegangsbeheer in Azure][2]

Functionaliteit in de klassieke Azure-portal Hallo kunnen SA's dat u bent aangemeld met een Microsoft-Account toochange Hallo directory waaraan een abonnement is gekoppeld met behulp van Hallo **Directory bewerken** opdracht op Hallo **Abonnementen** pagina in **instellingen**. Houd er rekening mee dat deze bewerking gevolgen voor toegangsbeheer Hallo van het abonnement heeft.

> [!NOTE]
> Hallo **Directory bewerken** opdracht in Hallo klassieke Azure portal is niet beschikbaar toousers die zijn aangemeld met een werk- of schoolaccount omdat deze accounts kunnen aanmelden alleen toohello directory toowhich ze behoren.
> 
> 

<br><br>![Eenvoudige Gebruikersstroom voor aanmelding][3]

In Hallo eenvoudige zaak, wordt een organisatie (bijvoorbeeld Contoso) afdwingen facturering en toegangsbeheer voor het hele Hallo dezelfde van abonnementen set. Hallo-map is gekoppeld toosubscriptions die eigendom zijn van één Azure-Account. Gebruikers zien bij geslaagde aanmelding toohello klassieke Azure-portal, twee verzamelingen van bronnen (beschreven in oranje in de vorige afbeelding Hallo):

* Directory's waar hun gebruikersaccount bestaat (afkomstig is of als een foreign principal toegevoegd). Houd er rekening mee Hallo map gebruikt voor aanmelding bij is niet relevant toothis berekening, zodat uw directory's altijd weergegeven worden ongeacht waar u bent aangemeld.
* Resources die deel uitmaken van de abonnementen die zijn gekoppeld met Hallo directory gebruikt voor aanmelding en die gebruiker Hallo toegankelijk (waar ze zijn een SA- of CA).

<br><br>![Gebruiker met meerdere abonnementen en mappen][4]

Gebruikers met abonnementen op meerdere mappen hebben Hallo mogelijkheid tooswitch Hallo huidige context van Hallo klassieke Azure-portal met behulp van Hallo abonnementfilter. Onder Hallo dekt, resulteert dit in een afzonderlijke aanmelding tooa andere directory, maar dit wordt bereikt naadloos met eenmalige aanmelding (SSO).

Bewerkingen zoals het verplaatsen van resources tussen abonnementen kunnen worden moeilijker als gevolg van deze weergave één map van abonnementen. tooperform hello resource overdracht mogelijk toofirst hello gebruiken **Directory bewerken** opdracht op Hallo abonnementen pagina in **instellingen** tooassociate Hallo abonnementen toohello dezelfde directory .

## <a name="next-steps"></a>Volgende stappen
* toolearn informatie over hoe beheerders voor een Azure-abonnement toochange zien [hoe tooadd of wijzig Azure-beheerdersrollen](../billing/billing-add-change-azure-subscription-administrator.md)
* Zie voor meer informatie over hoe tooyour Azure-abonnement in Azure Active Directory is gekoppeld, [hoe Azure-abonnementen worden gekoppeld aan Azure Active Directory](active-directory-how-subscriptions-associated-directory.md)
* Voor meer informatie over het tooassign rollen in Azure AD, Zie [beheerdersrollen toewijzen in Azure Active Directory](active-directory-assign-admin-roles.md)

<!--Image references-->
[1]: ./media/active-directory-understanding-resource-access/IC707931.png
[2]: ./media/active-directory-understanding-resource-access/IC707932.png
[3]: ./media/active-directory-understanding-resource-access/IC707933.png
[4]: ./media/active-directory-understanding-resource-access/IC707934.png
