---
title: aaaResources, rollen en -toegangsbeheer in Azure Application Insights | Microsoft Docs
description: Eigenaren, bijdragers en lezers van inzicht in uw organisatie.
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 49f736a5-67fe-4cc6-b1ef-51b993fb39bd
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/17/2017
ms.author: bwren
ms.openlocfilehash: a6f6ca0443b5f60239f094606e124f856967d8ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="resources-roles-and-access-control-in-application-insights"></a>Resources, rollen en toegangsbeheer in Application Insights
U kunt bepalen wie heeft lees- en toegang tooyour gegevens bijwerken in Azure [Application Insights][start], met behulp van [toegangsbeheer op basis van rollen in Microsoft Azure](../active-directory/role-based-access-control-configure.md).

> [!IMPORTANT]
> Toewijzen van toegang toousers in Hallo **resourcegroep of abonnement** toowhich die uw toepassingsresource - niet in Hallo resource zelf behoort. Hallo toewijzen **Application Insights-onderdeelinzender** rol. Dit zorgt ervoor uniform beheer van toegang tooweb tests en waarschuwingen samen met de bron van uw toepassing. [Meer informatie](#access).
> 
> 

## <a name="resources-groups-and-subscriptions"></a>Bronnen, groepen en abonnementen
Eerste, sommige definities:

* **Resource** : een exemplaar van een Microsoft Azure-service. Uw Application Insights-resource verzamelt, analyseert en Hallo telemetriegegevens verzonden van uw toepassing worden weergegeven.  Andere soorten Azure-resources zijn web-apps, databases en virtuele machines.
  
    uw resources, opent u toosee hello [Azure Portal][portal], aanmelden en alle Resources op. toofind een resource, typ een gedeelte van de naam in het filterveld Hallo.
  
    ![Lijst met Azure-resources](./media/app-insights-resources-roles-access-control/10-browse.png)

<a name="resource-group"></a>

* [**Resourcegroep** ] [ group] -elke resource tooone groep behoort. Een groep is een handige manier toomanage verwante resources, met name voor toegangsbeheer. In één resource bijvoorbeeld geëxporteerde groep kan u een Web-App, een Application Insights resource toomonitor Hallo-app en een resource opslag tookeep geplaatst gegevens.

    ![Kies Bladeren, resourcegroepen, en vervolgens kiest u een groep](./media/app-insights-resources-roles-access-control/11-group.png)

* [**Abonnement** ](https://manage.windowsazure.com) -toouse Application Insights of andere Azure-resources, u zich aanmeldt tooan Azure-abonnement. Elke resourcegroep hoort tooone Azure-abonnement, waar u kiest uw pakket prijs en, als het een organisatie-abonnement, kiest u Hallo-leden en hun machtigingen voor toegang.
* [**Microsoft-account** ] [ account] -Hallo gebruikersnaam en het wachtwoord dat u toosign in tooMicrosoft Azure-abonnementen, XBox Live, Outlook.com en andere Microsoft-services.

## <a name="access"></a>Toegang beheren in de resourcegroep Hallo
Het is belangrijk toounderstand dat in de toevoeging toohello bron die u voor uw toepassing hebt gemaakt, er zijn ook afzonderlijke verborgen bronnen voor waarschuwingen en webtests. Ze zijn aangesloten toohello dezelfde [resourcegroep](#resource-group) als uw toepassing. Mogelijk hebt u andere Azure-services in, zoals websites of opslag is er ook plaatsen.

![Resources in Application Insights](./media/app-insights-resources-roles-access-control/00-resources.png)

toegang tot toocontrol toothese-bronnen die daarom het raadzaam naar:

* Toegangsbeheer op Hallo **resourcegroep of abonnement** niveau.
* Hallo toewijzen **Application Insights-onderdeelinzender** toousers rol. Hierdoor kunnen ze tooedit webtests, waarschuwingen en Application Insights-resources, zonder dat toegang tooany andere services in Hallo-groep.

## <a name="tooprovide-access-tooanother-user"></a>tooprovide toegang tooanother gebruiker
U moet de eigenaar van rechten toohello abonnement of resourcegroep Hallo hebben.

Hallo-gebruiker moet beschikken over een [Microsoft-Account][account], of u toegang tot tootheir [organisatie Microsoft-Account](../active-directory/sign-up-organization.md). U kunt opgeven toegang tooindividuals en toouser groepen gedefinieerd in Azure Active Directory.

#### <a name="navigate-toohello-resource-group"></a>Navigeer toohello resourcegroep
Er Hallo gebruiker toevoegen.

![In de resourceblade van uw toepassing, Essentials openen, open Hallo resourcegroep en er instellingen/gebruikers te selecteren. Klik op Add.](./media/app-insights-resources-roles-access-control/01-add-user.png)

Of u kan hoofdmap en Hallo gebruiker toohello abonnement toevoegen.

#### <a name="select-a-role"></a>Rol selecteren
![Selecteer een rol voor de nieuwe gebruiker Hallo](./media/app-insights-resources-roles-access-control/03-role.png)

| Rol | In de resourcegroep Hallo |
| --- | --- |
| Eigenaar |Alles, waaronder gebruikerstoegang kunt wijzigen |
| Inzender |Alles zijn, met inbegrip van alle resources kunt bewerken |
| Application Insights-onderdeelinzender |Application Insights-resources, webtests en waarschuwingen kunt bewerken |
| Lezer |Kunt bekijken maar niet van belang. |

De bewerking' omvat het maken, verwijderen en bijwerken:

* Resources
* Webtests
* Waarschuwingen
* Continue export

#### <a name="select-hello-user"></a>Hallo gebruiker selecteren

Als Hallo gebruiker die zich niet in Hallo directory, kunt u iedereen met een Microsoft-account kunt uitnodigen.
(Als deze services zoals Outlook.com, OneDrive, Windows Phone of XBox Live, beschikken over een Microsoft-account.)

## <a name="related-content"></a>Gerelateerde inhoud

* [Op rollen gebaseerde toegangsbeheer in Azure](../active-directory/role-based-access-control-configure.md)

<!--Link references-->

[account]: https://account.microsoft.com
[group]: ../azure-resource-manager/resource-group-overview.md
[portal]: https://portal.azure.com/
[start]: app-insights-overview.md
