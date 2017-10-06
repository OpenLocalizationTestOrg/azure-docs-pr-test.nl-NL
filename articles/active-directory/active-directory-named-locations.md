---
title: aaaNamed locaties in Azure Active Directory | Microsoft Docs
description: Door te configureren met de naam locaties, kunt u voorkomen dat IP-adressen die eigendom zijn van uw organisatie valse positieven genereren voor Hallo onmogelijke reis tooatypical locaties gebeurtenistype risico.
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: f56e042a-78d5-4ea3-be33-94004f2a0fc3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 591e4b94b2ec9d45e20c01711e922f9972e047e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="named-locations-in-azure-active-directory"></a>Benoemde locaties in Azure Active Directory

Met Hallo met de naam locaties functie van Azure Active Directory, kunt u een vertrouwde IP-adresbereiken label in uw organisatie. In uw omgeving, kunt u met de naam locaties in de context van Hallo van Hallo detectie van [bestaat de kans dat gebeurtenissen](active-directory-reporting-risk-events.md). Hallo functie vermindert het aantal gerapporteerde fout-positieven voor Hallo Hallo *onmogelijke reis tooatypical locaties* gebeurtenistype risico. 

## <a name="configuration"></a>Configuratie

tooconfigure een benoemde locatie:

1. Meld u aan toohello [Azure-portal](https://portal.azure.com) als globale beheerder.

2. Klik in het linkerdeelvenster Hallo **Azure Active Directory**.

    ![Hello Azure Active Directory-koppeling in het linkerdeelvenster Hallo](./media/active-directory-named-locations/01.png)

3. Op Hallo **Azure Active Directory** blade in Hallo **beveiliging** sectie, klikt u op **voorwaardelijke toegang**.

    ![Hallo opdracht voorwaardelijke toegang](./media/active-directory-named-locations/05.png)


4. Op Hallo **voorwaardelijke toegang** blade in Hallo **beheren** sectie, klikt u op **locaties met de naam**.

    ![Hallo benoemde locaties opdracht](./media/active-directory-named-locations/06.png)


5. Op Hallo **locaties met de naam** blade, klikt u op **nieuwe locatie**.

    ![Hallo nieuwe locatie-opdracht](./media/active-directory-named-locations/07.png)


6. Op Hallo **nieuw** blade Hallo te volgen:

    ![Nieuwe blade Hallo](./media/active-directory-named-locations/08.png)

    a. In Hallo **naam** typt u een naam voor uw benoemde locatie.

    b. In Hallo **IP-adresbereiken** typt u een IP-adresbereik. Hallo IP-adresbereik moet toobe in Hallo *Classless Inter-Domain Routing* notatie (Classless).  

    c. Klik op **Create**.



## <a name="what-you-should-know"></a>Wat u moet weten

**Bulksgewijs updates**: wanneer u maken of bijwerken van de benoemde locaties, voor bulksgewijze updates, kunt u uploaden of downloaden van een CSV-bestand met de Hallo IP-adresbereiken. Een upload voegt Hallo IP-adresbereiken in Hallo bestandslijst toohello in plaats van het Hallo-lijst wordt overschreven.

![Hallo uploaden en downloaden van koppelingen](./media/active-directory-named-locations/09.png)


**Beperkingen**: U kunt maximaal 60 benoemde locaties, met één IP-bereik dat is toegewezen tooeach hiervan definiëren. Als u slechts één benoemde locatie geconfigureerd hebt, kunt u geen too500 IP-bereiken definiëren voor deze.


## <a name="next-steps"></a>Volgende stappen

Zie toolearn meer informatie over de risico's [Azure Active Directory-risicogebeurtenissen](active-directory-reporting-risk-events.md).

