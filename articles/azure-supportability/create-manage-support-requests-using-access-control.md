---
title: aaaAzure op rollen gebaseerde toegangsbeheer (RBAC) toocontrol rechten toocreate raadplegen en beheren van ondersteuningsaanvragen | Microsoft Docs
description: Azure op rollen gebaseerde toegangsbeheer (RBAC) toocontrol rechten toocreate raadplegen en beheren van aanvragen voor ondersteuning
author: ganganarayanan
ms.author: gangan
ms.date: 1/31/2017
ms.topic: article
ms.service: microsoft-docs
ms.assetid: 58a0ca9d-86d2-469a-9714-3b8320c33cf5
ms.openlocfilehash: c68a699ac870fa6bf371deb8ed0424848f39acf0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-role-based-access-control-rbac-toocontrol-access-rights-toocreate-and-manage-support-requests"></a>Azure op rollen gebaseerde toegangsbeheer (RBAC) toocontrol rechten toocreate raadplegen en beheren van aanvragen voor ondersteuning

[Op rollen gebaseerde toegangsbeheer (RBAC)](https://docs.microsoft.com/azure/active-directory/role-based-access-control-what-is) kunt Geavanceerd toegangsbeheer voor Azure.
Ondersteuning voor het maken van de aanvraag in hello Azure-portal [portal.azure.com](https://portal.azure.com), maakt gebruik van Azure RBAC-model toodefine die maken en beheren van aanvragen voor ondersteuning.
Toegang is verleend door toe te wijzen Hallo juiste RBAC-rol toousers, groepen en toepassingen op een bepaalde scope, kan dit een abonnement, resourcegroep of een resource.

Voorbeeld: als een eigenaar van de groep resource met leesmachtigingen op Hallo abonnementsbereik u alle Hallo resources onder de resourcegroep hello, zoals websites, virtuele machines en subnetten kunt beheren.
Echter, wanneer u een ondersteuningsaanvraag in voor de bron van de virtuele machine Hallo toocreate, u tegenkomt Hallo volgende fout

![Abonnement-fout](./media/create-manage-support-requests-using-access-control/subscription-error.png)

In het beheer van de aanvraag van ondersteuning u moet de machtiging schrijven of een rol heeft die over Hallo actie Microsoft.Support/* Hallo abonnement bereik toobe kunnen toocreate ondersteunen en ondersteuningsaanvragen beheren.

Hallo volgende artikel wordt uitgelegd hoe u Azure aangepaste op rollen gebaseerde toegangsbeheer (RBAC) toocreate gebruiken en beheren ondersteuningsaanvragen in hello Azure-portal.

## <a name="getting-started"></a>Aan de slag

Hallo bovenstaande voorbeeld gebruikt, zou u kunnen toocreate een verzoek om ondersteuning voor uw resource als u een aangepaste RBAC-rol op Hallo abonnement zijn toegewezen door de eigenaar van de Hallo-abonnement.
[Aangepaste RBAC-rollen](https://azure.microsoft.com/documentation/articles/role-based-access-control-custom-roles/) kunnen worden gemaakt met Azure PowerShell, Azure-opdrachtregelinterface (CLI) en Hallo REST-API.

Hallo acties eigenschap van een aangepaste rol geeft hello Azure-bewerkingen toowhich Hallo rol toegang verleent.
een aangepaste rol voor het beheer van de aanvraag ondersteuning toocreate, Hallo rol moet beschikken over Hallo actie Microsoft.Support/*

Hier volgt een voorbeeld van een aangepaste rol die u kunt toocreate gebruiken en beheren ondersteuning aanvragen.
We deze rol 'Ondersteuning vragen Inzender' hebt genoemd en dat is hoe we de aangepaste rol toohello in dit artikel verwijzen.

``` Json
{
    "Name":  "Support Request Contributor",
    "Id":  "1f2aad59-39b0-41da-b052-2fb070bd7942",
    "IsCustom":  true,
    "Description":  "Lets you create and manage support tickets.",
    "Actions":  [
                    "Microsoft.Support/*"
                ],
    "NotActions":  [
                   ],
    "AssignableScopes":  [
                             "/"
                         ]
}
```

Hallo stappen die worden beschreven in [in deze video](https://www.youtube.com/watch?v=-PaBaDmfwKI) toolearn hoe toocreate een aangepaste beveiligingsrol voor uw abonnement.

## <a name="create-and-manage-support-requests-in-hello-azure-portal"></a>Maken en beheren van ondersteuningsaanvragen in hello Azure-portal

Voorbeeld: u bent Hallo eigenaar van het abonnement "Visual Studio MSDN-abonnement."
Jan is de peer die is een resource-eigenaar toosome van resourcegroepen Hallo in dit abonnement en machtiging toohello abonnement is gelezen.
U wilt toogive toegang tooyour peer, Jan, Hallo mogelijkheid toocreate en ondersteuningstickets voor Hallo resources onder dit abonnement beheren.

1. de eerste stap Hallo is toogo toohello abonnement en onder 'Instellingen' ziet u een lijst met gebruikers. Klik op Hallo gebruiker Jan die leestoegang hebben op Hallo abonnement en gaan we een nieuwe aangepaste rol toohim toewijzen.

    ![Functie toevoegen](./media/create-manage-support-requests-using-access-control/add-role.png)

2. Klik op "Toevoegen" onder Hallo 'Gebruikers' blade. Selecteer Hallo aangepaste rol 'Ondersteuning vragen Inzender' in hello lijst met rollen

    ![Ondersteuning voor de rol van Inzender toevoegen](./media/create-manage-support-requests-using-access-control/add-support-contributor-role.png)

3. Na het selecteren van de rolnaam hello, klik op 'Gebruikers toevoegen' en Voer Hallo Joe's e-referenties. Klik op 'Selecteren'

    ![Gebruikers toevoegen](./media/create-manage-support-requests-using-access-control/add-users.png)

4. Klik op 'Ok' tooproceed

    ![Toegang toevoegen](./media/create-manage-support-requests-using-access-control/add-access.png)

5. U ziet nu Hallo-gebruiker met Hallo toegevoegde aangepaste rol 'Ondersteuning vragen Inzender' Hallo-abonnement waarvoor u Hallo eigenaar bent

    ![Toegevoegde gebruiker](./media/create-manage-support-requests-using-access-control/user-added.png)

    Wanneer de Hallo portal Jan zich aanmeldt, ziet hij Hallo abonnement toowhich die hij is toegevoegd.

7. Jan klikt op 'Nieuw ondersteuningsverzoek' Hallo 'Help en ondersteuning voor' blade en ondersteuningsaanvragen kunt maken voor 'Visual Studio Ultimate met MSDN'

    ![Nieuw ondersteuningsverzoek](./media/create-manage-support-requests-using-access-control/new-support-request.png)

8. Te klikken op 'Alle ondersteunen aanvragen' Jan overzicht Hallo van ondersteuningsaanvragen gemaakt voor dit abonnement ![Aanvraagdetails weergeven](./media/create-manage-support-requests-using-access-control/case-details-view.png)

## <a name="remove-support-request-access-in-hello-azure-portal"></a>Toegang voor ondersteuning aanvragen in hello Azure-portal verwijderen

Omdat deze mogelijk toogrant toegang tooa gebruiker toocreate en ondersteuningsaanvragen beheren, is het mogelijk tooremove-toegang voor ook Hallo-gebruiker.
tooremove mogelijkheid toocreate Hallo ondersteuningsaanvragen beheren, gaat u toohello abonnement, klik op 'Instellingen' en op Hallo gebruiker (in dit geval Jan).
Met de rechtermuisknop op Hallo rolnaam, 'Ondersteuning vragen Inzender' en klik op 'Verwijderen'

![Ondersteuning aanvragen voor toegang verwijderen](./media/create-manage-support-requests-using-access-control/remove-support-request-access.png)

Wanneer Jan toohello portal aanmeldt en toocreate ondersteuning aan te vragen probeert, hij Hallo volgende fout aangetroffen

![Abonnement fout-2](./media/create-manage-support-requests-using-access-control/subscription-error-2.png)

Jan niet zien alle aanvragen ondersteunen wanneer hij klikt op "Alle ondersteuning aanvragen"

![Aanvraagdetails weergave-2](./media/create-manage-support-requests-using-access-control/case-details-view-2.png)
