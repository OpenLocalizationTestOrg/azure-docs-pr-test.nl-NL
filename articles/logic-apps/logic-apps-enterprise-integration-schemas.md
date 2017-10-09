---
title: aaaSchemas voor XML-validatie - Azure Logic Apps | Microsoft Docs
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
ms.openlocfilehash: 87cf92741e10ff7cccd260f27442909e34928903
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="validate-xml-with-schemas-for-azure-logic-apps-and-hello-enterprise-integration-pack"></a><span data-ttu-id="c4181-103">XML-validatie met schema's voor Azure Logic Apps en Hallo Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="c4181-103">Validate XML with schemas for Azure Logic Apps and hello Enterprise Integration Pack</span></span>

<span data-ttu-id="c4181-104">Schema's bevestigen dat Hallo XML-documenten die u ontvangt geldig zijn en Hallo gegevens in een vooraf gedefinieerde indeling verwachte.</span><span class="sxs-lookup"><span data-stu-id="c4181-104">Schemas confirm that hello XML documents you receive are valid and have hello expected data in a predefined format.</span></span> <span data-ttu-id="c4181-105">Schema's kunnen ook berichten die worden uitgewisseld in een B2B-scenario te valideren.</span><span class="sxs-lookup"><span data-stu-id="c4181-105">Schemas also help validate messages that are exchanged in a B2B scenario.</span></span>

## <a name="add-a-schema"></a><span data-ttu-id="c4181-106">Een schema toevoegen</span><span class="sxs-lookup"><span data-stu-id="c4181-106">Add a schema</span></span>

1. <span data-ttu-id="c4181-107">Selecteer in de Azure-portal hello, **meer services**.</span><span class="sxs-lookup"><span data-stu-id="c4181-107">In hello Azure portal, select **More services**.</span></span>

    ![Azure-portal 'Meer services'](media/logic-apps-enterprise-integration-schemas/overview-11.png)

2. <span data-ttu-id="c4181-109">Voer in het zoekvak Hallo-filter, **integratie**, en selecteer **Integratieaccounts** uit de lijst met resultaten Hallo.</span><span class="sxs-lookup"><span data-stu-id="c4181-109">In hello filter search box, enter **integration**, and select **Integration Accounts** from hello results list.</span></span>

    ![Zoekvak filteren](media/logic-apps-enterprise-integration-schemas/overview-21.png)

3. <span data-ttu-id="c4181-111">Selecteer Hallo **integratie account** waar u tooadd Hallo schema.</span><span class="sxs-lookup"><span data-stu-id="c4181-111">Select hello **integration account** where you want tooadd hello schema.</span></span>

    ![Lijst met integratieaccounts](media/logic-apps-enterprise-integration-schemas/overview-31.png)

4. <span data-ttu-id="c4181-113">Kies Hallo **schema's** tegel.</span><span class="sxs-lookup"><span data-stu-id="c4181-113">Choose hello **Schemas** tile.</span></span>

    ![Voorbeeld van de integratie-account, 'Schema'](media/logic-apps-enterprise-integration-schemas/schema-11.png)

### <a name="add-a-schema-file-smaller-than-2-mb"></a><span data-ttu-id="c4181-115">Toevoegen van een schemabestand dat kleiner is dan 2 MB</span><span class="sxs-lookup"><span data-stu-id="c4181-115">Add a schema file smaller than 2 MB</span></span>

1. <span data-ttu-id="c4181-116">In Hallo **schema's** blade die wordt geopend (van Hallo vorige stappen), kiest **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="c4181-116">In hello **Schemas** blade that opens (from hello preceding steps), choose **Add**.</span></span>

    ![Schema's blade "Toevoegen"](media/logic-apps-enterprise-integration-schemas/schema-21.png)

2. <span data-ttu-id="c4181-118">Voer een naam voor uw schema.</span><span class="sxs-lookup"><span data-stu-id="c4181-118">Enter a name for your schema.</span></span> <span data-ttu-id="c4181-119">Hallo-schema-bestand uploaden door het selecteren van Hallo map pictogram volgende toohello **Schema** vak.</span><span class="sxs-lookup"><span data-stu-id="c4181-119">Upload hello schema file by selecting hello folder icon next toohello **Schema** box.</span></span> <span data-ttu-id="c4181-120">Nadat het uploadproces Hallo is voltooid, selecteert u **OK**.</span><span class="sxs-lookup"><span data-stu-id="c4181-120">After hello upload process completes, select **OK**.</span></span>

    ![Schermopname van 'Toevoegen Schema', met 'Kleine file' gemarkeerd](media/logic-apps-enterprise-integration-schemas/schema-31.png)

### <a name="add-a-schema-file-larger-than-2-mb-up-too8-mb-maximum"></a><span data-ttu-id="c4181-122">Een schemabestand groter is dan 2 MB (omhoog too8 MB maximaal) toevoegen</span><span class="sxs-lookup"><span data-stu-id="c4181-122">Add a schema file larger than 2 MB (up too8 MB maximum)</span></span>

<span data-ttu-id="c4181-123">Deze stappen verschillen op basis van het toegangsniveau voor Hallo blob-container: **openbare** of **geen anonieme toegang**.</span><span class="sxs-lookup"><span data-stu-id="c4181-123">These steps differ based on hello blob container access level: **Public** or **No anonymous access**.</span></span>

<span data-ttu-id="c4181-124">**toodetermine dit toegangsniveau**</span><span class="sxs-lookup"><span data-stu-id="c4181-124">**toodetermine this access level**</span></span>

1.  <span data-ttu-id="c4181-125">Open **Azure Opslagverkenner**.</span><span class="sxs-lookup"><span data-stu-id="c4181-125">Open **Azure Storage Explorer**.</span></span> 

2.  <span data-ttu-id="c4181-126">Onder **Blob-Containers**, selecteer Hallo gewenste blob-container.</span><span class="sxs-lookup"><span data-stu-id="c4181-126">Under **Blob Containers**, select hello blob container you want.</span></span> 

3.  <span data-ttu-id="c4181-127">Selecteer **beveiliging**, **toegangsniveau**.</span><span class="sxs-lookup"><span data-stu-id="c4181-127">Select **Security**, **Access Level**.</span></span>

<span data-ttu-id="c4181-128">Als Hallo blob beveiligingsniveau toegang is **openbare**, als volgt te werk.</span><span class="sxs-lookup"><span data-stu-id="c4181-128">If hello blob security access level is **Public**, follow these steps.</span></span>

![Azure Storage Explorer met de 'Blob-Containers', 'Beveiliging' en 'Openbare' gemarkeerd](media/logic-apps-enterprise-integration-schemas/blob-public.png)

1. <span data-ttu-id="c4181-130">Hallo schema tooyour storage-account uploaden en kopieer Hallo URI.</span><span class="sxs-lookup"><span data-stu-id="c4181-130">Upload hello schema tooyour storage account, and copy hello URI.</span></span>

    ![Storage-account met URI gemarkeerd](media/logic-apps-enterprise-integration-schemas/schema-blob.png)

2. <span data-ttu-id="c4181-132">In **Schema toevoegen**, selecteer **groot bestand**, en geef Hallo URI in Hallo **inhoud URI** in het tekstvak.</span><span class="sxs-lookup"><span data-stu-id="c4181-132">In **Add Schema**, select **Large file**, and provide hello URI in hello **Content URI** text box.</span></span>

    ![Schema's met de knop 'Toevoegen' en 'Grote file' gemarkeerd](media/logic-apps-enterprise-integration-schemas/schema-largefile.png)

<span data-ttu-id="c4181-134">Als Hallo blob beveiligingsniveau toegang is **geen anonieme toegang**, als volgt te werk.</span><span class="sxs-lookup"><span data-stu-id="c4181-134">If hello blob security access level is **No anonymous access**, follow these steps.</span></span>

![Azure Storage Explorer met de 'Blob-Containers', 'Beveiliging' en 'Geen anonieme toegang' gemarkeerd](media/logic-apps-enterprise-integration-schemas/blob-1.png)

1. <span data-ttu-id="c4181-136">Hallo schema tooyour storage-account uploaden.</span><span class="sxs-lookup"><span data-stu-id="c4181-136">Upload hello schema tooyour storage account.</span></span>

    ![Storage-account](media/logic-apps-enterprise-integration-schemas/blob-3.png)

2. <span data-ttu-id="c4181-138">Een shared access signature voor Hallo schema genereren.</span><span class="sxs-lookup"><span data-stu-id="c4181-138">Generate a shared access signature for hello schema.</span></span>

    ![Storage-account met gedeelde toegang handtekeningen tabblad gemarkeerd](media/logic-apps-enterprise-integration-schemas/blob-2.png)

3. <span data-ttu-id="c4181-140">In **Schema toevoegen**, selecteer **groot bestand**, en geef Hallo shared access signature URI voor in Hallo **inhoud URI** in het tekstvak.</span><span class="sxs-lookup"><span data-stu-id="c4181-140">In **Add Schema**, select **Large file**, and provide hello shared access signature URI in hello **Content URI** text box.</span></span>

    ![Schema's met de knop 'Toevoegen' en 'Grote file' gemarkeerd](media/logic-apps-enterprise-integration-schemas/schema-largefile.png)

4. <span data-ttu-id="c4181-142">In Hallo **schema's** blade van uw account voor de integratie van uw zojuist toegevoegde schema moet worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="c4181-142">In hello **Schemas** blade of your integration account, your newly added schema should appear.</span></span>

    ![Uw account integratie met 'Schema' en de nieuwe schema Hallo gemarkeerd](media/logic-apps-enterprise-integration-schemas/schema-41.png)

## <a name="edit-schemas"></a><span data-ttu-id="c4181-144">Schema's bewerken</span><span class="sxs-lookup"><span data-stu-id="c4181-144">Edit schemas</span></span>

1. <span data-ttu-id="c4181-145">Kies Hallo **schema's** tegel.</span><span class="sxs-lookup"><span data-stu-id="c4181-145">Choose hello **Schemas** tile.</span></span>

2. <span data-ttu-id="c4181-146">Na het Hallo **schema's** blade wordt geopend, selecteer Hallo-schema dat u wilt dat tooedit.</span><span class="sxs-lookup"><span data-stu-id="c4181-146">After hello **Schemas** blade opens, select hello schema that you want tooedit.</span></span>

3. <span data-ttu-id="c4181-147">Op Hallo **schema's** blade kiezen **bewerken**.</span><span class="sxs-lookup"><span data-stu-id="c4181-147">On hello **Schemas** blade, choose **Edit**.</span></span>

    ![Schema's-blade](media/logic-apps-enterprise-integration-schemas/edit-12.png)

4. <span data-ttu-id="c4181-149">Selecteer Hallo schemabestand dat u wilt dat tooedit en selecteer **Open**.</span><span class="sxs-lookup"><span data-stu-id="c4181-149">Select hello schema file that you want tooedit, then select **Open**.</span></span>

    ![Open schema bestand tooedit](media/logic-apps-enterprise-integration-schemas/edit-31.png)

<span data-ttu-id="c4181-151">Azure toont een bericht dat Hallo schema zijn geüpload.</span><span class="sxs-lookup"><span data-stu-id="c4181-151">Azure shows a message that hello schema uploaded successfully.</span></span>

## <a name="delete-schemas"></a><span data-ttu-id="c4181-152">Schema's verwijderen</span><span class="sxs-lookup"><span data-stu-id="c4181-152">Delete schemas</span></span>

1. <span data-ttu-id="c4181-153">Kies Hallo **schema's** tegel.</span><span class="sxs-lookup"><span data-stu-id="c4181-153">Choose hello **Schemas** tile.</span></span>

2. <span data-ttu-id="c4181-154">Na het Hallo **schema's** blade wordt geopend, selecteer Hallo schema gewenste toodelete.</span><span class="sxs-lookup"><span data-stu-id="c4181-154">After hello **Schemas** blade opens, select hello schema you want toodelete.</span></span>

3. <span data-ttu-id="c4181-155">Op Hallo **schema's** blade kiezen **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="c4181-155">On hello **Schemas** blade, choose **Delete**.</span></span>

    ![Schema's-blade](media/logic-apps-enterprise-integration-schemas/delete-12.png)

4. <span data-ttu-id="c4181-157">schema dat u wilt dat toodelete hello tooconfirm hebt geselecteerd, kiest u **Ja**.</span><span class="sxs-lookup"><span data-stu-id="c4181-157">tooconfirm that you want toodelete hello selected schema, choose **Yes**.</span></span>

    ![Bevestigingsbericht 'Schema verwijderen'](media/logic-apps-enterprise-integration-schemas/delete-21.png)

    <span data-ttu-id="c4181-159">In Hallo **schema's** blade Hallo schema lijst wordt vernieuwd en bevat niet langer Hallo-schema dat u hebt verwijderd.</span><span class="sxs-lookup"><span data-stu-id="c4181-159">In hello **Schemas** blade, hello schema list refreshes  and no longer includes hello schema that you deleted.</span></span>

    ![Uw integratie met 'Schema' gemarkeerd-Account](media/logic-apps-enterprise-integration-schemas/delete-31.png)

## <a name="next-steps"></a><span data-ttu-id="c4181-161">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c4181-161">Next steps</span></span>
* <span data-ttu-id="c4181-162">[Meer informatie over Enterprise Integration Pack Hallo](logic-apps-enterprise-integration-overview.md "meer informatie over Hallo enterprise integration pack").</span><span class="sxs-lookup"><span data-stu-id="c4181-162">[Learn more about hello Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md "Learn about hello enterprise integration pack").</span></span>  

