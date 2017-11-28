---
title: Azure Access Configuratiescherm extensie voor IE met behulp van een groepsbeleidsobject aaaDeploy | Microsoft Docs
description: Hoe groepeert toouse beleid toodeploy Hallo Internet Explorer-invoegtoepassing voor Hallo mijn Apps portal.
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 7c2d49c8-5be0-4e7e-abac-332f9dfda736
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/02/2017
ms.author: markvi
ms.reviewer: asteen
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 926f15950bbe81d2fbfe1b0b856470da40880d7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodeploy-hello-access-panel-extension-for-internet-explorer-using-group-policy"></a><span data-ttu-id="52e01-103">Hoe tooDeploy uitbreiding voor toegang tot Configuratiescherm Hallo voor Internet Explorer met behulp van Groepsbeleid</span><span class="sxs-lookup"><span data-stu-id="52e01-103">How tooDeploy hello Access Panel Extension for Internet Explorer using Group Policy</span></span>
<span data-ttu-id="52e01-104">Deze zelfstudie laat zien hoe toouse Groepsbeleid tooremotely Hallo Toegangsvenster extensie voor Internet Explorer op uw gebruikers, computers installeren.</span><span class="sxs-lookup"><span data-stu-id="52e01-104">This tutorial shows how toouse group policy tooremotely install hello Access Panel extension for Internet Explorer on your users' machines.</span></span> <span data-ttu-id="52e01-105">Deze uitbreiding is vereist voor Internet Explorer-gebruikers hoeven te toosign in apps die zijn geconfigureerd met [op basis van wachtwoorden eenmalige aanmelding](active-directory-appssoaccess-whatis.md#password-based-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="52e01-105">This extension is required for Internet Explorer users who need toosign into apps that are configured using [password-based single sign-on](active-directory-appssoaccess-whatis.md#password-based-single-sign-on).</span></span>

<span data-ttu-id="52e01-106">Het is raadzaam dat beheerders Hallo-implementatie van deze extensie automatiseren.</span><span class="sxs-lookup"><span data-stu-id="52e01-106">It is recommended that admins automate hello deployment of this extension.</span></span> <span data-ttu-id="52e01-107">Anders gebruikers toodownload hebben en Hallo extensie zelf installeren, die foutgevoelig toouser fout en zijn beheerdersrechten vereist.</span><span class="sxs-lookup"><span data-stu-id="52e01-107">Otherwise, users have toodownload and install hello extension themselves, which is prone toouser error and requires administrator permissions.</span></span> <span data-ttu-id="52e01-108">Deze zelfstudie bevat één methode voor het software-implementaties automatiseren met behulp van Groepsbeleid.</span><span class="sxs-lookup"><span data-stu-id="52e01-108">This tutorial covers one method of automating software deployments by using group policy.</span></span> [<span data-ttu-id="52e01-109">Meer informatie over Groepsbeleid.</span><span class="sxs-lookup"><span data-stu-id="52e01-109">Learn more about group policy.</span></span>](https://technet.microsoft.com/windowsserver/bb310732.aspx)

<span data-ttu-id="52e01-110">Hallo Toegangsvenster uitbreiding is ook beschikbaar voor [Chrome](https://go.microsoft.com/fwLink/?LinkID=311859) en [Firefox](https://go.microsoft.com/fwLink/?LinkID=626998), geen van beide beheerder machtigingen tooinstall vereisen.</span><span class="sxs-lookup"><span data-stu-id="52e01-110">hello Access Panel extension is also available for [Chrome](https://go.microsoft.com/fwLink/?LinkID=311859) and [Firefox](https://go.microsoft.com/fwLink/?LinkID=626998), neither of which require administrator permissions tooinstall.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="52e01-111">Vereisten</span><span class="sxs-lookup"><span data-stu-id="52e01-111">Prerequisites</span></span>
* <span data-ttu-id="52e01-112">U hebt ingesteld [Active Directory Domain Services](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx), en u uw gebruikers machines tooyour domein hebt toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="52e01-112">You have set up [Active Directory Domain Services](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx), and you have joined your users' machines tooyour domain.</span></span>
* <span data-ttu-id="52e01-113">Hallo 'Instellingen bewerken' machtiging tooedit Hallo groepsbeleidsobject (GPO), moet u hebben.</span><span class="sxs-lookup"><span data-stu-id="52e01-113">You must have hello "Edit settings" permission tooedit hello Group Policy Object (GPO).</span></span> <span data-ttu-id="52e01-114">Standaard hebben leden van beveiligingsgroepen na Hallo deze machtiging: Domeinadministrators, Ondernemingsadministrators en Maker Eigenaar Groepsbeleid.</span><span class="sxs-lookup"><span data-stu-id="52e01-114">By default, members of hello following security groups have this permission: Domain Administrators, Enterprise Administrators, and Group Policy Creator Owners.</span></span> [<span data-ttu-id="52e01-115">Meer informatie.</span><span class="sxs-lookup"><span data-stu-id="52e01-115">Learn more.</span></span>](https://technet.microsoft.com/library/cc781991%28v=ws.10%29.aspx)

## <a name="step-1-create-hello-distribution-point"></a><span data-ttu-id="52e01-116">Stap 1: Maak Hallo-distributiepunt</span><span class="sxs-lookup"><span data-stu-id="52e01-116">Step 1: Create hello Distribution Point</span></span>
<span data-ttu-id="52e01-117">U moet eerst Hallo installer-pakket op een netwerklocatie die toegankelijk zijn voor het Hallo-machines die u wilt dat tooremotely installeren Hallo-extensie op plaatsen.</span><span class="sxs-lookup"><span data-stu-id="52e01-117">First, you must place hello installer package on a network location that can be accessed by hello machines that you wish tooremotely install hello extension on.</span></span> <span data-ttu-id="52e01-118">toodo dit als volgt te werk:</span><span class="sxs-lookup"><span data-stu-id="52e01-118">toodo this, follow these steps:</span></span>

1. <span data-ttu-id="52e01-119">Meld u als beheerder op de server toohello</span><span class="sxs-lookup"><span data-stu-id="52e01-119">Log on toohello server as an administrator</span></span>
2. <span data-ttu-id="52e01-120">In Hallo **Serverbeheer** venster te gaan**bestanden- en opslagservices**.</span><span class="sxs-lookup"><span data-stu-id="52e01-120">In hello **Server Manager** window, go too**Files and Storage Services**.</span></span>
   
    ![Geopende bestanden- en opslagservices](./media/active-directory-saas-ie-group-policy/files-services.png)
3. <span data-ttu-id="52e01-122">Ga toohello **Shares** tabblad. Klik vervolgens op **taken** > **nieuwe Share...**</span><span class="sxs-lookup"><span data-stu-id="52e01-122">Go toohello **Shares** tab. Then click **Tasks** > **New Share...**</span></span>
   
    ![Geopende bestanden- en opslagservices](./media/active-directory-saas-ie-group-policy/shares.png)
4. <span data-ttu-id="52e01-124">Volledige Hallo **Wizard Nieuwe Share** en set machtigingen tooensure dat deze kan worden geopend op uw gebruikers-machines.</span><span class="sxs-lookup"><span data-stu-id="52e01-124">Complete hello **New Share Wizard** and set permissions tooensure that it can be accessed from your users' machines.</span></span> [<span data-ttu-id="52e01-125">Meer informatie over shares.</span><span class="sxs-lookup"><span data-stu-id="52e01-125">Learn more about shares.</span></span>](https://technet.microsoft.com/library/cc753175.aspx)
5. <span data-ttu-id="52e01-126">Downloaden van Microsoft Windows Installer-pakket (MSI-bestand) te volgen Hallo: [toegang Configuratiescherm Extension.msi](https://account.activedirectory.windowsazure.com/Applications/Installers/x64/Access Panel Extension.msi)</span><span class="sxs-lookup"><span data-stu-id="52e01-126">Download hello following Microsoft Windows Installer package (.msi file): [Access Panel Extension.msi](https://account.activedirectory.windowsazure.com/Applications/Installers/x64/Access Panel Extension.msi)</span></span>
6. <span data-ttu-id="52e01-127">Kopiëren Hallo installer-pakket tooa gewenste locatie op Hallo-share.</span><span class="sxs-lookup"><span data-stu-id="52e01-127">Copy hello installer package tooa desired location on hello share.</span></span>
   
    ![Hallo MSI-bestandsshare toohello kopiëren.](./media/active-directory-saas-ie-group-policy/copy-package.png)
7. <span data-ttu-id="52e01-129">Controleer of uw clientcomputers kunnen tooaccess Hallo installer-pakket van Hallo-share.</span><span class="sxs-lookup"><span data-stu-id="52e01-129">Verify that your client machines are able tooaccess hello installer package from hello share.</span></span> 

## <a name="step-2-create-hello-group-policy-object"></a><span data-ttu-id="52e01-130">Stap 2: Hallo Group Policy Object maken</span><span class="sxs-lookup"><span data-stu-id="52e01-130">Step 2: Create hello Group Policy Object</span></span>
1. <span data-ttu-id="52e01-131">Meld u aan toohello-server die als host fungeert voor de installatie van Active Directory Domain Services (AD DS).</span><span class="sxs-lookup"><span data-stu-id="52e01-131">Log on toohello server that hosts your Active Directory Domain Services (AD DS) installation.</span></span>
2. <span data-ttu-id="52e01-132">Ga te in Hallo Serverbeheer,**extra** > **Group Policy Management**.</span><span class="sxs-lookup"><span data-stu-id="52e01-132">In hello Server Manager, go too**Tools** > **Group Policy Management**.</span></span>
   
    ![Ga tooTools > Group Policy Management](./media/active-directory-saas-ie-group-policy/tools-gpm.png)
3. <span data-ttu-id="52e01-134">In het linkerdeelvenster van Hallo Hallo **Group Policy Management** venster weergeven van uw hiërarchie van organisatie-eenheid (OE) en bepalen bij welke bereik gewenst tooapply Hallo-Groepsbeleid.</span><span class="sxs-lookup"><span data-stu-id="52e01-134">In hello left pane of hello **Group Policy Management** window, view your Organizational Unit (OU) hierarchy and determine at which scope you would like tooapply hello group policy.</span></span> <span data-ttu-id="52e01-135">Bijvoorbeeld, kunt u beslissen toopick een kleine organisatie-eenheid toodeploy tooa enkele gebruikers voor het testen of kiest u een site op het hoogste organisatie-eenheid toodeploy tooyour hele organisatie.</span><span class="sxs-lookup"><span data-stu-id="52e01-135">For instance, you may decide toopick a small OU toodeploy tooa few users for testing, or you may pick a top-level OU toodeploy tooyour entire organization.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="52e01-136">Als u wilt wel toocreate en bewerken van uw organisatie-eenheden (OE's), overschakelen back toohello Serverbeheer en gaat u te**extra** > **Active Directory: gebruikers en Computers**.</span><span class="sxs-lookup"><span data-stu-id="52e01-136">If you would like toocreate or edit your Organization Units (OUs), switch back toohello Server Manager and go too**Tools** > **Active Directory Users and Computers**.</span></span>
   > 
   > 
4. <span data-ttu-id="52e01-137">Nadat u een organisatie-eenheid hebt geselecteerd, met de rechtermuisknop en selecteer **een groepsbeleidsobject in dit domein maken en hier een koppeling...**</span><span class="sxs-lookup"><span data-stu-id="52e01-137">Once you have selected an OU, right-click it and select **Create a GPO in this domain, and Link it here...**</span></span>
   
    ![Een nieuw groepsbeleidsobject maken](./media/active-directory-saas-ie-group-policy/create-gpo.png)
5. <span data-ttu-id="52e01-139">In Hallo **nieuw groepsbeleidsobject** gevraagd, typt u een naam op voor nieuwe Group Policy Object Hallo.</span><span class="sxs-lookup"><span data-stu-id="52e01-139">In hello **New GPO** prompt, type in a name for hello new Group Policy Object.</span></span>
   
    ![Naam Hallo nieuw groepsbeleidsobject](./media/active-directory-saas-ie-group-policy/name-gpo.png)
6. <span data-ttu-id="52e01-141">Klik met de rechtermuisknop Hallo Group Policy Object dat u maakte en selecteer **bewerken**.</span><span class="sxs-lookup"><span data-stu-id="52e01-141">Right-click hello Group Policy Object that you created, and select **Edit**.</span></span>
   
    ![Hallo nieuw groepsbeleidsobject te bewerken](./media/active-directory-saas-ie-group-policy/edit-gpo.png)

## <a name="step-3-assign-hello-installation-package"></a><span data-ttu-id="52e01-143">Stap 3: Hallo installatiepakket toewijzen</span><span class="sxs-lookup"><span data-stu-id="52e01-143">Step 3: Assign hello Installation Package</span></span>
1. <span data-ttu-id="52e01-144">Bepalen of u toodeploy Hallo-extensie op basis wilt van **Computerconfiguratie** of **Gebruikersconfiguratie**.</span><span class="sxs-lookup"><span data-stu-id="52e01-144">Determine whether you would like toodeploy hello extension based on **Computer Configuration** or **User Configuration**.</span></span> <span data-ttu-id="52e01-145">Wanneer u [Computerconfiguratie](https://technet.microsoft.com/library/cc736413%28v=ws.10%29.aspx), Hallo-extensie op Hallo computer ongeacht welke gebruikers zich tooit aanmelden is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="52e01-145">When using [computer configuration](https://technet.microsoft.com/library/cc736413%28v=ws.10%29.aspx), hello extension is installed on hello computer regardless of which users log on tooit.</span></span> <span data-ttu-id="52e01-146">Met [Gebruikersconfiguratie](https://technet.microsoft.com/library/cc781953%28v=ws.10%29.aspx), gebruikers hebben geïnstalleerd voor deze ongeacht welke computers ze zich aanmelden op Hallo-extensie.</span><span class="sxs-lookup"><span data-stu-id="52e01-146">With [user configuration](https://technet.microsoft.com/library/cc781953%28v=ws.10%29.aspx), users have hello extension installed for them regardless of which computers they log on to.</span></span>
2. <span data-ttu-id="52e01-147">In het linkerdeelvenster van Hallo Hallo **Editor voor Groepsbeleidsbeheer** venster Ga tooeither Hallo mappaden, afhankelijk van welk type van de configuratie die u hebt gekozen te volgen:</span><span class="sxs-lookup"><span data-stu-id="52e01-147">In hello left pane of hello **Group Policy Management Editor** window, go tooeither of hello following folder paths, depending on which type of configuration you chose:</span></span>
   
   * `Computer Configuration/Policies/Software Settings/`
   * `User Configuration/Policies/Software Settings/`
3. <span data-ttu-id="52e01-148">Met de rechtermuisknop op **Software-installatie**, selecteer daarna **nieuw** > **pakket...**</span><span class="sxs-lookup"><span data-stu-id="52e01-148">Right-click **Software installation**, then select **New** > **Package...**</span></span>
   
    ![Maak een nieuw pakket van de software-installatie](./media/active-directory-saas-ie-group-policy/new-package.png)
4. <span data-ttu-id="52e01-150">Ga toohello gedeelde map met Hallo installer-pakket van [stap 1: Hallo distributiepunt maakt](#step-1-create-the-distribution-point), selecteer Hallo MSI-bestand en klik op **Open**.</span><span class="sxs-lookup"><span data-stu-id="52e01-150">Go toohello shared folder that contains hello installer package from [Step 1: Create hello Distribution Point](#step-1-create-the-distribution-point), select hello .msi file, and click **Open**.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="52e01-151">Als Hallo-share bevindt zich op deze server, controleert u of u via Hallo netwerk bestandspad in plaats van het lokale bestandspad Hallo Hallo .msi opent.</span><span class="sxs-lookup"><span data-stu-id="52e01-151">If hello share is located on this same server, verify that you are accessing hello .msi through hello network file path, rather than hello local file path.</span></span>
   > 
   > 
   
    ![Selecteer Hallo-installatiepakket uit Hallo gedeelde map.](./media/active-directory-saas-ie-group-policy/select-package.png)
5. <span data-ttu-id="52e01-153">In Hallo **Software distribueren** vragen, selecteer **toegewezen** voor uw implementatiemethode.</span><span class="sxs-lookup"><span data-stu-id="52e01-153">In hello **Deploy Software** prompt, select **Assigned** for your deployment method.</span></span> <span data-ttu-id="52e01-154">Klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="52e01-154">Then click **OK**.</span></span>
   
    ![Selecteer toegewezen en klik op OK.](./media/active-directory-saas-ie-group-policy/deployment-method.png)

<span data-ttu-id="52e01-156">Hallo-extensie is nu geïmplementeerde toohello organisatie-eenheid die u hebt geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="52e01-156">hello extension is now deployed toohello OU that you selected.</span></span> [<span data-ttu-id="52e01-157">Meer informatie over Software-installatie.</span><span class="sxs-lookup"><span data-stu-id="52e01-157">Learn more about Group Policy Software Installation.</span></span>](https://technet.microsoft.com/library/cc738858%28v=ws.10%29.aspx)

## <a name="step-4-auto-enable-hello-extension-for-internet-explorer"></a><span data-ttu-id="52e01-158">Stap 4: Auto-Enable Hallo-extensie voor Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="52e01-158">Step 4: Auto-Enable hello Extension for Internet Explorer</span></span>
<span data-ttu-id="52e01-159">Bovendien toorunning Hallo installatieprogramma van alle uitbreidingen voor Internet Explorer moet ingeschakeld zijn voordat deze kan worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="52e01-159">In addition toorunning hello installer, every extension for Internet Explorer must be explicitly enabled before it can be used.</span></span> <span data-ttu-id="52e01-160">Volg de stappen Hallo hieronder tooenable Hallo uitbreiding voor toegang tot Configuratiescherm met behulp van Groepsbeleid:</span><span class="sxs-lookup"><span data-stu-id="52e01-160">Follow hello steps below tooenable hello Access Panel Extension using group policy:</span></span>

1. <span data-ttu-id="52e01-161">In Hallo **Editor voor Groepsbeleidsbeheer** venster Ga tooeither Hallo paden, afhankelijk van welk type van de configuratie die u kiest in volgende [stap 3: toewijzen Hallo installatiepakket](#step-3-assign-the-installation-package):</span><span class="sxs-lookup"><span data-stu-id="52e01-161">In hello **Group Policy Management Editor** window, go tooeither of hello following paths, depending on which type of configuration you chose in [Step 3: Assign hello Installation Package](#step-3-assign-the-installation-package):</span></span>
   
   * `Computer Configuration/Policies/Administrative Templates/Windows Components/Internet Explorer/Security Features/Add-on Management`
   * `User Configuration/Policies/Administrative Templates/Windows Components/Internet Explorer/Security Features/Add-on Management`
2. <span data-ttu-id="52e01-162">Met de rechtermuisknop op **lijst met invoegtoepassingen**, en selecteer **bewerken**.</span><span class="sxs-lookup"><span data-stu-id="52e01-162">Right-click **Add-on List**, and select **Edit**.</span></span>
    <span data-ttu-id="52e01-163">![Invoegtoepassing lijst niet bewerken.](./media/active-directory-saas-ie-group-policy/edit-add-on-list.png)</span><span class="sxs-lookup"><span data-stu-id="52e01-163">![Edit Add-on List.](./media/active-directory-saas-ie-group-policy/edit-add-on-list.png)</span></span>
3. <span data-ttu-id="52e01-164">In Hallo **lijst met invoegtoepassingen** Selecteer **ingeschakeld**.</span><span class="sxs-lookup"><span data-stu-id="52e01-164">In hello **Add-on List** window, select **Enabled**.</span></span> <span data-ttu-id="52e01-165">Klik vervolgens onder Hallo **opties** sectie, klikt u op **weergeven...** .</span><span class="sxs-lookup"><span data-stu-id="52e01-165">Then, under hello **Options** section, click **Show...**.</span></span>
   
    ![Klik op inschakelen en klik vervolgens op weergeven...](./media/active-directory-saas-ie-group-policy/edit-add-on-list-window.png)
4. <span data-ttu-id="52e01-167">In Hallo **inhoud weergeven** venster Hallo volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="52e01-167">In hello **Show Contents** window, perform hello following steps:</span></span>
   
   1. <span data-ttu-id="52e01-168">Voor de eerste kolom hello (Hallo **waardenaam** veld), kopiëren en plakken Hallo volgende klasse-ID:`{030E9A3F-7B18-4122-9A60-B87235E4F59E}`</span><span class="sxs-lookup"><span data-stu-id="52e01-168">For hello first column (hello **Value Name** field), copy and paste hello following Class ID: `{030E9A3F-7B18-4122-9A60-B87235E4F59E}`</span></span>
   2. <span data-ttu-id="52e01-169">Voor de tweede kolom hello (Hallo **waarde** veld), typt u Hallo waarde te volgen:`1`</span><span class="sxs-lookup"><span data-stu-id="52e01-169">For hello second column (hello **Value** field), type in hello following value: `1`</span></span>
   3. <span data-ttu-id="52e01-170">Klik op **OK** tooclose hello **inhoud weergeven** venster.</span><span class="sxs-lookup"><span data-stu-id="52e01-170">Click **OK** tooclose hello **Show Contents** window.</span></span>
      
      ![Vul Hallo waarden zoals hierboven.](./media/active-directory-saas-ie-group-policy/show-contents.png)
5. <span data-ttu-id="52e01-172">Klik op **OK** tooapply uw wijzigingen en sluiten Hallo **lijst met invoegtoepassingen** venster.</span><span class="sxs-lookup"><span data-stu-id="52e01-172">Click **OK** tooapply your changes and close hello **Add-on List** window.</span></span>

<span data-ttu-id="52e01-173">Hallo extensie moet nu worden ingeschakeld voor Hallo-machines in Hallo geselecteerd organisatie-eenheid.</span><span class="sxs-lookup"><span data-stu-id="52e01-173">hello extension should now be enabled for hello machines in hello selected OU.</span></span> [<span data-ttu-id="52e01-174">Meer informatie over het gebruik van de Groepsbeleid tooenable- of uitschakelen van invoegtoepassingen voor Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="52e01-174">Learn more about using group policy tooenable or disable Internet Explorer add-ons.</span></span>](https://technet.microsoft.com/library/dn454941.aspx)

## <a name="step-5-optional-disable-remember-password-prompt"></a><span data-ttu-id="52e01-175">Stap 5 (optioneel): 'Wachtwoord onthouden' Prompt uitschakelen</span><span class="sxs-lookup"><span data-stu-id="52e01-175">Step 5 (Optional): Disable "Remember Password" Prompt</span></span>
<span data-ttu-id="52e01-176">Wanneer gebruikers aanmelden toowebsites met Hallo uitbreiding voor toegang tot Configuratiescherm, Internet Explorer mogelijk weergeven Hallo volgende gevraagd gevraagd "wilt u toostore uw wachtwoord?"</span><span class="sxs-lookup"><span data-stu-id="52e01-176">When users sign-in toowebsites using hello Access Panel Extension, Internet Explorer may show hello following prompt asking "Would you like toostore your password?"</span></span>

![](./media/active-directory-saas-ie-group-policy/remember-password-prompt.png)

<span data-ttu-id="52e01-177">Als u wenst dat tooprevent uw gebruikers kunnen deze vraag te zien, stappen Hallo hieronder tooprevent automatisch aanvullen van onthouden wachtwoorden:</span><span class="sxs-lookup"><span data-stu-id="52e01-177">If you wish tooprevent your users from seeing this prompt, then follow hello steps below tooprevent auto-complete from remembering passwords:</span></span>

1. <span data-ttu-id="52e01-178">In Hallo **Editor voor Groepsbeleidsbeheer** venster, Ga toohello pad hieronder vermeld.</span><span class="sxs-lookup"><span data-stu-id="52e01-178">In hello **Group Policy Management Editor** window, go toohello path listed below.</span></span> <span data-ttu-id="52e01-179">Deze configuratieinstelling is alleen beschikbaar onder **Gebruikersconfiguratie**.</span><span class="sxs-lookup"><span data-stu-id="52e01-179">This configuration setting is only available under **User Configuration**.</span></span>
   
   * `User Configuration/Policies/Administrative Templates/Windows Components/Internet Explorer/`
2. <span data-ttu-id="52e01-180">Hallo-instelling met de naam zoeken **Hallo automatisch aanvullen functie voor gebruikersnamen en wachtwoorden op formulieren inschakelen**.</span><span class="sxs-lookup"><span data-stu-id="52e01-180">Find hello setting named **Turn on hello auto-complete feature for user names and passwords on forms**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="52e01-181">Eerdere versies van Active Directory kunnen deze instelling met de naam van de Hallo lijst **niet toestaan dat wachtwoorden voor automatisch aanvullen toosave**.</span><span class="sxs-lookup"><span data-stu-id="52e01-181">Previous versions of Active Directory may list this setting with hello name **Do not allow auto-complete toosave passwords**.</span></span> <span data-ttu-id="52e01-182">Hallo-configuratie voor de instelling verschilt van het Hallo instelling beschreven in deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="52e01-182">hello configuration for that setting differs from hello setting described in this tutorial.</span></span>
   > 
   > 
   
    ![Vergeet niet toolook voor dit onder gebruikersinstellingen.](./media/active-directory-saas-ie-group-policy/disable-auto-complete.png)
3. <span data-ttu-id="52e01-184">Hallo hierboven instelling klik met de rechtermuisknop en selecteer **bewerken**.</span><span class="sxs-lookup"><span data-stu-id="52e01-184">Right click hello above setting, and select **Edit**.</span></span>
4. <span data-ttu-id="52e01-185">Hallo-venster met de titel **Hallo automatisch aanvullen functie voor gebruikersnamen en wachtwoorden op formulieren inschakelen**, selecteer **uitgeschakelde**.</span><span class="sxs-lookup"><span data-stu-id="52e01-185">In hello window titled **Turn on hello auto-complete feature for user names and passwords on forms**, select **Disabled**.</span></span>
   
    ![Selecteer uitschakelen](./media/active-directory-saas-ie-group-policy/disable-passwords.png)
5. <span data-ttu-id="52e01-187">Klik op **OK** tooapply deze wijzigingen en het venster sluiten Hallo.</span><span class="sxs-lookup"><span data-stu-id="52e01-187">Click **OK** tooapply these changes and close hello window.</span></span>

<span data-ttu-id="52e01-188">Gebruikers wordt niet meer kunnen toostore hun referenties of automatisch aanvullen tooaccess eerder opgeslagen referenties gebruiken.</span><span class="sxs-lookup"><span data-stu-id="52e01-188">Users will no longer be able toostore their credentials or use auto-complete tooaccess previously stored credentials.</span></span> <span data-ttu-id="52e01-189">Echter, dit beleid staat toe dat gebruikers toocontinue toouse automatisch aanvullen voor andere soorten formuliervelden, zoals zoekvelden.</span><span class="sxs-lookup"><span data-stu-id="52e01-189">However, this policy does allow users toocontinue toouse auto-complete for other types of form fields, such as search fields.</span></span>

> [!WARNING]
> <span data-ttu-id="52e01-190">Als dit beleid is ingeschakeld, nadat gebruikers hebt gekozen toostore sommige referenties, dit beleid wordt *niet* wissen Hallo-referenties die al zijn opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="52e01-190">If this policy is enabled after users have chosen toostore some credentials, this policy will *not* clear hello credentials that have already been stored.</span></span>
> 
> 

## <a name="step-6-testing-hello-deployment"></a><span data-ttu-id="52e01-191">Stap 6: Hallo implementatie testen</span><span class="sxs-lookup"><span data-stu-id="52e01-191">Step 6: Testing hello Deployment</span></span>
<span data-ttu-id="52e01-192">Voer onderstaande tooverify Hallo stappen als Hallo extensie implementatie geslaagd is:</span><span class="sxs-lookup"><span data-stu-id="52e01-192">Follow hello steps below tooverify if hello extension deployment was successful:</span></span>

1. <span data-ttu-id="52e01-193">Als u hebt geïmplementeerd met behulp van **Computerconfiguratie**, meld u aan bij een clientcomputer die deel uitmaakt van de organisatie-eenheid die u hebt geselecteerd in toohello [stap 2: Maak Hallo Group Policy Object](#step-2-create-the-group-policy-object).</span><span class="sxs-lookup"><span data-stu-id="52e01-193">If you deployed using **Computer Configuration**, sign into a client machine that belongs toohello OU that you selected in [Step 2: Create hello Group Policy Object](#step-2-create-the-group-policy-object).</span></span> <span data-ttu-id="52e01-194">Als u hebt geïmplementeerd met behulp van **Gebruikersconfiguratie**, zorg ervoor dat toosign in als een gebruiker die lid is van toothat organisatie-eenheid.</span><span class="sxs-lookup"><span data-stu-id="52e01-194">If you deployed using **User Configuration**, make sure toosign in as a user who belongs toothat OU.</span></span>
2. <span data-ttu-id="52e01-195">Het duurt een paar aanmelding modules voor Groepsbeleid Hallo toofully update wijzigingen aan deze machine.</span><span class="sxs-lookup"><span data-stu-id="52e01-195">It may take a couple sign ins for hello group policy changes toofully update with this machine.</span></span> <span data-ttu-id="52e01-196">tooforce hello update, open een **opdrachtprompt** venster en Voer Hallo volgende opdracht:`gpupdate /force`</span><span class="sxs-lookup"><span data-stu-id="52e01-196">tooforce hello update, open a **Command Prompt** window and run hello following command: `gpupdate /force`</span></span>
3. <span data-ttu-id="52e01-197">Hallo-machine voor Hallo installatie tootake plaats, moet u opnieuw.</span><span class="sxs-lookup"><span data-stu-id="52e01-197">You must restart hello machine for hello installation tootake place.</span></span> <span data-ttu-id="52e01-198">Wanneer kan aanzienlijk langer duren dan normaal tijdens het Hallo-extensie wordt geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="52e01-198">Bootup may take significantly more time than usual while hello extension installs.</span></span>
4. <span data-ttu-id="52e01-199">Start opnieuw op en open **Internet Explorer**.</span><span class="sxs-lookup"><span data-stu-id="52e01-199">After restarting, open **Internet Explorer**.</span></span> <span data-ttu-id="52e01-200">Op Hallo rechterbovenhoek van Hallo-venster, klikt u op **extra** (Hallo tandwielpictogram pictogram) en selecteer vervolgens **invoegtoepassingen beheren**.</span><span class="sxs-lookup"><span data-stu-id="52e01-200">On hello upper-right corner of hello window, click **Tools** (hello gear icon), and then select **Manage add-ons**.</span></span>
   
    ![Ga tooTools > invoegtoepassingen beheren](./media/active-directory-saas-ie-group-policy/manage-add-ons.png)
5. <span data-ttu-id="52e01-202">In Hallo **invoegtoepassingen beheren** venster controleren die Hallo **Configuratiescherm-uitbreiding voor toegang tot** is geïnstalleerd en dat de **Status** te is ingesteld**ingeschakeld**.</span><span class="sxs-lookup"><span data-stu-id="52e01-202">In hello **Manage Add-ons** window, verify that hello **Access Panel Extension** has been installed and that its **Status** has been set too**Enabled**.</span></span>
   
    ![Controleer of deze Hallo uitbreiding van het Configuratiescherm toegang is geïnstalleerd en ingeschakeld.](./media/active-directory-saas-ie-group-policy/verify-install.png)

## <a name="related-articles"></a><span data-ttu-id="52e01-204">Verwante artikelen</span><span class="sxs-lookup"><span data-stu-id="52e01-204">Related Articles</span></span>
* <span data-ttu-id="52e01-205">[Article Index for Application Management in Azure Active Directory](active-directory-apps-index.md) (Artikelindex voor toepassingsbeheer in Azure Active Directory)</span><span class="sxs-lookup"><span data-stu-id="52e01-205">[Article Index for Application Management in Azure Active Directory](active-directory-apps-index.md)</span></span>
* [<span data-ttu-id="52e01-206">Toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="52e01-206">Application access and single sign-on with Azure Active Directory</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="52e01-207">Hallo Configuratiescherm-uitbreiding voor toegang tot het oplossen van problemen voor Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="52e01-207">Troubleshooting hello Access Panel Extension for Internet Explorer</span></span>](active-directory-saas-ie-troubleshooting.md)

