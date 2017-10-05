---
title: (afgeschaft) Veelgestelde vragen over - publiceren en gebruiken van Machine Learning-apps in Azure Marketplace | Microsoft Docs
description: (afgeschaft) Veelgestelde vragen over Machine Learning-apps publiceren in Azure Marketplace
services: machine-learning
documentationcenter: 
author: bharaths
manager: jhubbard
editor: cgronlun
ms.assetid: 26b3a1e7-8b9a-4004-98bc-17456d4c25e8
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: bharaths
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: TRUE
ms.openlocfilehash: a4631dfeb2f817b3a3c612a8f6af48398e4f2ab9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="deprecated-publishing-and-using-machine-learning-apps-in-the-azure-marketplace-faq"></a><span data-ttu-id="55296-103">(afgeschaft) Publiceren en gebruiken van Machine Learning-apps in Azure Marketplace: veelgestelde vragen</span><span class="sxs-lookup"><span data-stu-id="55296-103">(deprecated) Publishing and using Machine Learning apps in the Azure Marketplace: FAQ</span></span>

> [!NOTE]
> <span data-ttu-id="55296-104">DataMarket en Data Services worden gesteld en bestaande abonnementen wordt buiten gebruik worden gesteld en geannuleerd vanaf 3/31/2017.</span><span class="sxs-lookup"><span data-stu-id="55296-104">DataMarket and Data Services are being retired, and existing subscriptions will be retired and cancelled starting 3/31/2017.</span></span> <span data-ttu-id="55296-105">Als gevolg hiervan wordt in dit artikel afgeschaft.</span><span class="sxs-lookup"><span data-stu-id="55296-105">As a result, this article is being deprecated.</span></span> 
> 
> <span data-ttu-id="55296-106">Als alternatief kunt u uw Machine Learning-experimenten te publiceren de [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com/) ten behoeve van de community van de wetenschappelijke gegevens.</span><span class="sxs-lookup"><span data-stu-id="55296-106">As an alternative, you can publish your Machine Learning experiments to the [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com/) for the benefit of the data science community.</span></span> <span data-ttu-id="55296-107">Zie voor meer informatie [Share en het detecteren van bronnen in de Cortana Intelligence Gallery](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-gallery-how-to-use-contribute-publish).</span><span class="sxs-lookup"><span data-stu-id="55296-107">For more information, see [Share and discover resources in the Cortana Intelligence Gallery](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-gallery-how-to-use-contribute-publish).</span></span>


## <a name="questions-about-consuming-from-marketplace"></a><span data-ttu-id="55296-108">Vragen over het gebruiken van Marketplace</span><span class="sxs-lookup"><span data-stu-id="55296-108">Questions about consuming from Marketplace</span></span>
<span data-ttu-id="55296-109">**1. Waarom krijg ik het volgende foutbericht weergegeven wanneer ik invoer hebt ingevoerd voor de webservice:**</span><span class="sxs-lookup"><span data-stu-id="55296-109">**1. Why do I get the following error message after I enter input for the web service:**</span></span>

<span data-ttu-id="55296-110">**De aanvraag heeft een back-end time-out- of back-end-fout. Het team onderzoekt het probleem. We kunnen onze excuses voor het ongemak. (500)**</span><span class="sxs-lookup"><span data-stu-id="55296-110">**The request resulted in a back-end time out or back-end error. The team is investigating the issue. We are sorry for the inconvenience. (500)**</span></span>

<span data-ttu-id="55296-111">De parameters mogelijk niet overeen met de vereiste indeling voor de specifieke webservice.</span><span class="sxs-lookup"><span data-stu-id="55296-111">Your input parameter(s) may not conform to the required format for the specific web service.</span></span> <span data-ttu-id="55296-112">Raadpleeg de bijbehorende documentatie-koppeling om de juiste notatie voor de invoerparameters en de beperkingen van deze webservice te vinden.</span><span class="sxs-lookup"><span data-stu-id="55296-112">Please refer to the corresponding documentation link to find the correct format for input parameters and the limitations of this web service.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="55296-113">**2. Als het kopiëren van de API-koppeling voor de webservice die op de pagina 'Verkennen deze gegevensset' en plak deze in een ander browservenster wat referenties moet ik gebruiken voor toegang tot de resultaten en hoe kan ik ze zien?**</span><span class="sxs-lookup"><span data-stu-id="55296-113">**2. If I copy the API link for the web service that I see on the "Explore this dataset" page and paste it into another browser window, what credentials should I use to access the results, and how do I see them?**</span></span>

<span data-ttu-id="55296-114">U moet uw Marketplace-account gebruiken als de gebruikersnaam en de primaire toegangssleutel als het wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="55296-114">You should use your Marketplace account as the username and the primary account key as the password.</span></span> <span data-ttu-id="55296-115">Primaire sleutel vindt u op de **verkennen van deze gegevensset** pagina onder de beschrijving van de webservice (Klik op de **weergeven** knop).</span><span class="sxs-lookup"><span data-stu-id="55296-115">The primary account key can be found on the **Explore this dataset** page under the description of the web service (click the **show** button).</span></span> <span data-ttu-id="55296-116">Het resultaat wordt mogelijk weergegeven in de browser of mogelijk worden gedownload, afhankelijk van welke browser die u gebruikt.</span><span class="sxs-lookup"><span data-stu-id="55296-116">The result may display in the browser or it may be available to  download, depending on which browser you are using.</span></span>

<span data-ttu-id="55296-117">**3. Waarom krijg ik het volgende foutbericht weergegeven wanneer ik de invoer hebt ingevoerd voor de webservice op de pagina 'Verkennen deze gegevensset':**</span><span class="sxs-lookup"><span data-stu-id="55296-117">**3. Why do I get the following error message after I enter the input for the web service on the "Explore this dataset" page:**</span></span> 

<span data-ttu-id="55296-118">**Een onverwachte fout opgetreden tijdens het verwerken van uw aanvraag. Probeer het opnieuw.**</span><span class="sxs-lookup"><span data-stu-id="55296-118">**An unexpected error occurred while processing your request. Please try again.**</span></span>

<span data-ttu-id="55296-119">Een of meer invoerparameters van uw web-service kunnen hebben overschrijdt de maximale lengte wanneer de web-service op marketplace worden verbruikt **verkennen van deze gegevensset** pagina.</span><span class="sxs-lookup"><span data-stu-id="55296-119">One or more input parameters of your web service may have exceeded the length limit when consuming the web service on the marketplace **Explore this dataset** page.</span></span> <span data-ttu-id="55296-120">De services kunnen worden aangeroepen met een meer invoerlengte via HTTP POST-methoden.</span><span class="sxs-lookup"><span data-stu-id="55296-120">The services can be called with a longer input length by using HTTP POST methods.</span></span> <span data-ttu-id="55296-121">Zie voor voorbeelden [steekproef oplossingen met R op Machine Learning en gepubliceerd naar Marketplace](machine-learning-r-csharp-web-service-examples.md).</span><span class="sxs-lookup"><span data-stu-id="55296-121">For examples, see [Sample solutions using R on Machine Learning and published to Marketplace](machine-learning-r-csharp-web-service-examples.md).</span></span>

<span data-ttu-id="55296-122">**4. Waarom kan ik niet zien in de 'API EXPLORER' tabblad int het archief in de klassieke Azure Portal niets?**</span><span class="sxs-lookup"><span data-stu-id="55296-122">**4. Why do I not see anything in the "API EXPLORER" tab int the Store in the Azure Classic Portal?**</span></span> 

<span data-ttu-id="55296-123">Dit is een bekend probleem met de klassieke Azure Portal Marketplace.</span><span class="sxs-lookup"><span data-stu-id="55296-123">This is a known issue with the Azure Classic Portal Marketplace.</span></span> <span data-ttu-id="55296-124">Dit probleem oplossen door werkt het team.</span><span class="sxs-lookup"><span data-stu-id="55296-124">The team is working to resolve this issue.</span></span> 

## <a name="questions-about-publishing-from-azure-machine-learning-on-marketplace"></a><span data-ttu-id="55296-125">Vragen over het publiceren van Azure Machine Learning op Marketplace</span><span class="sxs-lookup"><span data-stu-id="55296-125">Questions about publishing from Azure Machine Learning on Marketplace</span></span>
<span data-ttu-id="55296-126">**1. Waarom zijn mijn transacties logo's of afbeeldingen niet vernieuwen voor Mijn webservice?**</span><span class="sxs-lookup"><span data-stu-id="55296-126">**1. Why are my transactions of logos or images not refreshing for my web service?**</span></span> 

<span data-ttu-id="55296-127">Logo's en afbeeldingen in cache zijn opgeslagen in de portal voor publiceren en het duurt maximaal 10 dagen voor de nieuwe logo of de afbeelding om bij te werken op de portal.</span><span class="sxs-lookup"><span data-stu-id="55296-127">Logos and images are cached in the publishing portal, and it may take up to 10 days for the new logo or image to update on the portal.</span></span>

<span data-ttu-id="55296-128">**2. Waarom is het tabblad 'Details' van Mijn webservice op Marketplace een foutbericht weergegeven?**</span><span class="sxs-lookup"><span data-stu-id="55296-128">**2. Why is the “Detail" tab of my web service on Marketplace showing an error message?**</span></span>

<span data-ttu-id="55296-129">Er is een bekend probleem in de Marketplace bij het verbinden met Azure Machine Learning voor service-informatie.</span><span class="sxs-lookup"><span data-stu-id="55296-129">There is a known Marketplace issue when connecting to Azure Machine Learning for service details.</span></span> <span data-ttu-id="55296-130">Dit probleem oplossen door werkt het team.</span><span class="sxs-lookup"><span data-stu-id="55296-130">The team is working to resolve this issue.</span></span>

<span data-ttu-id="55296-131">**3. Waarom de voorbeeldcode R in de Azure Machine Learning-webservices werkt niet voor het verbruik van de web-services Marketplace?**</span><span class="sxs-lookup"><span data-stu-id="55296-131">**3. Why does the R sample code in the Azure Machine Learning web services not work for consuming the web services in Marketplace?**</span></span>

<span data-ttu-id="55296-132">De verificatiesystemen zijn verschillend bij het verbinden met Azure Machine Learning-webservices rechtstreeks vergeleken met de verbinding te maken met deze webservices via de Marketplace.</span><span class="sxs-lookup"><span data-stu-id="55296-132">The authentication systems are different when connecting to Azure Machine Learning web services directly compared to connecting to these web services through the Marketplace.</span></span> <span data-ttu-id="55296-133">De services in Marketplace OData-services zijn en ze kunnen worden aangeroepen met de methoden GET of POST.</span><span class="sxs-lookup"><span data-stu-id="55296-133">The services in Marketplace are OData services, and they can be called with GET or POST methods.</span></span> 

<span data-ttu-id="55296-134">**4. Waarom zijn de koppelingen voor ondersteuning van mijn web-service biedt voor sommige mijn aanbiedingen niet correct bijgewerkt?**</span><span class="sxs-lookup"><span data-stu-id="55296-134">**4. Why are the support links of my web service offers not updating correctly for some of my offers?**</span></span>

<span data-ttu-id="55296-135">De koppelingen ondersteuning zijn globaal per uitgever, niet per aanbieding.</span><span class="sxs-lookup"><span data-stu-id="55296-135">The support links are global per publisher, not per offer.</span></span> 

<span data-ttu-id="55296-136">**5. Hoe kan ik een webservice met invoer batchmodus publiceren in de Marketplace?**</span><span class="sxs-lookup"><span data-stu-id="55296-136">**5. How do I publish a web service with batch input mode in Marketplace?**</span></span>

<span data-ttu-id="55296-137">De invoermodus batch wordt momenteel niet ondersteund in de Marketplace-webservices.</span><span class="sxs-lookup"><span data-stu-id="55296-137">The batch input mode is currently not supported in Marketplace web services.</span></span>

<span data-ttu-id="55296-138">**6. Wie moet ik contact opnemen voor hulp als ik vragen hebt over een uitgever is of als er problemen tijdens de publicatie?**</span><span class="sxs-lookup"><span data-stu-id="55296-138">**6. Who should I contact to get help if I have questions about becoming a data publisher, or if I have issues during publishing?**</span></span>

<span data-ttu-id="55296-139">Neem contact op met het team van Azure Marketplace via < mailto:datamarketbd@microsoft.com > voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="55296-139">Please contact the Azure Marketplace team at <mailto:datamarketbd@microsoft.com> for more information.</span></span>

