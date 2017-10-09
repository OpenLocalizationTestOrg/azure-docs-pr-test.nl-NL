---
title: aaaHandling beveiligingswaarschuwingen in Azure Security Center | Microsoft Docs
description: Dit document helpt u toohandle beveiligingsincidenten voor toouse Azure Security Center mogelijkheden.
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: e8feb669-8f30-49eb-ba38-046edf3f9656
ms.service: security-center
ms.topic: hero-article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/27/2017
ms.author: yurid
ms.openlocfilehash: edb911c298a2ce93cd0ea5b22ce002005040090f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="handling-security-incidents-in-azure-security-center"></a>Beveiligingsincidenten afhandelen in Azure Security Center
Gesorteerd en beveiligingswaarschuwingen onderzoeken kunnen enige tijd duren voor de meest ervaren beveiligingsanalisten zelfs Hallo en voor veel is harde tooeven weet waar toobegin. Met behulp van [analytics](security-center-detection-capabilities.md) tooconnect Hallo informatie tussen verschillende [beveiligingswaarschuwingen](security-center-managing-and-responding-alerts.md), Security Center kunt u kennismaken met één enkele weergave van een campagne aanval en alle Hallo gerelateerde waarschuwingen – u kunt snel inzicht in welke acties Hallo aanvaller vond en welke bronnen zijn veranderd.

Dit document wordt beschreven hoe toouse beveiliging mogelijkheden in Security Center tooassist waarschuwt u afhandelen van beveiligingsincidenten.

## <a name="what-is-a-security-incident"></a>Wat is een beveiligingsincident?
In het Beveiligingscentrum is een beveiligingsincident een samenloop van alle waarschuwingen voor een resource die overeenstemt met [kill chain](https://blogs.technet.microsoft.com/office365security/addressing-your-cxos-top-five-cloud-security-concerns/)-patronen. Incidenten verschijnen in Hallo [beveiligingswaarschuwingen](security-center-managing-and-responding-alerts.md) tegel en blade. Een Incident onthullen Hallo lijst met verwante waarschuwingen, waarmee u tooobtain meer informatie over elk exemplaar.

## <a name="managing-security-incidents"></a>Beveiligingsincidenten beheren
U kunt uw huidige beveiligingsincidenten controleren door te kijken Hallo waarschuwingen beveiligingstegel. Toegang tot hello Azure-Portal en stappen Hallo hieronder toosee meer informatie over elk beveiligingsincident:

1. Op Hallo Security Center-dashboard, ziet u Hallo **beveiligingswaarschuwingen** tegel.

    ![De tegel Beveiligingswaarschuwingen in Security Center](./media/security-center-incident/security-center-incident-fig1.png)

2. Klik op deze tegel tooexpand en als een beveiligingsincident voordoet wordt gedetecteerd, wordt deze weergegeven bij Hallo beveiliging waarschuwingen grafiek zoals hieronder wordt weergegeven:

    ![Beveiligingsincident](./media/security-center-incident/security-center-incident-fig2.png)

3. U ziet dat Hallo security incident beschrijving een ander pictogram heeft vergeleken tooother waarschuwingen. Klik op het tooview om meer details over dit incident.

    ![Beveiligingsincident](./media/security-center-incident/security-center-incident-fig3.png)

4. Op Hallo **incident** blade u meer ziet details over deze veiligheidsincident, waaronder de volledige beschrijving, de ernst (die in dit geval is hoog), de huidige status (in dit geval is nog steeds *active*, een actie tooit die impliceert Hallo gebruiker nog niet uitgevoerde - kunt u dit doen met de rechtermuisknop te klikken op Hallo incident in Hallo **beveiligingswaarschuwingen** blade), Hallo aangevallen resource (in dit geval *VM1*), Hallo herstelstappen voor Hallo incident en in Hallo onderste deelvenster hebt u Hallo-waarschuwingen die zijn opgenomen in dit incident. Als u meer informatie over elke waarschuwing tooobtain wilt, wordt Klik op het bestand en een andere blade geopend, zoals hieronder wordt weergegeven:

    ![Beveiligingsincident](./media/security-center-incident/security-center-incident-fig4.png)

Hallo-informatie over deze blade varieert volgens toohello waarschuwing. Lees [beheren en reageert toosecurity waarschuwingen in Azure Security Center](security-center-managing-and-responding-alerts.md) voor meer informatie over het toomanage deze waarschuwingen. Enkele belangrijke overwegingen met betrekking tot deze mogelijkheid:

* Een nieuw filter kunt u uw weergave tooIncident alleen waarschuwingen alleen toocustomize of beide.
* Hallo dezelfde waarschuwing als onderdeel van een Incident (indien van toepassing), evenals de toobe zichtbaar als een zelfstandige waarschuwing kan bestaan.

## <a name="see-also"></a>Zie ook
In dit document hebt u geleerd hoe toouse Hallo security incident mogelijkheden in Security Center. toolearn meer informatie over Security Center Hallo ziet:

* [Beheren en erop reageren toosecurity waarschuwingen in Azure Security Center](security-center-managing-and-responding-alerts.md)
* [Detectiemogelijkheden van Azure Security Center](security-center-detection-capabilities.md)
* [Plannings- en bedieningsgids voor Azure Security Center](security-center-planning-and-operations-guide.md)
* [Beheren en erop reageren toosecurity waarschuwingen in Azure Security Center](security-center-managing-and-responding-alerts.md)
* [Veelgestelde vragen over Azure Security Center](security-center-faq.md)--Raadpleeg Veelgestelde vragen over het gebruik van Hallo-service.
* [Azure-beveiligingsblog](http://blogs.msdn.com/b/azuresecurity/): lees blogberichten over de beveiliging en naleving van Azure.
