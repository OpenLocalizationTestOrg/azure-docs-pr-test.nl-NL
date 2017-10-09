---
title: aaaNo-werkgroep connector gevonden voor een toepassing toepassingsproxy | Microsoft Docs
description: Oplossingen voor problemen die optreden mogelijk wanneer er geen be-Connector in een groep Connector voor uw toepassing Hello Azure AD-toepassingsproxy
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 4c4baf296b316db131929c9a7c618fb9960713e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="no-working-connector-group-found-for-an-application-proxy-application"></a>Er is geen werkgroep connector gevonden voor een toepassing toepassingsproxy

Dit artikel Help-onderwerp u tooresolve Hallo veelvoorkomende problemen wanneer er geen een gedetecteerd voor een toepassing Application Proxy connector geïntegreerd met Azure Active Directory.

## <a name="overview-of-steps"></a>Overzicht van stappen
Als er geen be-Connector in een groep Connector voor uw toepassing, moet u er een aantal manieren tooresolve Hallo probleem zijn:

-   Als u geen connectors in de groep Hallo hebt, kunt u:

    -   Een nieuwe Connector op Hallo rechts on-premises server downloaden en deze toothis groep toewijzen

    -   Een actieve Connector naar Hallo groep verplaatsen

-   Als u geen actieve connectors in Hallo groep hebt, kunt u:

    -   Hallo reden die de Connector niet actief is identificeren en oplossen

    -   Een actieve Connector naar Hallo groep verplaatsen

tooknow welke van de volgende Hallo-probleem is met de Hallo 'Application Proxy' menu openen in uw toepassing en bekijkt hello Connector groep waarschuwingsbericht staan aangegeven. Er worden opgegeven die Hallo-groep moet ten minste één Connector (u hebt geen zijn in de groep Hallo) of als er geen actieve Connectors (Hoewel u waarschijnlijk inactieve Connectors hebt).

   ![De selectie van connector in Azure Portal](./media/application-proxy-connectivity-no-working-connector/no-active-connector.png)

Zie voor meer informatie over elk van deze opties Hallo overeenkomstige sectie hieronder. Elk van deze wordt ervan uitgegaan dat u op pagina Hallo Connector-beheer begint. Als u bovenstaande Hallo foutbericht bekijkt, gaat u toothis pagina door te klikken op de waarschuwing het Hallo-bericht. Anders dit kunt u vinden door te gaan**Azure Active Directory**, te klikken op **bedrijfstoepassingen**, klikt u vervolgens **Application Proxy.**

   ![Connector-groepsbeheer in Azure Portal](./media/application-proxy-connectivity-no-working-connector/app-proxy.png)

## <a name="download-a-new-connector"></a>Een nieuwe Connector downloaden

een nieuwe Connector toodownload gebruik Hallo 'Connector downloaden' knop bovenaan Hallo Hallo pagina.

Opmerking Hallo Connector behoeften toobe geïnstalleerd op een computer met rechtstreeks toohello back-end-toepassing en meestal wordt geplaatst op dezelfde server als de toepassing hello Hallo. Nadat u hebt gedownload, wordt in dit menu Hallo Connector weergegeven. Klik op Hallo Connector, en Hallo 'Connector groep' vervolgkeuzelijst toomake ervoor dat het juiste toohello-groep behoort. Hallo wijziging opslaan.

   ![Hallo connector downloaden van hello Azure Portal](./media/application-proxy-connectivity-no-working-connector/download-connector.png)
   
## <a name="move-an-active-connector"></a>Verplaatsen van een actieve Connector

Als er een actieve Connector die moet deel uitmaken van de groep toohello en onbelemmerd zicht toohello doeltoepassing back-end heeft, kunt u Hallo Connector verplaatsen in de groep Hallo toegewezen. toodo is dus, klikt u op Hallo Connector. Hallo vervolgkeuzelijst tooselect Hallo juiste groep gebruiken in Hallo ' Connector ' groepsveld, en klik op opslaan.

## <a name="resolve-an-inactive-connector"></a>Een inactieve Connector oplossen

Als hello alleen Connectors in Hallo-groep niet actief zijn, zijn waarschijnlijk op een computer die niet zijn alle Hallo nodig poorten dan gedeblokkeerd.

Zie Hallo poorten document voor meer informatie over het onderzoeken van dit probleem oplossen.

## <a name="next-steps"></a>Volgende stappen
[Azure AD-toepassingsproxy connectors begrijpen](application-proxy-understand-connectors.md)


