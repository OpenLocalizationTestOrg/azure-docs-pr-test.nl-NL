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
ms.openlocfilehash: 6f00995e54c9f9ef27cc51e38f3de07cd5817cc1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-configure-ui-customization-in-a-custom-policy"></a><span data-ttu-id="488d2-103">Azure Active Directory B2C: UI-aanpassing in een aangepast beleid configureren</span><span class="sxs-lookup"><span data-stu-id="488d2-103">Azure Active Directory B2C: Configure UI customization in a custom policy</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="488d2-104">Nadat u dit artikel hebt voltooid, hebt u een aangepast beleid voor aanmelden en aanmelden met uw merk en identiteit.</span><span class="sxs-lookup"><span data-stu-id="488d2-104">After you complete this article, you will have a sign-up and sign-in custom policy with your brand and appearance.</span></span> <span data-ttu-id="488d2-105">Met Azure Active Directory B2C (Azure AD B2C), u krijgt bijna volledig beheer van de inhoud HTML en CSS Hallo dat toousers heeft ingediend.</span><span class="sxs-lookup"><span data-stu-id="488d2-105">With Azure Active Directory B2C (Azure AD B2C), you get nearly full control of hello HTML and CSS content that's presented toousers.</span></span> <span data-ttu-id="488d2-106">Wanneer u een aangepast beleid gebruikt, configureert u de UI-aanpassing in XML in plaats van het gebruik van besturingselementen in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="488d2-106">When you use a custom policy, you configure UI customization in XML instead of using controls in hello Azure portal.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="488d2-107">Vereisten</span><span class="sxs-lookup"><span data-stu-id="488d2-107">Prerequisites</span></span>

<span data-ttu-id="488d2-108">Voordat u begint, voltooien [aan de slag met aangepaste beleidsregels](active-directory-b2c-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="488d2-108">Before you begin, complete [Getting started with custom policies](active-directory-b2c-get-started-custom.md).</span></span> <span data-ttu-id="488d2-109">U hebt een werkende aangepast beleid voor aanmelden en aanmelden met lokale accounts.</span><span class="sxs-lookup"><span data-stu-id="488d2-109">You should have a working custom policy for sign-up and sign-in with local accounts.</span></span>

## <a name="page-ui-customization"></a><span data-ttu-id="488d2-110">Page UI-aanpassing</span><span class="sxs-lookup"><span data-stu-id="488d2-110">Page UI customization</span></span>

<span data-ttu-id="488d2-111">Hallo pagina UI aanpassing functie gebruikt, kunt u Hallo uiterlijk van het aangepaste beleid aanpassen.</span><span class="sxs-lookup"><span data-stu-id="488d2-111">By using hello page UI customization feature, you can customize hello look and feel of any custom policy.</span></span> <span data-ttu-id="488d2-112">U kunt ook behouden merk en visuele consistentie tussen uw toepassing en de Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="488d2-112">You can also maintain brand and visual consistency between your application and Azure AD B2C.</span></span>

<span data-ttu-id="488d2-113">Dit is hoe het werkt: Azure AD B2C wordt code wordt uitgevoerd in de browser van uw klant en maakt gebruik van een benadering van moderne aangeroepen [Cross-Origin-Resource delen (CORS)](http://www.w3.org/TR/cors/).</span><span class="sxs-lookup"><span data-stu-id="488d2-113">Here's how it works: Azure AD B2C runs code in your customer's browser and uses a modern approach called [Cross-Origin Resource Sharing (CORS)](http://www.w3.org/TR/cors/).</span></span> <span data-ttu-id="488d2-114">Geef eerst een URL in Hallo aangepast beleid met aangepaste HTML-inhoud.</span><span class="sxs-lookup"><span data-stu-id="488d2-114">First, you specify a URL in hello custom policy with customized HTML content.</span></span> <span data-ttu-id="488d2-115">Azure AD B2C-UI-elementen met Hallo HTML-inhoud die is geladen vanaf uw URL en wordt vervolgens weergegeven Hallo pagina toohello klant samenvoegingen.</span><span class="sxs-lookup"><span data-stu-id="488d2-115">Azure AD B2C merges UI elements with hello HTML content that's loaded from your URL and then displays hello page toohello customer.</span></span>

## <a name="create-your-html5-content"></a><span data-ttu-id="488d2-116">Uw HTML5 inhoud maken</span><span class="sxs-lookup"><span data-stu-id="488d2-116">Create your HTML5 content</span></span>

<span data-ttu-id="488d2-117">Maak HTML inhoud met de naam van uw product in Hallo titel.</span><span class="sxs-lookup"><span data-stu-id="488d2-117">Create HTML content with your product's brand name in hello title.</span></span>

1. <span data-ttu-id="488d2-118">Kopieer Hallo HTML-fragment te volgen.</span><span class="sxs-lookup"><span data-stu-id="488d2-118">Copy hello following HTML snippet.</span></span> <span data-ttu-id="488d2-119">Indeling geldig is HTML5 met een leeg element aangeroepen  *\<div-id = 'api'\>\</div\>*  zich binnen Hallo  *\<hoofdtekst\>*  labels.</span><span class="sxs-lookup"><span data-stu-id="488d2-119">It is well-formed HTML5 with an empty element called *\<div id="api"\>\</div\>* located within hello *\<body\>* tags.</span></span> <span data-ttu-id="488d2-120">Dit element geeft aan waar Azure AD B2C inhoud toobe ingevoegd.</span><span class="sxs-lookup"><span data-stu-id="488d2-120">This element indicates where Azure AD B2C content is toobe inserted.</span></span>

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
   ><span data-ttu-id="488d2-121">Uit veiligheidsoverwegingen is Hallo gebruik van JavaScript momenteel geblokkeerd om aan te passen.</span><span class="sxs-lookup"><span data-stu-id="488d2-121">For security reasons, hello use of JavaScript is currently blocked for customization.</span></span>

2. <span data-ttu-id="488d2-122">Hallo gekopieerd codefragment in een teksteditor plakken en sla Hallo-bestand als *aanpassen ui.html*.</span><span class="sxs-lookup"><span data-stu-id="488d2-122">Paste hello copied snippet in a text editor, and then save hello file as *customize-ui.html*.</span></span>

## <a name="create-an-azure-blob-storage-account"></a><span data-ttu-id="488d2-123">Een Azure Blob storage-account maken</span><span class="sxs-lookup"><span data-stu-id="488d2-123">Create an Azure Blob storage account</span></span>

>[!NOTE]
> <span data-ttu-id="488d2-124">In dit artikel gebruiken we Azure Blob storage toohost onze content.</span><span class="sxs-lookup"><span data-stu-id="488d2-124">In this article, we use Azure Blob storage toohost our content.</span></span> <span data-ttu-id="488d2-125">U kunt toohost uw inhoud op een webserver, maar u moet [CORS zijn ingeschakeld op uw webserver](https://enable-cors.org/server.html).</span><span class="sxs-lookup"><span data-stu-id="488d2-125">You can choose toohost your content on a web server, but you must [enable CORS on your web server](https://enable-cors.org/server.html).</span></span>

<span data-ttu-id="488d2-126">toohost deze HTML-inhoud in Blob storage, Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="488d2-126">toohost this HTML content in Blob storage, do hello following:</span></span>

1. <span data-ttu-id="488d2-127">Meld u aan toohello [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="488d2-127">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="488d2-128">Op Hallo **Hub** selecteert u **nieuw** > **opslag** > **opslagaccount**.</span><span class="sxs-lookup"><span data-stu-id="488d2-128">On hello **Hub** menu, select **New** > **Storage** > **Storage account**.</span></span>
3. <span data-ttu-id="488d2-129">Voer een unieke **naam** voor uw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="488d2-129">Enter a unique **Name** for your storage account.</span></span>
4. <span data-ttu-id="488d2-130">**Implementatiemodel** kan blijven **Resource Manager**.</span><span class="sxs-lookup"><span data-stu-id="488d2-130">**Deployment model** can remain **Resource Manager**.</span></span>
5. <span data-ttu-id="488d2-131">Wijziging **soort Account** te**Blob storage**.</span><span class="sxs-lookup"><span data-stu-id="488d2-131">Change **Account Kind** too**Blob storage**.</span></span>
6. <span data-ttu-id="488d2-132">**Prestaties** kan blijven **standaard**.</span><span class="sxs-lookup"><span data-stu-id="488d2-132">**Performance** can remain **Standard**.</span></span>
7. <span data-ttu-id="488d2-133">**Replicatie** kan blijven **RA-GRS**.</span><span class="sxs-lookup"><span data-stu-id="488d2-133">**Replication** can remain **RA-GRS**.</span></span>
8. <span data-ttu-id="488d2-134">**Toegangslaag** kan blijven **Hot**.</span><span class="sxs-lookup"><span data-stu-id="488d2-134">**Access tier** can remain **Hot**.</span></span>
9. <span data-ttu-id="488d2-135">**Versleuteling van de opslagruimte** kan blijven **uitgeschakelde**.</span><span class="sxs-lookup"><span data-stu-id="488d2-135">**Storage service encryption** can remain **Disabled**.</span></span>
10. <span data-ttu-id="488d2-136">Selecteer een **abonnement** voor uw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="488d2-136">Select a **Subscription** for your storage account.</span></span>
11. <span data-ttu-id="488d2-137">Maak een **resourcegroep** of een bestaande set selecteren.</span><span class="sxs-lookup"><span data-stu-id="488d2-137">Create a **Resource group** or select an existing one.</span></span>
12. <span data-ttu-id="488d2-138">Selecteer Hallo **geografische locatie** voor uw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="488d2-138">Select hello **Geographic location** for your storage account.</span></span>
13. <span data-ttu-id="488d2-139">Klik op **maken** toocreate Hallo storage-account.</span><span class="sxs-lookup"><span data-stu-id="488d2-139">Click **Create** toocreate hello storage account.</span></span>  
    <span data-ttu-id="488d2-140">Nadat het Hallo-implementatie is voltooid, Hallo **opslagaccount** blade wordt automatisch geopend.</span><span class="sxs-lookup"><span data-stu-id="488d2-140">After hello deployment is completed, hello **Storage account** blade opens automatically.</span></span>

## <a name="create-a-container"></a><span data-ttu-id="488d2-141">Een container maken</span><span class="sxs-lookup"><span data-stu-id="488d2-141">Create a container</span></span>

<span data-ttu-id="488d2-142">een openbare Blob storage-container toocreate Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="488d2-142">toocreate a public container in Blob storage, do hello following:</span></span>

1. <span data-ttu-id="488d2-143">Klik op Hallo **overzicht** tabblad.</span><span class="sxs-lookup"><span data-stu-id="488d2-143">Click hello **Overview** tab.</span></span>
2. <span data-ttu-id="488d2-144">Klik op **Container**.</span><span class="sxs-lookup"><span data-stu-id="488d2-144">Click **Container**.</span></span>
3. <span data-ttu-id="488d2-145">Voor **naam**, type **$root**.</span><span class="sxs-lookup"><span data-stu-id="488d2-145">For **Name**, type **$root**.</span></span>
4. <span data-ttu-id="488d2-146">Stel **toegangstype** te**Blob**.</span><span class="sxs-lookup"><span data-stu-id="488d2-146">Set **Access type** too**Blob**.</span></span>
5. <span data-ttu-id="488d2-147">Klik op **$root** tooopen Hallo nieuwe container.</span><span class="sxs-lookup"><span data-stu-id="488d2-147">Click **$root** tooopen hello new container.</span></span>
6. <span data-ttu-id="488d2-148">Klik op **Uploaden**.</span><span class="sxs-lookup"><span data-stu-id="488d2-148">Click **Upload**.</span></span>
7. <span data-ttu-id="488d2-149">Klik op het pictogram map Hallo volgende te**selecteert u een bestand**.</span><span class="sxs-lookup"><span data-stu-id="488d2-149">Click hello folder icon next too**Select a file**.</span></span>
8. <span data-ttu-id="488d2-150">Ga te**aanpassen ui.html**, die u eerder in Hallo gemaakt [Page UI-aanpassing](#the-page-ui-customization-feature) sectie.</span><span class="sxs-lookup"><span data-stu-id="488d2-150">Go too**customize-ui.html**, which you created earlier in hello [Page UI customization](#the-page-ui-customization-feature) section.</span></span>
9. <span data-ttu-id="488d2-151">Klik op **Uploaden**.</span><span class="sxs-lookup"><span data-stu-id="488d2-151">Click **Upload**.</span></span>
10. <span data-ttu-id="488d2-152">Selecteer Hallo aanpassen ui.html blob die u hebt geüpload.</span><span class="sxs-lookup"><span data-stu-id="488d2-152">Select hello customize-ui.html blob that you uploaded.</span></span>
11. <span data-ttu-id="488d2-153">Volgende te**URL**, klikt u op **kopie**.</span><span class="sxs-lookup"><span data-stu-id="488d2-153">Next too**URL**, click **Copy**.</span></span>
12. <span data-ttu-id="488d2-154">In een browser, plak de URL van de Hallo gekopieerd en gaat u toohello site.</span><span class="sxs-lookup"><span data-stu-id="488d2-154">In a browser, paste hello copied URL, and go toohello site.</span></span> <span data-ttu-id="488d2-155">Als Hallo site is niet toegankelijk is, controleert u of Hallo container toegangstype te is ingesteld**blob**.</span><span class="sxs-lookup"><span data-stu-id="488d2-155">If hello site is inaccessible, make sure hello container access type is set too**blob**.</span></span>

## <a name="configure-cors"></a><span data-ttu-id="488d2-156">CORS configureren</span><span class="sxs-lookup"><span data-stu-id="488d2-156">Configure CORS</span></span>

<span data-ttu-id="488d2-157">Blob-opslag configureren voor het delen van Cross-Origin-Resource door Hallo volgende te doen:</span><span class="sxs-lookup"><span data-stu-id="488d2-157">Configure Blob storage for Cross-Origin Resource Sharing by doing hello following:</span></span>

>[!NOTE]
><span data-ttu-id="488d2-158">Tootry uit Hallo-functie voor het aanpassen van gebruikersinterface wilt met behulp van onze voorbeeldinhoud HTML en CSS?</span><span class="sxs-lookup"><span data-stu-id="488d2-158">Want tootry out hello UI customization feature by using our sample HTML and CSS content?</span></span> <span data-ttu-id="488d2-159">We bieden [een eenvoudige helper hulpprogramma](active-directory-b2c-reference-ui-customization-helper-tool.md) die uploadt en configureert u onze voorbeelden op uw Blob storage-account.</span><span class="sxs-lookup"><span data-stu-id="488d2-159">We've provided [a simple helper tool](active-directory-b2c-reference-ui-customization-helper-tool.md) that uploads and configures our sample content on your Blob storage account.</span></span> <span data-ttu-id="488d2-160">Als u Hallo-hulpprogramma gebruikt, gaat u verder te[wijzigen van het aangepaste beleid registreren of aanmelden](#modify-your-sign-up-or-sign-in-custom-policy).</span><span class="sxs-lookup"><span data-stu-id="488d2-160">If you use hello tool, skip ahead too[Modify your sign-up or sign-in custom policy](#modify-your-sign-up-or-sign-in-custom-policy).</span></span>

1. <span data-ttu-id="488d2-161">Op Hallo **opslag** blade onder **instellingen**Open **CORS**.</span><span class="sxs-lookup"><span data-stu-id="488d2-161">On hello **Storage** blade, under **Settings**, open **CORS**.</span></span>
2. <span data-ttu-id="488d2-162">Klik op **Add**.</span><span class="sxs-lookup"><span data-stu-id="488d2-162">Click **Add**.</span></span>
3. <span data-ttu-id="488d2-163">Voor **toegestane oorsprongen**, typt u een sterretje (\*).</span><span class="sxs-lookup"><span data-stu-id="488d2-163">For **Allowed origins**, type an asterisk (\*).</span></span>
4. <span data-ttu-id="488d2-164">In Hallo **toegestane termen** vervolgkeuzelijst, selecteer **ophalen** en **opties**.</span><span class="sxs-lookup"><span data-stu-id="488d2-164">In hello **Allowed verbs** drop-down list, select both **GET** and **OPTIONS**.</span></span>
5. <span data-ttu-id="488d2-165">Voor **toegestaan headers**, typt u een sterretje (\*).</span><span class="sxs-lookup"><span data-stu-id="488d2-165">For **Allowed headers**, type an asterisk (\*).</span></span>
6. <span data-ttu-id="488d2-166">Voor **blootgesteld headers**, typt u een sterretje (\*).</span><span class="sxs-lookup"><span data-stu-id="488d2-166">For **Exposed headers**, type an asterisk (\*).</span></span>
7. <span data-ttu-id="488d2-167">Voor **maximale leeftijd (seconden)**, type **200**.</span><span class="sxs-lookup"><span data-stu-id="488d2-167">For **Maximum age (seconds)**, type **200**.</span></span>
8. <span data-ttu-id="488d2-168">Klik op **Add**.</span><span class="sxs-lookup"><span data-stu-id="488d2-168">Click **Add**.</span></span>

## <a name="test-cors"></a><span data-ttu-id="488d2-169">Test CORS</span><span class="sxs-lookup"><span data-stu-id="488d2-169">Test CORS</span></span>

<span data-ttu-id="488d2-170">Valideren dat u klaar bent door Hallo volgende te doen:</span><span class="sxs-lookup"><span data-stu-id="488d2-170">Validate that you're ready by doing hello following:</span></span>

1. <span data-ttu-id="488d2-171">Ga toohello [test cors.org](http://test-cors.org/) website en plakken Hallo-URL in Hallo **externe URL** vak.</span><span class="sxs-lookup"><span data-stu-id="488d2-171">Go toohello [test-cors.org](http://test-cors.org/) website, and then paste hello URL in hello **Remote URL** box.</span></span>
2. <span data-ttu-id="488d2-172">Klik op **aanvraag verzenden**.</span><span class="sxs-lookup"><span data-stu-id="488d2-172">Click **Send Request**.</span></span>  
    <span data-ttu-id="488d2-173">Als u een foutbericht ontvangt, controleert u of uw [CORS-instellingen voor](#configure-cors) juist zijn.</span><span class="sxs-lookup"><span data-stu-id="488d2-173">If you receive an error, make sure that your [CORS settings](#configure-cors) are correct.</span></span> <span data-ttu-id="488d2-174">Of u kunt mogelijk ook tooclear uw browser-cache een browsersessie van privé-openen door op Ctrl + Shift + P te drukken.</span><span class="sxs-lookup"><span data-stu-id="488d2-174">You might also need tooclear your browser cache or open an in-private browsing session by pressing Ctrl+Shift+P.</span></span>

## <a name="modify-your-sign-up-or-sign-in-custom-policy"></a><span data-ttu-id="488d2-175">Wijzigen van het aangepaste beleid registreren of aanmelden</span><span class="sxs-lookup"><span data-stu-id="488d2-175">Modify your sign-up or sign-in custom policy</span></span>

<span data-ttu-id="488d2-176">Onder Hallo op het hoogste niveau  *\<TrustFrameworkPolicy\>*  labels, zult u  *\<BuildingBlocks\>*  label.</span><span class="sxs-lookup"><span data-stu-id="488d2-176">Under hello top-level *\<TrustFrameworkPolicy\>* tag, you should find *\<BuildingBlocks\>* tag.</span></span> <span data-ttu-id="488d2-177">Binnen Hallo  *\<BuildingBlocks\>*  tags, Voeg een  *\<ContentDefinitions\>*  code door te kopiëren Hallo voorbeeld te volgen.</span><span class="sxs-lookup"><span data-stu-id="488d2-177">Within hello *\<BuildingBlocks\>* tags, add a *\<ContentDefinitions\>* tag by copying hello following example.</span></span> <span data-ttu-id="488d2-178">Vervang *your_storage_account* met Hallo-naam van uw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="488d2-178">Replace *your_storage_account* with hello name of your storage account.</span></span>

  ```xml
  <BuildingBlocks>
    <ContentDefinitions>
      <ContentDefinition Id="api.idpselections">
        <LoadUri>https://{your_storage_account}.blob.core.windows.net/customize-ui.html</LoadUri>
      </ContentDefinition>
    </ContentDefinitions>
  </BuildingBlocks>
  ```

## <a name="upload-your-updated-custom-policy"></a><span data-ttu-id="488d2-179">Upload uw bijgewerkte aangepast beleid</span><span class="sxs-lookup"><span data-stu-id="488d2-179">Upload your updated custom policy</span></span>

1. <span data-ttu-id="488d2-180">In Hallo [Azure-portal](https://portal.azure.com), [schakelen naar de context van uw Azure AD B2C-tenant hello](active-directory-b2c-navigate-to-b2c-context.md), en open vervolgens Hallo **Azure AD B2C** blade.</span><span class="sxs-lookup"><span data-stu-id="488d2-180">In hello [Azure portal](https://portal.azure.com), [switch into hello context of your Azure AD B2C tenant](active-directory-b2c-navigate-to-b2c-context.md), and then open hello **Azure AD B2C** blade.</span></span>
2. <span data-ttu-id="488d2-181">Klik op **alle beleidsregels**.</span><span class="sxs-lookup"><span data-stu-id="488d2-181">Click **All Policies**.</span></span>
3. <span data-ttu-id="488d2-182">Klik op **uploaden beleid**.</span><span class="sxs-lookup"><span data-stu-id="488d2-182">Click **Upload Policy**.</span></span>
4. <span data-ttu-id="488d2-183">Uploaden `SignUpOrSignin.xml` Hello  *\<ContentDefinitions\>*  code die u eerder hebt toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="488d2-183">Upload `SignUpOrSignin.xml` with hello *\<ContentDefinitions\>* tag that you added previously.</span></span>

## <a name="test-hello-custom-policy-by-using-run-now"></a><span data-ttu-id="488d2-184">Hallo aangepast beleid testen met behulp van **nu uitvoeren**</span><span class="sxs-lookup"><span data-stu-id="488d2-184">Test hello custom policy by using **Run now**</span></span>

1. <span data-ttu-id="488d2-185">Op Hallo **Azure AD B2C** blade te gaan**alle beleidsregels**.</span><span class="sxs-lookup"><span data-stu-id="488d2-185">On hello **Azure AD B2C** blade, go too**All polices**.</span></span>
2. <span data-ttu-id="488d2-186">Selecteer Hallo aangepaste beleid dat u hebt geüpload en klikt u op Hallo **nu uitvoeren** knop.</span><span class="sxs-lookup"><span data-stu-id="488d2-186">Select hello custom policy that you uploaded, and click hello **Run now** button.</span></span>
3. <span data-ttu-id="488d2-187">U moet kunnen toosign up met behulp van een e-mailadres.</span><span class="sxs-lookup"><span data-stu-id="488d2-187">You should be able toosign up by using an email address.</span></span>

## <a name="reference"></a><span data-ttu-id="488d2-188">Naslaginformatie</span><span class="sxs-lookup"><span data-stu-id="488d2-188">Reference</span></span>

<span data-ttu-id="488d2-189">Voor de UI-aanpassing Hier vindt u voorbeeldsjablonen:</span><span class="sxs-lookup"><span data-stu-id="488d2-189">You can find sample templates for UI customization here:</span></span>

```
git clone https://github.com/azureadquickstarts/b2c-azureblobstorage-client
```

<span data-ttu-id="488d2-190">Hallo sample_templates/wingtip map bevat Hallo volgende HTML-bestanden:</span><span class="sxs-lookup"><span data-stu-id="488d2-190">hello sample_templates/wingtip folder contains hello following HTML files:</span></span>

| <span data-ttu-id="488d2-191">HTML5-sjabloon</span><span class="sxs-lookup"><span data-stu-id="488d2-191">HTML5 template</span></span> | <span data-ttu-id="488d2-192">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="488d2-192">Description</span></span> |
|----------------|-------------|
| <span data-ttu-id="488d2-193">*phonefactor.HTML*</span><span class="sxs-lookup"><span data-stu-id="488d2-193">*phonefactor.html*</span></span> | <span data-ttu-id="488d2-194">Dit bestand als sjabloon gebruiken voor een multi-factor authentication-pagina.</span><span class="sxs-lookup"><span data-stu-id="488d2-194">Use this file as a template for a multi-factor authentication page.</span></span> |
| <span data-ttu-id="488d2-195">*ResetPassword.HTML*</span><span class="sxs-lookup"><span data-stu-id="488d2-195">*resetpassword.html*</span></span> | <span data-ttu-id="488d2-196">Dit bestand te gebruiken als een sjabloon voor een wachtwoordpagina vergeten.</span><span class="sxs-lookup"><span data-stu-id="488d2-196">Use this file as a template for a forgot password page.</span></span> |
| <span data-ttu-id="488d2-197">*selfasserted.HTML*</span><span class="sxs-lookup"><span data-stu-id="488d2-197">*selfasserted.html*</span></span> | <span data-ttu-id="488d2-198">Dit bestand als een sjabloon voor een aanmeldingspagina sociale account, de aanmeldingspagina van een lokaal account of een aanmeldingspagina lokale account gebruiken.</span><span class="sxs-lookup"><span data-stu-id="488d2-198">Use this file as a template for a social account sign-up page, a local account sign-up page, or a local account sign-in page.</span></span> |
| <span data-ttu-id="488d2-199">*Unified.HTML*</span><span class="sxs-lookup"><span data-stu-id="488d2-199">*unified.html*</span></span> | <span data-ttu-id="488d2-200">Dit bestand als sjabloon gebruiken voor een uniforme registreren of aanmelden pagina.</span><span class="sxs-lookup"><span data-stu-id="488d2-200">Use this file as a template for a unified sign-up or sign-in page.</span></span> |
| <span data-ttu-id="488d2-201">*updateprofile.HTML*</span><span class="sxs-lookup"><span data-stu-id="488d2-201">*updateprofile.html*</span></span> | <span data-ttu-id="488d2-202">Dit bestand als een sjabloon voor een update-profielpagina gebruiken.</span><span class="sxs-lookup"><span data-stu-id="488d2-202">Use this file as a template for a profile update page.</span></span> |

<span data-ttu-id="488d2-203">In Hallo [, wijzigt u de sectie registreren of aanmelden aangepast beleid](#modify-your-sign-up-or-sign-in-custom-policy), u hebt geconfigureerd Hallo inhoud definitie voor `api.idpselections`.</span><span class="sxs-lookup"><span data-stu-id="488d2-203">In hello [Modify your sign-up or sign-in custom policy section](#modify-your-sign-up-or-sign-in-custom-policy), you configured hello content definition for `api.idpselections`.</span></span> <span data-ttu-id="488d2-204">Hallo volledige set van inhoud definitie-id's die worden herkend door hello Azure AD B2C identiteit ervaring framework en de bijbehorende beschrijvingen zijn in de volgende tabel Hallo:</span><span class="sxs-lookup"><span data-stu-id="488d2-204">hello full set of content definition IDs that are recognized by hello Azure AD B2C identity experience framework and their descriptions are in hello following table:</span></span>

| <span data-ttu-id="488d2-205">De definitie van de inhoud-ID</span><span class="sxs-lookup"><span data-stu-id="488d2-205">Content definition ID</span></span> | <span data-ttu-id="488d2-206">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="488d2-206">Description</span></span> | 
|-----------------------|-------------|
| <span data-ttu-id="488d2-207">*API.Error*</span><span class="sxs-lookup"><span data-stu-id="488d2-207">*api.error*</span></span> | <span data-ttu-id="488d2-208">**Foutpagina**.</span><span class="sxs-lookup"><span data-stu-id="488d2-208">**Error page**.</span></span> <span data-ttu-id="488d2-209">Deze pagina wordt weergegeven wanneer een uitzondering of een fout is opgetreden.</span><span class="sxs-lookup"><span data-stu-id="488d2-209">This page is displayed when an exception or an error is encountered.</span></span> |
| <span data-ttu-id="488d2-210">*API.idpselections*</span><span class="sxs-lookup"><span data-stu-id="488d2-210">*api.idpselections*</span></span> | <span data-ttu-id="488d2-211">**Id-provider selectiepagina**.</span><span class="sxs-lookup"><span data-stu-id="488d2-211">**Identity provider selection page**.</span></span> <span data-ttu-id="488d2-212">Deze pagina bevat een lijst met de id-providers die gebruiker Hallo uit tijdens het aanmelden kiezen kunnen.</span><span class="sxs-lookup"><span data-stu-id="488d2-212">This page contains a list of identity providers that hello user can choose from during sign-in.</span></span> <span data-ttu-id="488d2-213">Deze opties zijn enterprise identiteitsproviders, sociale id-providers zoals Facebook en Google + of lokale accounts.</span><span class="sxs-lookup"><span data-stu-id="488d2-213">These options are either enterprise identity providers, social identity providers such as Facebook and Google+, or local accounts.</span></span> |
| <span data-ttu-id="488d2-214">*API.idpselections.Signup*</span><span class="sxs-lookup"><span data-stu-id="488d2-214">*api.idpselections.signup*</span></span> | <span data-ttu-id="488d2-215">**Selectie van de id-provider voor registratie**.</span><span class="sxs-lookup"><span data-stu-id="488d2-215">**Identity provider selection for sign-up**.</span></span> <span data-ttu-id="488d2-216">Deze pagina bevat een lijst met providers die gebruiker Hallo uit tijdens de registratie kiezen kunnen van de identiteit.</span><span class="sxs-lookup"><span data-stu-id="488d2-216">This page contains a list of identity providers that hello user can choose from during sign-up.</span></span> <span data-ttu-id="488d2-217">Deze opties zijn enterprise identiteitsproviders, sociale id-providers zoals Facebook en Google + of lokale accounts.</span><span class="sxs-lookup"><span data-stu-id="488d2-217">These options are either enterprise identity providers, social identity providers such as Facebook and Google+, or local accounts.</span></span> |
| <span data-ttu-id="488d2-218">*API.localaccountpasswordreset*</span><span class="sxs-lookup"><span data-stu-id="488d2-218">*api.localaccountpasswordreset*</span></span> | <span data-ttu-id="488d2-219">**Wachtwoordpagina vergeten**.</span><span class="sxs-lookup"><span data-stu-id="488d2-219">**Forgot password page**.</span></span> <span data-ttu-id="488d2-220">Deze pagina bevat een formulier die gebruiker Hallo tooinitiate het wachtwoord moet voltooien.</span><span class="sxs-lookup"><span data-stu-id="488d2-220">This page contains a form that hello user must complete tooinitiate a password reset.</span></span>  |
| <span data-ttu-id="488d2-221">*API.localaccountsignin*</span><span class="sxs-lookup"><span data-stu-id="488d2-221">*api.localaccountsignin*</span></span> | <span data-ttu-id="488d2-222">**Aanmeldingspagina voor lokaal account**.</span><span class="sxs-lookup"><span data-stu-id="488d2-222">**Local account sign-in page**.</span></span> <span data-ttu-id="488d2-223">Deze pagina bevat een formulier-in voor het aanmelden met een lokaal account dat is gebaseerd op een e-mailadres of een gebruikersnaam.</span><span class="sxs-lookup"><span data-stu-id="488d2-223">This page contains a sign-in form for signing in with a local account that is based on an email address or a user name.</span></span> <span data-ttu-id="488d2-224">Hallo formulier kan een tekstinvoervak en wachtwoordvak vermelding bevatten.</span><span class="sxs-lookup"><span data-stu-id="488d2-224">hello form can contain a text input box and password entry box.</span></span> |
| <span data-ttu-id="488d2-225">*API.localaccountsignup*</span><span class="sxs-lookup"><span data-stu-id="488d2-225">*api.localaccountsignup*</span></span> | <span data-ttu-id="488d2-226">**Lokaal account aanmeldingspagina**.</span><span class="sxs-lookup"><span data-stu-id="488d2-226">**Local account sign-up page**.</span></span> <span data-ttu-id="488d2-227">Deze pagina bevat een aanmeldingsformulier hebt ingevuld voor het aanmelden voor een lokaal account dat is gebaseerd op een e-mailadres of een gebruikersnaam.</span><span class="sxs-lookup"><span data-stu-id="488d2-227">This page contains a sign-up form for signing up for a local account that is based on an email address or a user name.</span></span> <span data-ttu-id="488d2-228">Hallo formulier kan verschillende invoer besturingselementen bevatten, zoals een tekstinvoervak vak een wachtwoord, een keuzerondje, één vervolgkeuzelijsten en meervoudige selectie selectievakjes.</span><span class="sxs-lookup"><span data-stu-id="488d2-228">hello form can contain various input controls, such as a text input box, a password entry box, a radio button, single-select drop-down boxes, and multi-select check boxes.</span></span> |
| <span data-ttu-id="488d2-229">*API.phonefactor*</span><span class="sxs-lookup"><span data-stu-id="488d2-229">*api.phonefactor*</span></span> | <span data-ttu-id="488d2-230">**Multi-factor authentication-pagina**.</span><span class="sxs-lookup"><span data-stu-id="488d2-230">**Multi-factor authentication page**.</span></span> <span data-ttu-id="488d2-231">Op deze pagina, kunnen gebruikers hun telefoonnummers (met behulp van tekst of stem) controleren tijdens het registreren of aanmelden.</span><span class="sxs-lookup"><span data-stu-id="488d2-231">On this page, users can verify their phone numbers (by using text or voice) during sign-up or sign-in.</span></span> |
| <span data-ttu-id="488d2-232">*API.selfasserted*</span><span class="sxs-lookup"><span data-stu-id="488d2-232">*api.selfasserted*</span></span> | <span data-ttu-id="488d2-233">**De aanmeldpagina sociale account**.</span><span class="sxs-lookup"><span data-stu-id="488d2-233">**Social account sign-up page**.</span></span> <span data-ttu-id="488d2-234">Deze pagina bevat een aanmeldingsformulier hebt ingevuld die gebruikers moeten worden voltooid wanneer ze zich registreren met behulp van een bestaand account van een identiteitsprovider van sociale zoals Facebook of Google +.</span><span class="sxs-lookup"><span data-stu-id="488d2-234">This page contains a sign-up form that users must complete when they sign up by using an existing account from a social identity provider such as Facebook or Google+.</span></span> <span data-ttu-id="488d2-235">Deze pagina is vergelijkbaar toohello voorafgaand aan de aanmeldingspagina sociale account, behalve Hallo wachtwoord invoervelden.</span><span class="sxs-lookup"><span data-stu-id="488d2-235">This page is similar toohello preceding social account sign-up page, except for hello password entry fields.</span></span> |
| <span data-ttu-id="488d2-236">*API.selfasserted.profileupdate*</span><span class="sxs-lookup"><span data-stu-id="488d2-236">*api.selfasserted.profileupdate*</span></span> | <span data-ttu-id="488d2-237">**Update profielpagina**.</span><span class="sxs-lookup"><span data-stu-id="488d2-237">**Profile update page**.</span></span> <span data-ttu-id="488d2-238">Deze pagina bevat een formulier dat gebruikers tooupdate hun profiel gebruiken kunnen.</span><span class="sxs-lookup"><span data-stu-id="488d2-238">This page contains a form that users can use tooupdate their profile.</span></span> <span data-ttu-id="488d2-239">Deze pagina is vergelijkbaar toohello sociale account aanmeldingspagina, met uitzondering van invoervelden Hallo-wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="488d2-239">This page is similar toohello social account sign-up page, except for hello password entry fields.</span></span> |
| <span data-ttu-id="488d2-240">*API.signuporsignin*</span><span class="sxs-lookup"><span data-stu-id="488d2-240">*api.signuporsignin*</span></span> | <span data-ttu-id="488d2-241">**Unified registreren of aanmelden pagina**.</span><span class="sxs-lookup"><span data-stu-id="488d2-241">**Unified sign-up or sign-in page**.</span></span> <span data-ttu-id="488d2-242">Deze pagina verwerkt beide Hallo zich kunnen registreren en aanmelden van gebruikers, die enterprise identiteitsproviders, sociale id-providers zoals Facebook of Google + of lokale accounts kunnen gebruiken.</span><span class="sxs-lookup"><span data-stu-id="488d2-242">This page handles both hello sign-up and sign-in of users, who can use enterprise identity providers, social identity providers such as Facebook or Google+, or local accounts.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="488d2-243">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="488d2-243">Next steps</span></span>

<span data-ttu-id="488d2-244">Zie voor meer informatie over de UI-elementen die kunnen worden aangepast, [Naslaggids voor aanpassing van de gebruikersinterface voor ingebouwde beleid](active-directory-b2c-reference-ui-customization.md).</span><span class="sxs-lookup"><span data-stu-id="488d2-244">For additional information about UI elements that can be customized, see [reference guide for UI customization for built-in policies](active-directory-b2c-reference-ui-customization.md).</span></span>
