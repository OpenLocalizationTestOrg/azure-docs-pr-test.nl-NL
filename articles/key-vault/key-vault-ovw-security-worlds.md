---
ms.assetid: 
title: aaaAzure Sleutelkluis beveiligingswerelden | Microsoft Docs
ms.service: key-vault
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.date: 07/03/2017
ms.openlocfilehash: 1995119c9e9886829d6c50af921f275d10e382f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-key-vault-security-worlds-and-geographic-boundaries"></a><span data-ttu-id="e5bd4-102">Beveiligingswerelden voor Azure Sleutelkluis en de geografische grenzen</span><span class="sxs-lookup"><span data-stu-id="e5bd4-102">Azure Key Vault security worlds and geographic boundaries</span></span>

<span data-ttu-id="e5bd4-103">Azure Sleutelkluis is een multitenant-service en een pool van Hardware Security Modules (HSM's) in elke Azure-locatie gebruikt.</span><span class="sxs-lookup"><span data-stu-id="e5bd4-103">Azure Key Vault is a multi-tenant service and uses a pool of Hardware Security Modules (HSMs) in each Azure location.</span></span> 

<span data-ttu-id="e5bd4-104">Alle HSM's op Azure locaties in Hallo Hallo dezelfde geografische regio delen dezelfde grens van cryptografische (Beveiligingswereld Thales).</span><span class="sxs-lookup"><span data-stu-id="e5bd4-104">All HSMs at Azure locations in hello same geographic region share hello same cryptographic boundary (Thales Security World).</span></span> <span data-ttu-id="e5bd4-105">Bijvoorbeeld, Hallo VS-Oost en West, VS delen dezelfde beveiligingswereld omdat ze toohello VS geografische locatie horen.</span><span class="sxs-lookup"><span data-stu-id="e5bd4-105">For example, East US and West US share hello same security world because they belong toohello US geo location.</span></span> <span data-ttu-id="e5bd4-106">Op deze manier alle Azure locaties in Japan share Hallo dezelfde beveiligingswereld en alle Azure locaties in Australië, India, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="e5bd4-106">Similarly, all Azure locations in Japan share hello same security world and all Azure locations in Australia, India, and so on.</span></span> 

## <a name="backup-and-restore-behavior"></a><span data-ttu-id="e5bd4-107">Gedrag van back-up en herstel</span><span class="sxs-lookup"><span data-stu-id="e5bd4-107">Backup and restore behavior</span></span>

<span data-ttu-id="e5bd4-108">Een back-up van een sleutel van een sleutelkluis in een Azure-locatie kan worden hersteld tooa sleutelkluis in een andere Azure-locatie, mits beide volgende voorwaarden voldaan wordt:</span><span class="sxs-lookup"><span data-stu-id="e5bd4-108">A backup taken of a key from a key vault in one Azure location can be restored tooa key vault in another Azure location, as long as both of these conditions are true:</span></span>

- <span data-ttu-id="e5bd4-109">Beide hello Azure locaties behoren toohello dezelfde geografische locatie</span><span class="sxs-lookup"><span data-stu-id="e5bd4-109">Both of hello Azure locations belong toohello same geographical location</span></span>
- <span data-ttu-id="e5bd4-110">Beide Hallo sleutelkluizen toohello deel uitmaken van hetzelfde Azure-abonnement</span><span class="sxs-lookup"><span data-stu-id="e5bd4-110">Both of hello key vaults belong toohello same Azure subscription</span></span>

<span data-ttu-id="e5bd4-111">Een back-up door een bepaald abonnement van een sleutel in een sleutelkluis in India West, kan bijvoorbeeld alleen worden teruggezet tooanother sleutelkluis in Hallo hetzelfde abonnement en dezelfde geografische locatie; India West, India centraal of Zuid, India.</span><span class="sxs-lookup"><span data-stu-id="e5bd4-111">For example, a backup taken by a given subscription of a key in a key vault in West India, can only be restored tooanother key vault in hello same subscription and geo location; West India, Central India or South India.</span></span>

## <a name="regions-and-products"></a><span data-ttu-id="e5bd4-112">Regio's en -producten</span><span class="sxs-lookup"><span data-stu-id="e5bd4-112">Regions and products</span></span>

- [<span data-ttu-id="e5bd4-113">Azure-regio's</span><span class="sxs-lookup"><span data-stu-id="e5bd4-113">Azure regions</span></span>](https://azure.microsoft.com/regions/)
- [<span data-ttu-id="e5bd4-114">Microsoft-producten per regio</span><span class="sxs-lookup"><span data-stu-id="e5bd4-114">Microsoft products by region</span></span>](https://azure.microsoft.com/regions/services/)

<span data-ttu-id="e5bd4-115">Regio's zijn toegewezen toosecurity werelden, weergegeven als primaire koppen in Hallo tabellen:</span><span class="sxs-lookup"><span data-stu-id="e5bd4-115">Regions are mapped toosecurity worlds, shown as major headings in hello tables:</span></span>

<span data-ttu-id="e5bd4-116">In Hallo producten per regio artikel, bijvoorbeeld Hallo **Americas** tabblad bevat Oost US, VS-midden, VS-WEST alle toewijzing toohello Americas regio.</span><span class="sxs-lookup"><span data-stu-id="e5bd4-116">In hello products by region article, for example, hello **Americas** tab contains EAST US, CENTRAL US, WEST US all mapping toohello Americas region.</span></span> 

>[!NOTE]
><span data-ttu-id="e5bd4-117">Een uitzondering is dat ons DOD Oost en ons DOD centrale hun eigen beveiligingswerelden hebben.</span><span class="sxs-lookup"><span data-stu-id="e5bd4-117">An exception is that US DOD EAST and US DOD CENTRAL have their own security worlds.</span></span> 

<span data-ttu-id="e5bd4-118">Op deze manier op Hallo **Europa** tabblad Noord-Europa en WEST-Europa beide toohello Europa regio toegewezen.</span><span class="sxs-lookup"><span data-stu-id="e5bd4-118">Similarly, on hello **Europe** tab, NORTH EUROPE and WEST EUROPE both map toohello Europe region.</span></span> <span data-ttu-id="e5bd4-119">Hallo geldt ook op Hallo **Azië** tabblad.</span><span class="sxs-lookup"><span data-stu-id="e5bd4-119">hello same is also true on hello **Asia Pacific** tab.</span></span>



