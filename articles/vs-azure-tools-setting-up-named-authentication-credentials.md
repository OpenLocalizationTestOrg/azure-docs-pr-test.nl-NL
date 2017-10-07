---
title: aaaSetting Up met de naam verificatiereferenties | Microsoft Docs
description: 'Meer informatie over hoe tootooprovide referenties waarmee Visual Studio tooauthenticate aanvragen tooAzure toopublish een tooAzure toepassing vanuit Visual Studio of een bestaande toomonitor kunt cloudservice... '
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 61570907-42a1-40e8-bcd6-952b21a55786
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 8/22/2017
ms.author: kraigb
ms.openlocfilehash: 3cc147a2f7a3e766293ca282f56078cf24281346
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="setting-up-named-authentication-credentials"></a>Benoemde verificatiereferenties in te stellen
een toepassing tooAzure vanuit Visual Studio of een bestaande cloudservice toomonitor toopublish, moet u referenties opgeven waarmee Visual Studio tooauthenticate kunt tooAzure-aanvragen. Er zijn verschillende plaatsen in Visual Studio, waar u zich in tooprovide deze referenties aanmelden kunt. Vanuit Hallo Server Explorer, kunt u bijvoorbeeld Hallo snelmenu voor Hallo openen **Azure** knooppunt en kies **tooMicrosoft Azure-abonnement verbinden...** . Wanneer u zich aanmeldt, Hallo abonnement informatie die is gekoppeld aan uw Azure-account is beschikbaar in Visual Studio en er is niets meer dat u toodo hebt.

Azure-hulpprogramma's ondersteunt ook een oudere manier van het bieden van referenties, het gebruik van Hallo abonnementsbestand (.publishsettings-bestand). Dit onderwerp beschrijft deze methode wordt nog steeds ondersteund in de Azure SDK 2.2.

Hallo volgende items zijn vereist voor verificatie tooAzure:

* Uw abonnements-ID
* Een geldig X.509 v3-certificaat

> [!NOTE]
> Hallo-lengte van sleutel Hallo X.509 v3-certificaat moet ten minste 2048 bits. Azure weigert alle certificaten die niet voldoen aan deze eis of die is niet geldig.
>
>

Visual Studio gebruikt uw abonnements-ID samen met de certificaatgegevens Hallo als referenties. de juiste referenties Hello wordt verwezen in Hallo abonnementsbestand (.publishsettings-bestand) dat een openbare sleutel voor Hallo certificaat bevat. Hallo abonnementsbestand kan referenties voor meer dan één abonnement bevatten.

Kunt u de abonnementsgegevens Hallo van Hallo **nieuw/bewerken abonnement** in het dialoogvenster zoals verderop in dit onderwerp wordt uitgelegd.

Als u toocreate een certificaat zelf wilt, raadpleegt u de instructies toohello in [maken en uploaden van een Beheercertificaat voor Azure](https://msdn.microsoft.com/library/windowsazure/gg551722.aspx) en vervolgens handmatig uploaden Hallo certificaat toohello [klassieke Azure-portal ](http://go.microsoft.com/fwlink/?LinkID=213885).

> [!NOTE]
> Deze referenties die Visual Studio toomanage die uw cloudservices zijn niet vereist Hallo dezelfde referenties die vereist tooauthenticate zijn een aanvraag in voor hello Azure storage-services.
>
>

## <a name="import-set-up-or-edit-authentication-credentials-in-visual-studio"></a>Importeren, instellen of bewerken van referenties voor verificatie in Visual Studio
U kunt importeren, instellen of wijzigen van uw referenties voor verificatie in Hallo **nieuw abonnement** in het dialoogvenster dat wordt weergegeven als u Hallo na actie uitvoeren:

* In **Server Explorer**Open Hallo snelmenu voor Hallo **Azure** knooppunt, kies **beheren en Filter abonnementen...** , kies Hallo **certificaten** tabblad en voer een van de volgende Hallo:

    * Kies **importeren** tooopen Hallo Microsoft Azure-abonnementen importeren dialoogvenster waarin u Hallo abonnementen bestand voor Hallo momenteel downloaden kunt geladen abonnement, bladeren tooits downloadlocatie en vervolgens importeren voor gebruik in -verificatie.
    * Kies **nieuw** tooopen Hallo nieuw abonnement dialoogvenster waarin u een nieuw abonnement voor gebruik bij verificatie kunt instellen.
    * Kies **bewerken** (na uw actief abonnement te kiezen) tooopen Hallo abonnement bewerken dialoogvenster waarin u een bestaand abonnement voor gebruik bij verificatie kunt bewerken. 

Hallo volgende procedure wordt ervan uitgegaan dat Hallo **nieuw abonnement** dialoogvenster is geopend.

### <a name="tooset-up-authentication-credentials-in-visual-studio"></a>tooset up verificatiereferenties in Visual Studio
1. In Hallo **Selecteer een bestaand certificaat** voor verificatielijst, selecteer een certificaat.
2. Kies Hallo **volledig pad kopiëren Hallo** koppeling. Hallo-pad voor Hallo-certificaat (.cer-bestand) is gekopieerde toohello Klembord.

   > [!IMPORTANT]
   > toopublish uw Azure-toepassing vanuit Visual Studio, moet u deze toohello certificaat uploaden [Azure-portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).
   >
   >
3. tooupload hello certificaat toohello Azure-portal:

   1. Open Hallo [Azure-portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).
   2. Als u wordt gevraagd, toohello portal aanmelden en navigeert u vervolgens te**instellingen**, **Beheercertificaten**.
   3. Kies in Hallo Management certificaten deelvenster **uploaden**.
   4. Selecteer uw Azure-abonnement, plak Hallo volledige pad van Hallo cer-bestand dat u zojuist hebt gemaakt en kies **uploaden**.
