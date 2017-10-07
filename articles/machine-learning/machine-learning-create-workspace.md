---
title: een Machine Learning-werkruimte aaaCreate | Microsoft Docs
description: Hoe toocreate een werkruimte voor Azure Machine Learning Studio
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: aa96b784-ac6c-44bc-a28a-85d49fbe90a2
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/27/2017
ms.author: garye;bradsev;ahgyger
ms.openlocfilehash: 178293af222365993fade666124f34269d892325
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-share-an-azure-machine-learning-workspace"></a>Een Azure Machine Learning-werkruimte maken en delen
Dit menu koppelingen tootopics waarin wordt beschreven hoe tooset up Hallo verschillende gegevens wetenschappelijke omgevingen gebruikt door Hallo Cortana Analytics proces (CAP's).

[!INCLUDE [data-science-environment-setup](../../includes/cap-setup-environments.md)]

Azure Machine Learning Studio toouse, moet u toohave een Machine Learning-werkruimte. Deze werkruimte bevat Hallo hulpmiddelen die u nodig hebt toocreate, beheren en experimenten publiceren.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

### <a name="toocreate-a-workspace"></a>toocreate een werkruimte
1. Meld u aan toohello [Azure-portal](https://portal.azure.com/)

    > [!NOTE]
    > toosign in en een werkruimte maken, moet u toobe Azure-abonnementbeheerder. 
    >
    > 

2. Klik op **+ nieuw**

3. Selecteer **Intelligence en analyse**, klikt u op **Machine Learning-werkruimte**, klikt u vervolgens op **maken**

4. Voer uw werkruimtegegevens

    - Hallo *Werkruimtenaam* mogelijk up too260 tekens, niet eindigen met een spatie. Hallo-naam kan niet deze tekens bevatten:`< > * % & : \ ? + /`
    - Hallo *web service-abonnement* u kiest (of maken), samen met de Hallo gekoppeld *prijscategorie* u selecteert, wordt gebruikt als u web-services uit deze werkruimte implementeert.

    ![Maak een nieuwe werkruimte](media/machine-learning-create-workspace/create-new-workspace.png)

5. Klik op **Maken**.

Zodra Hallo werkruimte is geïmplementeerd, kunt u deze kunt openen in Machine Learning Studio.

1. Blader tooMachine Learning Studio op [https://studio.azureml.net/](https://studio.azureml.net/).

2. Selecteer uw werkruimte in Hallo upper--rechterhoek.

    ![Werkruimte selecteren](media/machine-learning-create-workspace/open-workspace.png)

3. Klik op **mijn experimenten**.

    ![Open experimenten](media/machine-learning-create-workspace/my-experiments.png)

Zie voor meer informatie over het beheren van uw werkruimte [beheren van een Azure Machine Learning-werkruimte](machine-learning-manage-workspace.md).
Als er een probleem bij het maken van uw werkruimte optreden, Raadpleeg [Troubleshooting guide: maken en koppelen van de Machine Learning-werkruimte tooa](machine-learning-troubleshooting-creating-ml-workspace.md).


## <a name="sharing-an-azure-machine-learning-workspace"></a>Delen van een Azure Machine Learning-werkruimte
Zodra een Machine Learning-werkruimte is gemaakt, kunt u uitnodigen gebruikers tooyour werkruimte tooshare toegang tooyour werkruimte en alle bijbehorende experimenten, gegevenssets, laptops, enzovoort. U kunt gebruikers toevoegen in een van twee functies:

* **Gebruiker** -werkruimte van een gebruiker kunt maken, openen, wijzigen en experimenten, gegevenssets, enz. in de werkruimte Hallo verwijderen.
* **Eigenaar** - eigenaar kunt uitnodigen en gebruikers in de werkruimte Hallo in toowhat toevoeging van een gebruiker verwijderen kunnen doen.

> [!NOTE]
> Hallo administrator-account dat Hallo werkruimte maakt toohello werkruimte automatisch toegevoegd als eigenaar-werkruimte. Echter andere beheerders of gebruikers in de betreffende abonnement zijn niet automatisch toegangsrechten toohello-werkruimte: u hebt tooinvite nodig ze expliciet.
> 
> 

### <a name="tooshare-a-workspace"></a>tooshare een werkruimte

1. Meld u aan tooMachine Learning Studio [https://studio.azureml.net/Home](https://studio.azureml.net/Home)

2. Klik in het linkerdeelvenster Hallo **instellingen**

3. Klik op Hallo **gebruikers** tabblad

4. Klik op **meer gebruikers UITNODIGEN** onderaan Hallo Hallo pagina

    ![Studio-instellingen](media/machine-learning-create-workspace/settings.png)

5. Voer een of meer e-mailadressen. Hallo-gebruikers moeten een geldig Microsoft-account of een organisatie-account (van Azure Active Directory).

6. Selecteer of u wilt dat tooadd Hallo gebruikers als eigenaar of gebruiker.

7. Klik op Hallo **OK** vinkje knop.

Elke gebruiker die u toevoegt, ontvangt een e-mail met instructies over hoe toosign in toohello werkruimte gedeeld.

> [!NOTE]
> Voor gebruikers toobe kunnen toodeploy of webservices in deze werkruimte wilt beheren, moeten ze een bijdrager of een beheerder in hello Azure-abonnement. 



