---
title: aaaCreate en Azure portal dashboards delen | Microsoft Docs
description: Dit artikel wordt uitgelegd hoe dashboards toocreate en bewerken in hello Azure-portal.
services: azure-portal
documentationcenter: 
author: sewatson
manager: timlt
editor: tysonn
ms.assetid: ff422f36-47d2-409b-8a19-02e24b03ffe7
ms.service: multiple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 09/06/2016
ms.author: sewatson
ms.openlocfilehash: 0facd10fe3284d7ad9a9e29791e5af5b5b95c97f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-share-dashboards-in-hello-azure-portal"></a>Maken en delen van dashboards in hello Azure-portal
U kunt meerdere dashboards maken en ze delen met anderen die toegang tooyour Azure hebben abonnementen.  In dit artikel gaat door Hallo grondbeginselen van het maken, bewerken, publiceren en beheren van toegang toodashboards.

## <a name="create-a-dashboard"></a>Een dashboard maken
toocreate een dashboard, selecteer Hallo **nieuwe dashboard** knop volgende toohello huidige de naam van dashboard.  

![dashboard maken](./media/azure-portal-dashboards/new-dashboard.png)

Deze actie wordt een nieuw, leeg, persoonlijke dashboard gemaakt en wordt u aanpassing modus kunt u uw dashboard name en toevoegen of tegels opnieuw rangschikken.  In deze modus tegel Hallo samenvouwbare galerie vergt via Hallo linkernavigatievenster menu.  Hallo tegel galerij kunt u tegels vinden voor uw Azure-resources op verschillende manieren: u kunt bladeren door [resourcegroep](../azure-resource-manager/resource-group-overview.md#resource-groups), door resource typt, by [tag](../azure-resource-manager/resource-group-using-tags.md), of door te zoeken voor uw resource met de naam.  

![dashboard aanpassen](./media/azure-portal-dashboards/customize-dashboard.png)

Tegels toevoegen door slepen en neerzetten op Hallo dashboard oppervlak elke gewenste locatie.

Er is een nieuwe categorie met de naam **algemene** voor tegels die niet gekoppeld aan een bepaalde bron zijn.  In dit voorbeeld vastmaken we Hallo Markdown tegel.  U dit dashboard tegel tooadd aangepaste inhoud tooyour gebruiken.  Hallo tegel ondersteunt tekst zonder opmaak, [Markdown-syntaxis](https://daringfireball.net/projects/markdown/syntax), en een beperkte set van HTML-code.  (Voor de veiligheid, niet zoiets als injecteren `<script>` tags of bepaalde element stijlen van CSS die met het Hallo-portal conflicteren mogelijk gebruiken.) 

![markdown toevoegen](./media/azure-portal-dashboards/add-markdown.png)

## <a name="edit-a-dashboard"></a>Een dashboard bewerken
Nadat uw dashboard is gemaakt, kunt u tegels van Hallo tegel galerie of Hallo tegel representatie van blades vastmaken. Laten we vastmaken Hallo-weergave van de resourcegroep. U kunt ofwel bij het bladeren door Hallo item, of van de resourcegroepblade Hallo vastmaken. Beide benaderingen leiden tot Hallo tegel weergave van de resourcegroep Hallo vastmaken.

![Pincode toodashboard](./media/azure-portal-dashboards/pin-to-dashboard.png)

Na het vastmaken Hallo item, wordt deze weergegeven op uw dashboard.

![weergave-dashboard](./media/azure-portal-dashboards/view-dashboard.png)

Nu dat we een Markdown-tegel en een dashboard resource groep vastgemaakt toohello hebben, kunnen we vergroten of verkleinen en Hallo tegels rangschikken in een geschikte indeling.

Door de muiswijzer en '...' selecteren of met de rechtermuisknop op een tegel ziet u alle contextuele Hallo-opdrachten voor deze tegel. Standaard zijn er twee items:

1. **Losmaken van dashboard** – verwijdert Hallo tegel vanuit Hallo-dashboard
2. **Aanpassen** – krijgt de modus aanpassen

![tegel aanpassen](./media/azure-portal-dashboards/customize-tile.png)

Door te selecteren aanpassen, kunt u het formaat en tegels opnieuw rangschikken. tooresize een tegel, selecteer Hallo nieuwe grootte in Hallo contextafhankelijke menu, zoals wordt weergegeven in Hallo installatiekopie te volgen.

![tegel vergroten of verkleinen](./media/azure-portal-dashboards/resize-tile.png)

Of als Hallo tegel elke grootte ondersteunt, kunt u Hallo onder rechterhoek toohello gewenst grootte.

![tegel vergroten of verkleinen](./media/azure-portal-dashboards/resize-corner.png)

Na het formaat van tegels wijzigen, moet u Hallo-dashboard weergeven.

![tegel](./media/azure-portal-dashboards/view-tile.png)

Zodra u klaar bent met een dashboard aanpassen, selecteert u Hallo **gedaan aanpassen** tooexit modus aanpassen of met de rechtermuisknop op en selecteer **gedaan aanpassen** in het contextmenu Hallo.

## <a name="publish-a-dashboard-and-manage-access-control"></a>Een dashboard publiceren en beheren van toegangsbeheer
Wanneer u een dashboard maakt, is het persoonlijke standaard, wat betekent dat u bent Hallo enige die deze kan zien.  toomake deze zichtbaar tooothers gebruiken Hallo **Share** knop die wordt weergegeven naast de andere opdrachten dashboard Hallo.

![dashboard delen](./media/azure-portal-dashboards/share-dashboard.png)

U wordt gevraagd een abonnement en de resource-groep voor uw dashboard toobe gepubliceerd naar toochoose. tooseamlessly dashboards integreren in Hallo ecosysteem, we hebben gedeelde dashboards geïmplementeerd als Azure-resources (zodat u niet delen door een e-mailadres in te voeren).  Toegang tot toohello informatie weergegeven voor de meeste Hallo tegels in Hallo portal vallen [Azure Toegangsbeheerrol](../active-directory/role-based-access-control-configure.md). Gedeelde dashboards zijn vanuit een access control-perspectief niet anders als een virtuele machine of een opslagaccount.  

Stel dat u hebt een Azure-abonnement en leden van uw team zijn toegewezen rollen Hallo van **eigenaar**, **Inzender**, of **lezer** van Hallo-abonnement.  Gebruikers die eigenaar of inzenders kunnen toolist, weergave zijn, maken, wijzigen of verwijderen van dashboards binnen dat abonnement.  Gebruikers die lezers zijn kunnen toolist en bekijk de dashboards zijn, maar kunnen niet worden gewijzigd of verwijderd.  Gebruikers met leestoegang hebben kunnen toomake lokale bewerkingen tooa gedeelde dashboard zijn, maar er kan geen toopublish zijn die wijzigingen back toohello-server.  Ze kunnen echter een persoonlijke kopie van Hallo dashboard voor eigen gebruik maken.  Afzonderlijke tegels op Hallo dashboard afdwingen als altijd hun eigen regels voor toegang op basis van Hallo bronnen die ze met overeenkomen.  

Voor het gemak Hallo portal ervaring handleidingen u naar een patroon waar u dashboards in een resourcegroep plaatsen opgeroepen de publiceren **dashboards**.  

![dashboard publiceren](./media/azure-portal-dashboards/publish-dashboard.png)

U kunt een resourcegroep dashboard tooa bepaalde ook toopublish.  Hallo-toegangsbeheer voor dit dashboard komt overeen met de Hallo toegangsbeheer voor Hallo resourcegroep.  Gebruikers die kunnen resources in die resourcegroep Hallo beheren hebben ook toegang toohello dashboards.

![dashboard tooresource groep publiceren](./media/azure-portal-dashboards/publish-to-resource-group.png)

Nadat uw dashboard is gepubliceerd, Hallo **delen + toegang** besturingselementvenster wordt vernieuwen en u meer informatie over Hallo gepubliceerde dashboard, met inbegrip van een koppeling toomanage toegang toohello gebruikersdashboard weergeven.  Deze koppeling wordt gestart Hallo standaard rollen gebaseerd toegangsbeheer blade gebruikt toomanage toegang voor een Azure-resource.  U kunt altijd teruggaan toothis weergeven door te selecteren **Share**.

![toegang beheren](./media/azure-portal-dashboards/manage-access.png)

## <a name="next-steps"></a>Volgende stappen
* toomanage resources, Zie [beheren Azure-resources via de portal](../azure-resource-manager/resource-group-portal.md).
* toodeploy resources, Zie [implementeren van resources met Resource Manager-sjablonen en Azure-portal](../azure-resource-manager/resource-group-template-deploy-portal.md).

