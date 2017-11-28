---
title: aaaDeploying grote implementaties
description: Meer informatie over hoe toodeploy grote implementaties met behulp van Azure Toolkit voor Eclipse Hallo.
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
ms.openlocfilehash: 6b1d2a7a5e49c78154fc856a221e64ca8dcfbe9a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploying-large-deployments"></a><span data-ttu-id="2379f-103">Implementatie van grote implementaties</span><span class="sxs-lookup"><span data-stu-id="2379f-103">Deploying Large Deployments</span></span>
<span data-ttu-id="2379f-104">Als uw implementatie te groot toobe opgenomen in de standaardmap approot hello is, kunt u een resource voor lokale opslag gebruiken als hoofdmap Hallo-implementatie voor uw JDK en toepassingsservers.</span><span class="sxs-lookup"><span data-stu-id="2379f-104">If your deployment is too large toobe contained in hello default approot folder, you can use a local storage resource as hello deployment root folder for your JDK and application server.</span></span>

## <a name="toouse-a-local-storage-resource-as-hello-deployment-root-folder-for-large-deployments"></a><span data-ttu-id="2379f-105">toouse een resource lokale opslag als Hallo implementatie-hoofdmap voor grote implementaties</span><span class="sxs-lookup"><span data-stu-id="2379f-105">toouse a local storage resource as hello deployment root folder for large deployments</span></span>
1. <span data-ttu-id="2379f-106">Maak een nieuwe resource van de lokale opslag.</span><span class="sxs-lookup"><span data-stu-id="2379f-106">Create a new local storage resource.</span></span> <span data-ttu-id="2379f-107">Hallo-naam van Hallo resource maakt niet uit.</span><span class="sxs-lookup"><span data-stu-id="2379f-107">hello name of hello resource does not matter.</span></span> <span data-ttu-id="2379f-108">Storage-resources zijn gedefinieerd op Hallo rolniveau.</span><span class="sxs-lookup"><span data-stu-id="2379f-108">Storage resources are defined at hello role level.</span></span> <span data-ttu-id="2379f-109">Hallo snelste manier tooaccess Hallo lokale opslag configuratiedialoogvenster, van waaruit u een nieuwe resource van de lokale opslag kunt maken, is via Hallo stappen te volgen: klik met de rechtermuisknop Hallo rol in Hallo **Projectverkenner** weergave (Vouw uw Azure-projectknooppunt als er geen rol Hallo), klikt u op **Azure**, en klik vervolgens op **lokale opslag**.</span><span class="sxs-lookup"><span data-stu-id="2379f-109">hello quickest way tooaccess hello local storage configuration dialog, from which you could create a new local storage resource, is by using hello following steps: Right-click hello role in hello **Project Explorer** view (expand your Azure project node if you don't see hello role), click **Azure**, and then click **Local Storage**.</span></span> <span data-ttu-id="2379f-110">Binnen Hallo **lokale opslag** dialoogvenster, klikt u op **toevoegen** toocreate een nieuwe resource van de lokale opslag.</span><span class="sxs-lookup"><span data-stu-id="2379f-110">Within hello **Local Storage** dialog, click **Add** toocreate a new local storage resource.</span></span>

2. <span data-ttu-id="2379f-111">Set Hallo gewenst grootte tooat minimaal 2048 MB (iets minder kan Hallo hetzelfde bestand grootte problemen veroorzaken zoals u zou optreden in Hallo approot).</span><span class="sxs-lookup"><span data-stu-id="2379f-111">Set hello desired size tooat least 2048 MB (anything less may cause hello same file size problems as you would encounter in hello approot).</span></span>

3. <span data-ttu-id="2379f-112">Zorg ervoor dat **opschonen Hallo inhoud wanneer Hallo rolinstantie gerecycled wordt** is ingeschakeld; Dit helpt voorkomen dat opstartlogica Hallo-implementatie worden uitgevoerd in conflicten met vooraf bestaande bestanden in de resource Hallo wanneer Hallo rol exemplaar wordt gerecycled.</span><span class="sxs-lookup"><span data-stu-id="2379f-112">Ensure that **Clean hello contents when hello role instance is recycled** is checked; this will help prevent hello deployment's startup logic from running into conflicts with pre-existing files in hello resource when hello role instance is recycled.</span></span>

4. <span data-ttu-id="2379f-113">Zorg ervoor dat Hallo **omgeving variabele opslaan van de bron-mappad Hallo na implementatie** waarde is ingesteld toohello tekenreeks **DEPLOYROOT**.</span><span class="sxs-lookup"><span data-stu-id="2379f-113">Ensure that hello **Environment variable storing hello resource's directory path after deployment** value is set toohello string **DEPLOYROOT**.</span></span> <span data-ttu-id="2379f-114">Uw lokale opslag resource dialoogvenster ziet er vergelijkbare toohello volgende.</span><span class="sxs-lookup"><span data-stu-id="2379f-114">Your local storage resource dialog will look similar toohello following.</span></span>

   ![][ic667943]

<span data-ttu-id="2379f-115">U kunt ook als u **DEPLOYROOT** als Hallo *naam* van uw lokale resource en u Hallo automatisch gegenereerde naam van omgevingsvariabele niet wijzigen (die te worden ingesteld **DEPLOYROOT_PATH** in dat geval), die voor uw toepassing ook zou werken.</span><span class="sxs-lookup"><span data-stu-id="2379f-115">Alternatively, if you use **DEPLOYROOT** as hello *name* of your local resource and you do not change hello automatically-generated environment variable name (which will be set too**DEPLOYROOT_PATH** in that case), that would work for your application as well.</span></span>

<span data-ttu-id="2379f-116">Als u meer informatie over het maken van een resource voor lokale opslag kan worden gevonden op [eigenschappen van lokale opslag][Local storage properties].</span><span class="sxs-lookup"><span data-stu-id="2379f-116">Additional information about creating a local storage resource can be found at [Local storage properties][Local storage properties].</span></span>

## <a name="see-also"></a><span data-ttu-id="2379f-117">Zie ook</span><span class="sxs-lookup"><span data-stu-id="2379f-117">See Also</span></span>
<span data-ttu-id="2379f-118">[Azure Toolkit voor Eclipse][Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="2379f-118">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span></span>

<span data-ttu-id="2379f-119">[Maken van een Hallo wereld-toepassing voor Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="2379f-119">[Creating a Hello World Application for Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span></span>

<span data-ttu-id="2379f-120">[Hello Azure Toolkit voor Eclipse installeren][Installing hello Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="2379f-120">[Installing hello Azure Toolkit for Eclipse][Installing hello Azure Toolkit for Eclipse]</span></span> 

<span data-ttu-id="2379f-121">Zie voor meer informatie over het gebruik van Azure met Java Hallo [Azure Java Developer Center][Azure Java Developer Center].</span><span class="sxs-lookup"><span data-stu-id="2379f-121">For more information about using Azure with Java, see hello [Azure Java Developer Center][Azure Java Developer Center].</span></span>

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546
[Local storage properties]: http://go.microsoft.com/fwlink/?LinkID=699525#local_storage_properties

<!-- IMG List -->

[ic667943]: ./media/azure-toolkit-for-eclipse-deploying-large-deployments/ic667943.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/dn268601.aspx -->
