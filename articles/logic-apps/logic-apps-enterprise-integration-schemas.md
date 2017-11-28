---
title: Schema's voor XML-validatie - Azure Logic Apps | Microsoft Docs
description: XML-documenten met schema's voor Azure Logic Apps en Enterprise Integration Pack valideren
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: anneta
editor: cgronlun
ms.assetid: 56c5846c-5d8c-4ad4-9652-60b07aa8fc3b
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/29/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 4f58a587c1f10aea1cee89e46fa9ec340e0d21c6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="validate-xml-with-schemas-for-azure-logic-apps-and-the-enterprise-integration-pack"></a><span data-ttu-id="1a2ab-103">XML-validatie met schema's voor Azure Logic Apps en de Enterprise-integratiepakket</span><span class="sxs-lookup"><span data-stu-id="1a2ab-103">Validate XML with schemas for Azure Logic Apps and the Enterprise Integration Pack</span></span>

<span data-ttu-id="1a2ab-104">Schema's Bevestig dat de XML-documenten die u ontvangt geldig zijn en de verwachte gegevens in een vooraf gedefinieerde indeling hebben.</span><span class="sxs-lookup"><span data-stu-id="1a2ab-104">Schemas confirm that the XML documents you receive are valid and have the expected data in a predefined format.</span></span> <span data-ttu-id="1a2ab-105">Schema's kunnen ook berichten die worden uitgewisseld in een B2B-scenario te valideren.</span><span class="sxs-lookup"><span data-stu-id="1a2ab-105">Schemas also help validate messages that are exchanged in a B2B scenario.</span></span>

## <a name="add-a-schema"></a><span data-ttu-id="1a2ab-106">Een schema toevoegen</span><span class="sxs-lookup"><span data-stu-id="1a2ab-106">Add a schema</span></span>

1. <span data-ttu-id="1a2ab-107">Selecteer in de Azure-portal **meer services**.</span><span class="sxs-lookup"><span data-stu-id="1a2ab-107">In the Azure portal, select **More services**.</span></span>

    ![Azure-portal 'Meer services'](media/logic-apps-enterprise-integration-schemas/overview-11.png)

2. <span data-ttu-id="1a2ab-109">Voer in het zoekvak filter **integratie**, en selecteer **Integratieaccounts** uit de lijst met resultaten.</span><span class="sxs-lookup"><span data-stu-id="1a2ab-109">In the filter search box, enter **integration**, and select **Integration Accounts** from the results list.</span></span>

    ![Zoekvak filteren](media/logic-apps-enterprise-integration-schemas/overview-21.png)

3. <span data-ttu-id="1a2ab-111">Selecteer de **integratie account** waar u het schema worden toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="1a2ab-111">Select the **integration account** where you want to add the schema.</span></span>

    ![Lijst met integratieaccounts](media/logic-apps-enterprise-integration-schemas/overview-31.png)

4. <span data-ttu-id="1a2ab-113">Kies de **schema's** tegel.</span><span class="sxs-lookup"><span data-stu-id="1a2ab-113">Choose the **Schemas** tile.</span></span>

    ![Voorbeeld van de integratie-account, 'Schema'](media/logic-apps-enterprise-integration-schemas/schema-11.png)

### <a name="add-a-schema-file-smaller-than-2-mb"></a><span data-ttu-id="1a2ab-115">Toevoegen van een schemabestand dat kleiner is dan 2 MB</span><span class="sxs-lookup"><span data-stu-id="1a2ab-115">Add a schema file smaller than 2 MB</span></span>

1. <span data-ttu-id="1a2ab-116">In de **schema's** blade die wordt geopend (van de voorgaande stappen), kiest **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="1a2ab-116">In the **Schemas** blade that opens (from the preceding steps), choose **Add**.</span></span>

    ![Schema's blade "Toevoegen"](media/logic-apps-enterprise-integration-schemas/schema-21.png)

2. <span data-ttu-id="1a2ab-118">Voer een naam voor uw schema.</span><span class="sxs-lookup"><span data-stu-id="1a2ab-118">Enter a name for your schema.</span></span> <span data-ttu-id="1a2ab-119">Uploaden van het schemabestand door het selecteren van het pictogram naast de **Schema** vak.</span><span class="sxs-lookup"><span data-stu-id="1a2ab-119">Upload the schema file by selecting the folder icon next to the **Schema** box.</span></span> <span data-ttu-id="1a2ab-120">Nadat het uploadproces is voltooid, selecteert u **OK**.</span><span class="sxs-lookup"><span data-stu-id="1a2ab-120">After the upload process completes, select **OK**.</span></span>

    ![Schermopname van 'Toevoegen Schema', met 'Kleine file' gemarkeerd](media/logic-apps-enterprise-integration-schemas/schema-31.png)

### <a name="add-a-schema-file-larger-than-2-mb-up-to-8-mb-maximum"></a><span data-ttu-id="1a2ab-122">Toevoegen van een schemabestand groter is dan 2 MB (maximaal 8 MB)</span><span class="sxs-lookup"><span data-stu-id="1a2ab-122">Add a schema file larger than 2 MB (up to 8 MB maximum)</span></span>

<span data-ttu-id="1a2ab-123">Deze stappen verschillen op basis van het toegangsniveau van de blob-container: **openbare** of **geen anonieme toegang**.</span><span class="sxs-lookup"><span data-stu-id="1a2ab-123">These steps differ based on the blob container access level: **Public** or **No anonymous access**.</span></span>

<span data-ttu-id="1a2ab-124">**Dit toegangsniveau bepalen**</span><span class="sxs-lookup"><span data-stu-id="1a2ab-124">**To determine this access level**</span></span>

1.  <span data-ttu-id="1a2ab-125">Open **Azure Opslagverkenner**.</span><span class="sxs-lookup"><span data-stu-id="1a2ab-125">Open **Azure Storage Explorer**.</span></span> 

2.  <span data-ttu-id="1a2ab-126">Onder **Blob-Containers**, de blob-container die u wilt selecteren.</span><span class="sxs-lookup"><span data-stu-id="1a2ab-126">Under **Blob Containers**, select the blob container you want.</span></span> 

3.  <span data-ttu-id="1a2ab-127">Selecteer **beveiliging**, **toegangsniveau**.</span><span class="sxs-lookup"><span data-stu-id="1a2ab-127">Select **Security**, **Access Level**.</span></span>

<span data-ttu-id="1a2ab-128">Als het toegangsniveau voor beveiliging van blob is **openbare**, als volgt te werk.</span><span class="sxs-lookup"><span data-stu-id="1a2ab-128">If the blob security access level is **Public**, follow these steps.</span></span>

![Azure Storage Explorer met de 'Blob-Containers', 'Beveiliging' en 'Openbare' gemarkeerd](media/logic-apps-enterprise-integration-schemas/blob-public.png)

1. <span data-ttu-id="1a2ab-130">Het schema uploaden naar uw opslagaccount en kopieer de URI.</span><span class="sxs-lookup"><span data-stu-id="1a2ab-130">Upload the schema to your storage account, and copy the URI.</span></span>

    ![Storage-account met URI gemarkeerd](media/logic-apps-enterprise-integration-schemas/schema-blob.png)

2. <span data-ttu-id="1a2ab-132">In **Schema toevoegen**, selecteer **groot bestand**, en geeft u de URI in de **inhoud URI** in het tekstvak.</span><span class="sxs-lookup"><span data-stu-id="1a2ab-132">In **Add Schema**, select **Large file**, and provide the URI in the **Content URI** text box.</span></span>

    ![Schema's met de knop 'Toevoegen' en 'Grote file' gemarkeerd](media/logic-apps-enterprise-integration-schemas/schema-largefile.png)

<span data-ttu-id="1a2ab-134">Als het toegangsniveau voor beveiliging van blob is **geen anonieme toegang**, als volgt te werk.</span><span class="sxs-lookup"><span data-stu-id="1a2ab-134">If the blob security access level is **No anonymous access**, follow these steps.</span></span>

![Azure Storage Explorer met de 'Blob-Containers', 'Beveiliging' en 'Geen anonieme toegang' gemarkeerd](media/logic-apps-enterprise-integration-schemas/blob-1.png)

1. <span data-ttu-id="1a2ab-136">Het schema uploaden naar uw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="1a2ab-136">Upload the schema to your storage account.</span></span>

    ![Storage-account](media/logic-apps-enterprise-integration-schemas/blob-3.png)

2. <span data-ttu-id="1a2ab-138">Genereer een shared access signature voor het schema.</span><span class="sxs-lookup"><span data-stu-id="1a2ab-138">Generate a shared access signature for the schema.</span></span>

    ![Storage-account met gedeelde toegang handtekeningen tabblad gemarkeerd](media/logic-apps-enterprise-integration-schemas/blob-2.png)

3. <span data-ttu-id="1a2ab-140">In **Schema toevoegen**, selecteer **groot bestand**, en geef de shared access signature URI in de **inhoud URI** in het tekstvak.</span><span class="sxs-lookup"><span data-stu-id="1a2ab-140">In **Add Schema**, select **Large file**, and provide the shared access signature URI in the **Content URI** text box.</span></span>

    ![Schema's met de knop 'Toevoegen' en 'Grote file' gemarkeerd](media/logic-apps-enterprise-integration-schemas/schema-largefile.png)

4. <span data-ttu-id="1a2ab-142">In de **schema's** blade van uw account voor de integratie van uw zojuist toegevoegde schema moet worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="1a2ab-142">In the **Schemas** blade of your integration account, your newly added schema should appear.</span></span>

    ![Uw account integratie met 'Schema' en het nieuwe schema gemarkeerd](media/logic-apps-enterprise-integration-schemas/schema-41.png)

## <a name="edit-schemas"></a><span data-ttu-id="1a2ab-144">Schema's bewerken</span><span class="sxs-lookup"><span data-stu-id="1a2ab-144">Edit schemas</span></span>

1. <span data-ttu-id="1a2ab-145">Kies de **schema's** tegel.</span><span class="sxs-lookup"><span data-stu-id="1a2ab-145">Choose the **Schemas** tile.</span></span>

2. <span data-ttu-id="1a2ab-146">Na de **schema's** blade wordt geopend, selecteert u het schema dat u wilt bewerken.</span><span class="sxs-lookup"><span data-stu-id="1a2ab-146">After the **Schemas** blade opens, select the schema that you want to edit.</span></span>

3. <span data-ttu-id="1a2ab-147">Op de **schema's** blade kiezen **bewerken**.</span><span class="sxs-lookup"><span data-stu-id="1a2ab-147">On the **Schemas** blade, choose **Edit**.</span></span>

    ![Schema's-blade](media/logic-apps-enterprise-integration-schemas/edit-12.png)

4. <span data-ttu-id="1a2ab-149">Selecteer het schemabestand dat u wilt bewerken, en selecteer vervolgens **Open**.</span><span class="sxs-lookup"><span data-stu-id="1a2ab-149">Select the schema file that you want to edit, then select **Open**.</span></span>

    ![Open het schemabestand te bewerken](media/logic-apps-enterprise-integration-schemas/edit-31.png)

<span data-ttu-id="1a2ab-151">Azure ziet u een bericht of het schema is geüpload.</span><span class="sxs-lookup"><span data-stu-id="1a2ab-151">Azure shows a message that the schema uploaded successfully.</span></span>

## <a name="delete-schemas"></a><span data-ttu-id="1a2ab-152">Schema's verwijderen</span><span class="sxs-lookup"><span data-stu-id="1a2ab-152">Delete schemas</span></span>

1. <span data-ttu-id="1a2ab-153">Kies de **schema's** tegel.</span><span class="sxs-lookup"><span data-stu-id="1a2ab-153">Choose the **Schemas** tile.</span></span>

2. <span data-ttu-id="1a2ab-154">Na de **schema's** blade wordt geopend, selecteer het schema dat u wilt verwijderen.</span><span class="sxs-lookup"><span data-stu-id="1a2ab-154">After the **Schemas** blade opens, select the schema you want to delete.</span></span>

3. <span data-ttu-id="1a2ab-155">Op de **schema's** blade kiezen **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="1a2ab-155">On the **Schemas** blade, choose **Delete**.</span></span>

    ![Schema's-blade](media/logic-apps-enterprise-integration-schemas/delete-12.png)

4. <span data-ttu-id="1a2ab-157">Om te bevestigen dat u wilt verwijderen van het geselecteerde schema, kies **Ja**.</span><span class="sxs-lookup"><span data-stu-id="1a2ab-157">To confirm that you want to delete the selected schema, choose **Yes**.</span></span>

    ![Bevestigingsbericht 'Schema verwijderen'](media/logic-apps-enterprise-integration-schemas/delete-21.png)

    <span data-ttu-id="1a2ab-159">In de **schema's** blade de schema-lijst wordt vernieuwd en bevat niet langer het schema dat u hebt verwijderd.</span><span class="sxs-lookup"><span data-stu-id="1a2ab-159">In the **Schemas** blade, the schema list refreshes  and no longer includes the schema that you deleted.</span></span>

    ![Uw integratie met 'Schema' gemarkeerd-Account](media/logic-apps-enterprise-integration-schemas/delete-31.png)

## <a name="next-steps"></a><span data-ttu-id="1a2ab-161">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="1a2ab-161">Next steps</span></span>
* <span data-ttu-id="1a2ab-162">[Meer informatie over het Enterprise-integratiepakket](logic-apps-enterprise-integration-overview.md "meer informatie over het enterprise-integratiepakket").</span><span class="sxs-lookup"><span data-stu-id="1a2ab-162">[Learn more about the Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md "Learn about the enterprise integration pack").</span></span>  

