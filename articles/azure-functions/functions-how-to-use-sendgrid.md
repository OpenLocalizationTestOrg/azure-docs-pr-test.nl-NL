---
title: aaaHow toouse SendGrid in Azure Functions | Microsoft Docs
description: Toont hoe toouse SendGrid in Azure Functions
services: functions
documentationcenter: na
author: rachelappel
manager: erikre
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 01/31/2017
ms.author: rachelap
ms.openlocfilehash: a0ffdae04e5924c773d2d26427626fc1f570f7ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-sendgrid-in-azure-functions"></a>Hoe toouse SendGrid in Azure Functions

## <a name="sendgrid-overview"></a>SendGrid-overzicht

Azure Functions ondersteunt SendGrid uitvoer bindingen tooenable uw functies toosend e-mailberichten met een paar regels code en een SendGrid-account.

toouse hello SendGrid-API in een Azure-functie, hebt u een [SendGrid account](http://SendGrid.com). Bovendien moet u een SendGrid-API-sleutel hebben. Meld u bij tooyour SendGrid-account en klikt u op **instellingen** vervolgens **API-sleutel** toogenerate een API-sleutel. Houd deze sleutel is beschikbaar wanneer u deze in een toekomstige stap gebruiken.

U bent nu klaar toocreate een Azure-functie-app.

## <a name="create-an-azure-function-app"></a>Een Azure-functie-app maken 

Apps van Azure functie zijn containers voor een of meer Azure functions. Azure functions meer zijn dan - functie. Elke Azure-functie is gebonden tooone worden geactiveerd, dit is een gebeurtenis die het Hallo functie toorun veroorzaakt.
Elke functie kan bevatten een willekeurig aantal invoer of uitvoer bindingen. Bindingen zijn services die u in een functie gebruiken kunt. SendGrid is een binding u uitvoer toosend e-mail kunt gebruiken. 

1. Meld u bij toohello Azure-portal en [maken van een Azure-functie-App](https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function) of open een bestaande functie-app. 
2. Maak een Azure-functie. tookeep het eenvoudig, kies een handmatige trigger en C#. 

 ![Een Azure-functie maken](./media/functions-how-to-use-sendgrid/functions-new-function-manual-trigger-page.png)

## <a name="configure-sendgrid-for-use-in-an-azure-function-app"></a>SendGrid configureren voor gebruik in een Azure-functie-app

U moet uw SendGrid-API-sleutel opslaan als een toouse app-instelling in een functie. Hallo ApiKey veld is niet uw werkelijke SendGrid-API-sleutel, maar een instelling die u app definiëren waarmee uw werkelijke API-sleutel. Uw sleutel opslaan op deze manier is voor beveiliging, omdat het gescheiden van alle code of bestanden die kunnen worden gecontroleerd in broncodebeheer.

- Maak een **AppSettings** sleutel in de functie-app **toepassingsinstellingen**.

 ![Een Azure-functie maken](./media/functions-how-to-use-sendgrid/functions-configure-sendgrid-api-key-app-settings.png)

## <a name="configure-sendgrid-output-bindings"></a>SendGrid uitvoer bindingen configureren

SendGrid is beschikbaar als een Azure functie uitvoer binding. een SendGrid toocreate uitvoer binding:

1. Ga toohello **integreren** tabblad van de functie Hallo in hello Azure-portal.
2. Klik op **nieuwe uitvoer** toocreate een SendGrid uitvoer binding.
3. Vul Hallo **API-sleutel** en **bericht parameternaam** eigenschappen. Als u wilt, kunt u nu andere eigenschappen hello, of ze in plaats daarvan code. Deze instellingen kunnen worden gebruikt als standaardwaarden.

 ![SendGrid uitvoer bindingen configureren](./media/functions-how-to-use-sendgrid/functions-configure-sendgrid-output-bindings.png)

Toevoegen van een binding tooa functie maakt een bestand met de naam **function.json** in de map van de functie. Dit bestand bevat alle dezelfde informatie die u in hello Azure functie ziet Hallo **integreren** tabblad, maar in Json-indeling. Instelling Hallo **ApiKey**, **bericht**, en **van** velden maken de volgende vermeldingen in Hallo Hallo **function.json** bestand: 

```json
{
  "bindings": [    
    {
      "type": "sendGrid",
      "name": "message",
      "apiKey": "SendGridKey",
      "direction": "out",
      "from": "azure@contoso.com"
    }
  ],
  "disabled": false
}
```

Als u liever, kunt u deze mogelijk wijzigen zelf rechtstreeks bestand.

Nu dat u hebt gemaakt en geconfigureerd Hallo functie-App en de functie, kunt u een e-mailbericht Hallo code toosend schrijven.

## <a name="write-code-that-creates-and-sends-email"></a>Schrijven van code die wordt gemaakt en verzendt e-mailbericht

Hallo SendGrid-API bevat alle Hallo opdrachten u toocreate nodig hebt en een e-mail sturen.  

- Hallo-code in Hallo functie vervangen door Hallo code te volgen:

```cs
#r "SendGrid"
using System;
using SendGrid.Helpers.Mail;

public static void Run(TraceWriter log, string input, out Mail message)
{
    message = new Mail
    {        
        Subject = "Azure news"          
    };

    var personalization = new Personalization();
    // change tooemail of recipient
    personalization.AddTo(new Email("MoreEmailPlease@contoso.com"));   

    Content content = new Content
    {
        Type = "text/plain",
        Value = input
    };
    message.AddContent(content);
    message.AddPersonalization(personalization);
}
```

Kennisgeving Hallo eerste regel bevat Hallo ```#r``` richtlijn die verwijst naar Hallo SendGrid-assembly. Daarna kunt u een ```using``` instructie toomore eenvoudig toegang krijgen tot Hallo-objecten in die naamruimte. Maak in code hello, exemplaren van ```Mail```, ```Personalization```, en ```Content``` objecten uit Hallo SendGrid-API die e-mailbericht Hallo opstellen. Wanneer u Hallo-bericht terugkeert, wordt het door SendGrid biedt. 

Hallo van functie handtekening bevat ook een extra uitvoerparameter van het type ```Mail``` met de naam ```message```. Beide invoer en bindingen express zelf uitvoer als parameters van de functie in de code. 

2. Testen van uw code door te klikken op **Test** en u een bericht in Hallo invoert **aanvraagtekst** veld en vervolgens te klikken op Hallo **uitvoeren** knop.

 ![Testen van uw code](./media/functions-how-to-use-sendgrid/functions-develop-test-sendgrid.png)

3. Controleer de e-tooverify dat SendGrid Hallo e-mailadres verzonden. Het moet gaan toohello adres in Hallo code uit stap 1 en Hallo-bericht van Hallo bevatten **aanvraagtekst**.

## <a name="next-steps"></a>Volgende stappen
In dit artikel is gebleken hoe toouse SendGrid service toocreate Hallo en e-mail te sturen. toolearn meer informatie over het gebruik van Azure Functions in uw apps, Zie Hallo volgende onderwerpen: 

- [Aanbevolen procedures voor Azure Functions](functions-best-practices.md) vindt u enkele aanbevolen procedures toouse bij het maken van Azure Functions.

- [Naslaginformatie over Azure Functions developer](functions-reference.md) programmeurs verwijzing voor het coderen van functies en definiëren van triggers en bindingen.

- [Azure Functions testen](functions-test-a-function.md) beschrijving van verschillende hulpprogramma's en technieken voor het testen van uw functies.