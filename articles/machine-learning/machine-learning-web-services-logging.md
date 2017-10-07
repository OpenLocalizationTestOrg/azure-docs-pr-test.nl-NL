---
title: aaaLogging voor Machine Learning-webservices | Microsoft Docs
description: Meer informatie over hoe logboekregistratie tooenable voor Machine Learning-webservices. Logboekregistratie biedt aanvullende informatie toohelp oplossen Hallo API's.
services: machine-learning
documentationcenter: 
author: raymondlaghaeian
manager: jhubbard
editor: cgronlun
ms.assetid: c54d41e1-0300-46ef-bbfc-d6f7dca85086
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/15/2017
ms.author: raymondl;garye
ms.openlocfilehash: ed23933d52d2151af658af2307d7df8743071f65
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-logging-for-machine-learning-web-services"></a>Logboekregistratie inschakelen voor Machine Learning-webservices
Dit document bevat informatie over de mogelijkheden van Machine Learning-webservices logboekregistratie Hallo. Logboekregistratie biedt aanvullende informatie, dan slechts een foutnummer en een bericht die kan helpen bij het oplossen van uw aanroepen toohello Machine Learning API's.  

## <a name="how-tooenable-logging-for-a-web-service"></a>Hoe tooenable logboekregistratie voor een webservice

Inschakelen van logboekregistratie van Hallo [Azure Machine Learning-webservices](https://services.azureml.net) portal. 

1. Meld u aan toohello Azure Machine Learning-webservices-portal op [https://services.azureml.net](https://services.azureml.net). Voor een webservice klassiek kunt u ook toohello portal opvragen door te klikken op **nieuwe Services webervaring** op Hallo Machine Learning-webservices pagina in Machine Learning Studio.

   ![Nieuwe koppeling van de ervaring van de Web-Services](media/machine-learning-web-services-logging/new-web-services-experience-link.png)

2. Klik op de bovenste menubalk Hallo **Web Services** voor een nieuwe webservice of klik op **klassieke webservices** voor een klassiek webservice.

   ![Selecteer Nieuw of klassiek webservices](media/machine-learning-web-services-logging/select-web-service.png)

3. Een nieuwe webservice, klikt u op Hallo naam van de webservice. Voor een webservice klassieke op Hallo naam van de webservice en klik op de volgende pagina Hallo op Hallo juiste eindpunt.

4. Klik op de bovenste menubalk Hallo **configureren**.

5. Set Hallo **logboekregistratie inschakelen** te optie*fout* (toolog alleen fouten) of *alle* (voor volledige logboekregistratie).

   ![Niveau van logboekregistratie selecteren](media/machine-learning-web-services-logging/enable-logging.png)

6. Klik op **Opslaan**.

7. Voor klassieke webservices maken Hallo **ml diagnostics** container.

   Alle web service-logboeken worden opgeslagen in een blob-container met de naam **ml diagnostics** in Hallo storage-account is gekoppeld aan het Hallo-webservice. Voor nieuwe web-services, wordt deze container gemaakt Hallo eerste keer dat u toegang Hallo-webservice tot. Voor klassieke webservices moet u toocreate Hallo container als deze niet al bestaat. 

   1. In Hallo [Azure-portal](https://portal.azure.com), gaat u toohello storage-account is gekoppeld aan het Hallo-webservice.

   2. Onder **Blob-Service**, klikt u op **Containers**.

   3. Als Hallo container **ml diagnostics** niet bestaat, klikt u op **+ Container**, geven Hallo container Hallo naam 'ml-diagnostics' en selecteer Hallo **toegangstype** als 'Blob'. Klik op **OK**.

      ![Niveau van logboekregistratie selecteren](media/machine-learning-web-services-logging/create-ml-diagnostics-container.png)

> [!TIP]
>
> Hallo Web Services-Dashboard in Machine Learning Studio heeft ook een switch tooenable logboekregistratie voor een webservice klassiek. Aangezien logboekregistratie wordt nu beheerd via Hallo Web Services-portal, moet u echter tooenable logboekregistratie via Hallo-portal, zoals beschreven in dit artikel. Als u al ingeschakeld logboekregistratie in Studio, in Hallo Web Services-Portal, logboekregistratie uitschakelen en opnieuw inschakelen.


## <a name="hello-effects-of-enabling-logging"></a>Hallo gevolgen van het inschakelen van logboekregistratie
Als logboekregistratie is ingeschakeld, Hallo diagnostische gegevens en fouten van webservice-eindpunt Hallo worden vastgelegd in Hallo **ml diagnostics** blob-container in hello Azure Storage-Account gekoppeld aan van de gebruiker van het Hallo-werkruimte. Deze container bevat alle Hallo diagnostische gegevens voor alle Hallo webservice-eindpunten voor alle Hallo werkruimten die zijn gekoppeld aan dit opslagaccount.

Hallo logboeken kunnen worden weergegeven met behulp van een Hallo beschikbaar tooexplore van verschillende hulpprogramma's voor een Azure Storage-Account. Hallo eenvoudigste kan worden toonavigate toohello storage-account in hello Azure-portal, klikt u op **Containers**, en klik vervolgens op Hallo container **ml diagnostics**.  

## <a name="log-blob-detail-information"></a>Blob-logboekgegevens
Elke blob in de container Hallo bevat Hallo diagnostische gegevens voor exact één van de volgende activiteiten Hallo:

* De uitvoering van Hallo Batchuitvoering methode  
* Uitvoering van een van de methode Hallo aanvragen en antwoorden  
* Initialisatie van een container van aanvragen en antwoorden

Hallo-naam van elke blob heeft een voorvoegsel Hallo formulier te volgen: 


`{Workspace Id}-{Web service Id}-{Endpoint Id}/{Log type}`


Waar _type logboek registreren_ is een van de volgende waarden Hallo:  

* Batch  
* score/aanvragen  
* score/init  

