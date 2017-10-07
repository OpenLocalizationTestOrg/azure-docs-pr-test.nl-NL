---
title: aaaData-beleid in Azure Time Series Insights | Microsoft Docs
description: In deze zelfstudie leert u toomanage gegevenstoegangsbeleid in tijd reeks inzichten
keywords: 
services: time-series-insights
documentationcenter: 
author: op-ravi
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/01/2017
ms.author: omravi
ms.openlocfilehash: f286d26c8c5c851c523e9384760dc4b10711fa3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="grant-data-access-tooa-time-series-insights-environment-using-azure-portal"></a>Data access tooa Time Series Insights-omgeving met Azure portal verlenen

Time Series Insights-omgevingen hebben twee onafhankelijke typen toegangsbeleid:

* Beleid voor beheertoegang
* Beleid voor gegevenstoegang

Beide soorten beleid verlenen Azure Active Directory-principals (gebruikers en apps) verschillende machtigingen voor een specifieke omgeving. Hallo principals (gebruikers en apps) moeten behoren toohello active directory (of 'Azure-tenant') die zijn gekoppeld aan het Hallo-abonnement met Hallo-omgeving.

Beheerbeleid toegang verlenen machtigingen gerelateerde toohello configuratie van Hallo-omgeving, zoals
*   Verwijzen naar gegevenssets, maken en verwijderen van Hallo-omgeving, bronnen van gebeurtenissen en
*   Beheer van Hallo gegevenstoegangsbeleid.

Gegevenstoegangsbeleid machtigingen verlenen gegevensquery's tooissue, referentiegegevens in Hallo omgeving bewerkt en opgeslagen query's en perspectieven die zijn gekoppeld aan de omgeving Hallo delen.

Hallo twee soorten beleid toestaan duidelijke scheiding tussen toohello toegangsbeheer van Hallo-omgeving en toegang tot toohello gegevens binnen Hallo-omgeving. Het is bijvoorbeeld mogelijk toosetup een omgeving zodat Hallo eigenaar/maker van Hallo omgeving uit Hallo gegevenstoegang wordt verwijderd. En de gebruikers en services die zijn toegestaan tooread gegevens van Hallo-omgeving kan worden verleend geen toegang tot toohello configuratie van Hallo-omgeving.

## <a name="grant-data-access"></a>Gegevenstoegang verlenen
Hallo volgende stappen laten zien hoe toogrant toegang tot de gegevens voor de principal van een gebruiker:

1.  Meld u aan toohello [Azure-portal](https://portal.azure.com).
2.  Klik op 'Alle resources' in hello menu aan de linkerkant Hallo Hallo Azure-portal.
3.  Selecteer uw Time Series Insights-omgeving.

  ![Beheren van Hallo Time Series Insights-bron - omgeving](media/data-access/getstarted-grant-data-access1.png)

4.  Selecteer Toegang gegevenslaag en klik op Toevoegen

  ![Hallo Time Series Insights bron beheren: toevoegen](media/data-access/getstarted-grant-data-access2.png)

5.  Klik op Gebruiker selecteren.
6.  Zoek en selecteer gebruiker via e-mail Hallo.
7.  Klik op de blade Gebruiker selecteren op Selecteren.

  ![Hallo Time Series Insights-bron - Selecteer de gebruiker beheren](media/data-access/getstarted-grant-data-access3.png)

8.  Klik op Rol selecteren.
9.  Selecteer 'Inzender' als u tooallow gebruiker toochange referentiegegevens wilt en opgeslagen query's en perspectieven met andere gebruikers van Hallo-omgeving delen. Anders 'Lezer' tooallow gebruikersgegevens query selecteren in Hallo-omgeving en persoonlijke (niet-gedeelde) query's opslaan in Hallo-omgeving.
10. Klik op 'Ok' Hallo 'Rol selecteren' blade.

  ![Hallo Time Series Insights-bron - Functieservices selecteren beheren](media/data-access/getstarted-grant-data-access4.png)

11. Klik op 'Ok' Hallo 'Gebruikersrol selecteren' blade.
12. U ziet het volgende:

  ![Hallo Time Series Insights-bron - resultaten beheren](media/data-access/getstarted-grant-data-access5.png)

## <a name="next-steps"></a>Volgende stappen

* [Een gebeurtenisbron maken](time-series-insights-add-event-source.md)
* [Verzenden van gebeurtenissen](time-series-insights-send-events.md) toohello gebeurtenisbron
* Uw omgeving bekijken in de [Time Series Insights-portal](https://insights.timeseries.azure.com)
