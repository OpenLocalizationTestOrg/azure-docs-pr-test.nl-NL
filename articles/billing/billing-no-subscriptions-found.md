---
title: Er zijn geen abonnementen gevonden fout wanneer probeert aan te melden bij Azure portal of Azure-accountcentrum | Microsoft Docs
description: De oplossing biedt voor een probleem waarbij geen abonnementen gevonden fout treedt op wanneer zich bij Azure portal of Azure-accountcentrum.
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
ms.openlocfilehash: a4ce9b219c05f8469379c2aac5241fcfffd16033
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="no-subscriptions-found-error-in-azure-portal-or-azure-account-center"></a>Er zijn geen abonnementen heeft een fout gevonden in Azure portal of Azure-accountcentrum
U ontvangt mogelijk een foutbericht van de 'Geen abonnementen gevonden' wanneer u probeert aan te melden bij de [Azure-portal](https://portal.azure.com/) of de [Azure-accountcentrum](https://account.windowsazure.com/Subscriptions). In dit artikel biedt een oplossing voor dit probleem.

## <a name="symptom"></a>Symptoom

Wanneer u probeert aan te melden bij de [Azure-portal](https://portal.azure.com/) of de [Azure-accountcentrum](https://account.windowsazure.com/Subscriptions), verschijnt het volgende foutbericht weergegeven: 'Geen abonnementen gevonden'.

## <a name="cause"></a>Oorzaak

Dit probleem treedt op als uw account niet voldoende machtigingen hebben. 

## <a name="solution"></a>Oplossing

Zorg ervoor dat u zich als beheerder van de juiste aanmelden. Een beheerder Account toegang tot alleen de Center-Account. Service-beheerders (SA) en Medebeheerders (CA) hebben toegang tot de Azure portal of de klassieke Azure portal.

### <a name="scenario-1-error-message-is-received-in-the-azure-portalhttpsportalazurecom"></a>Scenario 1: Foutbericht ontvangen in de [Azure-portal](https://portal.azure.com)

Dit probleem oplossen:

* Zorg ervoor dat de juiste Azure-map is geselecteerd door te klikken op uw account in de rechterbovenhoek.

  ![Selecteer de map boven rechts van de Azure-portal](./media/billing-no-subscriptions-found/directory-switch.png)

* Als de juiste Azure-map is geselecteerd, maar u nog steeds het foutbericht ontvangen [uw account wordt toegevoegd als een eigenaar](billing-add-change-azure-subscription-administrator.md).

### <a name="scenario-2-error-message-is-received-in-the-azure-account-centerhttpsaccountwindowsazurecomsubscriptions"></a>Scenario 2: Foutbericht ontvangen in de [Azure account center](https://account.windowsazure.com/Subscriptions)

Controleer of het account dat u gebruikt de accountbeheerder. Om te controleren wie de accountbeheerder is, de volgende stappen uit:

1. Meld u aan bij [Azure Portal](https://portal.azure.com).
2. Selecteer in het menu Hub **abonnement**.
3. Selecteer het abonnement dat u wilt controleren, en selecteer vervolgens **instellingen**.
4. Selecteer **eigenschappen**. De accountbeheerder van het abonnement wordt weergegeven in de **accountbeheerder** vak.

## <a name="need-help-contact-support"></a>Hulp nodig? Neem contact op met ondersteuning.
Als u nog hulp nodig hebt, [contact op met ondersteuning](http://go.microsoft.com/fwlink/?linkid=544831&clcid=0x409) ophalen van uw probleem snel worden opgelost. 
