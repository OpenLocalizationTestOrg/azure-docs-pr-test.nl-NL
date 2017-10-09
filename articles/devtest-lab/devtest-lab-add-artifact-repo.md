---
title: aaaAdd een Git-opslagplaats tooa lab in Azure DevTest Labs | Microsoft Docs
description: Toevoegen van een GitHub of Visual Studio Team Services Git-opslagplaats voor uw aangepaste artefacten-bron in Azure DevTest Labs
services: devtest-lab,virtual-machines,visual-studio-online
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 01b459f7-eaf2-45a8-b4b5-2c0a821b33c8
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/11/2017
ms.author: tarcher
ms.openlocfilehash: e590559ffb2d497e39823e35c3f66974f42f13c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-git-repository-toostore-custom-artifacts-and-azure-resource-manager-templates"></a>Voeg een Git-opslagplaats toostore aangepaste artefacten en Azure Resource Manager-sjablonen

Als u wilt dat te[aangepaste artefacten maken](devtest-lab-artifact-author.md) voor Hallo VM's in uw lab of [gebruik van Azure Resource Manager-sjablonen toocreate een aangepaste testomgeving](devtest-lab-create-environment-from-arm.md), moet u ook een persoonlijke Git-opslagplaats tooinclude toevoegen Hallo artefacten of Azure Resource Manager-sjablonen die uw team maakt. Hallo-opslagplaats kan worden gehost op [GitHub](https://github.com) of op [Visual Studio Team Services (VSTS)](https://visualstudio.com).

We hebt opgegeven een [Github-opslagplaats van artefacten](https://github.com/Azure/azure-devtestlab/tree/master/Artifacts) die u kunt implementeren als- of aanpassen voor uw labs. Wanneer u een artefact maken of aanpassen, moet u ze niet opslaan in de openbare opslagplaats Hallo – moet u uw eigen persoonlijke opslagplaats maken. 

Wanneer u een virtuele machine maakt, kunt u hello Azure Resource Manager-sjabloon opslaan, aanpassen als u wilt en gebruikt u deze later tooeasily meer virtuele machines maken. Uw aangepaste sjablonen voor Azure Resource Manager, moet u uw eigen persoonlijke opslagplaats toostore maken.  

* hoe toocreate GitHub-opslagplaats zien toolearn [GitHub Bootcamp](https://help.github.com/categories/bootcamp/).
* hoe een Team Services-project met een Git-opslagplaats toocreate zien toolearn [tooVisual Studio Team Services verbinding](https://www.visualstudio.com/get-started/setup/connect-to-visual-studio-online).

Hallo toont volgende schermafbeelding een voorbeeld van hoe een opslagplaats met artefacten in GitHub eruit:  
![Voorbeeld GitHub-repo-artefacten](./media/devtest-lab-add-repo/devtestlab-github-artifact-repo-home.png)

## <a name="get-hello-repository-information-and-credentials"></a>Hallo-opslagplaats informatie en referenties ophalen
tooadd een opslagplaats tooyour lab, moet u eerst ophalen bepaalde gegevens van uw opslagplaats. Hallo volgende secties helpen u bij het ophalen van deze informatie voor opslagplaatsen gehost op GitHub en Visual Studio Team Services.

### <a name="get-hello-github-repository-clone-url-and-personal-access-token"></a>Hallo GitHub-opslagplaats kloon-URL en personal access token ophalen
Ga als volgt tooget hello GitHub-opslagplaats kloon-URL en persoonlijke toegangstoken:

1. Blader toohello introductiepagina van Hallo GitHub-opslagplaats met Hallo artefacten of Sjabloondefinities van Azure Resource Manager.
2. Selecteer **klonen of downloaden**.
3. Selecteer Hallo knop toocopy hello **url voor HTTPS-kloon** toohello Klembord, en het Hallo-URL voor later gebruik opslaan.
4. Selecteer Hallo profiel installatiekopie in Hallo rechterbovenhoek van GitHub, en selecteer **instellingen**.
5. In Hallo **persoonlijke instellingen** menu op Hallo links, selecteer **persoonlijke toegangstokens**.
6. Selecteer **nieuw token genereren**.
7. Op Hallo **nieuwe persoonlijke toegangstoken** pagina, voert u een **Token beschrijving**, Hallo standaarditems in Hallo accepteren **Selecteer scopes**, en kies vervolgens **genereren Token**.
8. Hallo gegenereerd token niet opslaan omdat u deze later nodig.
9. GitHub kunt u nu sluiten.   
10. Doorgaan toohello [verbinding maken met uw lab toohello opslagplaats](#connect-your-lab-to-the-repository) sectie.

### <a name="get-hello-visual-studio-team-services-repository-clone-url-and-personal-access-token"></a>Hallo Visual Studio Team Services opslagplaats kloon-URL en personal access token ophalen
Ga als volgt tooget Hallo Visual Studio Team Services opslagplaats kloon-URL en persoonlijke toegangstoken:

1. Open Hallo-startpagina van de verzameling van uw team (bijvoorbeeld `https://contoso-web-team.visualstudio.com`), en selecteer vervolgens uw project.
2. Selecteer op de startpagina van Hallo project **Code**.
3. tooview Hallo-kloon-URL, op Hallo project **Code** pagina **kloon**.
4. Hallo URL opslaan als u dit later in deze zelfstudie nodig.
5. toocreate een Personal Access Token, selecteer **Mijn profiel** in het vervolgkeuzemenu voor het gebruikersaccountmenu Hallo.
6. Selecteer op de pagina profiel hello, **beveiliging**.
7. Op Hallo **beveiliging** tabblad **toevoegen**.
8. In Hallo **maken van een persoonlijk toegangstoken** pagina:

   * Voer een **beschrijving** voor Hallo-token.
   * Selecteer **180 dagen** van Hallo **verloopt In** lijst.
   * Kies **alle toegankelijke accounts** van Hallo **Accounts** lijst.
   * Kies Hallo **alle scopes** optie.
   * Kies **Token aanmaken**.
9. Als u klaar bent Hallo nieuw token wordt weergegeven in Hallo **persoonlijke toegangstokens** lijst. Selecteer **kopie Token**, en sla Hallo token waarde voor later gebruik.
10. Doorgaan toohello [verbinding maken met uw lab toohello opslagplaats](#connect-your-lab-to-the-repository) sectie.

## <a name="connect-your-lab-toohello-repository"></a>Verbinding maken met uw lab toohello opslagplaats
1. Meld u aan toohello [Azure-portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).
2. Selecteer **meer Services**, en selecteer vervolgens **DevTest Labs** uit Hallo-lijst.
3. Selecteer de gewenste lab Hallo in lijst Hallo van labs.   
4. Selecteer in het linkerdeelvenster hello, **configuratie en het beleid**.
5. Op de Hallo lab **configuratie en het beleid** gebied, selecteer **opslagplaatsen**.
6. Op Hallo **opslagplaatsen** gebied, selecteer **+ toevoegen**.

    ![Knop opslagplaats toevoegen](./media/devtest-lab-add-repo/devtestlab-add-repo.png)
7. Op Hallo tweede **opslagplaatsen** pagina, geeft u Hallo volgende informatie:

   * **Naam** -Voer een naam voor het Hallo-opslagplaats.
   * **GIT kloon-Url** -Voer Hallo Git HTTPS-kloon-URL die u eerder hebt gekopieerd in GitHub of Visual Studio Team Services.
   * **Vertakking** -Voer Hallo vertakking tooget uw definities.
   * **Personal Access Token** -Voer Hallo persoonlijke toegangstoken u eerder hebt verkregen in GitHub of Visual Studio Team Services.
   * **Paden voor mappen** -Voer ten minste één map pad relatief toohello kloon-URL die uw artefacten of Sjabloondefinities van Azure Resource Manager-bevat. Wanneer u een submap opgeeft, zorg ervoor dat tooinclude Hallo schuine streep in pad naar de Hallo.

     ![Opslagplaatsen gebied](./media/devtest-lab-add-repo/devtestlab-repo-blade.png)
8. Selecteer **Opslaan**.

## <a name="next-steps"></a>Volgende stappen
Nadat u uw persoonlijke Git-opslagplaats hebt gemaakt, kunt u een of beide van de volgende hello, afhankelijk van uw behoeften doen:
* Store uw [aangepaste artefacten](devtest-lab-artifact-author.md), die u kunt later toocreate nieuwe virtuele machines.
* [Meerdere VM-omgevingen en PaaS-resources met Azure Resource Manager-sjablonen maken](devtest-lab-create-environment-from-arm.md) en Hallo sjablonen op te slaan in de opslagplaats van uw persoonlijke.

Wanneer u een virtuele machine maakt, kunt u verifiëren dat het Hallo-artefacten of sjablonen tooyour Git-opslagplaats worden toegevoegd. Ze zijn direct in Hallo lijst met artefacten of sjablonen, met de naam van uw persoonlijke opslagplaats weergegeven Hallo kolom Hallo bron geeft Hallo beschikbaar. 

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

### <a name="related-blog-posts"></a>Verwante blogberichten
* [Hoe tootroubleshoot artefacten in Azure DevTest Labs mislukt](devtest-lab-troubleshoot-artifact-failure.md)
* [Deelnemen aan een VM-tooexisting AD-domein met een resource manager-sjabloon in Azure DevTest Labs](http://www.visualstudiogeeks.com/blog/DevOps/Join-a-VM-to-existing-AD-domain-using-ARM-template-AzureDevTestLabs)
