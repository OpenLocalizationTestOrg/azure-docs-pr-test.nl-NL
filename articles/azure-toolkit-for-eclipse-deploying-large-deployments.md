---
title: Implementatie van grote implementaties
description: Informatie over het implementeren van grote implementaties met de Azure-Toolkit voor Eclipse.
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 5e18bace-5df0-4af8-ad86-6151ea8bd823
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: e12e379e2b6727653e2377b1760c3745596a1e9c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="deploying-large-deployments"></a><span data-ttu-id="89190-103">Implementatie van grote implementaties</span><span class="sxs-lookup"><span data-stu-id="89190-103">Deploying Large Deployments</span></span>
<span data-ttu-id="89190-104">Als uw implementatie te groot om te worden opgenomen in de standaard approot-map is, kunt u een resource voor lokale opslag gebruiken als de hoofdmap van de implementatie voor uw JDK en toepassingsservers.</span><span class="sxs-lookup"><span data-stu-id="89190-104">If your deployment is too large to be contained in the default approot folder, you can use a local storage resource as the deployment root folder for your JDK and application server.</span></span>

## <a name="to-use-a-local-storage-resource-as-the-deployment-root-folder-for-large-deployments"></a><span data-ttu-id="89190-105">De bron van een lokale opslag gebruiken als de hoofdmap van de implementatie voor grote implementaties</span><span class="sxs-lookup"><span data-stu-id="89190-105">To use a local storage resource as the deployment root folder for large deployments</span></span>
1. <span data-ttu-id="89190-106">Maak een nieuwe resource van de lokale opslag.</span><span class="sxs-lookup"><span data-stu-id="89190-106">Create a new local storage resource.</span></span> <span data-ttu-id="89190-107">De naam van de resource niet van belang.</span><span class="sxs-lookup"><span data-stu-id="89190-107">The name of the resource does not matter.</span></span> <span data-ttu-id="89190-108">Storage-resources zijn gedefinieerd op het rolniveau van de.</span><span class="sxs-lookup"><span data-stu-id="89190-108">Storage resources are defined at the role level.</span></span> <span data-ttu-id="89190-109">De snelste manier toegang krijgen tot het configuratiedialoogvenster van de lokale opslag, van waaruit u een nieuwe resource van de lokale opslag kunt maken is met behulp van de volgende stappen uit: met de rechtermuisknop op de rol in de **Projectverkenner** weergave (Vouw uw Azure-project knooppunt als de functie niet wordt weergegeven), klikt u op **Azure**, en klik vervolgens op **lokale opslag**.</span><span class="sxs-lookup"><span data-stu-id="89190-109">The quickest way to access the local storage configuration dialog, from which you could create a new local storage resource, is by using the following steps: Right-click the role in the **Project Explorer** view (expand your Azure project node if you don't see the role), click **Azure**, and then click **Local Storage**.</span></span> <span data-ttu-id="89190-110">Binnen de **lokale opslag** dialoogvenster, klikt u op **toevoegen** voor het maken van een nieuwe resource van de lokale opslag.</span><span class="sxs-lookup"><span data-stu-id="89190-110">Within the **Local Storage** dialog, click **Add** to create a new local storage resource.</span></span>

2. <span data-ttu-id="89190-111">Stel de gewenste grootte op ten minste 2048 MB (iets minder kan hetzelfde bestand grootte problemen veroorzaken zoals u zou optreden in de approot).</span><span class="sxs-lookup"><span data-stu-id="89190-111">Set the desired size to at least 2048 MB (anything less may cause the same file size problems as you would encounter in the approot).</span></span>

3. <span data-ttu-id="89190-112">Zorg ervoor dat **opschonen van de inhoud wanneer de rolinstantie gerecycled wordt** is ingeschakeld; Dit helpt voorkomen dat opstartlogica van de implementatie worden uitgevoerd in conflicten met vooraf bestaande bestanden in de bron wanneer het rolexemplaar gerecycled.</span><span class="sxs-lookup"><span data-stu-id="89190-112">Ensure that **Clean the contents when the role instance is recycled** is checked; this will help prevent the deployment's startup logic from running into conflicts with pre-existing files in the resource when the role instance is recycled.</span></span>

4. <span data-ttu-id="89190-113">Zorg ervoor dat de **omgevingsvariabele pad van de resource opslaan na implementatie** waarde is ingesteld op de tekenreeks **DEPLOYROOT**.</span><span class="sxs-lookup"><span data-stu-id="89190-113">Ensure that the **Environment variable storing the resource's directory path after deployment** value is set to the string **DEPLOYROOT**.</span></span> <span data-ttu-id="89190-114">Uw lokale opslag resource dialoogvenster ziet er ongeveer als volgt.</span><span class="sxs-lookup"><span data-stu-id="89190-114">Your local storage resource dialog will look similar to the following.</span></span>

   ![][ic667943]

<span data-ttu-id="89190-115">U kunt ook als u **DEPLOYROOT** als de *naam* van uw lokale resource en voer de automatisch gegenereerde naam van omgevingsvariabele wijzigingen (die wordt ingesteld op **DEPLOYROOT_ PAD** in dat geval), die voor uw toepassing ook zou werken.</span><span class="sxs-lookup"><span data-stu-id="89190-115">Alternatively, if you use **DEPLOYROOT** as the *name* of your local resource and you do not change the automatically-generated environment variable name (which will be set to **DEPLOYROOT_PATH** in that case), that would work for your application as well.</span></span>

<span data-ttu-id="89190-116">Als u meer informatie over het maken van een resource voor lokale opslag kan worden gevonden op [eigenschappen van lokale opslag][Local storage properties].</span><span class="sxs-lookup"><span data-stu-id="89190-116">Additional information about creating a local storage resource can be found at [Local storage properties][Local storage properties].</span></span>

## <a name="see-also"></a><span data-ttu-id="89190-117">Zie ook</span><span class="sxs-lookup"><span data-stu-id="89190-117">See Also</span></span>
<span data-ttu-id="89190-118">[Azure Toolkit voor Eclipse][Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="89190-118">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span></span>

<span data-ttu-id="89190-119">[Maken van een Hallo wereld-toepassing voor Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="89190-119">[Creating a Hello World Application for Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span></span>

<span data-ttu-id="89190-120">[De installatie van de Azure Toolkit voor Eclipse][Installing the Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="89190-120">[Installing the Azure Toolkit for Eclipse][Installing the Azure Toolkit for Eclipse]</span></span> 

<span data-ttu-id="89190-121">Zie voor meer informatie over het gebruik van Azure met Java de [Azure Java Developer Center][Azure Java Developer Center].</span><span class="sxs-lookup"><span data-stu-id="89190-121">For more information about using Azure with Java, see the [Azure Java Developer Center][Azure Java Developer Center].</span></span>

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing the Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546
[Local storage properties]: http://go.microsoft.com/fwlink/?LinkID=699525#local_storage_properties

<!-- IMG List -->

[ic667943]: ./media/azure-toolkit-for-eclipse-deploying-large-deployments/ic667943.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/dn268601.aspx -->
