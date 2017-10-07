---
title: een Batch-account in Azure-portal Hallo aaaCreate | Microsoft Docs
description: Meer informatie over hoe toocreate een Azure Batch-account in Azure portal toorun Hallo grootschalige parallelle workloads in Hallo cloud
services: batch
documentationcenter: 
author: tamram
manager: timlt
editor: 
ms.assetid: 3fbae545-245f-4c66-aee2-e25d7d5d36db
ms.service: batch
ms.workload: big-compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/20/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2176f88ba0a1a3298023de8f520d46ef28a664b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-batch-account-with-hello-azure-portal"></a>Een Batch-account maken met hello Azure-portal

> [!div class="op_single_selector"]
> * [Azure Portal](batch-account-create-portal.md)
> * [Batch Management .NET](batch-management-dotnet.md)
>
>

Meer informatie over hoe toocreate een Azure Batch-account in Hallo [Azure-portal][azure_portal], en kies Hallo accounteigenschappen die aansluiten bij uw rekenscenario. Meer informatie over waar de belangrijke accounteigenschappen toofind zoals toegangstoetsen en account-URL's.

Zie voor achtergrondinformatie over Batch-accounts en scenario's, Hallo [functie overzicht](batch-api-basics.md).



## <a name="create-a-batch-account"></a>Batch-account maken

Hallo portal toocreate een Batch-account gebruiken in een van twee Hallo *groep toewijzing modi*: **Batch-service** modus of nieuwere Hallo **gebruikerabonnement** modus, die meer vereist de configuratie. Zie voor informatie over deze twee modi Hallo [functie overzicht](batch-api-basics.md#account). Voor de onderdelen van de gebruikersmodus abonnement hello, Zie ook Hallo [blogbericht](https://blogs.technet.microsoft.com/windowshpc/2017/03/17/azure-batch-vnet-and-custom-image-support-for-virtual-machine-pools/).

## <a name="batch-service-mode"></a>Modus Batch-service



1. Meld u aan toohello [Azure-portal][azure_portal].
2. Klik op **Nieuw** > **Berekenen** > **Batch-service**.

    ![Batch in Hallo Marketplace][marketplace_portal]
3. Hallo **nieuw Batch-Account** blade wordt weergegeven. Zie de beschrijvingen Hallo hieronder van elk blade-element.

    ![Batch-account maken][account_portal]

    a. **Accountnaam**: Batch-accountnaam Hallo u kiest moet uniek zijn binnen hello Azure-regio waar Hallo-account wordt gemaakt (Zie **locatie** hieronder). Hallo-accountnaam mag alleen kleine letters of cijfers bevatten en moet 3 tot 24 tekens lang zijn.

    b. **Abonnement**: Hallo-abonnement in welke toocreate Hallo Batch-account. Als u slechts één abonnement hebt, is het standaard geselecteerd.

    c. **Groepstoewijzingsmodus**: selecteer **Batch-service**.

    c. **Resourcegroep**: Selecteer een bestaande resourcegroep voor het nieuwe Batch-account. U kunt er ook voor kiezen om een nieuwe resourcegroep te maken.

    d. **Locatie**: hello Azure-regio in welke toocreate Hallo Batch-account. Alleen Hallo-regio's wordt ondersteund door uw abonnement en resourcegroep worden als opties weergegeven.

    e. **Opslagaccount** (optioneel): een Azure Storage-account voor algemeen gebruik dat u koppelt aan het Batch-account. Dit wordt aanbevolen voor de meeste Batch-accounts. Zie [Gekoppeld Azure Storage-account](#linked-azure-storage-account) verderop in dit artikel voor meer informatie.

4. Klik op **maken** toocreate Hallo-account.

   Hallo portal geeft de implementatie wordt uitgevoerd. Na voltooiing wordt de melding **Implementaties geslaagd** weergegeven in **Meldingen**.

## <a name="user-subscription-mode"></a>Modus Gebruikersabonnement

### <a name="allow-azure-batch-tooaccess-hello-subscription-one-time-operation"></a>Azure Batch tooaccess Hallo-abonnement (eenmalige bewerking) toestaan
Bij het maken van uw eerste Batch-account in de gebruikersmodus abonnement, uw abonnement met Batch uitvoeren Hallo tooregister stappen te volgen. (Als u eerder dit hebt gedaan, toohello volgende sectie overslaan.)

1. Meld u aan toohello [Azure-portal][azure_portal].

2. Klik op **meer Services** > **abonnementen**, en klikt u op Hallo abonnement toouse voor gewenste Hallo Batch-account.

3. In Hallo **abonnement** blade, klikt u op **toegangsbeheer (IAM)** > **toevoegen**.

    ![Toegangsbeheer voor abonnement][subscription_access]

4. Op Hallo **machtigingen toevoegen** blade, selecteer Hallo **Inzender** rol, zoekt u Hallo Batch-API. Zoeken naar elk van deze tekenreeksen totdat u Hallo-API:
    1. **MicrosoftAzureBatch**.
    2. **Microsoft Azure Batch**. Nieuwere Azure AD-tenants kunnen deze naam gebruiken.
    3. **ddbf3205-c6bd-46ae-8127-60eb93363864** Hallo-id voor Hallo Batch-API. 

5. Als u Hallo Batch-API hebt gevonden, te selecteren en op **opslaan**.

    ![Batch-machtigingen toevoegen][add_permission]

### <a name="create-a-key-vault"></a>Een sleutelkluis maken
In de gebruikersmodus-abonnement, een Azure sleutelkluis is vereist dat toothe hoort dezelfde resourcegroep als Hallo Batch-account toobe gemaakt. Zorg ervoor dat Hallo resourcegroep bevindt zich in een regio waar de Batch is [beschikbaar](https://azure.microsoft.com/regions/services/) en die ondersteuning biedt voor uw abonnement.

1. In Hallo [Azure-portal][azure_portal], klikt u op **nieuw** > **beveiliging en identiteit** > **Sleutelkluis** .

2. In Hallo **Sleutelkluis maken** blade een naam voor de sleutelkluis hello en een resourcegroep in Hallo regio die u voor uw Batch-account wilt maken. Laat Hallo resterende instellingen op de standaardwaarden en klik vervolgens op **maken**.

### <a name="create-a-batch-account"></a>Batch-account maken

1. In Hallo [Azure-portal][azure_portal], klikt u op **nieuw** > **Compute** > **voorBatch-Service**.

    ![Batch in Hallo Marketplace][marketplace_portal]
3. Hallo **nieuw Batch-Account** blade wordt weergegeven. Zie de beschrijvingen Hallo hieronder van elk blade-element.

    ![Batch-account maken][account_portal_byos]

    a. **Accountnaam**: Batch-accountnaam Hallo u kiest moet uniek zijn binnen hello Azure-regio waar Hallo-account wordt gemaakt (Zie **locatie** hieronder). Hallo-accountnaam mag alleen kleine letters of cijfers bevatten en moet 3 tot 24 tekens lang zijn.

    b. **Abonnement**: als u meer dan één abonnement hebt, selecteert u Hallo-abonnement dat u bij Hallo Batch-service geregistreerd.

    c. **Groepstoewijzingsmodus**: selecteer **Gebruikersabonnement**.

    d. **Sleutelkluis**: Selecteer Hallo sleutelkluis u hebt gemaakt voor uw Batch-account in de vorige sectie Hallo. Maak desgewenst een nieuwe sleutelkluis. Selecteer na het selecteren van de kluis Hallo Hallo selectievakje toogrant Azure Batch toegang toohello sleutelkluis.

    c. **Resourcegroep**: Selecteer Hallo resourcegroep waarin u Hallo sleutelkluis hebt gemaakt.

    d. **Locatie**: hello Azure-regio waarin u de sleutelkluis Hallo voor Hallo Batch-account hebt gemaakt.

    e. **Opslagaccount** (optioneel): een Azure Storage-account voor algemeen gebruik dat u koppelt aan het Batch-account. Dit wordt aanbevolen voor de meeste Batch-accounts. Zie [Gekoppeld Azure Storage-account](#linked-azure-storage-account) hieronder voor meer informatie.

4. Klik op **maken** toocreate Hallo-account.

   Hallo portal geeft de implementatie wordt uitgevoerd. Na voltooiing wordt de melding **Implementaties geslaagd** weergegeven in **Meldingen**.



## <a name="view-batch-account-properties"></a>Eigenschappen van Batch-account weergeven
Wanneer het Hallo-account is gemaakt, kunt u Hallo openen **blade van de Batch-account** tooaccess de instellingen en eigenschappen. U kunt toegang tot alle instellingen en eigenschappen via Hallo linkermenu van blade Hallo Batch-account.

![Blade Batch-account in Azure Portal][account_blade]

* **Batch-account-URL**: wanneer u een toepassing Hello ontwikkelt [Batch-API's](batch-apis-tools.md#azure-accounts-for-batch-development), moet u een account URL tooaccess uw Batch-resources. De URL van een Batch-account heeft Hallo volgende indeling:

    `https://<account_name>.<region>.batch.azure.com`

![Batch-account-URL in de portal][account_url]

* **Toegangssleutels** (modus voor Batch-service): tooauthenticate toegang tooyour Batch-account van uw toepassing, moet u een toegangssleutel voor het account. (Deze instelling is niet beschikbaar in de modus Gebruikersabonnement, waarin u Azure Active Directory-verificatie gebruikt.)

    tooview of opnieuw genereren toegangssleutels van uw Batch-account, voer `keys` in het linkermenu Hallo **Search** vak op de blade Hallo Batch-account en selecteer vervolgens **sleutels**.

    ![Batch-accountsleutels in Azure Portal][account_keys]

[!INCLUDE [batch-pricing-include](../../includes/batch-pricing-include.md)]

## <a name="linked-azure-storage-account"></a>Gekoppeld Azure Storage-account

U kunt desgewenst een algemeen Azure Storage-account tooyour Batch-account koppelen. Hallo [toepassingspakketten](batch-application-packages.md) functie van Batch gebruikt Azure Blob storage, doet Hallo [Batch bestand conventies .NET](batch-task-output.md) bibliotheek. Deze optionele functies helpt u bij de implementatie Hallo-toepassingen die uw Batch-taken worden uitgevoerd en persistent maken Hallo-gegevens die ze produceren.

U wordt aangeraden een nieuw opslagaccount te maken dat alleen wordt gebruikt voor het Batch-account.

![Een opslagaccount voor algemeen gebruik maken][storage_account]

> [!NOTE]
> Azure Batch ondersteunt momenteel alleen Hallo algemeen type Opslagaccount. Dit accounttype wordt beschreven in stap 5 [Een opslagaccount maken] (../ storage/common/storage-create-storage-account.md#create-a-storage-account) in [Over Azure-opslagaccounts](../storage/common/storage-create-storage-account.md).
>
>

> [!WARNING]
> Wees voorzichtig met het Hallo toegangssleutels van een gekoppelde opslagaccount opnieuw genereren. Slechts één opslagaccountsleutel opnieuw genereren en klik op **sleutels synchroniseren** op Hallo gekoppeld blade Opslagaccount. Wacht vijf minuten tooallow Hallo sleutels toopropagate toohello rekenknooppunten in uw pools en vervolgens opnieuw genereren en synchroniseren Hallo andere sleutel indien nodig. Als u opnieuw beide genereert sleutels op Hallo dezelfde tijd, uw rekenknooppunten kunnen toosynchronize van sleutel, en worden ze toegang toohello Storage-account verliest.
>
>

![Sleutels van opslagaccounts opnieuw genereren][4]

## <a name="batch-service-quotas-and-limits"></a>Quota en limieten voor Batch-service
Houd er rekening mee dat als met uw Azure-abonnement en andere Azure-services, bepaalde u zich [quota en limieten](batch-quota-limit.md) tooBatch accounts van toepassing. De huidige quota voor een Batch-account worden weergegeven in Hallo account Hallo Portal **eigenschappen**.

![Batch-accountquota in Azure Portal][quotas]



Veel van deze quota kunnen bovendien worden verhoogd met een gratis product ondersteuningsaanvraag verzonden in hello Azure-portal. Zie [quota en limieten voor hello Azure Batch-service](batch-quota-limit.md) voor meer informatie over het aanvragen van quota toeneemt.

## <a name="other-batch-account-management-options"></a>Andere beheeropties voor uw Batch-account
Bovendien toousing hello Azure-portal, kunt u ook maken en beheren van Batch-accounts met Hallo volgende:

* [Batch-PowerShell-cmdlets](batch-powershell-cmdlets-get-started.md)
* [Azure CLI](batch-cli-get-started.md)
* [Batch Management .NET](batch-management-dotnet.md)

## <a name="next-steps"></a>Volgende stappen
* Zie Hallo [overzicht Batch-functies](batch-api-basics.md) toolearn meer over de concepten van de Batch-service en -functies. Hallo artikel Hallo primaire Batch-resources zoals pools, rekenknooppunten, jobs en taken besproken en u vindt een overzicht van Hallo servicefuncties waarmee grootschalige rekenworkloads kunnen worden uitgevoerd.
* Leer de basisbeginselen Hallo van het ontwikkelen van een Batch-toepassing hello met [clientbibliotheek Batch .NET](batch-dotnet-get-started.md) of [Python](batch-python-tutorial.md). Deze inleidende artikelen helpen u bij een werkende toepassing die gebruikmaakt van Hallo Batch-service tooexecute een workload op meerdere rekenknooppunten en omvat het gebruik van Azure Storage voor het Faseren en ophalen.

[api_net]: https://msdn.microsoft.com/library/azure/mt348682.aspx
[api_rest]: https://msdn.microsoft.com/library/azure/Dn820158.aspx

[azure_portal]: https://portal.azure.com
[batch_pricing]: https://azure.microsoft.com/pricing/details/batch/

[4]: ./media/batch-account-create-portal/batch_acct_04.png "Sleutels van opslagaccounts opnieuw genereren"
[marketplace_portal]: ./media/batch-account-create-portal/marketplace_batch.PNG
[account_blade]: ./media/batch-account-create-portal/batch_blade.png
[account_portal]: ./media/batch-account-create-portal/batch_acct_portal.png
[account_keys]: ./media/batch-account-create-portal/account_keys.PNG
[account_url]: ./media/batch-account-create-portal/account_url.png
[storage_account]: ./media/batch-account-create-portal/storage_account.png
[quotas]: ./media/batch-account-create-portal/quotas.png
[subscription_access]: ./media/batch-account-create-portal/subscription_iam.png
[add_permission]: ./media/batch-account-create-portal/add_permission.png
[account_portal_byos]: ./media/batch-account-create-portal/batch_acct_portal_byos.png
