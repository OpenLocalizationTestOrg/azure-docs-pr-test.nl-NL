---
title: aaaNo abonnementen gevonden fout wanneer probeert toosign in tooAzure portal of Azure-accountcentrum | Microsoft Docs
description: Hallo-oplossing biedt voor een probleem waarbij geen abonnementen gevonden fout treedt op wanneer zich tooAzure portal of Azure-accountcentrum.
services: 
documentationcenter: 
author: genlin
manager: jlian
editor: 
tags: billing
ms.assetid: d1545298-99db-4941-8e97-f24a06bb7cb6
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: genli
ms.openlocfilehash: def4d4a1f883dd948fe8132f2d85abc4c23ae624
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="no-subscriptions-found-error-in-azure-portal-or-azure-account-center"></a>Er zijn geen abonnementen heeft een fout gevonden in Azure portal of Azure-accountcentrum
U ontvangt mogelijk een foutbericht van de 'Geen abonnementen gevonden' wanneer u toosign in toohello probeert [Azure-portal](https://portal.azure.com/) of Hallo [Azure-accountcentrum](https://account.windowsazure.com/Subscriptions). In dit artikel biedt een oplossing voor dit probleem.

## <a name="symptom"></a>Symptoom

Wanneer u probeert toosign in toohello [Azure-portal](https://portal.azure.com/) of Hallo [Azure-accountcentrum](https://account.windowsazure.com/Subscriptions), ontvangen van Hallo volgende foutbericht weergegeven: 'Geen abonnementen gevonden'.

## <a name="cause"></a>Oorzaak

Dit probleem treedt op als uw account niet voldoende machtigingen hebben. 

## <a name="solution"></a>Oplossing

Zorg ervoor dat u zich als de juiste administrator Hallo aanmelden. Een beheerder Account toegang tot alleen Hallo-Accountcentrum. Service-beheerders (SA) en Medebeheerders (CA) hebben alleen toohello over machtigingen voor toegang tot Azure-portal of Hallo klassieke Azure-portal.

### <a name="scenario-1-error-message-is-received-in-hello-azure-portalhttpsportalazurecom"></a>Scenario 1: Foutbericht wordt ontvangen op Hallo [Azure-portal](https://portal.azure.com)

toofix dit probleem:

* Zorg ervoor dat Hallo juiste Azure-map is geselecteerd door te klikken op uw account Hallo rechts bovenaan.

  ![Selecteer Hallo directory op Hallo top rechts van hello Azure-portal](./media/billing-no-subscriptions-found/directory-switch.png)

* Als hello rechts Azure-map is geselecteerd, maar nog steeds hello foutbericht, [uw account wordt toegevoegd als een eigenaar](billing-add-change-azure-subscription-administrator.md).

### <a name="scenario-2-error-message-is-received-in-hello-azure-account-centerhttpsaccountwindowsazurecomsubscriptions"></a>Scenario 2: Foutbericht wordt ontvangen op Hallo [Azure account center](https://account.windowsazure.com/Subscriptions)

Controleer of Hallo-account waarmee u Hallo accountbeheerder. tooverify wie de accountbeheerder Hallo is, als volgt te werk:

1. Meld u aan toohello [Azure-portal](https://portal.azure.com).
2. Selecteer op de Hub-menu Hallo **abonnement**.
3. Selecteer Hallo-abonnement dat u toocheck wilt en selecteer vervolgens **instellingen**.
4. Selecteer **eigenschappen**. de accountbeheerder Hallo van Hallo abonnement wordt weergegeven in Hallo **accountbeheerder** vak.

## <a name="need-help-contact-support"></a>Hulp nodig? Neem contact op met ondersteuning.
Als u nog hulp nodig hebt, [contact op met ondersteuning](http://go.microsoft.com/fwlink/?linkid=544831&clcid=0x409) tooget uw probleem snel worden opgelost. 
