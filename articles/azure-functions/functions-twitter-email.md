---
title: "een functie die kan worden geïntegreerd met Azure Logic Apps aaaCreate | Microsoft Docs"
description: "Maken van een functie die kan worden geïntegreerd met Azure Logic Apps en cognitieve Azure-Services toocategorize tweet gevoel en meldingen te verzenden wanneer gevoel slecht is."
services: functions, logic-apps, cognitive-services
keywords: werkstroom, cloud-apps, cloudservices, bedrijfsprocessen, systeemintegratie, enterprise application integration, EAI
documentationcenter: 
author: ggailey777
manager: erikre
editor: 
ms.assetid: 60495cc5-1638-4bf0-8174-52786d227734
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: e176bd946af9a3684b3ad0e4b1bed1c3ee344019
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-that-integrates-with-azure-logic-apps"></a>Maken van een functie die kan worden geïntegreerd met Azure Logic Apps

Azure Functions integreert met Azure Logic Apps in Hallo Logic Apps Designer. Deze integratie kunt u Hallo rekenkracht van functies in integraties met andere Azure en services van derden gebruiken. 

Deze zelfstudie leert u hoe toouse functioneert met Logic Apps en cognitieve Azure-Services tooanalyze gevoel uit Twitter-berichten. Een functie HTTP geactiveerd categoriseert tweets als groen, geel of rood op basis van Hallo gevoel score. Een e-mailbericht wordt verzonden wanneer slechte gevoel wordt gedetecteerd. 

![afbeelding van de eerste twee stappen van de app in App-ontwerper voor logica](media/functions-twitter-email/designer1.png)

In deze zelfstudie leert u het volgende:

> [!div class="checklist"]
> * Maak een cognitieve Services-account.
> * Maak een functie die tweet gevoel ingedeeld.
> * Een logische app die is verbonden tooTwitter maken.
> * Gevoel detectie toohello logic app toevoegen. 
> * Verbinding maken Hallo logic app toohello functie.
> * Een e-mailbericht op basis van het antwoord van de functie Hallo Hallo verzenden.

## <a name="prerequisites"></a>Vereisten

+ Een actieve [Twitter](https://twitter.com/) account. 
+ Een [Outlook.com](https://outlook.com/) account (voor het verzenden van meldingen).
+ In dit onderwerp wordt gebruikt als het eerste punt Hallo resources gemaakt in [uw eerste functie maken vanuit Azure-portal Hallo](functions-create-first-azure-function.md).  
Als u dit nog niet hebt gedaan, voert u deze stappen nu toocreate functie-app.

## <a name="create-a-cognitive-services-account"></a>Een cognitieve Services-account maken

Een cognitieve Services-account is vereist toodetect Hallo gevoel tweets wordt bewaakt.

1. Meld u aan toohello [Azure-portal](https://portal.azure.com/).

2. Klik op Hallo **nieuw** knop gevonden op Hallo linkerbovenhoek Hallo Azure-portal.

3. Klik op **gegevens en analyse** > **cognitieve Services**. Vervolgens Hallo-instellingen gebruiken als opgegeven in de tabel hello, Hallo voorwaarden accepteren en Controleer **pincode toodashboard**.

    ![Blade cognitieve account maken](media/functions-twitter-email/cog_svcs_account.png)

    | Instelling      |  Voorgestelde waarde   | Beschrijving                                        |
    | --- | --- | --- |
    | **Naam** | MyCognitiveServicesAccnt | Kies een unieke naam. |
    | **API-type** | Tekstanalyse-API | API gebruikt tooanalyze tekst.  |
    | **Locatie** | VS - west | Op dit moment alleen **VS-West** is beschikbaar voor tekstanalyse. |
    | **Prijscategorie** | F0 | Beginnen met de laagste categorie Hallo. Als u weinig aanroepen, schalen tooa hogere lagen.|
    | **Resourcegroep** | myResourceGroup | Gebruik Hallo dezelfde resourcegroep voor alle services in deze zelfstudie.|

4. Klik op **maken** toocreate uw account. Nadat het Hallo-account is gemaakt, klikt u op uw nieuwe cognitieve Services-account vastgemaakt toohello dashboard. 

5. Hallo-account, klikt u op **sleutels**, en kopieer vervolgens Hallo-waarde van **Key 1** en op te slaan. U gebruikt deze sleutel tooconnect Hallo logic app tooyour cognitieve Services-account. 
 
    ![Sleutels](media/functions-twitter-email/keys.png)

## <a name="create-hello-function"></a>Hallo-functie maken

Functies biedt een goede manier toooffload verwerkingstaken in een werkstroom van logic apps. Deze zelfstudie maakt gebruik van een HTTP-geactiveerde functie tooprocess tweet gevoel scores van cognitieve Services en retourneren een categoriewaarde.  

1. Vouw de functie-app, klikt u op Hallo  **+**  knop naast te**functies**, klikt u op Hallo **HTTPTrigger** sjabloon. Type `CategorizeSentiment` voor Hallo functie **naam** en klik op **maken**.

    ![Functie Apps blade functies +](media/functions-twitter-email/add_fun.png)

2. Hallo-inhoud van Hallo run.csx bestand vervangen door Hallo code te volgen en klik vervolgens op **opslaan**:

    ```c#
    using System.Net;
    
    public static async Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
    {
        // hello sentiment category defaults too'GREEN'. 
        string category = "GREEN";
    
        // Get hello sentiment score from hello request body.
        double score = await req.Content.ReadAsAsync<double>();
        log.Info(string.Format("hello sentiment score received is '{0}'.",
                    score.ToString()));
    
        // Set hello category based on hello sentiment score.
        if (score < .3)
        {
            category = "RED";
        }
        else if (score < .6)
        {
            category = "YELLOW";
        }
        return req.CreateResponse(HttpStatusCode.OK, category);
    }
    ```
    Deze functiecode retourneert een kleurcategorie is gebaseerd op Hallo gevoel score Hallo-aanvraag. 

3. tootest Hallo-functie, klikt u op **Test** Hallo rechterkant tooexpand Hallo Test tabblad. Typ een waarde van `0.2` voor Hallo **aanvraagtekst**, en klik vervolgens op **uitvoeren**. Een waarde van **rood** Hallo hoofdtekst van antwoord Hallo wordt geretourneerd. 

    ![Hallo functie testen in hello Azure-portal](./media/functions-twitter-email/test.png)

U hebt nu een functie die gevoel scores ingedeeld. Vervolgens kunt u een logische app, die de functie kan worden geïntegreerd met uw accounts Twitter en cognitieve Services maken. 

## <a name="create-a-logic-app"></a>Een logische app maken   

1. In Azure-portal hello, klikt u op Hallo **nieuw** knop gevonden op Hallo linkerbovenhoek Hallo Azure-portal.

2. Klik op **Enterprise Integration** > **logische App**. Hallo-instellingen gebruiken als opgegeven in de tabel hello, Controleer **pincode toodashboard**, en klik op **maken**.
 
4. Typ een **naam** zoals `TweetSentiment`, Hallo-instellingen gebruiken die zijn opgegeven in de tabel Hallo Hallo voorwaarden accepteren en Controleer **pincode toodashboard**.

    ![Logische app maken in hello Azure-portal](./media/functions-twitter-email/new_logicApp.png)

    | Instelling      |  Voorgestelde waarde   | Beschrijving                                        |
    | ----------------- | ------------ | ------------- |
    | **Naam** | TweetSentiment | Kies een passende naam voor uw app. |
    | **Resourcegroep** | myResourceGroup | API gebruikt tooanalyze tekst.  |
    | **Locatie** | VS - oost | Kies een locatie sluiten tooyou. |
    | **Resourcegroep** | myResourceGroup | Kies Hallo dezelfde bestaande resourcegroep als voorheen.|

4. Klik op **maken** toocreate uw logische app. Nadat het Hallo-app is gemaakt, klikt u op uw nieuwe logische app vastgemaakt toohello dashboard. Klik in Logic Apps Designer Hallo, schuif naar beneden en klikt u op Hallo **lege logische App** sjabloon. 

    ![Lege Logic Apps-sjabloon](media/functions-twitter-email/blank.png)

U kunt nu Hallo Logic Apps Designer tooadd services en triggers tooyour-app gebruiken.

## <a name="connect-tootwitter"></a>Verbinding maken met tooTwitter

Maak eerst een verbinding tooyour Twitter-account. Hallo logische app worden opgevraagd op tweets Hallo app toorun wordt geactiveerd.

1. In de ontwerpfunctie hello, klikt u op Hallo **Twitter** service en klikt u op Hallo **wanneer een nieuwe tweet wordt gepost** trigger. Meld u aan tooyour Twitter-account en autoriseren van Logic Apps toouse uw account.

2. Hallo Twitter triggerinstellingen zoals opgegeven in de tabel hello gebruiken. 

    ![Instellingen voor Twitter-connector](media/functions-twitter-email/azure_tweet.png)

    | Instelling      |  Voorgestelde waarde   | Beschrijving                                        |
    | ----------------- | ------------ | ------------- |
    | **Zoektekst** | #Azure | Gebruik een hashtag die populaire voor nieuwe tweets toogenerate in hello gekozen-interval. Wanneer met behulp van de gratis laag Hallo en uw hashtag te populair is, kunt u snel omhoog Hallo transacties gebruiken in uw cognitieve Services-account. |
    | **Frequentie** | Minuut | Hallo frequentie eenheid gebruikt voor het polling-Twitter.  |
    | **Interval** | 15 | Hallo-tijd is verstreken tussen Twitter-aanvragen in de frequentie eenheden. |

3.  Klik op **opslaan** tooconnect tooyour Twitter-account. 

Uw app is nu verbonden tooTwitter. Vervolgens maakt u verbinding maken met tootext analytics toodetect Hallo gevoel verzamelde tweets.

## <a name="add-sentiment-detection"></a>Detectie van gevoel toevoegen

1. Klik op **nieuwe stap**, en vervolgens **een actie toevoegen**.

    ![Nieuwe stap, waarna een actie toevoegen](media/functions-twitter-email/new_step.png)

2. In **kiest u een actie**, klikt u op **Tekstanalyse**, en klik vervolgens op Hallo **detecteren gevoel** in te grijpen.

    ![Gevoel detecteren](media/functions-twitter-email/detect_sent.png)

3. Typ de naam van een verbinding zoals `MyCognitiveServicesConnection`, plak Hallo-sleutel voor uw cognitieve Services-dat u hebt opgeslagen account en klik op **maken**.  

4. Klik op **tekst tooanalyze** > **Tweet tekst**, en klik vervolgens op **opslaan**.  

    ![Gevoel detecteren](media/functions-twitter-email/ds_tta.png)

Nu dat gevoel detectie is geconfigureerd, kunt u een verbinding tooyour-functie die Hallo gevoel score uitvoer verbruikt kunt toevoegen.

## <a name="connect-sentiment-output-tooyour-function"></a>Verbinding maken met gevoel uitvoer tooyour functie

1. In Hallo Logic Apps Designer, klikt u op **nieuwe stap** > **een actie toevoegen**, en klik vervolgens op **Azure Functions**. 

2. Klik op **kiest u een Azure-functie**, selecteer Hallo **CategorizeSentiment** functie die u eerder hebt gemaakt.  

    ![Azure vak voor de functie kiezen met een Azure-functie](media/functions-twitter-email/choose_fun.png)

3. In **aanvraagtekst**, klikt u op **Score** en vervolgens **opslaan**.

    ![Score](media/functions-twitter-email/trigger_score.png)

De functie wordt nu worden geactiveerd wanneer een score gevoel wordt verzonden vanuit Hallo logische app. Een kleurcode categorie geretourneerd door Hallo functie toohello logische app. Vervolgens voegt u een e-mailbericht dat wordt verzonden als een waarde gevoel van **rood** wordt geretourneerd vanaf Hallo-functie. 

## <a name="add-email-notifications"></a>E-mailmeldingen toevoegen

Hallo laatste deel van de werkstroom Hallo is tootrigger een e-mailbericht wanneer Hallo gevoel wordt berekend als _rood_. In dit onderwerp gebruikt een Outlook.com-connector. U kunt vergelijkbare stappen toouse Gmail of Outlook van Office 365-connector kunt uitvoeren.   

1. In Hallo Logic Apps Designer, klikt u op **nieuwe stap** > **een voorwaarde toevoegen**. 

2. Klik op **kiest u een waarde**, klikt u vervolgens op **hoofdtekst**. Selecteer **gelijk is aan**, klikt u op **kiest u een waarde** en het type `RED`, en klik op **opslaan**. 

    ![Een voorwaarde toohello logische app toevoegen.](media/functions-twitter-email/condition.png)

3. In **zo ja, niets doen**, klikt u op **een actie toevoegen**, zoeken naar `outlook.com`, klikt u op **e-mailbericht verzenden**, en meld u aan tooyour Outlook.com-account.
    
    ![Kies een actie voor Hallo voorwaarde.](media/functions-twitter-email/outlook.png)

    > [!NOTE]
    > Als u geen een Outlook.com-account hebt, kunt u een andere connector, zoals Gmail of Office 365 Outlook

4. In Hallo **e-mailbericht verzenden** actie, gebruik Hallo e-mailinstellingen als opgegeven in de tabel Hallo. 

    ![Configureer Hallo e voor Hallo verzend een e-actie.](media/functions-twitter-email/sendemail.png)

    | Instelling      |  Voorgestelde waarde   | Beschrijving  |
    | ----------------- | ------------ | ------------- |
    | **Aan** | Typ uw e-mailadres | Hallo e-mailadres dat Hallo melding ontvangt. |
    | **Onderwerp** | Negatieve tweet gevoel gedetecteerd  | Hallo onderwerpregel van het e-mailmelding Hallo.  |
    | **Hoofdtekst** | Tweet tekst, locatie | Klik op Hallo **Tweet tekst** en **locatie** parameters. |

5.  Klik op **Opslaan**.

Nu dat Hallo werkstroom voltooid is, kunt u Hallo logische app- en Zie Hallo-functie op het werk.

## <a name="test-hello-workflow"></a>Test Hallo werkstroom

1. In Hallo Logic App-ontwerper, klikt u op **uitvoeren** toostart Hallo app.

2. Klik in de linkerkolom hello, **overzicht** toosee Hallo status van Hallo logische app. 
 
    ![Uitvoeringsstatus van Logic app](media/functions-twitter-email/over1.png)

3. (Optioneel) Klik op een hello wordt uitgevoerd toosee details van Hallo worden uitgevoerd.

4. Tooyour functie gaat, Hallo logboeken bekijken en controleren of gevoel waarden zijn ontvangen en verwerkt.
 
    ![Logboeken van de functie weergeven](media/functions-twitter-email/sent.png)

5. Wanneer een potentieel negatieve gevoel wordt gedetecteerd, krijgt u een e-mailbericht. Als u een e-mailbericht hebt ontvangen, kunt u elke keer Hallo functie code tooreturn rood wijzigen:

        return req.CreateResponse(HttpStatusCode.OK, "RED");

    Nadat u e-mailmeldingen hebt gecontroleerd, kunt u back toohello oorspronkelijke code wijzigen:

        return req.CreateResponse(HttpStatusCode.OK, category);

    > [!IMPORTANT]
    > Nadat u deze zelfstudie hebt voltooid, moet u Hallo logische app uitschakelen. Door het uitschakelen van Hallo app u voorkomen dat u in rekening gebracht voor uitvoeringen en met behulp van Hallo transacties in uw cognitieve Services-account.

Nu hebt u gezien hoe eenvoudig het is toointegrate functies in een werkstroom Logic Apps.

## <a name="disable-hello-logic-app"></a>Hallo logische app uitschakelen

toodisable hello logische app, klikt u op **overzicht** en klik vervolgens op **uitschakelen** Hallo boven aan het welkomstscherm. Hierdoor wordt voorkomen dat Hallo logische app uitgevoerd en steeds kosten zonder Hallo-app te verwijderen. 

![De functie Logboeken](media/functions-twitter-email/disable-logic-app.png)

## <a name="next-steps"></a>Volgende stappen

In deze zelfstudie heeft u het volgende geleerd:

> [!div class="checklist"]
> * Maak een cognitieve Services-account.
> * Maak een functie die tweet gevoel ingedeeld.
> * Een logische app die is verbonden tooTwitter maken.
> * Gevoel detectie toohello logic app toevoegen. 
> * Verbinding maken Hallo logic app toohello functie.
> * Een e-mailbericht op basis van het antwoord van de functie Hallo Hallo verzenden.

Hoe gaan van de volgende zelfstudie toolearn toohello toocreate een zonder Server API voor de functie.

> [!div class="nextstepaction"] 
> [Een serverloze API maken met behulp van Azure Functions](functions-create-serverless-api.md)

toolearn meer informatie over Logic Apps, Zie [Azure Logic Apps](../logic-apps/logic-apps-what-are-logic-apps.md).

