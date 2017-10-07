---
title: aaaHow toosecure toegang tooAzure Data Catalog | Microsoft Docs
description: In dit artikel wordt uitgelegd hoe toosecure catalogus met gegevens en de gegevensassets.
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/17/2017
ms.author: maroche
ms.openlocfilehash: d7c35fd57d8add1cdc152b75f111879288e1548f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosecure-access-toodata-catalog-and-data-assets"></a><span data-ttu-id="8b5c8-103">Hoe toosecure toegang krijgen tot de catalogus en gegevens activa toodata</span><span class="sxs-lookup"><span data-stu-id="8b5c8-103">How toosecure access toodata catalog and data assets</span></span>
> [!IMPORTANT]
> <span data-ttu-id="8b5c8-104">Deze functie is alleen beschikbaar in standard Hallo-editie van Azure Data Catalog.</span><span class="sxs-lookup"><span data-stu-id="8b5c8-104">This feature is available only in hello standard edition of Azure Data Catalog.</span></span>

<span data-ttu-id="8b5c8-105">Azure Data Catalog, kunt u toospecify die toegang hebben tot Hallo gegevenscatalogus en welke bewerkingen (registreren, aantekeningen toevoegen aan, eigenaar) ze van metagegevens in de catalogus Hallo kunnen uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="8b5c8-105">Azure Data Catalog allows you toospecify who can access hello data catalog and what operations (register, annotate, take ownership) they can perform on metadata in hello catalog.</span></span> 

## <a name="catalog-users-and-permissions"></a><span data-ttu-id="8b5c8-106">: Catalogusgebruikers en machtigingen</span><span class="sxs-lookup"><span data-stu-id="8b5c8-106">Catalog users and permissions</span></span>
<span data-ttu-id="8b5c8-107">toogive een gebruiker of een groep Hallo tooa gegevenscatalogus toegang en machtigingen instellen:</span><span class="sxs-lookup"><span data-stu-id="8b5c8-107">toogive a user or a group hello access tooa data catalog and set permissions:</span></span>

1. <span data-ttu-id="8b5c8-108">Op Hallo [startpagina van uw data catalog](http://www.azuredatacatalog.com), klikt u op **instellingen** op Hallo-werkbalk.</span><span class="sxs-lookup"><span data-stu-id="8b5c8-108">On hello [home page of your data catalog](http://www.azuredatacatalog.com),  click **Settings** on hello toolbar.</span></span>

    ![catalogus voor gegevens - instellingen](media/data-catalog-how-to-secure-catalog/data-catalog-settings.png)
2. <span data-ttu-id="8b5c8-110">Vouw in de pagina instellingen Hallo Hallo **Catalogusgebruikers** sectie.</span><span class="sxs-lookup"><span data-stu-id="8b5c8-110">In hello settings page, expand hello **Catalog Users** section.</span></span>
    <span data-ttu-id="8b5c8-111">![Gebruikers - catalogus toevoegen](media/data-catalog-how-to-secure-catalog/data-catalog-add-button.png)</span><span class="sxs-lookup"><span data-stu-id="8b5c8-111">![Catalog Users - Add](media/data-catalog-how-to-secure-catalog/data-catalog-add-button.png)</span></span>
3. <span data-ttu-id="8b5c8-112">Klik op **Add**.</span><span class="sxs-lookup"><span data-stu-id="8b5c8-112">Click **Add**.</span></span>
4. <span data-ttu-id="8b5c8-113">Voer Hallo volledig gekwalificeerd **gebruikersnaam** of de naam van Hallo **beveiligingsgroep** in Azure Active Directory (AAD) die zijn gekoppeld aan de catalogus Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="8b5c8-113">Enter hello fully qualified **user name** or name of hello **security group** in hello Azure Active Directory (AAD) associated with hello catalog.</span></span> <span data-ttu-id="8b5c8-114">Gebruik komma (', ') als scheidingsteken als u wilt toevoegen van meer dan één gebruiker of groep.</span><span class="sxs-lookup"><span data-stu-id="8b5c8-114">Use comma (\`,’) as a separator if you are adding more than one user or group.</span></span>
    <span data-ttu-id="8b5c8-115">![Gebruikers van de catalogus - gebruikers of groepen](media/data-catalog-how-to-secure-catalog/data-catalog-users-groups.png)</span><span class="sxs-lookup"><span data-stu-id="8b5c8-115">![Catalog Users - users or groups](media/data-catalog-how-to-secure-catalog/data-catalog-users-groups.png)</span></span>
5. <span data-ttu-id="8b5c8-116">Druk op **ENTER** of **tabblad** buiten het Hallo-tekstvak.</span><span class="sxs-lookup"><span data-stu-id="8b5c8-116">Press **ENTER** or **TAB** out of hello text box.</span></span> 
6.  <span data-ttu-id="8b5c8-117">Controleer of alle machtigingen (**aantekening**, **registreren**, en **eigenaar**) toothese gebruikers of groepen standaard toegewezen.</span><span class="sxs-lookup"><span data-stu-id="8b5c8-117">Confirm that all permissions (**Annotate**, **Register**, and **Take Ownership**) are assigned toothese users or groups by default.</span></span> <span data-ttu-id="8b5c8-118">Dat wil zeggen, Hallo gebruiker of groep kunt [registreren gegevensassets]( data-catalog-how-to-register.md), [aantekeningen toevoegen aan gegevensassets]( data-catalog-how-to-annotate.md), en [eigenaar worden van gegevensassets]( data-catalog-how-to-manage.md).</span><span class="sxs-lookup"><span data-stu-id="8b5c8-118">That is, hello user or group can [register data assets]( data-catalog-how-to-register.md), [annotate data assets]( data-catalog-how-to-annotate.md), and [take ownership of data assets]( data-catalog-how-to-manage.md).</span></span> 
    <span data-ttu-id="8b5c8-119">![Gebruikers van de catalogus - standaardmachtigingen](media/data-catalog-how-to-secure-catalog/data-catalog-default-permissions.png)</span><span class="sxs-lookup"><span data-stu-id="8b5c8-119">![Catalog Users - default permissions](media/data-catalog-how-to-secure-catalog/data-catalog-default-permissions.png)</span></span>
7.  <span data-ttu-id="8b5c8-120">toogive een gebruiker of groep alleen Hallo lezen toegang tot toohello catalogus wissen Hallo **aantekeningen toevoegen aan** optie voor die gebruiker of groep.</span><span class="sxs-lookup"><span data-stu-id="8b5c8-120">toogive a user or group only hello read access toohello catalog, clear hello **annotate** option for that user or group.</span></span> <span data-ttu-id="8b5c8-121">Wanneer u doet dit, Hallo gebruiker of groep kan niet gegevensassets in Hallo catalogus aantekeningen maar kunnen weergeven.</span><span class="sxs-lookup"><span data-stu-id="8b5c8-121">When you do so, hello user or group cannot annotate data assets in hello catalog but they can view them.</span></span> 
8.  <span data-ttu-id="8b5c8-122">toodeny een gebruiker of groep van het registreren van gegevensassets, schakelt u Hallo **registreren** optie voor die gebruiker of groep.</span><span class="sxs-lookup"><span data-stu-id="8b5c8-122">toodeny a user or group from registering data assets, clear hello **register** option for that user or group.</span></span>
9.  <span data-ttu-id="8b5c8-123">een gebruiker van de eigenaar van een gegevensasset, wissen Hallo toodeny **eigenaar** optie voor die gebruiker of groep.</span><span class="sxs-lookup"><span data-stu-id="8b5c8-123">toodeny a user from taking ownership of a data asset, clear hello **take ownership** option for that user or group.</span></span> 
10. <span data-ttu-id="8b5c8-124">toodelete een gebruiker of groep van catalogusgebruikers, klikt u op **x** voor Hallo gebruikersgroep Hallo Hallo lijst onderaan in.</span><span class="sxs-lookup"><span data-stu-id="8b5c8-124">toodelete a user/group from catalog users, click **x** for hello user/group at hello bottom of hello list.</span></span> 
    <span data-ttu-id="8b5c8-125">![Gebruikers van catalogus - gebruiker verwijderen](media/data-catalog-how-to-secure-catalog/data-catalog-delete-user.png)</span><span class="sxs-lookup"><span data-stu-id="8b5c8-125">![Catalog Users - delete user](media/data-catalog-how-to-secure-catalog/data-catalog-delete-user.png)</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="8b5c8-126">U wordt aangeraden dat u rechtstreeks toevoegen van beveiliging groepen toocatalog gebruikers in plaats van met toevoegen van gebruikers en machtigingen toe te wijzen.</span><span class="sxs-lookup"><span data-stu-id="8b5c8-126">We recommend that you add security groups toocatalog users rather than adding users directly and assign permissions.</span></span> <span data-ttu-id="8b5c8-127">Vervolgens voegt u gebruikers toohello beveiligingsgroepen die overeenkomen met hun rollen en de vereiste toegang toohello-catalogus.</span><span class="sxs-lookup"><span data-stu-id="8b5c8-127">Then, add users toohello security groups that match their roles and their required access toohello catalog.</span></span>

## <a name="special-considerations"></a><span data-ttu-id="8b5c8-128">Speciale overwegingen</span><span class="sxs-lookup"><span data-stu-id="8b5c8-128">Special considerations</span></span>

- <span data-ttu-id="8b5c8-129">Hallo machtigingen toegewezen groepen toosecurity additief zijn.</span><span class="sxs-lookup"><span data-stu-id="8b5c8-129">hello permissions assigned toosecurity groups are additive.</span></span> <span data-ttu-id="8b5c8-130">Een gebruiker is, en wel in twee groepen.</span><span class="sxs-lookup"><span data-stu-id="8b5c8-130">Say, a user is in two groups.</span></span> <span data-ttu-id="8b5c8-131">Één groep heeft aantekeningen toevoegen aan machtigingen en andere groep heeft geen hebben aantekeningen machtigingen.</span><span class="sxs-lookup"><span data-stu-id="8b5c8-131">One group has annotate permissions and other group does not have annotate permissions.</span></span> <span data-ttu-id="8b5c8-132">Gebruiker heeft vervolgens aantekeningen toevoegen aan machtigingen.</span><span class="sxs-lookup"><span data-stu-id="8b5c8-132">Then, user has annotate permissions.</span></span> 
- <span data-ttu-id="8b5c8-133">Hallo machtigingen toegewezen expliciet tooa gebruiker opheffen Hallo machtigingen worden toegewezen toogroups toowhich Hallo gebruiker behoort.</span><span class="sxs-lookup"><span data-stu-id="8b5c8-133">hello permissions assigned explicitly tooa user override hello permissions assigned toogroups toowhich hello user belongs.</span></span> <span data-ttu-id="8b5c8-134">In het vorige voorbeeld hello, bijvoorbeeld u Hallo gebruiker toocatalog gebruikers expliciet zijn toegevoegd en geen toewijzen aantekeningen toevoegen aan machtigingen.</span><span class="sxs-lookup"><span data-stu-id="8b5c8-134">In hello previous example, say, you explicitly added hello user toocatalog users and do not assign annotate permissions.</span></span> <span data-ttu-id="8b5c8-135">Hallo-gebruiker kan geen aantekeningen toevoegen aan gegevensassets Hoewel Hallo gebruiker is lid van een groep die beschikt over aantekeningen toevoegen aan machtigingen.</span><span class="sxs-lookup"><span data-stu-id="8b5c8-135">hello user cannot annotate data assets even though hello user is a member of a group that does have annotate permissions.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8b5c8-136">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8b5c8-136">Next steps</span></span>
- [<span data-ttu-id="8b5c8-137">Aan de slag met Azure Data Catalog</span><span class="sxs-lookup"><span data-stu-id="8b5c8-137">Get started with Azure Data Catalog</span></span>](data-catalog-get-started.md)

