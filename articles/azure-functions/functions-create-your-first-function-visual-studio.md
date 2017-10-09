---
title: uw eerste functie in Azure met behulp van Visual Studio aaaCreate | Microsoft Docs
description: Maken en publiceren van een eenvoudige HTTP geactiveerd functie tooAzure met behulp van Azure Functions-hulpprogramma's voor Visual Studio.
services: functions
documentationcenter: na
author: rachelappel
manager: erikre
editor: 
tags: 
keywords: azure-functies, functies, gebeurtenisverwerking, berekenen, architectuur zonder server
ms.assetid: 82db1177-2295-4e39-bd42-763f6082e796
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 07/05/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 851e5b98dcc2da00334620896a0ea31f566589f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-function-using-visual-studio"></a>Uw eerste functie maken met Visual Studio

Azure Functions, kunt u uw code in een omgeving zonder server uitvoeren zonder toofirst een virtuele machine maken of een webtoepassing publiceert.

In dit onderwerp leert u hoe toouse 2017 voor Visual Studio-hulpprogramma's voor Azure Functions toocreate Hallo en de functie van een 'Hallo wereld' lokaal testen. Vervolgens wordt u Hallo functie code tooAzure publiceren. Deze hulpprogramma's zijn beschikbaar als onderdeel van hello Azure ontwikkeling werkbelasting in Visual Studio 2017 versie 15,3 of een latere versie.

![Azure-functiecode in een Visual Studio-project](./media/functions-create-your-first-function-visual-studio/functions-vstools-intro.png)

## <a name="prerequisites"></a>Vereisten

toocomplete deze zelfstudie, installatie:

* [Visual Studio 2017 versie 15,3](https://www.visualstudio.com/vs/preview/), met inbegrip van Hallo **ontwikkelen van Azure** werkbelasting.

    ![Installeer Visual Studio 2017 met hello Azure ontwikkeling werkbelasting](./media/functions-create-your-first-function-visual-studio/functions-vs-workloads.png)
    
    >[!NOTE]  
    Nadat u installeren of upgraden van tooVisual Studio 2017 versie 15,3, moet u mogelijk ook toomanually update Hallo 2017 van Visual Studio-hulpprogramma's voor Azure Functions. U kunt bijwerken Hallo-hulpprogramma's van Hallo **extra** menu onder **uitbreidingen en Updates...**   >  **Updates** > **Visual Studio Marketplace** > **Azure Functions en Web extra taken**  >  **Update**. 

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)] 

## <a name="create-an-azure-functions-project-in-visual-studio"></a>Een Azure Functions-project in Visual Studio maken

[!INCLUDE [Create a project using hello Azure Functions template](../../includes/functions-vstools-create.md)]

Nu u Hallo-project hebt gemaakt, kunt u uw eerste functie maken.

## <a name="create-hello-function"></a>Hallo-functie maken

1. Klik in **Solution Explorer** met de rechtermuisknop op het projectknooppunt en selecteer  > **Nieuw item****Toevoegen**. Selecteer **Azure-functie** en klik op **Toevoegen**.

2. Selecteer **HttpTrigger**, typ een **Functienaam**, selecteer **Anoniem** bij **Toegangsrechten** en klik op **Maken**. Hallo-functie gemaakt, wordt geopend door een HTTP-aanvraag vanaf elke client. 

    ![Een nieuwe Azure-functie maken](./media/functions-create-your-first-function-visual-studio/functions-vstools-add-new-function-2.png)

    Een bestand met code toegevoegd tooyour project met een klasse die de functiecode implementeert. Deze code is gebaseerd op een sjabloon waarmee u een naamwaarde en het gebruik weer ontvangt. Hallo **functienaam** kenmerk Hallo-naam van de functie wordt ingesteld. Hallo **HttpTrigger** kenmerk geeft aan dat het Hallo-bericht waarmee Hallo-functie wordt geactiveerd. 

    ![Functie codebestand](./media/functions-create-your-first-function-visual-studio/functions-code-page.png)

Nu u een HTTP-geactiveerde-functie hebt gemaakt, kunt u deze testen op uw lokale computer.

## <a name="test-hello-function-locally"></a>Hallo functie lokaal testen

Met Azure Functions Core-hulpprogramma's kunt u Azure Functions-projecten uitvoeren op uw lokale ontwikkelcomputer. U bent na vragen aan gebruiker tooinstall deze hulpprogramma's Hallo eerste keer dat u een functie vanuit Visual Studio start.  

1. tootest uw functie druk op F5. Als u wordt gevraagd, Hallo verzoek van Visual Studio toodownload accepteert en hulpprogramma's voor Azure Functions Core (CLI) installeren.  U moet mogelijk ook een firewall-uitzondering tooenable zodat Hallo hulpprogramma's voor HTTP-aanvragen kunnen verwerken.

2. Hallo-URL kopiëren van de functie van Azure Functions-runtime Hallo uitvoer.  

    ![Lokale Azure-runtime](./media/functions-create-your-first-function-visual-studio/functions-vstools-f5.png)

3. Hallo-URL voor Hallo HTTP-aanvraag in de adresbalk van uw browser plakken. Hallo-queryreeks toevoegen `&name=<yourname>` toothis URL en Hallo aanvraag uit te voeren. Hallo hieronder vindt u antwoord Hallo in Hallo browser toohello lokale GET-aanvraag geretourneerd door de functie Hallo: 

    ![Functie localhost-respons in Hallo-browser](./media/functions-create-your-first-function-visual-studio/functions-test-local-browser.png)

4. toostop foutopsporing, klikt u op Hallo **stoppen** op de werkbalk van Hallo Visual Studio.

Nadat u hebt gecontroleerd of de functie Hallo correct wordt uitgevoerd op de lokale computer, is het tijd toopublish Hallo project tooAzure.

## <a name="publish-hello-project-tooazure"></a>Hallo project tooAzure publiceren

Voordat u uw project kunt publiceren, moet u een functie-app in uw Azure-abonnement hebben. U kunt rechtstreeks vanuit Visual Studio een functie-app maken.

[!INCLUDE [Publish hello project tooAzure](../../includes/functions-vstools-publish.md)]

## <a name="test-your-function-in-azure"></a>Uw functie testen in Azure

1. Hallo basis-URL van de functie-app Hallo van Hallo publiceren profielpagina kopiëren. Vervang Hallo `localhost:port` gedeelte van het Hallo-URL die u hebt gebruikt bij het testen van de functie Hallo lokaal met Hallo nieuwe basis-URL. Als voorheen Zorg ervoor dat tooappend Hallo-queryreeks `&name=<yourname>` toothis URL en Hallo aanvraag uit te voeren.

    Hallo-URL die uw HTTP-aanroepen geactiveerd functie ziet er als volgt:

        http://<functionappname>.azurewebsites.net/api/<functionname>?name=<yourname> 

2. Deze nieuwe URL voor Hallo HTTP-aanvraag in de adresbalk van uw browser plakken. Hallo hieronder vindt u antwoord Hallo in Hallo browser toohello externe GET-aanvraag geretourneerd door de functie Hallo: 

    ![Functie-respons in Hallo-browser](./media/functions-create-your-first-function-visual-studio/functions-test-remote-browser.png)
 
## <a name="next-steps"></a>Volgende stappen

Met de functie van een eenvoudige HTTP is geactiveerd, hebt u Visual Studio toocreate een C#-functie-app gebruikt. 

+ toolearn hoe tooconfigure uw project toosupport andere soorten triggers en bindingen, Zie Hallo [Hallo-project configureren voor lokale ontwikkeling](functions-develop-vs.md#configure-the-project-for-local-development) in sectie [Azure Functions-Tools voor Visual Studio](functions-develop-vs.md).
+ toolearn meer informatie over lokale testen en foutopsporing met hello Azure Functions Core's, Zie [Code en test Azure Functions lokaal](functions-run-local.md). 
+ toolearn meer informatie over het ontwikkelen van functies als .NET-klassebibliotheken, Zie [met behulp van .NET-klassebibliotheken met Azure Functions](functions-dotnet-class-library.md). 

