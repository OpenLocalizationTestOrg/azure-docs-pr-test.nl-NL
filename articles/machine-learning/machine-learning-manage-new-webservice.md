---
title: aaaUse hello Azure Machine Learning-webservices portal | Microsoft Docs
description: Toegang tooAzure Machine Learning werkruimten, beheren en implementeren en beheren van ML API-webservices
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: jhubbard
editor: cgronlun
ms.assetid: b62cf2ca-dd2a-4a83-bb54-469f948fb026
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/28/2017
ms.author: v-donglo
ms.openlocfilehash: 04b49027fc0ab227382b320310088bb66aafacc6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-a-web-service-using-hello-azure-machine-learning-web-services-portal"></a>Een webservice met hello Azure Machine Learning-webservices portal beheren
U kunt uw Machine Learning nieuwe en klassieke Web services met behulp van Hallo Microsoft Azure Machine Learning-webservices portal beheren. Aangezien klassieke webservices en nieuwe Web-services zijn gebaseerd op verschillende onderliggende technologieën, hebt u iets anders beheermogelijkheden voor elk van deze.

U kunt in Hallo Machine Learning-webservices-portal:

* Controleren hoe Hallo-webservice wordt gebruikt.
* Hallo beschrijving configureren, bijwerken Hallo sleutels voor Hallo web service (alleen nieuw), uw storage-account key (nieuw alleen) inschakelen aan te melden, bijwerken en in- of uitschakelen voorbeeldgegevens.
* Hallo webservice verwijderen.
* Maak, delete of update facturering plannen (alleen nieuw).
* Toevoegen en verwijderen van eindpunten (alleen klassiek)

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="permissions-toomanage-new-resources-manager-based-web-services"></a>Machtigingen toomanage nieuwe Resources Manager op basis van webservices

Nieuwe webservices worden geïmplementeerd als Azure-resources. U moet als zodanig hebben Hallo gemachtigd toodeploy en beheren van nieuwe webservices.  toodeploy of beheren van nieuwe webservices, moet u zijn toegewezen medewerker of beheerdersrol op Hallo abonnement toowhich Hallo-webservice wordt geïmplementeerd. Als u een andere gebruiker tooa machine learning-werkruimte uitnodigen, moet u ze toewijzen als tooa Inzender of administrator-rol op Hallo abonnement voordat ze kunnen implementeren of beheren van webservices. 

Als het Hallo-gebruiker heeft geen machtigingen tooaccess resources in Azure Machine Learning-webservices-portal Hallo corrigeren Hallo, ontvangt deze Hallo volgende fout wanneer u probeert toodeploy een webservice:

*Web Service-implementatie is mislukt. Dit account heeft niet voldoende toegang toohello Azure-abonnement dat Hallo werkruimte bevat. Toodeploy een webservice-tooAzure Hallo moet hetzelfde account zijn uitgenodigd toohello werkruimte en worden bepaalde access toohello Azure-abonnement dat Hallo werkruimte bevat.*

Zie voor meer informatie over het maken van een werkruimte [maken en delen van een Azure Machine Learning-werkruimte](machine-learning-create-workspace.md).

Zie voor meer informatie over toegangsmachtigingen instellen [toegangstoewijzingen weergeven voor gebruikers en groepen in Azure portal - openbare preview Hallo](../active-directory/role-based-access-control-manage-assignments.md).


## <a name="manage-new-web-services"></a>Nieuwe Web-services beheren
toomanage uw nieuwe Web-services:

1. Meld u aan toohello [Microsoft Azure Machine Learning-webservices](https://services.azureml.net/quickstart) portal met de Hallo account gebruiken dat gekoppeld aan uw Microsoft Azure-account - hello Azure-abonnement.
2. Klik op het menu Hallo **webservices**.

Dit geeft een lijst met geïmplementeerde Web-services voor uw abonnement. 

toomanage een webservice, klikt u op Web-Services. U kunt via Hallo Web Services-pagina:

* Klik op Hallo web service toomanage deze.
* Klik op Hallo facturering plannen voor Hallo web service tooupdate deze.
* Verwijderen van een webservice.
* Kopieer een webservice en implementeert u deze tooanother regio.

Wanneer u een webservice klikt, wordt de service Hallo-Quick Start webpagina geopend. Hallo pagina Quick Start webservice heeft twee opties waarmee u toomanage uw webservice:

* **DASHBOARD** -kunt u gebruik van tooview-service.
* **CONFIGUREER** - kunt u tooadd beschrijvende tekst update Hallo sleutel voor Hallo storage-account is gekoppeld aan Hallo webservice, en in- of uitschakelen voorbeeldgegevens.

### <a name="monitoring-how-hello-web-service-is-being-used"></a>Bewaking hoe Hallo-webservice wordt gebruikt
Klik op Hallo **DASHBOARD** tabblad.

U kunt algemene informatie over het gebruik van uw Web-service gedurende een periode weergeven vanuit Hallo-dashboard. U kunt Hallo periode tooview selecteren in Hallo periode vervolgkeuzemenu in de rechterbovenhoek Hallo Hallo gebruik grafieken. Hallo-dashboard ziet Hallo volgende informatie:

* **Aanvragen gedurende een periode** bevat een stap grafiek van Hallo aantal aanvragen gedurende Hallo geselecteerde periode. Kunt u identificeren als er pieken in gebruik.
* **Reactie op aanvragen aanvragen** Hallo kunt u het totale aantal aanvragen en antwoorden aanroepen Hallo-service heeft ontvangen via Hallo geselecteerde tijdsperiode en het aantal kunnen niet worden weergegeven.
* **Gemiddelde tijd voor aanvragen en antwoorden Compute** wordt een gemiddelde van tijd Hallo nodig tooexecute Hallo ontvangen aanvragen.
* **Batch-aanvragen** Hallo totaal aantal weergeven batchaanvragen Hallo service via Hallo geselecteerde periode heeft ontvangen en hoeveel is mislukt.
* **Gemiddelde latentie van de taak** wordt een gemiddelde van tijd Hallo nodig tooexecute Hallo ontvangen aanvragen.
* **Fouten** wordt Hallo cumulatieve aantal fouten die zijn opgetreden in aanroepen toohello-webservice.
* **Services-kosten** Hallo kosten voor Hallo-abonnement is gekoppeld aan het Hallo-service wordt weergegeven.

### <a name="configuring-hello-web-service"></a>Hallo-webservice configureren
Klik op Hallo **configureren** menuoptie.

Kunt u de volgende eigenschappen Hallo bijwerken:

* **Beschrijving** kunt u een beschrijving op voor Hallo webservice tooenter.
* **Titel** kunt u tooenter een titel voor het Hallo-webservice
* **Sleutels** toorotate, kunt u uw API primaire en secundaire sleutels.
* **Opslagaccountsleutel** kunt u tooupdate Hallo sleutel voor Hallo storage-account is gekoppeld aan Hallo Web servicewijzigingen. 
* **Inschakelen van voorbeeldgegevens** kunt u voorbeeldgegevens tooprovide waarmee u tootest Hallo aanvraag en antwoord-service kunt. Als u de webservice Hallo in Machine Learning Studio gemaakt, Hallo voorbeeldgegevens is genomen van Hallo gegevens uw gebruikte tootrain uw model. Als u Hallo-service via een programma hebt gemaakt, worden Hallo gegevens worden opgehaald van Hallo bijvoorbeeld gegevens die u hebt opgegeven als onderdeel van Hallo JSON-pakket.

### <a name="managing-billing-plans"></a>Het beheren van facturerings plannen
Klik op Hallo **plannen** menuoptie van de pagina Quick Start Hallo web-services. U kunt ook klikken op Hallo plan die zijn gekoppeld aan specifieke toomanage van de Web service die u van plan bent.

* **Nieuwe** kunt u een nieuw plan toocreate.
* **Abonnement toevoegen of verwijderen exemplaar** kunt u te 'uitschalen' een bestaand plan tooadd capaciteit.
* **Upgrade/DownGrade** kunt u te 'opschalen' een bestaand plan tooadd capaciteit.
* **Verwijder** kunt u een plan toodelete.

Klik op een tooview plan het dashboard. Hallo dashboard biedt u een momentopname of plan gebruik gedurende een geselecteerde periode. tooselect tijd periode tooview hello, klikt u op Hallo **periode** vervolgkeuzelijst in de rechterbovenhoek Hallo van dashboard. 

Hallo plan dashboard biedt Hallo volgende informatie:

* **Beschrijving van plan bent** geeft informatie weer over Hallo kosten en capaciteit die zijn gekoppeld aan het Hallo-plan.
* **Informatie over het gebruik van plan bent** Hallo aantal transacties en rekenuren die in rekening tegen Hallo plan gebracht is.
* **Webservices** geeft Hallo aantal Web-services die van dit plan gebruikmaken.
* **Top Webserviceaanroepen** Hallo boven vier webservices die aanroepen die in rekening tegen Hallo plan gebracht worden maken wordt weergegeven.
* **Web-Services door Compute uur Top** Hallo boven vier Web-services die gebruikmaken van rekenresources die in rekening tegen Hallo plan gebracht worden wordt weergegeven.

## <a name="manage-classic-web-services"></a>Klassieke webservices beheren
> [!NOTE]
> Hallo procedures in deze sectie zijn relevante toomanaging klassieke webservices via hello Azure Machine Learning-webservices-portal. Voor informatie over het beheren van klassieke Web services via Machine Learning Studio Hallo en hello Azure classic portal, Zie [beheren van een Azure Machine Learning-werkruimte](machine-learning-manage-workspace.md).
> 
> 

toomanage klassieke webservices:

1. Meld u aan toohello [Microsoft Azure Machine Learning-webservices](https://services.azureml.net/quickstart) portal met de Hallo account gebruiken dat gekoppeld aan uw Microsoft Azure-account - hello Azure-abonnement.
2. Klik op het menu Hallo **klassieke webservices**.

toomanage een klassieke webservice, klikt u op **klassieke webservices**. U kunt van Hallo klassieke Web Services-pagina:

* Klik op Hallo webservice-tooview Hallo gekoppeld eindpunten.
* Verwijderen van een webservice.

Wanneer u een klassieke webservice beheert, beheren u elke Hallo eindpunten afzonderlijk. Wanneer u een webservice in Hallo webservices pagina klikt, wordt Hallo-lijst met eindpunten die zijn gekoppeld aan het Hallo-service wordt geopend. 

U kunt op Hallo klassieke webservice-eindpunt pagina toevoegen en verwijderen van eindpunten op Hallo-service. Zie voor meer informatie over het toevoegen van eindpunten [eindpunten maken](machine-learning-create-endpoint.md).

Klik op een Hallo eindpunten tooopen Hallo Quick Start pagina van de webservice. Op de pagina Quick Start Hallo zijn er twee opties waarmee u toomanage uw webservice:

* **DASHBOARD** -kunt u gebruik van tooview-service.
* **CONFIGUREER** -kunt u beschrijvende tekst tooadd inschakelen fout logboekregistratie in- en uitschakelen update Hallo sleutel voor Hallo storage-account is gekoppeld aan Hallo webservice, en in- en uitschakelen van voorbeeldgegevens.

### <a name="monitoring-how-hello-web-service-is-being-used"></a>Bewaking hoe Hallo-webservice wordt gebruikt
Klik op Hallo **DASHBOARD** tabblad.

U kunt algemene informatie over het gebruik van uw Web-service gedurende een periode weergeven vanuit Hallo-dashboard. U kunt Hallo periode tooview selecteren in Hallo periode vervolgkeuzemenu in de rechterbovenhoek Hallo Hallo gebruik grafieken. Hallo-dashboard ziet Hallo volgende informatie:

* **Aanvragen gedurende een periode** bevat een stap grafiek van Hallo aantal aanvragen gedurende Hallo geselecteerde periode. Kunt u identificeren als er pieken in gebruik.
* **Reactie op aanvragen aanvragen** Hallo kunt u het totale aantal aanvragen en antwoorden aanroepen Hallo-service heeft ontvangen via Hallo geselecteerde tijdsperiode en het aantal kunnen niet worden weergegeven.
* **Gemiddelde tijd voor aanvragen en antwoorden Compute** wordt een gemiddelde van tijd Hallo nodig tooexecute Hallo ontvangen aanvragen.
* **Batch-aanvragen** Hallo totaal aantal weergeven batchaanvragen Hallo service via Hallo geselecteerde periode heeft ontvangen en hoeveel is mislukt.
* **Gemiddelde latentie van de taak** wordt een gemiddelde van tijd Hallo nodig tooexecute Hallo ontvangen aanvragen.
* **Fouten** wordt Hallo cumulatieve aantal fouten die zijn opgetreden in aanroepen toohello-webservice.
* **Services-kosten** Hallo kosten voor Hallo-abonnement is gekoppeld aan het Hallo-service wordt weergegeven.

### <a name="configuring-hello-web-service"></a>Hallo-webservice configureren
Klik op Hallo **configureren** menuoptie.

Kunt u de volgende eigenschappen Hallo bijwerken:

* **Beschrijving** kunt u een beschrijving op voor Hallo webservice tooenter. De beschrijving is een verplicht veld.
* **Logboekregistratie** kunt u tooenable of schakelt u fout bij het aanmelden Hallo-eindpunt. Zie voor meer informatie over logboekregistratie inschakelen [logboekregistratie voor Machine Learning-webservices](machine-learning-web-services-logging.md).
* **Inschakelen van voorbeeldgegevens** kunt u voorbeeldgegevens tooprovide waarmee u tootest Hallo aanvraag en antwoord-service kunt. Als u de webservice Hallo in Machine Learning Studio gemaakt, Hallo voorbeeldgegevens is genomen van Hallo gegevens uw gebruikte tootrain uw model. Als u Hallo-service via een programma hebt gemaakt, worden Hallo gegevens worden opgehaald van Hallo bijvoorbeeld gegevens die u hebt opgegeven als onderdeel van Hallo JSON-pakket.

## <a name="grant-or-suspend-access-tooweb-services-for-users-in-hello-portal"></a>Verleen of onderbreken tooWeb toegangsservices voor gebruikers in Hallo-portal
Hallo klassieke Azure-portal gebruikt, kunt u toestaan of toospecific gebruikers de toegang weigert.

### <a name="access-for-users-of-new-web-services"></a>Toegang voor gebruikers van de nieuwe Web-services
tooenable andere toowork gebruikers met uw Web-services in hello Azure Machine Learning-webservices-portal, moet u ze toevoegen als co-beheerders voor uw Azure-abonnement.

Meld u aan toohello [klassieke Azure-portal](https://manage.windowsazure.com/) met uw Microsoft Azure-account - Hallo account gebruiken dat is gekoppeld aan hello Azure-abonnement.

1. Klik in het navigatiedeelvenster hello, **instellingen**, klikt u vervolgens op **beheerders**.
2. Aan de onderkant van de Hallo van Hallo-venster, klikt u op **toevoegen**. 
3. In het dialoogvenster ADD A CO-ADMINISTRATOR hello, is type Hallo e-mailadres van de gewenste Hallo persoon tooadd als medebeheerder, en selecteer vervolgens Hallo-abonnement dat u wilt dat Hallo medebeheerder tooaccess.
4. Klik op **Opslaan**.

### <a name="access-for-users-of-classic-web-services"></a>Toegang voor gebruikers van klassieke webservices
toomanage een werkruimte:

Meld u aan toohello [klassieke Azure-portal](https://manage.windowsazure.com/) met uw Microsoft Azure-account - Hallo account gebruiken dat is gekoppeld aan hello Azure-abonnement.

1. In het Configuratiescherm Hallo Microsoft Azure-services, klikt u op **MACHINE LEARNING**.
2. Klik op de gewenste toomanage Hallo-werkruimte.
3. Klik op Hallo **configureren** tabblad.

U kunt vanaf het tabblad configuratie Hallo toegang toohello Machine Learning-werkruimte uitstellen door te klikken op **weigeren**. Gebruikers kunnen niet meer kunnen tooopen Hallo werkruimte in Machine Learning Studio. toegang tot toorestore, klikt u op **toestaan**.

toospecific gebruikers:

toomanage extra accounts die hebben toegang tot toohello werkruimte in Machine Learning Studio, klikt u op **aanmelden tooML Studio** in Hallo **DASHBOARD** tabblad. Hiermee opent u de werkruimte Hallo in Machine Learning Studio. Klik op Hallo van hieruit **instellingen** tabblad en vervolgens **gebruikers**. U kunt klikken op **meer gebruikers UITNODIGEN** toogive gebruikers toegang tot toohello werkruimte, of Selecteer een gebruiker en klikt u op **verwijderen**.

> [!NOTE]
> Hallo **aanmelden tooML Studio** koppeling Hallo u momenteel bent aangemeld bij Microsoft-Account met behulp van Machine Learning Studio wordt geopend. Hallo u toosign in toohello Azure classic portal toocreate een werkruimte gebruikt Microsoft-Account heeft automatisch geen machtiging tooopen die werkruimte. tooopen een werkruimte, moet u zijn aangemeld toohello Microsoft-Account dat is gedefinieerd als eigenaar van de werkruimte Hallo Hallo of moet u een uitnodiging uit Hallo eigenaar toojoin Hallo werkruimte tooreceive.
> 
> 

