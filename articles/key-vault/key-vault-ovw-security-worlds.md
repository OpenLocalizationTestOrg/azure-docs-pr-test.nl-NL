---
ms.assetid: 
title: Beveiligingswerelden voor Azure Sleutelkluis | Microsoft Docs
ms.service: key-vault
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.date: 07/03/2017
ms.openlocfilehash: 921bbd109c9ea98d8b5c286a7512bed026412d26
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-key-vault-security-worlds-and-geographic-boundaries"></a><span data-ttu-id="99cb7-102">Beveiligingswerelden voor Azure Sleutelkluis en de geografische grenzen</span><span class="sxs-lookup"><span data-stu-id="99cb7-102">Azure Key Vault security worlds and geographic boundaries</span></span>

<span data-ttu-id="99cb7-103">Azure Sleutelkluis is een multitenant-service en een pool van Hardware Security Modules (HSM's) in elke Azure-locatie gebruikt.</span><span class="sxs-lookup"><span data-stu-id="99cb7-103">Azure Key Vault is a multi-tenant service and uses a pool of Hardware Security Modules (HSMs) in each Azure location.</span></span> 

<span data-ttu-id="99cb7-104">Alle HSM's van Azure locaties in dezelfde geografische regio delen dezelfde cryptografische grens (Beveiligingswereld Thales).</span><span class="sxs-lookup"><span data-stu-id="99cb7-104">All HSMs at Azure locations in the same geographic region share the same cryptographic boundary (Thales Security World).</span></span> <span data-ttu-id="99cb7-105">Bijvoorbeeld, VS-Oost en VS-West delen de dezelfde beveiligingswereld omdat ze deel uitmaken van de VS geografische locatie.</span><span class="sxs-lookup"><span data-stu-id="99cb7-105">For example, East US and West US share the same security world because they belong to the US geo location.</span></span> <span data-ttu-id="99cb7-106">Op deze manier delen alle Azure locaties in Japan de dezelfde beveiligingswereld en alle Azure locaties in Australië en India.</span><span class="sxs-lookup"><span data-stu-id="99cb7-106">Similarly, all Azure locations in Japan share the same security world and all Azure locations in Australia, India, and so on.</span></span> 

## <a name="backup-and-restore-behavior"></a><span data-ttu-id="99cb7-107">Gedrag van back-up en herstel</span><span class="sxs-lookup"><span data-stu-id="99cb7-107">Backup and restore behavior</span></span>

<span data-ttu-id="99cb7-108">Een back-up van een sleutel van een sleutelkluis in een Azure-locatie kan worden hersteld naar een sleutelkluis in een andere Azure-locatie, mits beide volgende voorwaarden voldaan wordt:</span><span class="sxs-lookup"><span data-stu-id="99cb7-108">A backup taken of a key from a key vault in one Azure location can be restored to a key vault in another Azure location, as long as both of these conditions are true:</span></span>

- <span data-ttu-id="99cb7-109">Zowel de Azure locaties deel uitmaken van dezelfde geografische locatie</span><span class="sxs-lookup"><span data-stu-id="99cb7-109">Both of the Azure locations belong to the same geographical location</span></span>
- <span data-ttu-id="99cb7-110">Zowel de sleutelkluizen behoren tot dezelfde Azure-abonnement</span><span class="sxs-lookup"><span data-stu-id="99cb7-110">Both of the key vaults belong to the same Azure subscription</span></span>

<span data-ttu-id="99cb7-111">Bijvoorbeeld, kan een back-up door een bepaald abonnement van een sleutel in een sleutelkluis in India West, alleen worden teruggezet naar een andere sleutelkluis in hetzelfde abonnement en dezelfde geografische locatie; India West, India centraal of Zuid, India.</span><span class="sxs-lookup"><span data-stu-id="99cb7-111">For example, a backup taken by a given subscription of a key in a key vault in West India, can only be restored to another key vault in the same subscription and geo location; West India, Central India or South India.</span></span>

## <a name="regions-and-products"></a><span data-ttu-id="99cb7-112">Regio's en -producten</span><span class="sxs-lookup"><span data-stu-id="99cb7-112">Regions and products</span></span>

- [<span data-ttu-id="99cb7-113">Azure-regio's</span><span class="sxs-lookup"><span data-stu-id="99cb7-113">Azure regions</span></span>](https://azure.microsoft.com/regions/)
- [<span data-ttu-id="99cb7-114">Microsoft-producten per regio</span><span class="sxs-lookup"><span data-stu-id="99cb7-114">Microsoft products by region</span></span>](https://azure.microsoft.com/regions/services/)

<span data-ttu-id="99cb7-115">Regio's zijn toegewezen aan beveiligingswerelden, weergegeven als primaire koppen in de tabellen:</span><span class="sxs-lookup"><span data-stu-id="99cb7-115">Regions are mapped to security worlds, shown as major headings in the tables:</span></span>

<span data-ttu-id="99cb7-116">In de producten per regio artikel, bijvoorbeeld de **Americas** tabblad bevat Oost US, VS-midden, VS-WEST alle toewijzing voor de regio Americas.</span><span class="sxs-lookup"><span data-stu-id="99cb7-116">In the products by region article, for example, the **Americas** tab contains EAST US, CENTRAL US, WEST US all mapping to the Americas region.</span></span> 

>[!NOTE]
><span data-ttu-id="99cb7-117">Een uitzondering is dat ons DOD Oost en ons DOD centrale hun eigen beveiligingswerelden hebben.</span><span class="sxs-lookup"><span data-stu-id="99cb7-117">An exception is that US DOD EAST and US DOD CENTRAL have their own security worlds.</span></span> 

<span data-ttu-id="99cb7-118">Op deze manier op de **Europa** tabblad beide toegewezen aan de regio Europa Noord-Europa en WEST-Europa.</span><span class="sxs-lookup"><span data-stu-id="99cb7-118">Similarly, on the **Europe** tab, NORTH EUROPE and WEST EUROPE both map to the Europe region.</span></span> <span data-ttu-id="99cb7-119">Hetzelfde geldt ook voor de **Azië** tabblad.</span><span class="sxs-lookup"><span data-stu-id="99cb7-119">The same is also true on the **Asia Pacific** tab.</span></span>



