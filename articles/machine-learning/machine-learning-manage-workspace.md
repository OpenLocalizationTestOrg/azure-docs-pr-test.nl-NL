---
title: een Machine Learning-werkruimte aaaManage | Microsoft Docs
description: Toegang tooAzure Machine Learning werkruimten, beheren en implementeren en beheren van ML API-webservices
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: daf3d413-7a77-4beb-9a7a-6b4bdf717719
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/27/2017
ms.author: garye
ms.openlocfilehash: 7bd378d82aa46f4340ca974c7dc5a612c089cdca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-an-azure-machine-learning-workspace"></a>Een Azure Machine Learning-werkruimte beheren

> [!NOTE]
> Zie voor meer informatie over het beheren van Web-services Hallo Machine Learning-webservices portal [hello Azure Machine Learning-webservices portal met een webservice beheren](machine-learning-manage-new-webservice.md).
> 
> 

U kunt de werkruimten Machine Learning in beide hello Azure-portal beheren of Hallo klassieke Azure-portal.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="use-hello-azure-portal"></a>Gebruik hello Azure-portal

toomanage een werkruimte in hello Azure-portal:

1. Meld u aan toohello [Azure-portal](https://portal.azure.com/) met een administrator-account Azure-abonnement.
2. Voer 'machine learning werkruimten' in het zoekvak Hallo bovenaan Hallo Hallo pagina, en selecteer vervolgens **Machine Learning-werkruimten**.
3. Klik op de gewenste toomanage Hallo-werkruimte.

Bovendien toohello standaard resource management informatie en opties die beschikbaar zijn, kunt u:

- Weergave **eigenschappen** : deze pagina Hallo werkruimte en resource-informatie wordt weergegeven en kunt u Hallo-abonnement en resourcegroep die deze werkruimte is verbonden met.
- **Opslagsleutels Resync** -Hallo werkruimte onderhoudt sleutels toohello storage-account. Als sleutels Hallo storage-account wordt gewijzigd, wordt u kunt klikken op **sleutels synchroniseren** toosynchronize Hallo sleutels met Hallo-werkruimte.

toomanage Hallo-webservices die zijn gekoppeld aan deze werkruimte Hallo Machine Learning-webservices portal gebruiken. Zie [hello Azure Machine Learning-webservices portal met een webservice beheren](machine-learning-manage-new-webservice.md) voor volledige informatie.

> [!NOTE]
> toodeploy of beheren van nieuwe webservices, moet u zijn toegewezen medewerker of beheerdersrol op Hallo abonnement toowhich Hallo-webservice wordt geïmplementeerd. Als u een andere gebruiker tooa machine learning-werkruimte uitnodigen, moet u ze toewijzen als tooa Inzender of administrator-rol op Hallo abonnement voordat ze kunnen implementeren of beheren van webservices. 
> 
>Zie voor meer informatie over toegangsmachtigingen instellen [toegangstoewijzingen weergeven voor gebruikers en groepen in Azure portal - openbare preview Hallo](../active-directory/role-based-access-control-manage-assignments.md).

## <a name="use-hello-azure-classic-portal"></a>Hallo klassieke Azure-portal gebruiken

Hallo klassieke Azure-portal kunt u uw werkruimten Machine Learning om te beheren:

* Controleren hoe Hallo werkruimte wordt gebruikt
* Hallo werkruimte tooallow configureren of weigeren van toegang
* Webservices die zijn gemaakt in de werkruimte Hallo beheren
* Hallo werkruimte verwijderen

Hallo-dashboardtabblad biedt bovendien een overzicht van het gebruik van uw werkruimte en een snelle weergave van uw werkruimtegegevens.  

> [!TIP]
> In Azure Machine Learning Studio, op Hallo **WEBSERVICES** tabblad, u kunt toevoegen, bijwerken of verwijderen van een Machine Learning-webservice.
> 
> 

een werkruimte in de klassieke Azure-portal Hallo toomanage:

1. Meld u aan toohello [klassieke Azure-portal](https://manage.windowsazure.com/) met uw Microsoft Azure-account - Hallo account gebruiken dat is gekoppeld aan hello Azure-abonnement.
2. In het Configuratiescherm Hallo Microsoft Azure-services, klikt u op **MACHINE LEARNING**.
3. Klik op de gewenste toomanage Hallo-werkruimte.

Hallo-pagina voor werkruimte heeft drie tabbladen:

* **DASHBOARD** -kunt u tooview werkruimte gebruiks- en informatie
* **CONFIGUREER** -kunt u toomanage access toohello-werkruimte
* **WEBSERVICES** -kunt u toomanage webservices die zijn gepubliceerd vanuit deze werkruimte

### <a name="toomonitor-how-hello-workspace-is-being-used"></a>toomonitor hoe Hallo werkruimte wordt gebruikt
Klik op Hallo **DASHBOARD** tabblad.

U kunt vanuit Hallo-dashboard algemene informatie over het gebruik van uw werkruimte weergeven en ophalen van een snelle weergave van informatie van de werkruimte.

* Hallo **COMPUTE** diagram toont de rekenresources hello wordt gebruikt door het Hallo-werkruimte. U kunt Hallo weergave toodisplay relatieve of absolute waarden wijzigen en u Hallo tijdsbestek weergegeven in de grafiek Hallo kan wijzigen.
* **Overzicht gebruik** Azure-opslag wordt gebruikt door Hallo werkruimte wordt weergegeven.
* **Snelle weergave** bevat een samenvatting van de werkruimte informatie en nuttige koppelingen.

> [!NOTE]
> Hallo **aanmelden tooML Studio** koppeling Hallo u momenteel bent aangemeld bij Microsoft-Account met behulp van Machine Learning Studio wordt geopend. Hallo u toosign in toohello Azure classic portal toocreate een werkruimte gebruikt Microsoft-Account heeft automatisch geen machtiging tooopen die werkruimte. tooopen een werkruimte, moet u zijn aangemeld toohello Microsoft-Account dat is gedefinieerd als eigenaar van de werkruimte Hallo Hallo of moet u een uitnodiging uit Hallo eigenaar toojoin Hallo werkruimte tooreceive.
> 
> 

### <a name="toogrant-or-suspend-access-for-users"></a>toogrant of onderbreken van toegang voor gebruikers
Klik op Hallo **configureren** tabblad.

U kunt van tabblad Hallo-configuratie:

* Toegang toohello Machine Learning-werkruimte onderbreken door te klikken op weigeren. Gebruikers kunnen niet meer kunnen tooopen Hallo werkruimte in Machine Learning Studio. toorestore openen, klikt u op toestaan.

toomanage extra accounts die hebben toegang tot toohello werkruimte in Machine Learning Studio, klikt u op **aanmelden tooML Studio** in Hallo **DASHBOARD** tabblad (Zie Hallo voorgaande opmerking met betrekking tot  **Sign-in tooML Studio**). Hiermee opent u de werkruimte Hallo in Machine Learning Studio. Klik op Hallo van hieruit **instellingen** tabblad en vervolgens **gebruikers**. U kunt klikken op **meer gebruikers UITNODIGEN** toogive gebruikers toegang tot toohello werkruimte, of Selecteer een gebruiker en klikt u op **verwijderen**.

### <a name="toomanage-web-services-in-this-workspace"></a>webservices toomanage in deze werkruimte
Klik op Hallo **WEBSERVICES** tabblad.

Dit geeft een lijst van webservices die worden gepubliceerd vanuit deze werkruimte.
toomanage een webservice, klikt u op Hallo-naam in Hallo lijst tooopen Hallo pagina van de webservice.

Een webservice heeft misschien een of meer eindpunten zijn gedefinieerd.

* U kunt meer eindpunten in toevoeging toohello 'Default' eindpunt definiëren. tooadd Hallo eindpunt, klikt u op **eindpunten beheren** onderaan Hallo Hallo dashboard tooopen hello Azure Machine Learning-webservices-portal.
* toodelete eindpunt (u kunt Hallo 'Default' eindpunt niet verwijderen), klik op het selectievakje Hallo aan Hallo begin van Hallo eindpunt rij en klikt u op **verwijderen**. Hiermee verwijdert u Hallo endpoint van Hallo-webservice.
  
  > [!NOTE]
  > Als een toepassing hello webservice-eindpunt wanneer Hallo-eindpunt wordt verwijderd, ontvangt de toepassing hello een Hallo fout volgende keer dat deze tooaccess Hallo-service probeert.
  > 
  > 

Klik op de naam van een Web service-eindpunt tooopen Hallo deze. 

U kunt algemene informatie over het gebruik van uw Web-service gedurende een periode weergeven vanuit Hallo-dashboard. U kunt Hallo periode tooview selecteren in Hallo periode vervolgkeuzemenu in de rechterbovenhoek Hallo Hallo gebruik grafieken. Hallo-dashboard ziet Hallo volgende informatie:

* **Aanvragen gedurende een periode** bevat een stap grafiek van Hallo aantal aanvragen gedurende Hallo geselecteerde periode. Kunt u identificeren als er pieken in gebruik.
* **Reactie op aanvragen aanvragen** Hallo kunt u het totale aantal aanvragen en antwoorden aanroepen Hallo-service heeft ontvangen via Hallo geselecteerde tijdsperiode en het aantal kunnen niet worden weergegeven.
* **Gemiddelde tijd voor aanvragen en antwoorden Compute** wordt een gemiddelde van tijd Hallo nodig tooexecute Hallo ontvangen aanvragen.
* **Batch-aanvragen** Hallo totaal aantal weergeven batchaanvragen Hallo service via Hallo geselecteerde periode heeft ontvangen en hoeveel is mislukt.
* **Gemiddelde latentie van de taak** wordt een gemiddelde van tijd Hallo nodig tooexecute Hallo ontvangen aanvragen.
* **Fouten** wordt Hallo cumulatieve aantal fouten die zijn opgetreden in aanroepen toohello-webservice.
* **Services-kosten** Hallo kosten voor Hallo-abonnement is gekoppeld aan het Hallo-service wordt weergegeven.

Vanaf de configuratiepagina hello, kunt u de volgende eigenschappen Hallo bijwerken:

* **Beschrijving** kunt u een beschrijving op voor Hallo webservice tooenter. De beschrijving is een verplicht veld.
* **Logboekregistratie** kunt u tooenable of schakelt u fout bij het aanmelden Hallo-eindpunt. Zie voor meer informatie over logboekregistratie inschakelen [logboekregistratie voor Machine Learning-webservices](machine-learning-web-services-logging.md).
* **Inschakelen van voorbeeldgegevens** kunt u voorbeeldgegevens tooprovide waarmee u tootest Hallo aanvraag en antwoord-service kunt. Als u de webservice Hallo in Machine Learning Studio gemaakt, Hallo voorbeeldgegevens is genomen van Hallo gegevens uw gebruikte tootrain uw model. Als u Hallo-service via een programma hebt gemaakt, worden Hallo gegevens worden opgehaald van Hallo bijvoorbeeld gegevens die u hebt opgegeven als onderdeel van Hallo JSON-pakket.

