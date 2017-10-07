---
title: aaaMonitor Surface Hubs met Azure Log Analytics | Microsoft Docs
description: Gebruik Hallo Surface Hub-oplossing tootrack Hallo status van uw Surface Hubs en begrijpen hoe deze worden gebruikt.
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: 8b4e56bc-2d4f-4648-a236-16e9e732ebef
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/07/2017
ms.author: banders
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 623d30e749cafdd4a34ba0c5b3408164f1b4a95b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-surface-hubs-with-log-analytics-tootrack-their-health"></a>Surface Hubs met logboekanalyse tootrack hun status controleren

![Surface Hub symbool](./media/log-analytics-surface-hubs/surface-hub-symbol.png)

Dit artikel wordt beschreven hoe u Hallo Surface Hub-oplossing in logboekanalyse toomonitor Microsoft Surface Hub-apparaten met Hallo Microsoft Operations Management Suite (OMS) kunt gebruiken. Meld u Analytics kunt die u goed begrijpen hoe deze worden gebruikt Hallo status van uw Surface Hubs bijhouden.

Elke Surface Hub heeft Hallo die Microsoft Monitoring Agent geïnstalleerd. De via Hallo-agent die u kunt gegevens uit uw tooOMS Surface Hub te verzenden. Logboekbestanden worden gelezen uit uw Surface Hubs en worden vervolgens toohello OMS-service worden verzonden. Problemen worden zoals servers offline, Hallo kalender niet synchroniseert, of als Hallo apparaat account kan niet toolog in Skype weergegeven in OMS in Hallo Surface Hub-dashboard. Hallo-gegevens in Hallo dashboard gebruikt, kunt u apparaten die niet worden uitgevoerd, of die zijn andere problemen en oplossingen voor problemen gedetecteerd Hallo mogelijk van toepassing te identificeren.

## <a name="installing-and-configuring-hello-solution"></a>Installeren en configureren van Hallo-oplossing
Gebruik Hallo informatie tooinstall te volgen en Hallo oplossing configureren. In de volgorde toomanage uw Surface Hubs van Hallo Microsoft Operations Management Suite (OMS), moet u hello te volgen:

* Een geldig abonnement te[OMS](http://www.microsoft.com/oms).
* Een [OMS abonnement](https://azure.microsoft.com/pricing/details/log-analytics/) niveau die ondersteuning voor Hallo aantal bieden apparaten dat u wilt dat toomonitor. Prijzen van OMS varieert afhankelijk van hoeveel apparaten zijn ingeschreven en hoeveel gegevens deze processen. Moet u tootake dit in aanmerking bij het plannen van uw implementatie Surface Hub.

Vervolgens wordt u een OMS-abonnement tooyour bestaande Microsoft Azure-abonnement toevoegen of maak een nieuwe werkruimte rechtstreeks via Hallo OMS-portal. Gedetailleerde instructies voor het gebruik van beide methoden is op [aan de slag met logboekanalyse](log-analytics-get-started.md). Zodra Hallo OMS-abonnement is ingesteld, zijn er twee manieren tooenroll Surface Hub-apparaten:

* Automatisch via Intune
* Handmatig via **instellingen** op uw apparaat Surface Hub.

## <a name="set-up-monitoring"></a>Controle instellen
U kunt controleren Hallo status en activiteit van uw Surface Hub met logboekanalyse in OMS. U kunt Hallo Surface Hub in OMS inschrijven met behulp van Intune of lokaal via **instellingen** op Hallo Surface Hub.

## <a name="connect-surface-hubs-toooms-through-intune"></a>Verbinding maken met Surface Hubs tooOMS via Intune
U moet Hallo werkruimte-ID en werkruimtesleutel voor Hallo OMS-werkruimte die uw Surface Hubs zullen beheren. U kunt verkrijgen die uit Hallo OMS-portal.

Intune is een Microsoft-product waarmee u toocentrally Hallo OMS configuratie-instellingen die zijn toegepast tooone of meer van uw apparaten beheren. Volg deze stappen tooconfigure uw apparaten via Intune:

1. Meld u aan tooIntune.
2. Navigeer te**instellingen** > **verbonden bronnen**.
3. Maken of bewerken van een beleid op basis van Hallo Surface Hub-sjabloon.
4. Navigeer toohello OMS (Azure Operational Insights)-sectie van het Hallo-beleid en voeg Hallo *werkruimte-ID* en *Werkruimtesleutel* toohello beleid.
5. Hallo beleid opslaan.
6. Hallo-beleid koppelen aan de juiste groep Hallo van apparaten.

   ![Intune-beleid](./media/log-analytics-surface-hubs/intune.png)

Hallo OMS instellingen Intune vervolgens gesynchroniseerd met de Hallo-apparaten in de doelgroep hello, ze inschrijven in de OMS-werkruimte.

## <a name="connect-surface-hubs-toooms-using-hello-settings-app"></a>Verbinding maken met behulp van de app instellingen Hallo Surface Hubs-tooOMS
U moet Hallo werkruimte-ID en werkruimtesleutel voor Hallo OMS-werkruimte die uw Surface Hubs zullen beheren. U kunt verkrijgen die uit Hallo OMS-portal.

Als u geen Intune toomanage uw omgeving gebruikt, kunt u handmatig via apparaten inschrijven **instellingen** op elke Surface Hub:

1. Open in uw Surface Hub **instellingen**.
2. Voer Hallo apparaat beheerdersreferenties wanneer u wordt gevraagd.
3. Klik op **dit apparaat**, en Hallo onder **bewaking**, klikt u op **OMS-instellingen configureren**.
4. Selecteer **bewaking inschakelen**.
5. Typ in Hallo OMS instellingen dialoogvenster Hallo **werkruimte-ID** en type Hallo **Werkruimtesleutel**.  
   ![Instellingen](./media/log-analytics-surface-hubs/settings.png)
6. Klik op **OK** toocomplete Hallo configuratie.

Een bevestiging wordt weergegeven dat u al dan niet Hallo OMS configuratie correct is toegepast toohello apparaat. Als dit het geval is, wordt er een bericht weergegeven dat die agent Hallo toohello OMS-service is verbonden. Hallo apparaat vervolgens wordt gestart voor het verzenden van gegevens tooOMS waar u kunt weergeven en erop reageren.

## <a name="monitor-surface-hubs"></a>Monitor met Surface Hubs
Bewaking van uw Surface Hubs lijkt met behulp van OMS veel bewaking van andere geregistreerde apparaten.

1. Meld u aan toohello OMS-portal.
2. Navigeer dashboard pack toohello Surface Hub-oplossing.
3. Status van uw apparaat wordt weergegeven.

   ![Surface Hub-dashboard](./media/log-analytics-surface-hubs/surface-hub-dashboard.png)

U kunt maken [waarschuwingen](log-analytics-alerts.md) op basis van bestaande of aangepaste logboek zoekopdrachten. Hallo gegevens Hallo die OMS van uw Surface Hubs verzamelt gebruikt, kunt u zoeken naar problemen en de waarschuwing op Hallo voorwaarden die u voor uw apparaten definieert.

## <a name="next-steps"></a>Volgende stappen
* Gebruik [zoekopdrachten aanmelden met logboekanalyse](log-analytics-log-searches.md) tooview gedetailleerde Surface Hub-gegevens.
* Maak [waarschuwingen](log-analytics-alerts.md) toonotify u wanneer er problemen optreden met uw Surface Hubs.
