---
title: aaaCreate persoonlijke Docker-register - Azure-portal | Microsoft Docs
description: Maken en beheren van persoonlijke Docker-container registers Hello Azure-portal aan de slag
services: container-registry
documentationcenter: 
author: stevelas
manager: balans
editor: dlepow
tags: 
keywords: 
ms.assetid: 53a3b3cb-ab4b-4560-bc00-366e2759f1a1
ms.service: container-registry
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/24/2017
ms.author: stevelas
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 40f3ce44fea26e5fbeca865c9da6df55c2df9511
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-private-docker-container-registry-using-hello-azure-portal"></a>Maken van een persoonlijke Docker-container register met hello Azure-portal
Hello Azure portal toocreate een register container gebruiken en de instellingen beheren. U kunt ook maken en beheren van container registers met Hallo [2.0 voor Azure CLI-opdrachten](container-registry-get-started-azure-cli.md), [Azure PowerShell](container-registry-get-started-powershell.md) of programmatisch met Hallo Container register [REST-API](https://go.microsoft.com/fwlink/p/?linkid=834376).

Zie voor de achtergrond en concepten [Hallo overzicht](container-registry-intro.md).

## <a name="create-a-container-registry"></a>Een containerregister maken
1. In Hallo [Azure-portal](https://portal.azure.com), klikt u op **+ nieuw**.
2. Zoeken Hallo marketplace voor **Azure container register**.
3. Selecteer **Azure Container Registry** met als uitgever **Microsoft**.
    ![Container Registry-service in Azure Marketplace](./media/container-registry-get-started-portal/container-registry-marketplace.png)
4. Klik op **Create**. Hallo **Azure Container register** blade wordt weergegeven.

    ![Container Registry-instellingen](./media/container-registry-get-started-portal/container-registry-settings.png)
5. In Hallo **Azure Container register** blade Hallo volgende informatie invoeren. Klik op **Maken** wanneer u klaar bent.

    a. **Registernaam**: een unieke domeinnaam op het hoogste niveau voor uw specifieke register. In dit voorbeeld is de naam van Hallo register *myRegistry01*, maar vervangen door een unieke naam van uw eigen. Hallo-naam mag alleen letters en cijfers zijn.

    b. **Resourcegroep**: Selecteer een bestaande [resourcegroep](../azure-resource-manager/resource-group-overview.md#resource-groups) of Hallo typenaam voor een nieuwe resourcegroep.

    c. **Locatie**: Selecteer een Azure-datacenter locatie van Hallo service [beschikbaar](https://azure.microsoft.com/regions/services/), zoals **Zuid-centraal VS**.

    d. **Gebruiker met beheerdersrechten**: als u wilt, schakelt u het register voor een beheerder de gebruiker tooaccess Hallo. U kunt deze instelling na het maken van Hallo register kunt wijzigen.

      > [!IMPORTANT]
      > Bovendien tooproviding via een beheerdersaccount voor de gebruiker toegang krijgen tot, container registers ondersteund door de service-principals Azure Active Directory-verificatie ondersteunen. Bekijk voor meer informatie [Verifiëren met het containerregister](container-registry-authentication.md).
      >

    e. **Storage-account**: Hallo standaard instelling toocreate gebruiken een [opslagaccount](../storage/common/storage-introduction.md), of Selecteer een bestaand opslagaccount in Hallo dezelfde locatie. Premium-opslag wordt momenteel niet ondersteund.

## <a name="manage-registry-settings"></a>Registerinstellingen beheren
Na het maken van Hallo register Hallo zoeken registerinstellingen door op te starten op Hallo **Container registers** blade in Hallo-portal. Bijvoorbeeld, moet u mogelijk Hallo instellingen toolog in tooyour register of wilt u tooenable of Hallo beheerder gebruiker uitschakelen.

1. Op Hallo **Container registers** blade, klikt u op Hallo-naam van het register.

    ![Blade Container Registry](./media/container-registry-get-started-portal/container-registry-blade.png)
2. Toegangsinstellingen toomanage, klikt u op **toegangssleutel**.

    ![Toegang tot Container Registry](./media/container-registry-get-started-portal/container-registry-access.png)
3. Houd er rekening mee Hallo volgende instellingen:

   * **Aanmeldingsserver** -Hallo volledig gekwalificeerde naam u toolog in register toohello gebruiken. In dit voorbeeld is het `myregistry01.azurecr.io`.
   * **Gebruiker met beheerdersrechten** - in-of uitschakelen tooenable of van het register Hallo beheerder gebruikersaccount uitschakelen.
   * **Gebruikersnaam** en **wachtwoord** -referenties van Hallo beheerder gebruikersaccount Hallo (indien ingeschakeld) kunt u toolog in toohello register. U kunt eventueel Hallo wachtwoorden opnieuw te genereren. Twee wachtwoorden worden gemaakt, zodat u verbindingen toohello register onderhouden kunt met behulp van een wachtwoord tijdens het genereren van Hallo andere wachtwoord. tooauthenticate met een service-principal in plaats daarvan Zie [verifiëren met een persoonlijke Docker-container register](container-registry-authentication.md).

## <a name="next-steps"></a>Volgende stappen
* [Uw eerste installatiekopie met behulp van Docker CLI Hallo push](container-registry-get-started-docker-cli.md)
