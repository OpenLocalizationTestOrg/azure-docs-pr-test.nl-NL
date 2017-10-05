---
title: Een gebruikersinterface aanpassen met behulp van aangepaste beleidsregels - Azure AD B2C | Microsoft Docs
description: Meer informatie over het aanpassen van een gebruikersinterface (UI) tijdens het gebruik van aangepast beleid in Azure AD B2C.
services: active-directory-b2c
documentationcenter: 
author: saeedakhter-msft
manager: krassk
editor: parakhj
ms.assetid: 658c597e-3787-465e-b377-26aebc94e46d
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 04/04/2017
ms.author: saeedakhter-msft
ms.openlocfilehash: d5a3c0a323b31696d39e3d2b36317dec3a2337d7
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="azure-active-directory-b2c-configure-ui-customization-in-a-custom-policy"></a><span data-ttu-id="e9448-103">Azure Active Directory B2C: UI-aanpassing in een aangepast beleid configureren</span><span class="sxs-lookup"><span data-stu-id="e9448-103">Azure Active Directory B2C: Configure UI customization in a custom policy</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="e9448-104">Nadat u dit artikel hebt voltooid, hebt u een aangepast beleid voor aanmelden en aanmelden met uw merk en identiteit.</span><span class="sxs-lookup"><span data-stu-id="e9448-104">After you complete this article, you will have a sign-up and sign-in custom policy with your brand and appearance.</span></span> <span data-ttu-id="e9448-105">Met Azure Active Directory B2C (Azure AD B2C) dat u bijna volledig beheer van de HTML- en CSS-inhoud die wordt weergegeven aan gebruikers.</span><span class="sxs-lookup"><span data-stu-id="e9448-105">With Azure Active Directory B2C (Azure AD B2C), you get nearly full control of the HTML and CSS content that's presented to users.</span></span> <span data-ttu-id="e9448-106">Wanneer u een aangepast beleid gebruikt, configureert u de UI-aanpassing in XML in plaats van besturingselementen in de Azure portal.</span><span class="sxs-lookup"><span data-stu-id="e9448-106">When you use a custom policy, you configure UI customization in XML instead of using controls in the Azure portal.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="e9448-107">Vereisten</span><span class="sxs-lookup"><span data-stu-id="e9448-107">Prerequisites</span></span>

<span data-ttu-id="e9448-108">Voordat u begint, voltooien [aan de slag met aangepaste beleidsregels](active-directory-b2c-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="e9448-108">Before you begin, complete [Getting started with custom policies](active-directory-b2c-get-started-custom.md).</span></span> <span data-ttu-id="e9448-109">U hebt een werkende aangepast beleid voor aanmelden en aanmelden met lokale accounts.</span><span class="sxs-lookup"><span data-stu-id="e9448-109">You should have a working custom policy for sign-up and sign-in with local accounts.</span></span>

## <a name="page-ui-customization"></a><span data-ttu-id="e9448-110">Page UI-aanpassing</span><span class="sxs-lookup"><span data-stu-id="e9448-110">Page UI customization</span></span>

<span data-ttu-id="e9448-111">U kunt het uiterlijk van het aangepaste beleid aanpassen met behulp van de pagina UI aanpassing-functie.</span><span class="sxs-lookup"><span data-stu-id="e9448-111">By using the page UI customization feature, you can customize the look and feel of any custom policy.</span></span> <span data-ttu-id="e9448-112">U kunt ook behouden merk en visuele consistentie tussen uw toepassing en de Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="e9448-112">You can also maintain brand and visual consistency between your application and Azure AD B2C.</span></span>

<span data-ttu-id="e9448-113">Dit is hoe het werkt: Azure AD B2C wordt code wordt uitgevoerd in de browser van uw klant en maakt gebruik van een benadering van moderne aangeroepen [Cross-Origin-Resource delen (CORS)](http://www.w3.org/TR/cors/).</span><span class="sxs-lookup"><span data-stu-id="e9448-113">Here's how it works: Azure AD B2C runs code in your customer's browser and uses a modern approach called [Cross-Origin Resource Sharing (CORS)](http://www.w3.org/TR/cors/).</span></span> <span data-ttu-id="e9448-114">Eerst, geeft u een URL in het aangepaste beleid met aangepaste HTML-inhoud.</span><span class="sxs-lookup"><span data-stu-id="e9448-114">First, you specify a URL in the custom policy with customized HTML content.</span></span> <span data-ttu-id="e9448-115">Azure AD B2C samenvoegingen UI-elementen met de HTML-inhoud die is geladen vanaf uw URL en wordt de pagina weergegeven in de klant.</span><span class="sxs-lookup"><span data-stu-id="e9448-115">Azure AD B2C merges UI elements with the HTML content that's loaded from your URL and then displays the page to the customer.</span></span>

## <a name="create-your-html5-content"></a><span data-ttu-id="e9448-116">Uw HTML5 inhoud maken</span><span class="sxs-lookup"><span data-stu-id="e9448-116">Create your HTML5 content</span></span>

<span data-ttu-id="e9448-117">HTML-inhoud met de naam van uw product maken in de titel.</span><span class="sxs-lookup"><span data-stu-id="e9448-117">Create HTML content with your product's brand name in the title.</span></span>

1. <span data-ttu-id="e9448-118">Kopieer het volgende fragment in de HTML-code.</span><span class="sxs-lookup"><span data-stu-id="e9448-118">Copy the following HTML snippet.</span></span> <span data-ttu-id="e9448-119">Indeling geldig is HTML5 met een leeg element aangeroepen  *\<div-id = 'api'\>\</div\>*  zich binnen de  *\<hoofdtekst\>*  labels.</span><span class="sxs-lookup"><span data-stu-id="e9448-119">It is well-formed HTML5 with an empty element called *\<div id="api"\>\</div\>* located within the *\<body\>* tags.</span></span> <span data-ttu-id="e9448-120">Dit element geeft aan waar Azure AD B2C-inhoud moet worden ingevoegd.</span><span class="sxs-lookup"><span data-stu-id="e9448-120">This element indicates where Azure AD B2C content is to be inserted.</span></span>

   ```html
   <!DOCTYPE html>
   <html>
   <head>
       <title>My Product Brand Name</title>
   </head>
   <body>
       <div id="api"></div>
   </body>
   </html>
   ```

   >[!NOTE]
   ><span data-ttu-id="e9448-121">Uit veiligheidsoverwegingen is het gebruik van JavaScript momenteel geblokkeerd om aan te passen.</span><span class="sxs-lookup"><span data-stu-id="e9448-121">For security reasons, the use of JavaScript is currently blocked for customization.</span></span>

2. <span data-ttu-id="e9448-122">Plak de gekopieerde codefragment in een teksteditor en sla het bestand als *aanpassen ui.html*.</span><span class="sxs-lookup"><span data-stu-id="e9448-122">Paste the copied snippet in a text editor, and then save the file as *customize-ui.html*.</span></span>

## <a name="create-an-azure-blob-storage-account"></a><span data-ttu-id="e9448-123">Een Azure Blob storage-account maken</span><span class="sxs-lookup"><span data-stu-id="e9448-123">Create an Azure Blob storage account</span></span>

>[!NOTE]
> <span data-ttu-id="e9448-124">In dit artikel gebruiken we Azure Blob-opslag om onze inhoud te hosten.</span><span class="sxs-lookup"><span data-stu-id="e9448-124">In this article, we use Azure Blob storage to host our content.</span></span> <span data-ttu-id="e9448-125">U kunt kiezen voor het hosten van uw inhoud op een webserver, maar u moet [CORS zijn ingeschakeld op uw webserver](https://enable-cors.org/server.html).</span><span class="sxs-lookup"><span data-stu-id="e9448-125">You can choose to host your content on a web server, but you must [enable CORS on your web server](https://enable-cors.org/server.html).</span></span>

<span data-ttu-id="e9448-126">Voor het hosten van deze HTML-inhoud in de Blob-opslag, het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="e9448-126">To host this HTML content in Blob storage, do the following:</span></span>

1. <span data-ttu-id="e9448-127">Meld u aan bij [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e9448-127">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="e9448-128">Op de **Hub** selecteert u **nieuw** > **opslag** > **opslagaccount**.</span><span class="sxs-lookup"><span data-stu-id="e9448-128">On the **Hub** menu, select **New** > **Storage** > **Storage account**.</span></span>
3. <span data-ttu-id="e9448-129">Voer een unieke **naam** voor uw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="e9448-129">Enter a unique **Name** for your storage account.</span></span>
4. <span data-ttu-id="e9448-130">**Implementatiemodel** kan blijven **Resource Manager**.</span><span class="sxs-lookup"><span data-stu-id="e9448-130">**Deployment model** can remain **Resource Manager**.</span></span>
5. <span data-ttu-id="e9448-131">Wijziging **soort Account** naar **Blob storage**.</span><span class="sxs-lookup"><span data-stu-id="e9448-131">Change **Account Kind** to **Blob storage**.</span></span>
6. <span data-ttu-id="e9448-132">**Prestaties** kan blijven **standaard**.</span><span class="sxs-lookup"><span data-stu-id="e9448-132">**Performance** can remain **Standard**.</span></span>
7. <span data-ttu-id="e9448-133">**Replicatie** kan blijven **RA-GRS**.</span><span class="sxs-lookup"><span data-stu-id="e9448-133">**Replication** can remain **RA-GRS**.</span></span>
8. <span data-ttu-id="e9448-134">**Toegangslaag** kan blijven **Hot**.</span><span class="sxs-lookup"><span data-stu-id="e9448-134">**Access tier** can remain **Hot**.</span></span>
9. <span data-ttu-id="e9448-135">**Versleuteling van de opslagruimte** kan blijven **uitgeschakelde**.</span><span class="sxs-lookup"><span data-stu-id="e9448-135">**Storage service encryption** can remain **Disabled**.</span></span>
10. <span data-ttu-id="e9448-136">Selecteer een **abonnement** voor uw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="e9448-136">Select a **Subscription** for your storage account.</span></span>
11. <span data-ttu-id="e9448-137">Maak een **resourcegroep** of een bestaande set selecteren.</span><span class="sxs-lookup"><span data-stu-id="e9448-137">Create a **Resource group** or select an existing one.</span></span>
12. <span data-ttu-id="e9448-138">Selecteer de **geografische locatie** voor uw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="e9448-138">Select the **Geographic location** for your storage account.</span></span>
13. <span data-ttu-id="e9448-139">Klik op **Maken** om het opslagaccount te maken.</span><span class="sxs-lookup"><span data-stu-id="e9448-139">Click **Create** to create the storage account.</span></span>  
    <span data-ttu-id="e9448-140">Nadat de implementatie is voltooid, de **opslagaccount** blade wordt automatisch geopend.</span><span class="sxs-lookup"><span data-stu-id="e9448-140">After the deployment is completed, the **Storage account** blade opens automatically.</span></span>

## <a name="create-a-container"></a><span data-ttu-id="e9448-141">Een container maken</span><span class="sxs-lookup"><span data-stu-id="e9448-141">Create a container</span></span>

<span data-ttu-id="e9448-142">U maakt een openbare container in Blob-opslag door het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="e9448-142">To create a public container in Blob storage, do the following:</span></span>

1. <span data-ttu-id="e9448-143">Klik op de **overzicht** tabblad.</span><span class="sxs-lookup"><span data-stu-id="e9448-143">Click the **Overview** tab.</span></span>
2. <span data-ttu-id="e9448-144">Klik op **Container**.</span><span class="sxs-lookup"><span data-stu-id="e9448-144">Click **Container**.</span></span>
3. <span data-ttu-id="e9448-145">Voor **naam**, type **$root**.</span><span class="sxs-lookup"><span data-stu-id="e9448-145">For **Name**, type **$root**.</span></span>
4. <span data-ttu-id="e9448-146">Stel **toegangstype** naar **Blob**.</span><span class="sxs-lookup"><span data-stu-id="e9448-146">Set **Access type** to **Blob**.</span></span>
5. <span data-ttu-id="e9448-147">Klik op **$root** openen van de nieuwe container.</span><span class="sxs-lookup"><span data-stu-id="e9448-147">Click **$root** to open the new container.</span></span>
6. <span data-ttu-id="e9448-148">Klik op **Uploaden**.</span><span class="sxs-lookup"><span data-stu-id="e9448-148">Click **Upload**.</span></span>
7. <span data-ttu-id="e9448-149">Klik op het pictogram naast **selecteert u een bestand**.</span><span class="sxs-lookup"><span data-stu-id="e9448-149">Click the folder icon next to **Select a file**.</span></span>
8. <span data-ttu-id="e9448-150">Ga naar **aanpassen ui.html**, die u eerder hebt gemaakt in de [Page UI-aanpassing](#the-page-ui-customization-feature) sectie.</span><span class="sxs-lookup"><span data-stu-id="e9448-150">Go to **customize-ui.html**, which you created earlier in the [Page UI customization](#the-page-ui-customization-feature) section.</span></span>
9. <span data-ttu-id="e9448-151">Klik op **Uploaden**.</span><span class="sxs-lookup"><span data-stu-id="e9448-151">Click **Upload**.</span></span>
10. <span data-ttu-id="e9448-152">Selecteer de aanpassen ui.html blob die u hebt geüpload.</span><span class="sxs-lookup"><span data-stu-id="e9448-152">Select the customize-ui.html blob that you uploaded.</span></span>
11. <span data-ttu-id="e9448-153">Naast **URL**, klikt u op **kopie**.</span><span class="sxs-lookup"><span data-stu-id="e9448-153">Next to **URL**, click **Copy**.</span></span>
12. <span data-ttu-id="e9448-154">In een browser, plak de gekopieerde URL en Ga naar de site.</span><span class="sxs-lookup"><span data-stu-id="e9448-154">In a browser, paste the copied URL, and go to the site.</span></span> <span data-ttu-id="e9448-155">Als de site niet toegankelijk is, zorg ervoor dat het type van de container toegang is ingesteld op **blob**.</span><span class="sxs-lookup"><span data-stu-id="e9448-155">If the site is inaccessible, make sure the container access type is set to **blob**.</span></span>

## <a name="configure-cors"></a><span data-ttu-id="e9448-156">CORS configureren</span><span class="sxs-lookup"><span data-stu-id="e9448-156">Configure CORS</span></span>

<span data-ttu-id="e9448-157">Blob-opslag configureren voor het delen van Cross-Origin-Resource als volgt:</span><span class="sxs-lookup"><span data-stu-id="e9448-157">Configure Blob storage for Cross-Origin Resource Sharing by doing the following:</span></span>

>[!NOTE]
><span data-ttu-id="e9448-158">Wilt u de UI-functie voor aanpassing door het gebruik van onze voorbeeld HTML en CSS-inhoud uitproberen?</span><span class="sxs-lookup"><span data-stu-id="e9448-158">Want to try out the UI customization feature by using our sample HTML and CSS content?</span></span> <span data-ttu-id="e9448-159">We bieden [een eenvoudige helper hulpprogramma](active-directory-b2c-reference-ui-customization-helper-tool.md) die uploadt en configureert u onze voorbeelden op uw Blob storage-account.</span><span class="sxs-lookup"><span data-stu-id="e9448-159">We've provided [a simple helper tool](active-directory-b2c-reference-ui-customization-helper-tool.md) that uploads and configures our sample content on your Blob storage account.</span></span> <span data-ttu-id="e9448-160">Als u het hulpprogramma gebruikt, gaat u verder met [wijzigen van het aangepaste beleid registreren of aanmelden](#modify-your-sign-up-or-sign-in-custom-policy).</span><span class="sxs-lookup"><span data-stu-id="e9448-160">If you use the tool, skip ahead to [Modify your sign-up or sign-in custom policy](#modify-your-sign-up-or-sign-in-custom-policy).</span></span>

1. <span data-ttu-id="e9448-161">Op de **opslag** blade onder **instellingen**Open **CORS**.</span><span class="sxs-lookup"><span data-stu-id="e9448-161">On the **Storage** blade, under **Settings**, open **CORS**.</span></span>
2. <span data-ttu-id="e9448-162">Klik op **Add**.</span><span class="sxs-lookup"><span data-stu-id="e9448-162">Click **Add**.</span></span>
3. <span data-ttu-id="e9448-163">Voor **toegestane oorsprongen**, typt u een sterretje (\*).</span><span class="sxs-lookup"><span data-stu-id="e9448-163">For **Allowed origins**, type an asterisk (\*).</span></span>
4. <span data-ttu-id="e9448-164">In de **toegestane termen** vervolgkeuzelijst, selecteer **ophalen** en **opties**.</span><span class="sxs-lookup"><span data-stu-id="e9448-164">In the **Allowed verbs** drop-down list, select both **GET** and **OPTIONS**.</span></span>
5. <span data-ttu-id="e9448-165">Voor **toegestaan headers**, typt u een sterretje (\*).</span><span class="sxs-lookup"><span data-stu-id="e9448-165">For **Allowed headers**, type an asterisk (\*).</span></span>
6. <span data-ttu-id="e9448-166">Voor **blootgesteld headers**, typt u een sterretje (\*).</span><span class="sxs-lookup"><span data-stu-id="e9448-166">For **Exposed headers**, type an asterisk (\*).</span></span>
7. <span data-ttu-id="e9448-167">Voor **maximale leeftijd (seconden)**, type **200**.</span><span class="sxs-lookup"><span data-stu-id="e9448-167">For **Maximum age (seconds)**, type **200**.</span></span>
8. <span data-ttu-id="e9448-168">Klik op **Add**.</span><span class="sxs-lookup"><span data-stu-id="e9448-168">Click **Add**.</span></span>

## <a name="test-cors"></a><span data-ttu-id="e9448-169">Test CORS</span><span class="sxs-lookup"><span data-stu-id="e9448-169">Test CORS</span></span>

<span data-ttu-id="e9448-170">Valideren dat u klaar bent als volgt:</span><span class="sxs-lookup"><span data-stu-id="e9448-170">Validate that you're ready by doing the following:</span></span>

1. <span data-ttu-id="e9448-171">Ga naar de [test cors.org](http://test-cors.org/) website, en plak de URL in de **externe URL** vak.</span><span class="sxs-lookup"><span data-stu-id="e9448-171">Go to the [test-cors.org](http://test-cors.org/) website, and then paste the URL in the **Remote URL** box.</span></span>
2. <span data-ttu-id="e9448-172">Klik op **aanvraag verzenden**.</span><span class="sxs-lookup"><span data-stu-id="e9448-172">Click **Send Request**.</span></span>  
    <span data-ttu-id="e9448-173">Als u een foutbericht ontvangt, controleert u of uw [CORS-instellingen voor](#configure-cors) juist zijn.</span><span class="sxs-lookup"><span data-stu-id="e9448-173">If you receive an error, make sure that your [CORS settings](#configure-cors) are correct.</span></span> <span data-ttu-id="e9448-174">Mogelijk moet u ook uw browsercache wissen of een browsersessie in particuliere openen door op Ctrl + Shift + P te drukken.</span><span class="sxs-lookup"><span data-stu-id="e9448-174">You might also need to clear your browser cache or open an in-private browsing session by pressing Ctrl+Shift+P.</span></span>

## <a name="modify-your-sign-up-or-sign-in-custom-policy"></a><span data-ttu-id="e9448-175">Wijzigen van het aangepaste beleid registreren of aanmelden</span><span class="sxs-lookup"><span data-stu-id="e9448-175">Modify your sign-up or sign-in custom policy</span></span>

<span data-ttu-id="e9448-176">Onder de hoogste  *\<TrustFrameworkPolicy\>*  labels, zult u  *\<BuildingBlocks\>*  label.</span><span class="sxs-lookup"><span data-stu-id="e9448-176">Under the top-level *\<TrustFrameworkPolicy\>* tag, you should find *\<BuildingBlocks\>* tag.</span></span> <span data-ttu-id="e9448-177">Binnen de  *\<BuildingBlocks\>*  tags, Voeg een  *\<ContentDefinitions\>*  code door te kopiëren van het volgende voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="e9448-177">Within the *\<BuildingBlocks\>* tags, add a *\<ContentDefinitions\>* tag by copying the following example.</span></span> <span data-ttu-id="e9448-178">Vervang *your_storage_account* met de naam van uw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="e9448-178">Replace *your_storage_account* with the name of your storage account.</span></span>

  ```xml
  <BuildingBlocks>
    <ContentDefinitions>
      <ContentDefinition Id="api.idpselections">
        <LoadUri>https://{your_storage_account}.blob.core.windows.net/customize-ui.html</LoadUri>
      </ContentDefinition>
    </ContentDefinitions>
  </BuildingBlocks>
  ```

## <a name="upload-your-updated-custom-policy"></a><span data-ttu-id="e9448-179">Upload uw bijgewerkte aangepast beleid</span><span class="sxs-lookup"><span data-stu-id="e9448-179">Upload your updated custom policy</span></span>

1. <span data-ttu-id="e9448-180">In de [Azure-portal](https://portal.azure.com), [switch in de context van uw Azure AD B2C-tenant](active-directory-b2c-navigate-to-b2c-context.md), en open vervolgens de **Azure AD B2C** blade.</span><span class="sxs-lookup"><span data-stu-id="e9448-180">In the [Azure portal](https://portal.azure.com), [switch into the context of your Azure AD B2C tenant](active-directory-b2c-navigate-to-b2c-context.md), and then open the **Azure AD B2C** blade.</span></span>
2. <span data-ttu-id="e9448-181">Klik op **alle beleidsregels**.</span><span class="sxs-lookup"><span data-stu-id="e9448-181">Click **All Policies**.</span></span>
3. <span data-ttu-id="e9448-182">Klik op **uploaden beleid**.</span><span class="sxs-lookup"><span data-stu-id="e9448-182">Click **Upload Policy**.</span></span>
4. <span data-ttu-id="e9448-183">Uploaden `SignUpOrSignin.xml` met de  *\<ContentDefinitions\>*  code die u eerder hebt toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="e9448-183">Upload `SignUpOrSignin.xml` with the *\<ContentDefinitions\>* tag that you added previously.</span></span>

## <a name="test-the-custom-policy-by-using-run-now"></a><span data-ttu-id="e9448-184">Het aangepaste beleid testen met behulp van **nu uitvoeren**</span><span class="sxs-lookup"><span data-stu-id="e9448-184">Test the custom policy by using **Run now**</span></span>

1. <span data-ttu-id="e9448-185">Op de **Azure AD B2C** blade, gaat u naar **alle beleidsregels**.</span><span class="sxs-lookup"><span data-stu-id="e9448-185">On the **Azure AD B2C** blade, go to **All polices**.</span></span>
2. <span data-ttu-id="e9448-186">Selecteer het aangepaste beleid die u hebt geüpload en klik op de **nu uitvoeren** knop.</span><span class="sxs-lookup"><span data-stu-id="e9448-186">Select the custom policy that you uploaded, and click the **Run now** button.</span></span>
3. <span data-ttu-id="e9448-187">U moet kunnen aanmelden met een e-mailadres.</span><span class="sxs-lookup"><span data-stu-id="e9448-187">You should be able to sign up by using an email address.</span></span>

## <a name="reference"></a><span data-ttu-id="e9448-188">Naslaginformatie</span><span class="sxs-lookup"><span data-stu-id="e9448-188">Reference</span></span>

<span data-ttu-id="e9448-189">Voor de UI-aanpassing Hier vindt u voorbeeldsjablonen:</span><span class="sxs-lookup"><span data-stu-id="e9448-189">You can find sample templates for UI customization here:</span></span>

```
git clone https://github.com/azureadquickstarts/b2c-azureblobstorage-client
```

<span data-ttu-id="e9448-190">De map sample_templates/wingtip bevat de volgende HTML-bestanden:</span><span class="sxs-lookup"><span data-stu-id="e9448-190">The sample_templates/wingtip folder contains the following HTML files:</span></span>

| <span data-ttu-id="e9448-191">HTML5-sjabloon</span><span class="sxs-lookup"><span data-stu-id="e9448-191">HTML5 template</span></span> | <span data-ttu-id="e9448-192">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="e9448-192">Description</span></span> |
|----------------|-------------|
| <span data-ttu-id="e9448-193">*phonefactor.HTML*</span><span class="sxs-lookup"><span data-stu-id="e9448-193">*phonefactor.html*</span></span> | <span data-ttu-id="e9448-194">Dit bestand als sjabloon gebruiken voor een multi-factor authentication-pagina.</span><span class="sxs-lookup"><span data-stu-id="e9448-194">Use this file as a template for a multi-factor authentication page.</span></span> |
| <span data-ttu-id="e9448-195">*ResetPassword.HTML*</span><span class="sxs-lookup"><span data-stu-id="e9448-195">*resetpassword.html*</span></span> | <span data-ttu-id="e9448-196">Dit bestand te gebruiken als een sjabloon voor een wachtwoordpagina vergeten.</span><span class="sxs-lookup"><span data-stu-id="e9448-196">Use this file as a template for a forgot password page.</span></span> |
| <span data-ttu-id="e9448-197">*selfasserted.HTML*</span><span class="sxs-lookup"><span data-stu-id="e9448-197">*selfasserted.html*</span></span> | <span data-ttu-id="e9448-198">Dit bestand als een sjabloon voor een aanmeldingspagina sociale account, de aanmeldingspagina van een lokaal account of een aanmeldingspagina lokale account gebruiken.</span><span class="sxs-lookup"><span data-stu-id="e9448-198">Use this file as a template for a social account sign-up page, a local account sign-up page, or a local account sign-in page.</span></span> |
| <span data-ttu-id="e9448-199">*Unified.HTML*</span><span class="sxs-lookup"><span data-stu-id="e9448-199">*unified.html*</span></span> | <span data-ttu-id="e9448-200">Dit bestand als sjabloon gebruiken voor een uniforme registreren of aanmelden pagina.</span><span class="sxs-lookup"><span data-stu-id="e9448-200">Use this file as a template for a unified sign-up or sign-in page.</span></span> |
| <span data-ttu-id="e9448-201">*updateprofile.HTML*</span><span class="sxs-lookup"><span data-stu-id="e9448-201">*updateprofile.html*</span></span> | <span data-ttu-id="e9448-202">Dit bestand als een sjabloon voor een update-profielpagina gebruiken.</span><span class="sxs-lookup"><span data-stu-id="e9448-202">Use this file as a template for a profile update page.</span></span> |

<span data-ttu-id="e9448-203">In de [, wijzigt u de sectie registreren of aanmelden aangepast beleid](#modify-your-sign-up-or-sign-in-custom-policy), geconfigureerd van de inhoud definitie voor `api.idpselections`.</span><span class="sxs-lookup"><span data-stu-id="e9448-203">In the [Modify your sign-up or sign-in custom policy section](#modify-your-sign-up-or-sign-in-custom-policy), you configured the content definition for `api.idpselections`.</span></span> <span data-ttu-id="e9448-204">De volledige set van inhoud definitie-id's die worden herkend door het Azure AD B2C identiteit ervaring framework en de bijbehorende beschrijvingen zijn in de volgende tabel:</span><span class="sxs-lookup"><span data-stu-id="e9448-204">The full set of content definition IDs that are recognized by the Azure AD B2C identity experience framework and their descriptions are in the following table:</span></span>

| <span data-ttu-id="e9448-205">De definitie van de inhoud-ID</span><span class="sxs-lookup"><span data-stu-id="e9448-205">Content definition ID</span></span> | <span data-ttu-id="e9448-206">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="e9448-206">Description</span></span> | 
|-----------------------|-------------|
| <span data-ttu-id="e9448-207">*API.Error*</span><span class="sxs-lookup"><span data-stu-id="e9448-207">*api.error*</span></span> | <span data-ttu-id="e9448-208">**Foutpagina**.</span><span class="sxs-lookup"><span data-stu-id="e9448-208">**Error page**.</span></span> <span data-ttu-id="e9448-209">Deze pagina wordt weergegeven wanneer een uitzondering of een fout is opgetreden.</span><span class="sxs-lookup"><span data-stu-id="e9448-209">This page is displayed when an exception or an error is encountered.</span></span> |
| <span data-ttu-id="e9448-210">*API.idpselections*</span><span class="sxs-lookup"><span data-stu-id="e9448-210">*api.idpselections*</span></span> | <span data-ttu-id="e9448-211">**Id-provider selectiepagina**.</span><span class="sxs-lookup"><span data-stu-id="e9448-211">**Identity provider selection page**.</span></span> <span data-ttu-id="e9448-212">Deze pagina bevat een lijst met de id-providers die de gebruiker uit tijdens het aanmelden kiezen kan.</span><span class="sxs-lookup"><span data-stu-id="e9448-212">This page contains a list of identity providers that the user can choose from during sign-in.</span></span> <span data-ttu-id="e9448-213">Deze opties zijn enterprise identiteitsproviders, sociale id-providers zoals Facebook en Google + of lokale accounts.</span><span class="sxs-lookup"><span data-stu-id="e9448-213">These options are either enterprise identity providers, social identity providers such as Facebook and Google+, or local accounts.</span></span> |
| <span data-ttu-id="e9448-214">*API.idpselections.Signup*</span><span class="sxs-lookup"><span data-stu-id="e9448-214">*api.idpselections.signup*</span></span> | <span data-ttu-id="e9448-215">**Selectie van de id-provider voor registratie**.</span><span class="sxs-lookup"><span data-stu-id="e9448-215">**Identity provider selection for sign-up**.</span></span> <span data-ttu-id="e9448-216">Deze pagina bevat een lijst met de id-providers die de gebruiker uit tijdens de registratie kiezen kan.</span><span class="sxs-lookup"><span data-stu-id="e9448-216">This page contains a list of identity providers that the user can choose from during sign-up.</span></span> <span data-ttu-id="e9448-217">Deze opties zijn enterprise identiteitsproviders, sociale id-providers zoals Facebook en Google + of lokale accounts.</span><span class="sxs-lookup"><span data-stu-id="e9448-217">These options are either enterprise identity providers, social identity providers such as Facebook and Google+, or local accounts.</span></span> |
| <span data-ttu-id="e9448-218">*API.localaccountpasswordreset*</span><span class="sxs-lookup"><span data-stu-id="e9448-218">*api.localaccountpasswordreset*</span></span> | <span data-ttu-id="e9448-219">**Wachtwoordpagina vergeten**.</span><span class="sxs-lookup"><span data-stu-id="e9448-219">**Forgot password page**.</span></span> <span data-ttu-id="e9448-220">Deze pagina bevat een formulier dat de gebruiker moeten worden voltooid voor het initiëren van een wachtwoord opnieuw instellen.</span><span class="sxs-lookup"><span data-stu-id="e9448-220">This page contains a form that the user must complete to initiate a password reset.</span></span>  |
| <span data-ttu-id="e9448-221">*API.localaccountsignin*</span><span class="sxs-lookup"><span data-stu-id="e9448-221">*api.localaccountsignin*</span></span> | <span data-ttu-id="e9448-222">**Aanmeldingspagina voor lokaal account**.</span><span class="sxs-lookup"><span data-stu-id="e9448-222">**Local account sign-in page**.</span></span> <span data-ttu-id="e9448-223">Deze pagina bevat een formulier-in voor het aanmelden met een lokaal account dat is gebaseerd op een e-mailadres of een gebruikersnaam.</span><span class="sxs-lookup"><span data-stu-id="e9448-223">This page contains a sign-in form for signing in with a local account that is based on an email address or a user name.</span></span> <span data-ttu-id="e9448-224">Het formulier kan een tekstinvoervak en wachtwoordvak vermelding bevatten.</span><span class="sxs-lookup"><span data-stu-id="e9448-224">The form can contain a text input box and password entry box.</span></span> |
| <span data-ttu-id="e9448-225">*API.localaccountsignup*</span><span class="sxs-lookup"><span data-stu-id="e9448-225">*api.localaccountsignup*</span></span> | <span data-ttu-id="e9448-226">**Lokaal account aanmeldingspagina**.</span><span class="sxs-lookup"><span data-stu-id="e9448-226">**Local account sign-up page**.</span></span> <span data-ttu-id="e9448-227">Deze pagina bevat een aanmeldingsformulier hebt ingevuld voor het aanmelden voor een lokaal account dat is gebaseerd op een e-mailadres of een gebruikersnaam.</span><span class="sxs-lookup"><span data-stu-id="e9448-227">This page contains a sign-up form for signing up for a local account that is based on an email address or a user name.</span></span> <span data-ttu-id="e9448-228">Het formulier kan verschillende invoer besturingselementen bevatten, zoals een tekstinvoervak vak een wachtwoord, een keuzerondje, één vervolgkeuzelijsten en meervoudige selectie selectievakjes.</span><span class="sxs-lookup"><span data-stu-id="e9448-228">The form can contain various input controls, such as a text input box, a password entry box, a radio button, single-select drop-down boxes, and multi-select check boxes.</span></span> |
| <span data-ttu-id="e9448-229">*API.phonefactor*</span><span class="sxs-lookup"><span data-stu-id="e9448-229">*api.phonefactor*</span></span> | <span data-ttu-id="e9448-230">**Multi-factor authentication-pagina**.</span><span class="sxs-lookup"><span data-stu-id="e9448-230">**Multi-factor authentication page**.</span></span> <span data-ttu-id="e9448-231">Op deze pagina, kunnen gebruikers hun telefoonnummers (met behulp van tekst of stem) controleren tijdens het registreren of aanmelden.</span><span class="sxs-lookup"><span data-stu-id="e9448-231">On this page, users can verify their phone numbers (by using text or voice) during sign-up or sign-in.</span></span> |
| <span data-ttu-id="e9448-232">*API.selfasserted*</span><span class="sxs-lookup"><span data-stu-id="e9448-232">*api.selfasserted*</span></span> | <span data-ttu-id="e9448-233">**De aanmeldpagina sociale account**.</span><span class="sxs-lookup"><span data-stu-id="e9448-233">**Social account sign-up page**.</span></span> <span data-ttu-id="e9448-234">Deze pagina bevat een aanmeldingsformulier hebt ingevuld die gebruikers moeten worden voltooid wanneer ze zich registreren met behulp van een bestaand account van een identiteitsprovider van sociale zoals Facebook of Google +.</span><span class="sxs-lookup"><span data-stu-id="e9448-234">This page contains a sign-up form that users must complete when they sign up by using an existing account from a social identity provider such as Facebook or Google+.</span></span> <span data-ttu-id="e9448-235">Deze pagina is vergelijkbaar met de voorgaande sociale account aanmeldpagina, met uitzondering van de invoervelden wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="e9448-235">This page is similar to the preceding social account sign-up page, except for the password entry fields.</span></span> |
| <span data-ttu-id="e9448-236">*API.selfasserted.profileupdate*</span><span class="sxs-lookup"><span data-stu-id="e9448-236">*api.selfasserted.profileupdate*</span></span> | <span data-ttu-id="e9448-237">**Update profielpagina**.</span><span class="sxs-lookup"><span data-stu-id="e9448-237">**Profile update page**.</span></span> <span data-ttu-id="e9448-238">Deze pagina bevat een formulier dat gebruikers gebruiken kunnen om hun profiel bijwerken.</span><span class="sxs-lookup"><span data-stu-id="e9448-238">This page contains a form that users can use to update their profile.</span></span> <span data-ttu-id="e9448-239">Deze pagina is vergelijkbaar met de sociale account aanmeldpagina, met uitzondering van de invoervelden wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="e9448-239">This page is similar to the social account sign-up page, except for the password entry fields.</span></span> |
| <span data-ttu-id="e9448-240">*API.signuporsignin*</span><span class="sxs-lookup"><span data-stu-id="e9448-240">*api.signuporsignin*</span></span> | <span data-ttu-id="e9448-241">**Unified registreren of aanmelden pagina**.</span><span class="sxs-lookup"><span data-stu-id="e9448-241">**Unified sign-up or sign-in page**.</span></span> <span data-ttu-id="e9448-242">Deze pagina verwerkt de registreren en aanmelden van gebruikers, die enterprise identiteitsproviders, sociale id-providers zoals Facebook of Google + of lokale accounts kunnen gebruiken.</span><span class="sxs-lookup"><span data-stu-id="e9448-242">This page handles both the sign-up and sign-in of users, who can use enterprise identity providers, social identity providers such as Facebook or Google+, or local accounts.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="e9448-243">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e9448-243">Next steps</span></span>

<span data-ttu-id="e9448-244">Zie voor meer informatie over de UI-elementen die kunnen worden aangepast, [Naslaggids voor aanpassing van de gebruikersinterface voor ingebouwde beleid](active-directory-b2c-reference-ui-customization.md).</span><span class="sxs-lookup"><span data-stu-id="e9448-244">For additional information about UI elements that can be customized, see [reference guide for UI customization for built-in policies](active-directory-b2c-reference-ui-customization.md).</span></span>
