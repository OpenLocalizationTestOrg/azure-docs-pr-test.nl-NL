---
title: Veelgestelde vragen over IoT-Suite aaaAzure | Microsoft Docs
description: Veelgestelde vragen over IoT Suite
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: cb537749-a8a1-4e53-b3bf-f1b64a38188a
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/15/2017
ms.author: corywink
ms.openlocfilehash: cb39e24af6d1ce2afea554285512d05b2d7c721e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-for-iot-suite"></a>Veelgestelde vragen over IoT Suite

Zie ook Hallo verbonden factory specifieke [Veelgestelde vragen over](iot-suite-faq-cf.md).

### <a name="where-can-i-find-hello-source-code-for-hello-preconfigured-solutions"></a>Waar vind ik broncode Hallo Hallo vooraf geconfigureerde oplossingen

Hallo broncode is opgeslagen in Hallo GitHub-opslagplaatsen te volgen:
* [Vooraf geconfigureerde oplossing voor externe controle][lnk-remote-monitoring-github]
* [Oplossing voor voorspeld onderhoud vooraf geconfigureerde][lnk-predictive-maintenance-github]
* [Verbonden factory vooraf geconfigureerde oplossing](https://github.com/Azure/azure-iot-connected-factory)

### <a name="how-do-i-update-toohello-latest-version-of-hello-remote-monitoring-preconfigured-solution-that-uses-hello-iot-hub-device-management-features"></a>Hoe kan ik toohello meest recente versie van Hallo vooraf geconfigureerde oplossing voor externe controle dat maakt gebruik van IoT Hub apparaat-beheerfuncties Hallo bijwerken?

* Als u een vooraf geconfigureerde oplossing van Hallo https://www.azureiotsuite.com/ site implementeert, implementeert deze altijd een nieuw exemplaar van de meest recente versie van de Hallo van Hallo oplossing.
* Als u een vooraf geconfigureerde oplossing met behulp van de opdrachtregel Hallo implementeert, kunt u een bestaande implementatie bijwerken met nieuwe code. Zie [Cloud implementatie] [ lnk-cloud-deployment] in GitHub hello [opslagplaats][lnk-remote-monitoring-github].

### <a name="how-can-i-add-support-for-a-new-device-method-toohello-remote-monitoring-preconfigured-solution"></a>Hoe kan ik ondersteuning voor een vooraf geconfigureerde oplossing voor externe controle nieuwe apparaat methode toohello toevoegen?

Zie de sectie Hallo [ondersteuning toevoegen voor een nieuwe methode toohello simulator] [ lnk-add-method] in Hallo [aanpassen van een vooraf geconfigureerde oplossing] [ lnk-customize] artikel.

### <a name="hello-simulated-device-is-ignoring-my-desired-property-changes-why"></a>Hallo gesimuleerd apparaat negeert mijn gewenste eigenschapswijzigingen waarom?
In Hallo als externe controle vooraf geconfigureerde oplossing, gebruikt de Hallo gesimuleerd apparaatcode alleen Hallo **Desired.Config.TemperatureMeanValue** en **Desired.Config.TelemetryInterval** gewenst eigenschappen Hallo tooupdate gerapporteerd eigenschappen. Alle andere gewenste eigenschap wijzigingsaanvragen worden genegeerd.

### <a name="my-device-does-not-appear-in-hello-list-of-devices-in-hello-solution-dashboard-why"></a>Mijn apparaat niet wordt weergegeven in de lijst Hallo van apparaten in het dashboard van de oplossing hello, waarom?

lijst van apparaten in het dashboard van de oplossing Hallo Hallo maakt gebruik van een query tooreturn Hallo lijst met apparaten. Op dit moment wordt kan niet een query meer dan 10K apparaten retourneren. Probeer te Hallo zoekcriteria voor uw query meer beperkende maken.

### <a name="whats-hello-difference-between-deleting-a-resource-group-in-hello-azure-portal-and-clicking-delete-on-a-preconfigured-solution-in-azureiotsuitecom"></a>Wat is Hallo verschil tussen het verwijderen van een resourcegroep in hello Azure portal en te klikken op verwijderen op een vooraf geconfigureerde oplossing op azureiotsuite.com?

* Als u Hallo vooraf geconfigureerde oplossing in verwijdert [azureiotsuite.com][lnk-azureiotsuite], verwijdert u alle Hallo-resources die zijn ingericht toen u Hallo vooraf geconfigureerde oplossing hebt gemaakt. Als u aanvullende bronnen toohello resourcegroep hebt toegevoegd, worden deze resources worden ook verwijderd. 
* Als u de resourcegroep Hallo in Hallo verwijdert [Azure-portal][lnk-azure-portal], verwijdert u alleen Hallo resources in die resourcegroep. U moet ook toodelete hello Azure Active Directory-toepassing hello vooraf geconfigureerde oplossing in Hallo gekoppeld [klassieke Azure-portal][lnk-classic-portal].

### <a name="how-many-iot-hub-instances-can-i-provision-in-a-subscription"></a>Hoeveel exemplaren van de IoT Hub kan ik inrichten in een abonnement?

Standaard kunt u inrichten [10 IoT hubs per abonnement][link-azuresublimits]. Kunt u een [Azure-ondersteuningsticket] [ link-azuresupportticket] tooraise deze limiet. Als gevolg hiervan kunt sinds de bepalingen van elke vooraf geconfigureerde oplossing voor een nieuwe IoT Hub, u alleen richten up too10 vooraf oplossingen in een bepaald abonnement geconfigureerde. 

### <a name="how-many-azure-cosmos-db-instances-can-i-provision-in-a-subscription"></a>Hoeveel exemplaren van Azure DB die Cosmos kan ik inrichten in een abonnement?

Vijftig. Kunt u een [Azure-ondersteuningsticket] [ link-azuresupportticket] tooraise dit beperken, maar standaard kunt u alleen 50 exemplaren van de Cosmos-database per abonnement inrichten. 

### <a name="how-many-free-bing-maps-apis-can-i-provision-in-a-subscription"></a>Hoeveel gratis Bing Kaarten-API's kan ik inrichten met een abonnement?

Twee. U kunt slechts twee interne transacties niveau 1 Bing-kaarten voor Enterprise plannen in een Azure-abonnement maken. Hallo-oplossing voor externe controle is standaard ingericht met Hallo interne transacties niveau 1-plan. Als gevolg hiervan kunt u alleen inrichten up tootwo externe bewakingsoplossingen in een abonnement zonder wijzigingen.

### <a name="i-have-a-remote-monitoring-solution-deployment-with-a-static-map-how-do-i-add-an-interactive-bing-map"></a>Ik heb een implementatie van een externe bewakingsoplossing met een statische kaart, hoe voeg ik een interactieve Bing-kaart toe?

1. Ophalen van uw Bing kaarten-API voor Enterprise-querysleutel in [Azure-portal][lnk-azure-portal]: 
   
   1. Navigeer toohello resourcegroep waar uw Bing kaarten-API voor Enterprise zich in Hallo bevindt [Azure-portal][lnk-azure-portal].
   2. Klik op **alle instellingen**, klikt u vervolgens **Sleutelbeheer**. 
   3. U ziet twee sleutels: **hoofdsleutel** en **querysleutel**. Hallo-waarde voor kopiëren **querysleutel**.
      
      > [!NOTE]
      > U hebt geen Bing Kaarten-API voor Enterprise-account? Maken van een in Hallo [Azure-portal] [ lnk-azure-portal] door te klikken op + Nieuw, zoeken naar Bing kaarten-API voor Enterprise- en volg toocreate vraagt.
      > 
      > 
2. Ophalen van de meest recente code Hallo van Hallo [Azure-IoT-Remote-Monitoring][lnk-remote-monitoring-github].
3. Uitvoeren van een lokale implementatie of een cloudimplementatie Hallo opdrachtregelprogramma implementatierichtlijnen in Hallo /docs/ map in de opslagplaats hello te volgen. 
4. Nadat u hebt uitgevoerd van een lokale implementatie of een cloudimplementatie, zoekt u naar in de hoofdmap voor Hallo *. user.config-bestand gemaakt tijdens de implementatie. Open dit bestand in een teksteditor. 
5. Wijziging Hallo volgende regel tooinclude Hallo waarde die u hebt gekopieerd uit uw **querysleutel**: 
   
   `<setting name="MapApiQueryKey" value="" />`

### <a name="can-i-create-a-preconfigured-solution-if-i-have-microsoft-azure-for-dreamspark"></a>Kan ik een vooraf geconfigureerde oplossing maken als ik Microsoft Azure voor DreamSpark heb?

Op dit moment kunt u een vooraf geconfigureerde oplossing met geen maken een [Microsoft Azure voor DreamSpark] [ lnk-dreamspark] account. U kunt echter maken een [gratis proefaccount voor Azure] [ lnk-30daytrial] binnen een paar minuten waarmee u een vooraf geconfigureerde oplossing maken.

### <a name="can-i-create-a-preconfigured-solution-if-i-have-cloud-solution-provider-csp-subscription"></a>Kan ik een vooraf geconfigureerde oplossing maken als ik Cloud Solution Provider (CSP) abonnement?

U kunt op dit moment een vooraf geconfigureerde oplossing maken met een abonnement Cloud Solution Provider (CSP). U kunt echter maken een [gratis proefaccount voor Azure] [ lnk-30daytrial] binnen een paar minuten waarmee u een vooraf geconfigureerde oplossing maken.

### <a name="how-do-i-delete-an-aad-tenant"></a>Hoe verwijder ik een AAD-tenant?

Zie het blogbericht van Eric Golpe van [overzicht van het verwijderen van een Azure AD-Tenant][lnk-delete-aad-tennant].

### <a name="next-steps"></a>Volgende stappen

U kunt ook verkennen van Hallo andere functies en mogelijkheden van Hallo vooraf geconfigureerde IoT Suite-oplossingen:

* [Overzicht van voorspeld onderhoud vooraf geconfigureerde oplossing][lnk-predictive-overview]
* [Overzicht van de verbonden factory vooraf geconfigureerde oplossing](iot-suite-connected-factory-overview.md)
* [Beveiliging van de IoT van Hallo gemalen][lnk-security-groundup]

[lnk-predictive-overview]: iot-suite-predictive-overview.md
[lnk-security-groundup]: securing-iot-ground-up.md

[link-azuresupportticket]: https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade 
[link-azuresublimits]: https://azure.microsoft.com/documentation/articles/azure-subscription-service-limits/#iot-hub-limits
[lnk-azure-portal]: https://portal.azure.com
[lnk-azureiotsuite]: https://www.azureiotsuite.com/
[lnk-classic-portal]: https://manage.windowsazure.com
[lnk-remote-monitoring-github]: https://github.com/Azure/azure-iot-remote-monitoring 
[lnk-dreamspark]: https://www.dreamspark.com/Product/Product.aspx?productid=99 
[lnk-30daytrial]: https://azure.microsoft.com/free/
[lnk-delete-aad-tennant]: http://blogs.msdn.com/b/ericgolpe/archive/2015/04/30/walkthrough-of-deleting-an-azure-ad-tenant.aspx
[lnk-cloud-deployment]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/cloud-deployment.md
[lnk-add-method]: iot-suite-guidance-on-customizing-preconfigured-solutions.md#add-support-for-a-new-method-to-the-simulator
[lnk-customize]: iot-suite-guidance-on-customizing-preconfigured-solutions.md
[lnk-remote-monitoring-github]: https://github.com/Azure/azure-iot-remote-monitoring
[lnk-predictive-maintenance-github]: https://github.com/Azure/azure-iot-predictive-maintenance
