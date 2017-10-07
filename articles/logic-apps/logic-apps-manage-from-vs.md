---
title: aaaManage logische apps in Visual Studio - Azure Logic Apps | Microsoft Docs
description: Logische apps en andere Azure activa met Visual Studio Cloud Explorer beheren
author: klam
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 12/19/2016
ms.author: LADocs; klam
ms.openlocfilehash: 419f83eb062b56e4ac2642dea4de1a025f747521
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-your-logic-apps-with-visual-studio-cloud-explorer"></a>Beheren van uw logische apps met Visual Studio Cloud Explorer

Hoewel hello [Azure-portal](https://portal.azure.com/) een uitstekende manier biedt u toodesign en Azure Logic Apps beheren, kunt u Visual Studio Cloud Explorer voor het beheren van veel Azure activa, met inbegrip van logische apps. Visual Studio Cloud Explorer kunt u bladeren, beheren, bewerken en download gepubliceerde logic apps. Beheertaken omvatten inschakelen, uitschakelen en historie weergeven die worden uitgevoerd. 

Voordat u kunt toegang tot en beheren van uw logische apps in Visual Studio, installeren en configureren van deze Visual Studio-hulpprogramma's voor Azure Logic Apps. 

## <a name="prerequisites"></a>Vereisten

* [Visual Studio 2015 of Visual Studio 2017](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx)
* [Nieuwste Azure SDK](https://azure.microsoft.com/downloads/) (2.9.1 of hoger)
* [Visual Studio Cloud Explorer](https://marketplace.visualstudio.com/items?itemName=MicrosoftCloudExplorer.CloudExplorerforVisualStudio2015)
* De website toohello toegang wanneer u de ontwerpfunctie Hallo

## <a name="install-visual-studio-tools-for-logic-apps"></a>Installeer Visual Studio-hulpprogramma's voor Logic Apps

Nadat u Hallo vereisten hebt geïnstalleerd, downloaden en installeren van hello Azure Logic Apps-Tools voor Visual Studio.

1. Open Visual Studio. Op Hallo **extra** selecteert u **uitbreidingen en Updates**.
2. Vouw Hallo **Online** categorie zodat u online in Hallo Visual Studio-galerie zoeken kunt.
3. Blader of zoek naar **Logic Apps** totdat u **Azure Logic Apps-Tools voor Visual Studio**.
4. toodownload en installatie Hallo-extensie, klikt u op **downloaden**.
5. Visual Studio starten na de installatie.

> [!NOTE]
> toodownload hello Azure Logic Apps-Tools voor Visual Studio gaat u rechtstreeks toohello [Visual Studio Marketplace](https://visualstudiogallery.msdn.microsoft.com/e25ad307-46cf-412e-8ba5-5b555d53d2d9).

## <a name="browse-for-logic-apps-in-cloud-explorer"></a>Bladeren naar logische apps in de Cloud Explorer

1.  tooopen Cloud Explorer op Hallo **weergave** menu kiezen **Cloud Explorer**.
2.  Blader naar uw logische app, resourcegroep of brontype. 

    * Als u bladert per resourcetype, selecteert u uw Azure-abonnement, vouw Hallo **Logic Apps** uit en selecteer uw logische app. 
    * Als u door de resourcegroep bladeren, vouwt u de resourcegroep Hallo met uw logische app en selecteer uw logische app.

    tooview opdrachten voor uw logische app, met de rechtermuisknop op uw logische app of aan de onderkant van de Hallo van Cloud Explorer, kiezen uit Hallo **acties** menu.

    ![Blader naar uw logische app](./media/logic-apps-manage-from-vs/browse.png)

## <a name="edit-your-logic-app-with-logic-apps-designer"></a>Uw logische app met Logic Apps Designer bewerken

Vanuit de Cloud Explorer kunt u een momenteel geïmplementeerde logische app openen in Hallo dezelfde designer die u in hello Azure-portal gebruiken. 

* tooedit uw logische app, in de Cloud Explorer met de rechtermuisknop op uw logische app en selecteer **geopend met Logic App Editor**. 

* toopublish uw toohello updates cloud, kies **publiceren**. 

* Kies een nieuw run toostart **uitvoeren Trigger**.

![Logic Apps Designer](./media/logic-apps-manage-from-vs/designer.png)

Vanuit Hallo designer kunt u ook **downloaden** een logische app. Deze actie automatisch parameterizes Hallo logic app definitie en Hallo definitie opgeslagen als een Azure Resource Manager-implementatiesjabloon. U kunt deze implementatie tooyour Azure-resourcegroep sjabloonproject toevoegen.

## <a name="browse-your-logic-app-run-history"></a>Uw logische app uitvoeringsgeschiedenis bladeren

tooview hello geschiedenis voor uw logische app uitvoeren met de rechtermuisknop op uw logische app en selecteer **Open uitvoeringsgeschiedenis**. tooreorder uw uitvoeringsgeschiedenis op basis van een Hallo eigenschappen weergegeven, selecteer Hallo kolomkop te klikken.

![geschiedenis uitvoeren](media/logic-apps-manage-from-vs/runs.png)

tooshow Hallo geschiedenis voor een instantie uitvoeren zodat u resultaten, inclusief Hallo invoer en uitvoer van elke stap uitgevoerd Hallo kunt bekijken: Dubbelklik op een van de Hallo exemplaren uitvoeren.

![Uitvoeringsgeschiedenis resultaten, invoer en uitvoer van de stappen](./media/logic-apps-manage-from-vs/history.png)

## <a name="next-steps"></a>Volgende stappen

* [Een logische app maken](logic-apps-create-a-logic-app.md)
* [Ontwerpen, bouwen en implementeren van logische apps in Visual Studio](logic-apps-deploy-from-vs.md)
* [Algemene voorbeelden en scenario's weergeven](logic-apps-examples-and-scenarios.md)
* [Video: Automatiseren van bedrijfsprocessen met Azure Logic Apps](http://channel9.msdn.com/Events/Build/2016/T694)
* [Video: Uw systemen integreren met Azure Logic Apps](http://channel9.msdn.com/Events/Build/2016/P462)
