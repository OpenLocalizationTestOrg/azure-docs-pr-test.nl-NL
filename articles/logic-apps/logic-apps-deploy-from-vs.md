---
title: aaaCreate, bouwen en implementeren van logische apps in Visual Studio - Azure Logic Apps | Microsoft Docs
description: Visual Studio-projecten maken zodat u kunt ontwerpen, bouwen en implementeren van Azure Logic Apps.
author: jeffhollan
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: e484e5ce-77e9-4fa9-bcbe-f851b4eb42a6
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 2/14/2017
ms.author: LADocs; jehollan
ms.openlocfilehash: 5154cb05f9a48e9f0f2381a6953947217f7bb114
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="design-build-and-deploy-azure-logic-apps-in-visual-studio"></a>Ontwerpen, bouwen en implementeren van Azure Logic Apps in Visual Studio

Hoewel hello [Azure-portal](https://portal.azure.com/) een uitstekende manier biedt u toocreate en Azure Logic Apps beheren, kunt u Visual Studio voor het ontwerpen, bouwen en implementeren van uw logische apps. Visual Studio biedt uitgebreide hulpmiddelen zoals Hallo Logic App-ontwerper voor u toocreate logic apps, implementatie en automatisering sjablonen configureren en implementeren van tooany-omgeving. 

de slag met Azure Logic Apps tooget meer [hoe toocreate uw eerste logische app in Azure-portal Hallo](logic-apps-create-a-logic-app.md).

## <a name="installation-steps"></a>Installatiestappen

tooinstall en Visual Studio-hulpprogramma's configureren voor Azure Logic Apps, volgt u deze stappen.

### <a name="prerequisites"></a>Vereisten

* [Visual Studio 2017](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx) of Visual Studio 2015
* [Nieuwste Azure SDK](https://azure.microsoft.com/downloads/) (2.9.1 of hoger)
* [Azure PowerShell](https://github.com/Azure/azure-powershell#installation)
* De website toohello toegang wanneer u de ontwerpfunctie Hallo

### <a name="install-visual-studio-tools-for-azure-logic-apps"></a>Installeer Visual Studio-hulpprogramma's voor Azure Logic Apps

Nadat u Hallo-vereisten:

1. Open Visual Studio. Op Hallo **extra** selecteert u **uitbreidingen en Updates**.
2. Vouw Hallo **Online** categorie zodat u kunt online zoeken.
3. Blader of zoek naar **Logic Apps** totdat u **Azure Logic Apps-Tools voor Visual Studio**.
4. toodownload en installatie Hallo-extensie, klikt u op **downloaden**.
5. Visual Studio starten na de installatie.

> [!NOTE]
> U kunt ook downloaden [Azure Logic Apps-Tools voor Visual Studio 2017](https://marketplace.visualstudio.com/items?itemName=VinaySinghMSFT.AzureLogicAppsToolsforVisualStudio-18551) en Hallo [Azure Logic Apps-Tools voor Visual Studio 2015](https://marketplace.visualstudio.com/items?itemName=VinaySinghMSFT.AzureLogicAppsToolsforVisualStudio) rechtstreeks vanuit Visual Studio Marketplace Hallo.

Nadat u de installatie hebt voltooid, kunt u hello Azure-resourcegroepproject met Logic App-ontwerper.

## <a name="create-your-project"></a>Uw project maken

1. Op Hallo **bestand** menu te gaan**nieuw**, en selecteer **Project**. Of tooadd uw project tooan bestaande oplossing, ga te**toevoegen**, en selecteer **nieuw Project**.

    ![Menu Bestand](./media/logic-apps-deploy-from-vs/filemenu.png)

2. In Hallo **nieuw Project** venster vinden **Cloud**, en selecteer **Azure-resourcegroep**. Naam van uw project en klik op **OK**.

    ![Nieuw project toevoegen](./media/logic-apps-deploy-from-vs/addnewproject.png)

3. Selecteer Hallo **logische App** sjabloon waarmee u een lege logic app-implementatiesjabloon voor u toouse maakt. Nadat u de sjabloon hebt geselecteerd, klikt u op **OK**.

    ![Selecteer de sjabloon voor logische Apps](./media/logic-apps-deploy-from-vs/selectazuretemplate1.png)

    U hebt nu uw oplossing logic app-project tooyour toegevoegd. 
    Uw implementatiebestand moet in Hallo Solution Explorer, worden weergegeven.

    ![Implementatiebestand](./media/logic-apps-deploy-from-vs/deployment.png)

## <a name="create-your-logic-app-with-logic-app-designer"></a>Uw logische app maken met Logic App-ontwerper

Wanneer u een Azure-resourcegroepproject met een logische app hebt, kunt u Hallo Logic App-ontwerper openen in Visual Studio toocreate uw werkstroom. 

> [!NOTE]
> Hallo designer vereist een internetverbinding te connectors voor de beschikbare eigenschappen en gegevens opvragen. Als u Hallo Dynamics CRM Online connector gebruikt, vraagt Hallo designer bijvoorbeeld uw CRM-exemplaar tooshow beschikbaar aangepaste en de standaardeigenschappen.

1. Met de rechtermuisknop op uw `<template>.json` bestand en selecteer **openen met Logic App-ontwerper**. (`Ctrl+L`)

2. Kies uw Azure-abonnement, resourcegroep en locatie voor de implementatiesjabloon.

    > [!NOTE]
    > Het ontwerpen van een logische app, maakt resources van de API-verbinding die query voor eigenschappen tijdens de ontwerp. Visual Studio maakt gebruik van de geselecteerde resource groep toocreate deze verbindingen tijdens het ontwerpen. tooview of wijzigen van de API-verbindingen, gaat u toohello Azure-portal en bladert u naar **API verbindingen**.

    ![Abonnement kiezen](./media/logic-apps-deploy-from-vs/designer_picker.png)

    Hallo designer gebruikt Hallo definitie in Hallo `<template>.json` bestand voor de rendering.

4. Maken en ontwerpen van uw logische app. Uw implementatiesjabloon is bijgewerkt met de wijzigingen.

    ![App-ontwerper logica in Visual Studio](./media/logic-apps-deploy-from-vs/designer_in_vs.png)

Visual Studio voegt `Microsoft.Web/connections` resources te uw resourcebestand voor de verbindingen uw logische app moet toofunction. De eigenschappen van deze verbinding kunnen worden ingesteld bij het implementeren van, en nadat u hebt geïmplementeerd beheerd **API verbindingen** in hello Azure-portal.

### <a name="switch-toojson-code-view"></a>Switch tooJSON codeweergave

tooshow hello JSON-weergave voor uw logische app, selecteer Hallo **codeweergave** tabblad onderin Hallo Hallo Designer.

tooswitch back-toohello volledige resource JSON, met de rechtermuisknop op Hallo `<template>.json` bestand en selecteer **Open**.

### <a name="add-references-for-dependent-resources-toovisual-studio-deployment-templates"></a>Verwijzingen voor afhankelijke resources tooVisual Studio implementatiesjablonen toevoegen

Als u wilt dat uw logische app tooreference afhankelijke resources, kunt u [Azure Resource Manager-sjabloonfuncties](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-functions) in uw sjabloon logic app-implementatie. Bijvoorbeeld, kunt u uw logische app tooreference een Azure-functie of integratiepakket account dat u wilt dat toodeploy samen met uw logische app. Volg deze richtlijnen over hoe toouse parameters in de implementatiesjabloon voor de zodat die Logic App-ontwerper Hallo correct wordt gerenderd. 

U kunt logische app parameters in deze soorten triggers en acties:

*   Onderliggende werkstroom
*   Functie-app
*   APIM aanroep
*   De URL van de runtime verbinding API
*   Verbindingspad API

En u kunt een sjabloonfuncties, zoals parameters, variabelen, resourceId, concat, enzovoort. Dit is hoe u kunt vervangen hello Azure-functie resource-ID:

```
"parameters":{
    "functionName": {
        "type":"string",
        "minLength":1,
        "defaultValue":"<FunctionName>"
    }
},
```

En waar u parameters wilt gebruiken:

```
"MyFunction": {
    "type": "Function",
    "inputs": {
        "body":{},
        "function":{
            "id":"[resourceid('Microsoft.Web/sites/functions','functionApp',parameters('functionName'))]"
        }
    },
    "runAfter":{}
}
```
Als een ander voorbeeld kunt u Service Bus bericht verzendbewerking Hallo voorzien:

```
"Send_message": {
    "type": "ApiConnection",
        "inputs": {
            "host": {
                "connection": {
                    "name": "@parameters('$connections')['servicebus']['connectionId']"
                }
            },
            "method": "post",
            "path": "[concat('/@{encodeURIComponent(''', parameters('queueuname'), ''')}/messages')]",
            "body": {
                "ContentData": "@{base64(triggerBody())}"
            },
            "queries": {
                "systemProperties": "None"
            }
        },
        "runAfter": {}
    }
```
> [!NOTE] 
> host.runtimeUrl is optioneel en kan worden verwijderd uit de sjabloon, indien aanwezig.
> 


> [!NOTE] 
> Voor Hallo Logic App-ontwerper toowork wanneer u parameters, moet u standaardwaarden opgeven, bijvoorbeeld:
> 
> ```
> "parameters": {
>     "IntegrationAccount": {
>     "type":"string",
>     "minLength":1,
>     "defaultValue":"/subscriptions/<subscriptionID>/resourceGroups/<resourceGroupName>/providers/Microsoft.Logic/integrationAccounts/<integrationAccountName>"
>     }
> },
> ```

### <a name="save-your-logic-app"></a>Uw logische app opslaan

toosave uw logische app op elk gewenst moment, ga te**bestand** > **opslaan**. (`Ctrl+S`) 

Als uw logische app fouten heeft bij het opslaan van uw app, worden deze weergegeven in Visual Studio Hallo **uitvoer** venster.

## <a name="deploy-your-logic-app-from-visual-studio"></a>Uw logische app vanuit Visual Studio implementeren

Na het configureren van uw app kunt u rechtstreeks vanuit Visual Studio in een paar stappen implementeren. 

1. Met de rechtermuisknop op uw project in Solution Explorer en ga te**implementeren** > **nieuwe implementatie...**

    ![Nieuwe implementatie](./media/logic-apps-deploy-from-vs/newdeployment.png)

2. Wanneer u wordt gevraagd, meld u aan tooyour Azure-abonnement. 

3. U moet nu Hallo details voor de resourcegroep Hallo waar u toodeploy uw logische app wilt selecteren. Wanneer u bent klaar, selecteert u **implementeren**.

    > [!NOTE]
    > Zorg ervoor dat u de juiste sjabloon Hallo en parameterbestand voor resourcegroep Hallo selecteren. Als u toodeploy tooa productie-omgeving wilt, bijvoorbeeld Hallo productie parameterbestand kiezen.

    ![Tooresource groep implementeren](./media/logic-apps-deploy-from-vs/deploytoresourcegroup.png)

    Hallo-Implementatiestatus wordt weergegeven in Hallo **uitvoer** venster. 
    Moet u wellicht tooselect **Azure inrichting** in Hallo **tonen de uitvoer van** lijst.

    ![Implementatie statusuitvoer](./media/logic-apps-deploy-from-vs/output.png)

In toekomstige Hallo, kunt u uw logische app in broncodebeheer bewerken en nieuwe versies van Visual Studio toodeploy gebruiken.

> [!NOTE]
> Als u rechtstreeks Hallo definitie in hello Azure-portal wijzigt, worden deze wijzigingen overschreven wanneer u vanuit Visual Studio opnieuw implementeert. 

## <a name="add-your-logic-app-tooan-existing-resource-group-project"></a>Uw logische app tooan bestaande resourcegroep project toevoegen

Als u een bestaand project voor de resourcegroep hebt, kunt u uw logische app toothat-project in het venster van de JSON-overzicht Hallo kunt toevoegen. U kunt ook een andere logische app naast Hallo-app die u eerder hebt gemaakt toevoegen.

1. Open Hallo `<template>.json` bestand.

2. tooopen hello JSON overzichtsvenster te gaan**weergave** > **overige vensters** > **JSON-overzicht**.

3. tooadd toohello sjabloon bronbestand, klikt u op **Resource toevoegen** Hallo boven aan het venster van de JSON-overzicht Hallo. Of met de rechtermuisknop in het venster JSON-overzicht hello, **resources**, en selecteer **nieuwe Resource toevoegen**.

    ![Venster JSON-overzicht](./media/logic-apps-deploy-from-vs/jsonoutline.png)
    
4. In Hallo **Resource toevoegen** in het dialoogvenster, zoeken en selecteert u **logische App**. Naam van uw logische app en kies **toevoegen**.

    ![Resource toevoegen](./media/logic-apps-deploy-from-vs/addresource.png)

## <a name="next-steps"></a>Volgende stappen

* [Logic apps beheren met Visual Studio Cloud Explorer](logic-apps-manage-from-vs.md)
* [Algemene voorbeelden en scenario's weergeven](logic-apps-examples-and-scenarios.md)
* [Meer informatie over hoe tooautomate bedrijfsprocessen met Azure Logic Apps](http://channel9.msdn.com/Events/Build/2016/T694)
* [Meer informatie over hoe toointegrate uw systemen met Azure Logic Apps](http://channel9.msdn.com/Events/Build/2016/P462)
