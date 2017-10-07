---
title: 'Problemen oplossen: Maken en koppelen van Machine Learning-werkruimte tooa | Microsoft Docs'
description: Oplossingen voor algemene problemen bij het maken en verbinding maken met tooan Azure Machine Learning-werkruimte
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 1a8aec4b-35f9-44e8-9570-2575b8979ab1
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: garye
ms.openlocfilehash: 965a0025e85ba4e22c2b037edfa923e7f7599069
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-guide-create-and-connect-tooan-machine-learning-workspace"></a>Gids voor probleemoplossing: maken en koppelen tooan Machine Learning-werkruimte
Deze handleiding bevat oplossingen voor enkele uitdagingen vaak aangetroffen bij het instellen van Azure Machine Learning-werkruimten.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="workspace-owner"></a>De eigenaar van de werkruimte
tooopen een werkruimte in Machine Learning Studio, moet u zijn aangemeld toohello Microsoft-Account gebruikt toocreate Hallo werkruimte of moet u een uitnodiging uit Hallo eigenaar toojoin Hallo werkruimte tooreceive. U kunt hello Azure-portal Hallo-werkruimte, waaronder Hallo mogelijkheid tooconfigure toegang beheren.

Zie voor meer informatie over het beheren van een werkruimte [beheren van een Azure Machine Learning-werkruimte].

[beheren van een Azure Machine Learning-werkruimte]: machine-learning-manage-workspace.md

## <a name="allowed-regions"></a>Toegestane regio 's
Machine Learning is momenteel beschikbaar in een beperkt aantal regio's. Als uw abonnement niet onder een van deze gebieden, wordt er fout het Hallo-bericht, 'U hebt geen abonnementen in Hallo regio's toegestaan.'

toorequest die een regio zijn tooyour abonnement toegevoegd, een nieuw Microsoft-ondersteuningsverzoek maken vanuit hello Azure-portal, kies **facturering** als Hallo probleemtype en volg Hallo vraagt toosubmit uw aanvraag.

## <a name="storage-account"></a>Storage-account
Hallo Machine Learning-service moet een storage account toostore-gegevens. U kunt een bestaand opslagaccount gebruiken of u kunt een nieuw opslagaccount maken bij het maken van de nieuwe Machine Learning-werkruimte hello (als u een nieuw opslagaccount quotum toocreate hebt).

Nadat de nieuwe Machine Learning-werkruimte Hallo is gemaakt, kunt u tooMachine Learning Studio aanmelden met behulp van Microsoft-account Hallo toocreate Hallo werkruimte die wordt gebruikt. Als u het foutbericht Hallo tegenkomt, gebruik 'Werkruimte niet gevonden' (vergelijkbaar toohello volgende schermopname), Hallo toodelete stappen te volgen cookies in de browser.

![Werkruimte niet gevonden][screen3]

**browsercookies toodelete**

1. Als u Internet Explorer gebruikt, klikt u op Hallo **extra** in de rechterbovenhoek Hallo en selecteer **Internetopties**.  

![Internet-opties][screen4]

2. Onder Hallo **algemene** tabblad **verwijderen...**

![Tabblad Algemeen][screen5]

3. In Hallo **Browsegeschiedenis verwijderen** dialoogvenster zorg **Cookies en websitegegevens** is geselecteerd en klik op **verwijderen**.

![Verwijderen van cookies][screen6]

Hallo cookies zijn verwijderd, start Hallo browser opnieuw en ga toohello [Microsoft Azure Machine Learning](https://studio.azureml.net) pagina. Wanneer u wordt gevraagd een gebruikersnaam en wachtwoord, voert u Hallo hetzelfde Microsoft-account toocreate Hallo werkruimte die wordt gebruikt.

## <a name="comments"></a>Opmerkingen

Ons doel is toomake Hallo Machine Learning-ervaring zo weinig mogelijk. Neem na de eventuele opmerkingen en problemen op Hallo [Azure Machine Learning-forum](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=MachineLearning) toohelp ons u beter bedienen.

[screen1]:media/machine-learning-troubleshooting-creating-ml-workspace/screen1.png
[screen2]:media/machine-learning-troubleshooting-creating-ml-workspace/screen2.png
[screen3]:media/machine-learning-troubleshooting-creating-ml-workspace/screen3.png
[screen4]:media/machine-learning-troubleshooting-creating-ml-workspace/screen4.png
[screen5]:media/machine-learning-troubleshooting-creating-ml-workspace/screen5.png
[screen6]:media/machine-learning-troubleshooting-creating-ml-workspace/screen6.png
