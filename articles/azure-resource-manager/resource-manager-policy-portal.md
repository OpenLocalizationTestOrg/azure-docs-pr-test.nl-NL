---
title: portal voor bronbeleid aaaAzure | Microsoft Docs
description: Hierin wordt beschreven hoe toouse Azure portal toocreate en beheren van Resource Manager-beleid. Beleidsregels kunnen worden toegepast op Hallo abonnement of de resource-groepen.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: tomfitz
ms.openlocfilehash: ce6413386317e532b63761a24458b85c996af4a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-portal-tooassign-and-manage-resource-policies"></a>Azure portal tooassign gebruiken en beheren van bronbeleid
Hello Azure-portal kunt u tooassign beleid tooresource resourcegroepen en abonnementen. Hallo-gebruikersinterface kunt u eenvoudig tooselect Hallo beleid dat u tooassign wilt en parameterwaarden voor dat beleid toocustomize Hallo beleidsinstellingen opgeven. 

een beleid via de portal Hallo tooassign, Hallo beleidsdefinitie moet al bestaan in uw abonnement. Uw abonnement heeft diverse ingebouwde beleidsdefinities die gereed voor u tooassign tooresource groepen of abonnementen zijn. Ziet u deze beleidsregels ingebouwde en aangepaste beleidsregels die u hebt gedefinieerd wanneer met behulp van Hallo portal tooassign beleid. Zie voor een inleiding toopolicies en hoe toodefine aangepast beleid [Resource overzicht](resource-manager-policy.md).

Beleidsregels worden overgenomen door alle onderliggende resources. Dus als een beleid toegepast tooa resourcegroep is, van toepassing tooall Hallo resources in die resourcegroep is. In dit artikel Hallo term **bereik** toohello resourcegroep of abonnement dat is toegewezen Hallo beleid verwijst. 

Beleidsregels worden geëvalueerd wanneer maken en bijwerken van resources (plaatsen en PATCH operations).

## <a name="assign-a-policy"></a>Geen beleid toewijzen

1. tooassign een beleid tooeither een resourcegroep of abonnement, selecteert u de resourcegroep of abonnement. Selecteer in de instellingen van Hallo **beleid**.

   ![beleid selecteren](./media/resource-manager-policy-portal/select-policies.png)

2. Selecteer toocreate een beleidstoewijzing voor deze scope **toewijzing toevoegen**.

   ![toewijzing toevoegen](./media/resource-manager-policy-portal/add-assignment.png)

3. Selecteer de gewenste tooassign Hallo-beleid. Zelfs als u niet een beleid definities tooyour-abonnement hebt toegevoegd, ziet u Hallo ingebouwde beleidsregels die beschikbaar voor toewijzing zijn. Deze ingebouwde beleidsregels algemene scenario's uitgelegd.

   ![definitie selecteren](./media/resource-manager-policy-portal/select-definition.png)

4. Na het selecteren van een beleid, ziet u een beschrijving van Hallo beleid en parameters voor dat beleid. Hallo volgende afbeelding ziet u bijvoorbeeld Hallo **toegestaan locaties** parameter is vereist voor Hallo-beleid die Hallo beschikbare locaties beperkt.

   ![parameters weergeven](./media/resource-manager-policy-portal/show-parameters.png)

5. Selecteer via de gebruikersinterface Hallo Hallo waarden toospecify voor Hallo beleidsparameters (zoals Hallo locaties die kunnen worden gebruikt voor implementatie).

   ![Selecteer de parameterwaarden](./media/resource-manager-policy-portal/select-parameters.png)

6. Geef waarden op voor Hallo andere parameters. Hallo-scope wordt automatisch toegewezen op basis van het Hallo-blade die u hebt geselecteerd bij het starten van de beleidstoewijzing Hallo. Selecteer **OK** wanneer u gereed bent.

   ![parameters definiëren](./media/resource-manager-policy-portal/define-parameters.png)

  U hebt toegewezen Hallo beleid toohello opgegeven bereik.

## <a name="view-policy-assignments"></a>Beleidstoewijzingen weergeven

Na het toewijzen van een beleid voor bekijken u deze in de lijst Hallo van beleid voor deze scope. Hallo **Details** tabblad bevat een overzicht van de beleidstoewijzing Hallo.

![details weergeven](./media/resource-manager-policy-portal/show-details.png)

Hallo **toewijzingsregel** tabblad ziet u Hallo JSON voor Hallo-beleidsdefinitie.

![regel voor agenttoewijzing weergeven](./media/resource-manager-policy-portal/show-assignment-rule.png)

## <a name="change-an-existing-policy-assignment"></a>Wijzigen van een bestaande beleidstoewijzing van

selecteert u een beleid toochange **toewijzing bewerken** of **verwijderen**

![bewerken of verwijderen van toewijzing](./media/resource-manager-policy-portal/edit-delete-policy.png)

## <a name="assign-custom-policies"></a>Aangepast beleid toe te wijzen

Als u aangepaste beleidsregels hebt gedefinieerd in uw abonnement, zijn deze beleidsregels beschikbaar voor toewijzing via Hallo-portal. Deze beleidsregels worden voorafgegaan door **[Custom]**

![aangepast beleid](./media/resource-manager-policy-portal/show-custom-policy.png)

## <a name="next-steps"></a>Volgende stappen
* toolearn over Hallo JSON-syntaxis voor het definiëren van beleid, Zie [Resource overzicht](resource-manager-policy.md).
* Abonnementen voor instructies over hoe ondernemingen tooeffectively Resource Manager kunt beheren, Zie [Azure enterprise scaffold - prescriptieve abonnement governance](resource-manager-subscription-governance.md).
* Hallo beleid schema wordt gepubliceerd op [http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json](http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json). 

