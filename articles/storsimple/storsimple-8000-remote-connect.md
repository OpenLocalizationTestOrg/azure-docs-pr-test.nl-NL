---
title: aaaConnect op afstand tooyour StorSimple-apparaat | Microsoft Docs
description: Legt uit hoe tooconfigure uw apparaat voor extern beheer en hoe tooconnect tooWindows PowerShell voor StorSimple via HTTP of HTTPS.
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/07/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 38b6a6350891b9f6f8fdfc55880b2f47105d947c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-remotely-tooyour-storsimple-8000-series-device"></a><span data-ttu-id="acbac-103">Tooyour StorSimple 8000 series apparaat op afstand verbinding maken</span><span class="sxs-lookup"><span data-stu-id="acbac-103">Connect remotely tooyour StorSimple 8000 series device</span></span>

## <a name="overview"></a><span data-ttu-id="acbac-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="acbac-104">Overview</span></span>

<span data-ttu-id="acbac-105">U kunt tooyour apparaat via Windows PowerShell op afstand verbinding maken.</span><span class="sxs-lookup"><span data-stu-id="acbac-105">You can remotely connect tooyour device via Windows PowerShell.</span></span> <span data-ttu-id="acbac-106">Als u op deze manier verbinding maakt, ziet u niet een menu.</span><span class="sxs-lookup"><span data-stu-id="acbac-106">When you connect this way, you do not see a menu.</span></span> <span data-ttu-id="acbac-107">(Ziet u een menu alleen als u de seriële console Hallo op Hallo apparaat tooconnect gebruiken.) Met Windows PowerShell op afstand, moet u specifieke runspace tooa verbinden.</span><span class="sxs-lookup"><span data-stu-id="acbac-107">(You see a menu only if you use hello serial console on hello device tooconnect.) With Windows PowerShell remoting, you connect tooa specific runspace.</span></span> <span data-ttu-id="acbac-108">U kunt ook de weergavetaal Hallo opgeven.</span><span class="sxs-lookup"><span data-stu-id="acbac-108">You can also specify hello display language.</span></span>

<span data-ttu-id="acbac-109">Voor meer informatie over het gebruik van Windows PowerShell voor externe toegang toomanage uw apparaat gaat te[gebruik Windows PowerShell voor StorSimple tooadminister uw StorSimple-apparaat](storsimple-8000-windows-powershell-administration.md).</span><span class="sxs-lookup"><span data-stu-id="acbac-109">For more information about using Windows PowerShell remoting toomanage your device, go too[Use Windows PowerShell for StorSimple tooadminister your StorSimple device](storsimple-8000-windows-powershell-administration.md).</span></span>

<span data-ttu-id="acbac-110">Deze zelfstudie wordt uitgelegd hoe tooconfigure uw apparaat voor extern beheer en klikt u vervolgens het tooconnect tooWindows PowerShell voor StorSimple.</span><span class="sxs-lookup"><span data-stu-id="acbac-110">This tutorial explains how tooconfigure your device for remote management and then how tooconnect tooWindows PowerShell for StorSimple.</span></span> <span data-ttu-id="acbac-111">Kunt u HTTP of HTTPS tooremotely verbinden via Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="acbac-111">You can use HTTP or HTTPS tooremotely connect via Windows PowerShell.</span></span> <span data-ttu-id="acbac-112">Echter, wanneer u beslist hoe tooconnect tooWindows PowerShell voor StorSimple, overweeg Hallo volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="acbac-112">However, when you are deciding how tooconnect tooWindows PowerShell for StorSimple, consider hello following information:</span></span>

* <span data-ttu-id="acbac-113">Toohello rechtstreeks verbinding maken de seriële console apparaat beveiligd is, maar verbindende toohello seriële console via netwerkswitches is niet.</span><span class="sxs-lookup"><span data-stu-id="acbac-113">Connecting directly toohello device serial console is secure, but connecting toohello serial console over network switches is not.</span></span> <span data-ttu-id="acbac-114">Wees voorzichtig met van Hallo beveiligingsrisico, omdat het toohello de seriële console apparaat via netwerkswitches verbinding te maken.</span><span class="sxs-lookup"><span data-stu-id="acbac-114">Be cautious of hello security risk when connecting toohello device serial console over network switches.</span></span>
* <span data-ttu-id="acbac-115">Verbinding maken via een HTTP-sessie biedt meer beveiliging dan verbinding maken via de seriële console Hallo via Hallo netwerk mogelijk.</span><span class="sxs-lookup"><span data-stu-id="acbac-115">Connecting through an HTTP session might offer more security than connecting through hello serial console over hello network.</span></span> <span data-ttu-id="acbac-116">Hoewel dit niet de meest beveiligde methode hello, is het is acceptabel in vertrouwde netwerken.</span><span class="sxs-lookup"><span data-stu-id="acbac-116">Although this is not hello most secure method, it is acceptable on trusted networks.</span></span>
* <span data-ttu-id="acbac-117">Verbinding maken via een HTTPS-sessie met een zelfondertekend certificaat is Hallo veiligste en aanbevolen optie Hallo.</span><span class="sxs-lookup"><span data-stu-id="acbac-117">Connecting through an HTTPS session with a self-signed certificate is hello most secure and hello recommended option.</span></span>

<span data-ttu-id="acbac-118">U kunt verbinden op afstand toohello Windows PowerShell-interface.</span><span class="sxs-lookup"><span data-stu-id="acbac-118">You can connect remotely toohello Windows PowerShell interface.</span></span> <span data-ttu-id="acbac-119">Externe toegang tooyour StorSimple-apparaat via Windows PowerShell-interface Hallo is echter niet standaard ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="acbac-119">However, remote access tooyour StorSimple device via hello Windows PowerShell interface is not enabled by default.</span></span> <span data-ttu-id="acbac-120">U moet eerst extern beheer op Hallo apparaat inschakelen en klik vervolgens op Hallo client die wordt gebruikt tooaccess uw apparaat.</span><span class="sxs-lookup"><span data-stu-id="acbac-120">You must enable remote management on hello device first, and then on hello client that is used tooaccess your device.</span></span>

<span data-ttu-id="acbac-121">Hallo stappen in dit artikel zijn uitgevoerd op een hostsysteem met Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="acbac-121">hello steps described in this article were performed on a host system running Windows Server 2012 R2.</span></span>

## <a name="connect-through-http"></a><span data-ttu-id="acbac-122">Verbinding maken via HTTP</span><span class="sxs-lookup"><span data-stu-id="acbac-122">Connect through HTTP</span></span>

<span data-ttu-id="acbac-123">Een tooWindows PowerShell voor StorSimple verbinding via een HTTP-sessie, biedt betere beveiliging dan verbinding maken via de seriële console Hallo van uw StorSimple-apparaat.</span><span class="sxs-lookup"><span data-stu-id="acbac-123">Connecting tooWindows PowerShell for StorSimple through an HTTP session offers more security than connecting through hello serial console of your StorSimple device.</span></span> <span data-ttu-id="acbac-124">Hoewel dit niet de meest beveiligde methode hello, is het is acceptabel in vertrouwde netwerken.</span><span class="sxs-lookup"><span data-stu-id="acbac-124">Although this is not hello most secure method, it is acceptable on trusted networks.</span></span>

<span data-ttu-id="acbac-125">U kunt beide hello Azure portal of Hallo seriële console tooconfigure extern beheer gebruiken.</span><span class="sxs-lookup"><span data-stu-id="acbac-125">You can use either hello Azure portal or hello serial console tooconfigure remote management.</span></span> <span data-ttu-id="acbac-126">Selecteer een van de Hallo procedures te volgen:</span><span class="sxs-lookup"><span data-stu-id="acbac-126">Select from hello following procedures:</span></span>

* [<span data-ttu-id="acbac-127">Hello Azure portal tooenable extern beheer via HTTP gebruiken</span><span class="sxs-lookup"><span data-stu-id="acbac-127">Use hello Azure portal tooenable remote management over HTTP</span></span>](#use-the-azure-classic-portal-to-enable-remote-management-over-http)
* [<span data-ttu-id="acbac-128">Hallo seriële console tooenable extern beheer via HTTP gebruiken</span><span class="sxs-lookup"><span data-stu-id="acbac-128">Use hello serial console tooenable remote management over HTTP</span></span>](#use-the-serial-console-to-enable-remote-management-over-http)

<span data-ttu-id="acbac-129">Nadat u extern beheer inschakelen, gebruikt u hello te volgen procedure tooprepare Hallo-client voor een externe verbinding.</span><span class="sxs-lookup"><span data-stu-id="acbac-129">After you enable remote management, use hello following procedure tooprepare hello client for a remote connection.</span></span>

* [<span data-ttu-id="acbac-130">Hallo-client voorbereiden voor externe verbinding</span><span class="sxs-lookup"><span data-stu-id="acbac-130">Prepare hello client for remote connection</span></span>](#prepare-the-client-for-remote-connection)

### <a name="use-hello-azure-portal-tooenable-remote-management-over-http"></a><span data-ttu-id="acbac-131">Hello Azure portal tooenable extern beheer via HTTP gebruiken</span><span class="sxs-lookup"><span data-stu-id="acbac-131">Use hello Azure portal tooenable remote management over HTTP</span></span>

<span data-ttu-id="acbac-132">Voer Hallo stappen te volgen in hello Azure portal tooenable extern beheer via HTTP.</span><span class="sxs-lookup"><span data-stu-id="acbac-132">Perform hello following steps in hello Azure portal tooenable remote management over HTTP.</span></span>

#### <a name="tooenable-remote-management-through-hello-azure-portal"></a><span data-ttu-id="acbac-133">tooenable extern beheer via hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="acbac-133">tooenable remote management through hello Azure portal</span></span>

1. <span data-ttu-id="acbac-134">Ga tooyour Apparaatbeheer StorSimple-service.</span><span class="sxs-lookup"><span data-stu-id="acbac-134">Go tooyour StorSimple Device Manager service.</span></span> <span data-ttu-id="acbac-135">Selecteer **apparaten** en selecteer en klikt u op de gewenste tooconfigure voor extern beheer van Hallo-apparaat.</span><span class="sxs-lookup"><span data-stu-id="acbac-135">Select **Devices** and then select and click hello device you want tooconfigure for remote management.</span></span> <span data-ttu-id="acbac-136">Ga te**apparaatinstellingen > beveiliging**.</span><span class="sxs-lookup"><span data-stu-id="acbac-136">Go too**Device settings > Security**.</span></span>
2. <span data-ttu-id="acbac-137">In Hallo **beveiligingsinstellingen** blade, klikt u op **extern beheer**.</span><span class="sxs-lookup"><span data-stu-id="acbac-137">In hello **Security settings** blade, click **Remote Management**.</span></span>
3. <span data-ttu-id="acbac-138">In Hallo **extern beheer** blade ingesteld **extern beheer inschakelen** te**Ja**.</span><span class="sxs-lookup"><span data-stu-id="acbac-138">In hello **Remote management** blade, set **Enable Remote Management** too**Yes**.</span></span>
4. <span data-ttu-id="acbac-139">U kunt nu tooconnect via HTTP.</span><span class="sxs-lookup"><span data-stu-id="acbac-139">You can now choose tooconnect using HTTP.</span></span> <span data-ttu-id="acbac-140">(Hallo standaardwaarde is tooconnect via HTTPS). Zorg ervoor dat HTTP is geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="acbac-140">(hello default is tooconnect over HTTPS.) Make sure that HTTP is selected.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="acbac-141">Verbinding maken via HTTP is alleen acceptabel in vertrouwde netwerken.</span><span class="sxs-lookup"><span data-stu-id="acbac-141">Connecting over HTTP is acceptable only on trusted networks.</span></span>
   
5. <span data-ttu-id="acbac-142">Klik op **opslaan** en wanneer u om bevestiging gevraagd, selecteert u **Ja**.</span><span class="sxs-lookup"><span data-stu-id="acbac-142">Click **Save** and when prompted for confirmation, select **Yes**.</span></span>

### <a name="use-hello-serial-console-tooenable-remote-management-over-http"></a><span data-ttu-id="acbac-143">Hallo seriële console tooenable extern beheer via HTTP gebruiken</span><span class="sxs-lookup"><span data-stu-id="acbac-143">Use hello serial console tooenable remote management over HTTP</span></span>
<span data-ttu-id="acbac-144">Hallo volgende stappen uit op Hallo apparaat seriële console tooenable extern beheer uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="acbac-144">Perform hello following steps on hello device serial console tooenable remote management.</span></span>

#### <a name="tooenable-remote-management-through-hello-device-serial-console"></a><span data-ttu-id="acbac-145">extern beheer via de seriële console van Hallo apparaat tooenable</span><span class="sxs-lookup"><span data-stu-id="acbac-145">tooenable remote management through hello device serial console</span></span>
1. <span data-ttu-id="acbac-146">Selecteer optie 1 Hallo seriële consolemenu.</span><span class="sxs-lookup"><span data-stu-id="acbac-146">On hello serial console menu, select option 1.</span></span> <span data-ttu-id="acbac-147">Voor meer informatie over het gebruik van de seriële console Hallo op Hallo apparaat gaat te[tooWindows PowerShell voor StorSimple-verbinding via de seriële console apparaat](storsimple-8000-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="acbac-147">For more information about using hello serial console on hello device, go too[Connect tooWindows PowerShell for StorSimple via device serial console](storsimple-8000-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).</span></span>
2. <span data-ttu-id="acbac-148">Hallo opdrachtprompt, typt u:`Enable-HcsRemoteManagement –AllowHttp`</span><span class="sxs-lookup"><span data-stu-id="acbac-148">At hello prompt, type: `Enable-HcsRemoteManagement –AllowHttp`</span></span>
3. <span data-ttu-id="acbac-149">U wordt geïnformeerd over Hallo beveiligingsproblemen van het gebruik van HTTP-tooconnect toohello apparaat.</span><span class="sxs-lookup"><span data-stu-id="acbac-149">You are notified about hello security vulnerabilities of using HTTP tooconnect toohello device.</span></span> <span data-ttu-id="acbac-150">Bevestig door op te geven wanneer u wordt gevraagd, **Y**.</span><span class="sxs-lookup"><span data-stu-id="acbac-150">When prompted, confirm by typing **Y**.</span></span>
4. <span data-ttu-id="acbac-151">Controleer of HTTP is ingeschakeld door te typen:`Get-HcsSystem`</span><span class="sxs-lookup"><span data-stu-id="acbac-151">Verify that HTTP is enabled by typing: `Get-HcsSystem`</span></span>
5. <span data-ttu-id="acbac-152">Controleer of deze Hallo **RemoteManagementMode** veld bevat **HttpsAndHttpEnabled**.hello volgende afbeelding ziet u deze instellingen in de PuTTY.</span><span class="sxs-lookup"><span data-stu-id="acbac-152">Verify that hello **RemoteManagementMode** field shows **HttpsAndHttpEnabled**.hello following illustration shows these settings in PuTTY.</span></span>
   
     ![Seriële HTTPS en HTTP-ingeschakeld](./media/storsimple-remote-connect/HCS_SerialHttpsAndHttpEnabled.png)

### <a name="prepare-hello-client-for-remote-connection"></a><span data-ttu-id="acbac-154">Hallo-client voorbereiden voor externe verbinding</span><span class="sxs-lookup"><span data-stu-id="acbac-154">Prepare hello client for remote connection</span></span>
<span data-ttu-id="acbac-155">Hallo volgende stappen uit op Hallo client tooenable extern beheer uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="acbac-155">Perform hello following steps on hello client tooenable remote management.</span></span>

#### <a name="tooprepare-hello-client-for-remote-connection"></a><span data-ttu-id="acbac-156">tooprepare Hallo-client voor externe verbinding</span><span class="sxs-lookup"><span data-stu-id="acbac-156">tooprepare hello client for remote connection</span></span>
1. <span data-ttu-id="acbac-157">Start een Windows PowerShell-sessie als administrator.</span><span class="sxs-lookup"><span data-stu-id="acbac-157">Start a Windows PowerShell session as an administrator.</span></span>
2. <span data-ttu-id="acbac-158">Type Hallo volgende opdracht tooadd Hallo IP-adres van de lijst met vertrouwde hosts Hallo StorSimple-apparaat toohello van client:</span><span class="sxs-lookup"><span data-stu-id="acbac-158">Type hello following command tooadd hello IP address of hello StorSimple device toohello client’s trusted hosts list:</span></span>
   
     `Set-Item wsman:\localhost\Client\TrustedHosts <device_ip> -Concatenate -Force`
   
     <span data-ttu-id="acbac-159">Vervang <*device_ip*> met Hallo IP-adres van uw apparaat; bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="acbac-159">Replace <*device_ip*> with hello IP address of your device; for example:</span></span> 
   
     `Set-Item wsman:\localhost\Client\TrustedHosts 10.126.173.90 -Concatenate -Force`
3. <span data-ttu-id="acbac-160">Type Hallo opdracht toosave Hallo apparaat referenties in een variabele te volgen:</span><span class="sxs-lookup"><span data-stu-id="acbac-160">Type hello following command toosave hello device credentials in a variable:</span></span> 
   
    ```
    $cred = Get-Credential
    ```
    
4. <span data-ttu-id="acbac-161">In het dialoogvenster Hallo die wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="acbac-161">In hello dialog box that appears:</span></span>
   
   1. <span data-ttu-id="acbac-162">Typ de gebruikersnaam in deze indeling Hallo: *device_ip\SSAdmin*.</span><span class="sxs-lookup"><span data-stu-id="acbac-162">Type hello user name in this format: *device_ip\SSAdmin*.</span></span>
   2. <span data-ttu-id="acbac-163">Typ beheerderswachtwoord van het Hallo-apparaat dat is ingesteld wanneer het Hallo-apparaat is geconfigureerd met de wizard setup Hallo.</span><span class="sxs-lookup"><span data-stu-id="acbac-163">Type hello device administrator password that was set when hello device was configured with hello setup wizard.</span></span> <span data-ttu-id="acbac-164">is het standaardwachtwoord Hallo *Wachtwoord1*.</span><span class="sxs-lookup"><span data-stu-id="acbac-164">hello default password is *Password1*.</span></span>
5. <span data-ttu-id="acbac-165">Start een Windows PowerShell-sessie op Hallo apparaat door deze opdracht te typen:</span><span class="sxs-lookup"><span data-stu-id="acbac-165">Start a Windows PowerShell session on hello device by typing this command:</span></span>
   
     `Enter-PSSession -Credential $cred -ConfigurationName SSAdminConsole -ComputerName <device_ip>`
   
   > [!NOTE]
   > <span data-ttu-id="acbac-166">toocreate een Windows PowerShell-sessie voor gebruik met Hallo virtuele StorSimple-apparaat, append Hallo `–Port` parameter en geef Hallo openbare poort die u hebt geconfigureerd in externe toegang voor virtueel StorSimple-apparaat.</span><span class="sxs-lookup"><span data-stu-id="acbac-166">toocreate a Windows PowerShell session for use with hello StorSimple virtual device, append hello `–Port` parameter and specify hello public port that you configured in Remoting for StorSimple Virtual Appliance.</span></span>
   
   
<span data-ttu-id="acbac-167">Op dit moment hebt u een actieve externe Windows PowerShell-sessie toohello apparaat.</span><span class="sxs-lookup"><span data-stu-id="acbac-167">At this point, you should have an active remote Windows PowerShell session toohello device.</span></span>
   
![Externe communicatie via HTTP met PowerShell](./media/storsimple-remote-connect/HCS_PSRemotingUsingHTTP.png)

## <a name="connect-through-https"></a><span data-ttu-id="acbac-169">Verbinding maken via HTTPS</span><span class="sxs-lookup"><span data-stu-id="acbac-169">Connect through HTTPS</span></span>

<span data-ttu-id="acbac-170">Een tooWindows PowerShell voor StorSimple verbinding via een HTTPS-sessie Hallo veiligste en aanbevolen methode van Microsoft Azure StorSimple-apparaat voor op afstand verbinding tooyour.</span><span class="sxs-lookup"><span data-stu-id="acbac-170">Connecting tooWindows PowerShell for StorSimple through an HTTPS session is hello most secure and recommended method of remotely connecting tooyour Microsoft Azure StorSimple device.</span></span> <span data-ttu-id="acbac-171">Hallo volgen procedures wordt uitgelegd hoe tooset up Hallo seriële console en client-computers zodat u kunt HTTPS tooconnect tooWindows PowerShell voor StorSimple.</span><span class="sxs-lookup"><span data-stu-id="acbac-171">hello following procedures explain how tooset up hello serial console and client computers so that you can use HTTPS tooconnect tooWindows PowerShell for StorSimple.</span></span>

<span data-ttu-id="acbac-172">U kunt beide hello Azure portal of Hallo seriële console tooconfigure extern beheer gebruiken.</span><span class="sxs-lookup"><span data-stu-id="acbac-172">You can use either hello Azure portal or hello serial console tooconfigure remote management.</span></span> <span data-ttu-id="acbac-173">Selecteer een van de Hallo procedures te volgen:</span><span class="sxs-lookup"><span data-stu-id="acbac-173">Select from hello following procedures:</span></span>

* [<span data-ttu-id="acbac-174">Hello Azure portal tooenable extern beheer via HTTPS gebruiken</span><span class="sxs-lookup"><span data-stu-id="acbac-174">Use hello Azure portal tooenable remote management over HTTPS</span></span>](#use-the-azure-classic-portal-to-enable-remote-management-over-https)
* [<span data-ttu-id="acbac-175">Hallo seriële console tooenable extern beheer via HTTPS gebruiken</span><span class="sxs-lookup"><span data-stu-id="acbac-175">Use hello serial console tooenable remote management over HTTPS</span></span>](#use-the-serial-console-to-enable-remote-management-over-https)

<span data-ttu-id="acbac-176">Nadat u extern beheer inschakelen, Hallo procedures tooprepare Hallo host voor een extern beheer na gebruik en toohello apparaat verbinden van de externe host Hallo.</span><span class="sxs-lookup"><span data-stu-id="acbac-176">After you enable remote management, use hello following procedures tooprepare hello host for a remote management and connect toohello device from hello remote host.</span></span>

* [<span data-ttu-id="acbac-177">Hallo host voorbereiden voor extern beheer</span><span class="sxs-lookup"><span data-stu-id="acbac-177">Prepare hello host for remote management</span></span>](#prepare-the-host-for-remote-management)
* [<span data-ttu-id="acbac-178">Verbinding maken met toohello apparaat van de externe host Hallo</span><span class="sxs-lookup"><span data-stu-id="acbac-178">Connect toohello device from hello remote host</span></span>](#connect-to-the-device-from-the-remote-host)

### <a name="use-hello-azure-portal-tooenable-remote-management-over-https"></a><span data-ttu-id="acbac-179">Hello Azure portal tooenable extern beheer via HTTPS gebruiken</span><span class="sxs-lookup"><span data-stu-id="acbac-179">Use hello Azure portal tooenable remote management over HTTPS</span></span>

<span data-ttu-id="acbac-180">Voer Hallo stappen te volgen in hello Azure portal tooenable extern beheer via HTTPS.</span><span class="sxs-lookup"><span data-stu-id="acbac-180">Perform hello following steps in hello Azure portal tooenable remote management over HTTPS.</span></span>

#### <a name="tooenable-remote-management-over-https-from-hello-azure-portal"></a><span data-ttu-id="acbac-181">tooenable remote management via HTTPS van hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="acbac-181">tooenable remote management over HTTPS from hello Azure portal</span></span>

1. <span data-ttu-id="acbac-182">Ga tooyour Apparaatbeheer StorSimple-service.</span><span class="sxs-lookup"><span data-stu-id="acbac-182">Go tooyour StorSimple Device Manager service.</span></span> <span data-ttu-id="acbac-183">Selecteer **apparaten** en selecteer en klikt u op de gewenste tooconfigure voor extern beheer van Hallo-apparaat.</span><span class="sxs-lookup"><span data-stu-id="acbac-183">Select **Devices** and then select and click hello device you want tooconfigure for remote management.</span></span> <span data-ttu-id="acbac-184">Ga te**apparaatinstellingen > beveiliging**.</span><span class="sxs-lookup"><span data-stu-id="acbac-184">Go too**Device settings > Security**.</span></span>
2. <span data-ttu-id="acbac-185">In Hallo **beveiligingsinstellingen** blade, klikt u op **extern beheer**.</span><span class="sxs-lookup"><span data-stu-id="acbac-185">In hello **Security settings** blade, click **Remote Management**.</span></span>
3. <span data-ttu-id="acbac-186">Stel **extern beheer inschakelen** te**Ja**.</span><span class="sxs-lookup"><span data-stu-id="acbac-186">Set **Enable Remote Management** too**Yes**.</span></span>
4. <span data-ttu-id="acbac-187">U kunt nu tooconnect via HTTPS.</span><span class="sxs-lookup"><span data-stu-id="acbac-187">You can now choose tooconnect using HTTPS.</span></span> <span data-ttu-id="acbac-188">(Hallo standaardwaarde is tooconnect via HTTPS). Zorg ervoor dat HTTPS is geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="acbac-188">(hello default is tooconnect over HTTPS.) Make sure that HTTPS is selected.</span></span>
5. <span data-ttu-id="acbac-189">Klik op... en klik vervolgens op **certificaat voor extern beheer downloaden**.</span><span class="sxs-lookup"><span data-stu-id="acbac-189">Click ... and then click **Download Remote Management Certificate**.</span></span> <span data-ttu-id="acbac-190">Geef een locatie toosave dit bestand.</span><span class="sxs-lookup"><span data-stu-id="acbac-190">Specify a location toosave this file.</span></span> <span data-ttu-id="acbac-191">U moet dit certificaat op de client of hostcomputer computer Hallo die u tooconnect toohello apparaat gebruikt tooinstall.</span><span class="sxs-lookup"><span data-stu-id="acbac-191">You need tooinstall this certificate on hello client or host computer that you will use tooconnect toohello device.</span></span>
6. <span data-ttu-id="acbac-192">Klik op **opslaan** en klik vervolgens op **Ja** wanneer u om bevestiging wordt gevraagd.</span><span class="sxs-lookup"><span data-stu-id="acbac-192">Click **Save** and then click **Yes** when prompted for confirmation.</span></span>

### <a name="use-hello-serial-console-tooenable-remote-management-over-https"></a><span data-ttu-id="acbac-193">Hallo seriële console tooenable extern beheer via HTTPS gebruiken</span><span class="sxs-lookup"><span data-stu-id="acbac-193">Use hello serial console tooenable remote management over HTTPS</span></span>

<span data-ttu-id="acbac-194">Hallo volgende stappen uit op Hallo apparaat seriële console tooenable extern beheer uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="acbac-194">Perform hello following steps on hello device serial console tooenable remote management.</span></span>

#### <a name="tooenable-remote-management-through-hello-device-serial-console"></a><span data-ttu-id="acbac-195">extern beheer via de seriële console van Hallo apparaat tooenable</span><span class="sxs-lookup"><span data-stu-id="acbac-195">tooenable remote management through hello device serial console</span></span>
1. <span data-ttu-id="acbac-196">Selecteer optie 1 Hallo seriële consolemenu.</span><span class="sxs-lookup"><span data-stu-id="acbac-196">On hello serial console menu, select option 1.</span></span> <span data-ttu-id="acbac-197">Voor meer informatie over het gebruik van de seriële console Hallo op Hallo apparaat gaat te[tooWindows PowerShell voor StorSimple-verbinding via de seriële console apparaat](storsimple-8000-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="acbac-197">For more information about using hello serial console on hello device, go too[Connect tooWindows PowerShell for StorSimple via device serial console](storsimple-8000-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).</span></span>
2. <span data-ttu-id="acbac-198">Hallo opdrachtprompt, typt u:</span><span class="sxs-lookup"><span data-stu-id="acbac-198">At hello prompt, type:</span></span>
   
     `Enable-HcsRemoteManagement`
   
    <span data-ttu-id="acbac-199">Dit moet HTTPS inschakelen op uw apparaat.</span><span class="sxs-lookup"><span data-stu-id="acbac-199">This should enable HTTPS on your device.</span></span>
3. <span data-ttu-id="acbac-200">Controleer of HTTPS is ingeschakeld door te typen:</span><span class="sxs-lookup"><span data-stu-id="acbac-200">Verify that HTTPS has been enabled by typing:</span></span> 
   
     `Get-HcsSystem`
   
    <span data-ttu-id="acbac-201">Zorg ervoor dat Hallo **RemoteManagementMode** veld bevat **HttpsEnabled**.hello volgende afbeelding ziet u deze instellingen in de PuTTY.</span><span class="sxs-lookup"><span data-stu-id="acbac-201">Make sure that hello **RemoteManagementMode** field shows **HttpsEnabled**.hello following illustration shows these settings in PuTTY.</span></span>
   
     ![Seriële HTTPS-functionaliteit](./media/storsimple-remote-connect/HCS_SerialHttpsEnabled.png)
4. <span data-ttu-id="acbac-203">Vanuit de uitvoer Hallo van `Get-HcsSystem`, serienummer Hallo Hallo apparaat kopiëren en opslaan voor later gebruik.</span><span class="sxs-lookup"><span data-stu-id="acbac-203">From hello output of `Get-HcsSystem`, copy hello serial number of hello device and save it for later use.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="acbac-204">Hallo serienummer maps toohello CN-naam in Hallo certificaat.</span><span class="sxs-lookup"><span data-stu-id="acbac-204">hello serial number maps toohello CN name in hello certificate.</span></span>
   
5. <span data-ttu-id="acbac-205">Een certificaat voor extern beheer verkrijgen door te typen:</span><span class="sxs-lookup"><span data-stu-id="acbac-205">Obtain a remote management certificate by typing:</span></span> 
   
     `Get-HcsRemoteManagementCert`
   
    <span data-ttu-id="acbac-206">Een certificaat vergelijkbare toohello volgende wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="acbac-206">A certificate similar toohello following will appear.</span></span>
   
    ![Extern beheercertificaat ophalen](./media/storsimple-remote-connect/HCS_GetRemoteManagementCertificate.png)
6. <span data-ttu-id="acbac-208">Hallo gegevens kopiëren in Hallo-certificaat van **---BEGIN CERTIFICATE---** te**---EINDCERTIFICAAT---** in een teksteditor zoals Kladblok en sla deze op te geven als een .cer-bestand.</span><span class="sxs-lookup"><span data-stu-id="acbac-208">Copy hello information in hello certificate from **-----BEGIN CERTIFICATE-----** too**-----END CERTIFICATE-----** into a text editor such as Notepad, and save it as a .cer file.</span></span> <span data-ttu-id="acbac-209">(Kopieert u dit bestand tooyour externe host wanneer u Hallo host voorbereidt.)</span><span class="sxs-lookup"><span data-stu-id="acbac-209">(You will copy this file tooyour remote host when you prepare hello host.)</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="acbac-210">een nieuw certificaat toogenerate gebruiken Hallo `Set-HcsRemoteManagementCert` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="acbac-210">toogenerate a new certificate, use hello `Set-HcsRemoteManagementCert` cmdlet.</span></span>
   
### <a name="prepare-hello-host-for-remote-management"></a><span data-ttu-id="acbac-211">Hallo host voorbereiden voor extern beheer</span><span class="sxs-lookup"><span data-stu-id="acbac-211">Prepare hello host for remote management</span></span>

<span data-ttu-id="acbac-212">het Hallo-hostcomputer tooprepare voor een externe verbinding die gebruikmaakt van een HTTPS-sessie uitvoeren Hallo procedures te volgen:</span><span class="sxs-lookup"><span data-stu-id="acbac-212">tooprepare hello host computer for a remote connection that uses an HTTPS session, perform hello following procedures:</span></span>

* <span data-ttu-id="acbac-213">[Importeren Hallo cer-bestand in de basisarchief Hallo van Hallo-client of de externe host](#to-import-the-certificate-on-the-remote-host).</span><span class="sxs-lookup"><span data-stu-id="acbac-213">[Import hello .cer file into hello root store of hello client or remote host](#to-import-the-certificate-on-the-remote-host).</span></span>
* <span data-ttu-id="acbac-214">[Hallo apparaat serienummers toohello hosts-bestand op de externe host toevoegen](#to-add-device-serial-numbers-to-the-remote-host).</span><span class="sxs-lookup"><span data-stu-id="acbac-214">[Add hello device serial numbers toohello hosts file on your remote host](#to-add-device-serial-numbers-to-the-remote-host).</span></span>

<span data-ttu-id="acbac-215">Elk van de voorgaande procedures, Hallo wordt hieronder beschreven.</span><span class="sxs-lookup"><span data-stu-id="acbac-215">Each of hello preceding procedures, is described below.</span></span>

#### <a name="tooimport-hello-certificate-on-hello-remote-host"></a><span data-ttu-id="acbac-216">tooimport hello certificaat op de externe host Hallo</span><span class="sxs-lookup"><span data-stu-id="acbac-216">tooimport hello certificate on hello remote host</span></span>
1. <span data-ttu-id="acbac-217">Met de rechtermuisknop op Hallo cer-bestand en selecteer **installeren certificaat**.</span><span class="sxs-lookup"><span data-stu-id="acbac-217">Right-click hello .cer file and select **Install certificate**.</span></span> <span data-ttu-id="acbac-218">Hallo Wizard Certificaat importeren wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="acbac-218">This starts hello Certificate Import Wizard.</span></span>
   
    ![Wizard Certificaat importeren 1](./media/storsimple-remote-connect/HCS_CertificateImportWizard1.png)
2. <span data-ttu-id="acbac-220">Voor **archieflocatie**, selecteer **lokale Machine**, en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="acbac-220">For **Store location**, select **Local Machine**, and then click **Next**.</span></span>
3. <span data-ttu-id="acbac-221">Selecteer **alle certificaten in Hallo volgende archief plaatsen**, en klik vervolgens op **Bladeren**.</span><span class="sxs-lookup"><span data-stu-id="acbac-221">Select **Place all certificates in hello following store**, and then click **Browse**.</span></span> <span data-ttu-id="acbac-222">Navigeer toohello basisarchief van de externe host, en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="acbac-222">Navigate toohello root store of your remote host, and then click **Next**.</span></span>
   
    ![Wizard Certificaat importeren 2](./media/storsimple-remote-connect/HCS_CertificateImportWizard2.png)
4. <span data-ttu-id="acbac-224">Klik op **Voltooien**.</span><span class="sxs-lookup"><span data-stu-id="acbac-224">Click **Finish**.</span></span> <span data-ttu-id="acbac-225">Er verschijnt een bericht dat aangeeft dat Hallo importeren geslaagd is.</span><span class="sxs-lookup"><span data-stu-id="acbac-225">A message that tells you that hello import was successful appears.</span></span>
   
    ![Wizard Certificaat importeren 3](./media/storsimple-remote-connect/HCS_CertificateImportWizard3.png)

#### <a name="tooadd-device-serial-numbers-toohello-remote-host"></a><span data-ttu-id="acbac-227">tooadd apparaat serienummers toohello externe host</span><span class="sxs-lookup"><span data-stu-id="acbac-227">tooadd device serial numbers toohello remote host</span></span>
1. <span data-ttu-id="acbac-228">Kladblok start als beheerder en open vervolgens Hallo hosts-bestand op \Windows\System32\Drivers\etc.</span><span class="sxs-lookup"><span data-stu-id="acbac-228">Start Notepad as an administrator, and then open hello hosts file located at \Windows\System32\Drivers\etc.</span></span>
2. <span data-ttu-id="acbac-229">Hallo na drie vermeldingen tooyour hosts-bestand toevoegen: **DATA 0-IP-adres**, **Controller 0 vast IP-adres**, en **Controller 1 vast IP-adres**.</span><span class="sxs-lookup"><span data-stu-id="acbac-229">Add hello following three entries tooyour hosts file: **DATA 0 IP address**, **Controller 0 Fixed IP address**, and **Controller 1 Fixed IP address**.</span></span>
3. <span data-ttu-id="acbac-230">Voer het serienummer van het Hallo-apparaat dat u eerder hebt opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="acbac-230">Enter hello device serial number that you saved earlier.</span></span> <span data-ttu-id="acbac-231">Dit toohello IP-adres toewijzen zoals weergegeven in Hallo installatiekopie te volgen.</span><span class="sxs-lookup"><span data-stu-id="acbac-231">Map this toohello IP address as shown in hello following image.</span></span> <span data-ttu-id="acbac-232">Voor Controller 0 en Controller 1 toevoegen **Controller0** en **Controller1** aan Hallo einde van het serienummer hello (CN-naam).</span><span class="sxs-lookup"><span data-stu-id="acbac-232">For Controller 0 and Controller 1, append **Controller0** and **Controller1** at hello end of hello serial number (CN name).</span></span>
   
    ![CN-naam toohosts bestand toe te voegen](./media/storsimple-remote-connect/HCS_AddingCNNameToHostsFile.png)
4. <span data-ttu-id="acbac-234">Hallo hosts-bestand opslaan.</span><span class="sxs-lookup"><span data-stu-id="acbac-234">Save hello hosts file.</span></span>

### <a name="connect-toohello-device-from-hello-remote-host"></a><span data-ttu-id="acbac-235">Verbinding maken met toohello apparaat van de externe host Hallo</span><span class="sxs-lookup"><span data-stu-id="acbac-235">Connect toohello device from hello remote host</span></span>

<span data-ttu-id="acbac-236">Gebruik Windows PowerShell- en SSL tooenter een SSAdmin-sessie op uw apparaat vanaf een externe host of de client.</span><span class="sxs-lookup"><span data-stu-id="acbac-236">Use Windows PowerShell and SSL tooenter an SSAdmin session on your device from a remote host or client.</span></span> <span data-ttu-id="acbac-237">Hallo SSAdmin sessie toegewezen toooption 1 in Hallo [seriële console](storsimple-8000-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console) menu van uw apparaat.</span><span class="sxs-lookup"><span data-stu-id="acbac-237">hello SSAdmin session maps toooption 1 in hello [serial console](storsimple-8000-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console) menu of your device.</span></span>

<span data-ttu-id="acbac-238">Hallo na de procedure op Hallo computer van waaruit u toomake Hallo externe Windows PowerShell verbinding wilt uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="acbac-238">Perform hello following procedure on hello computer from which you want toomake hello remote Windows PowerShell connection.</span></span>

#### <a name="tooenter-an-ssadmin-session-on-hello-device-by-using-windows-powershell-and-ssl"></a><span data-ttu-id="acbac-239">tooenter een SSAdmin-sessie op Hallo apparaat via Windows PowerShell- en SSL</span><span class="sxs-lookup"><span data-stu-id="acbac-239">tooenter an SSAdmin session on hello device by using Windows PowerShell and SSL</span></span>
1. <span data-ttu-id="acbac-240">Start een Windows PowerShell-sessie als administrator.</span><span class="sxs-lookup"><span data-stu-id="acbac-240">Start a Windows PowerShell session as an administrator.</span></span>
2. <span data-ttu-id="acbac-241">Hallo IP-adres toohello apparaatclient van vertrouwde hosts toevoegen door te typen:</span><span class="sxs-lookup"><span data-stu-id="acbac-241">Add hello device IP address toohello client’s trusted hosts by typing:</span></span>
   
     `Set-Item wsman:\localhost\Client\TrustedHosts <device_ip> -Concatenate -Force`
   
    <span data-ttu-id="acbac-242">Waarbij <*device_ip*> Hallo IP-adres van uw apparaat is; bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="acbac-242">Where <*device_ip*> is hello IP address of your device; for example:</span></span> 
   
     `Set-Item wsman:\localhost\Client\TrustedHosts 10.126.173.90 -Concatenate -Force`
3. <span data-ttu-id="acbac-243">een nieuwe referentie toocreate typt u:</span><span class="sxs-lookup"><span data-stu-id="acbac-243">toocreate a new credential, type:</span></span>
   
     `$cred = New-Object pscredential @("<IP of target device>\SSAdmin", (ConvertTo-SecureString -Force -AsPlainText "<Device Administrator Password>"))`
   
    <span data-ttu-id="acbac-244">Waarbij <*IP-adres van het doelapparaat*> Hallo IP-adres van de DATA 0 voor uw apparaat; bijvoorbeeld **10.126.173.90** zoals weergegeven in de voorafgaande aan de installatiekopie van het hosts-bestand Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="acbac-244">Where <*IP of target device*> is hello IP address of DATA 0 for your device; for example, **10.126.173.90** as shown in hello preceding image of hello hosts file.</span></span> <span data-ttu-id="acbac-245">Hallo beheerderswachtwoord voor uw apparaat ook opgeven.</span><span class="sxs-lookup"><span data-stu-id="acbac-245">Also, supply hello administrator password for your device.</span></span>
4. <span data-ttu-id="acbac-246">Een sessie maken door te typen:</span><span class="sxs-lookup"><span data-stu-id="acbac-246">Create a session by typing:</span></span>
   
     `$session = New-PSSession -UseSSL -ComputerName <Serial number of target device> -Credential $cred -ConfigurationName "SSAdminConsole"`
   
    <span data-ttu-id="acbac-247">Hallo - ComputerName parameter in Hallo-cmdlet, bieden Hallo <*serienummer van het doelapparaat*>.</span><span class="sxs-lookup"><span data-stu-id="acbac-247">For hello -ComputerName parameter in hello cmdlet, provide hello <*serial number of target device*>.</span></span> <span data-ttu-id="acbac-248">Dit serienummer is toegewezen toohello IP-adres van de DATA 0 Hallo hostbestand op de externe host; bijvoorbeeld: **SHX0991003G44MT** zoals weergegeven in Hallo installatiekopie te volgen.</span><span class="sxs-lookup"><span data-stu-id="acbac-248">This serial number was mapped toohello IP address of DATA 0 in hello hosts file on your remote host; for example, **SHX0991003G44MT** as shown in hello following image.</span></span>
5. <span data-ttu-id="acbac-249">Type:</span><span class="sxs-lookup"><span data-stu-id="acbac-249">Type:</span></span>
   
     `Enter-PSSession $session`
6. <span data-ttu-id="acbac-250">U toowait moet een paar minuten en vervolgens kunt u zich verbonden tooyour apparaat via HTTPS via SSL.</span><span class="sxs-lookup"><span data-stu-id="acbac-250">You will need toowait a few minutes, and then you will be connected tooyour device via HTTPS over SSL.</span></span> <span data-ttu-id="acbac-251">U ziet een bericht dat aangeeft dat u verbonden tooyour apparaat.</span><span class="sxs-lookup"><span data-stu-id="acbac-251">You see a message that indicates you are connected tooyour device.</span></span>
   
    ![PowerShell voor externe toegang met behulp van HTTPS- en SSL](./media/storsimple-remote-connect/HCS_PSRemotingUsingHTTPSAndSSL.png)

## <a name="next-steps"></a><span data-ttu-id="acbac-253">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="acbac-253">Next steps</span></span>

* <span data-ttu-id="acbac-254">Meer informatie over [uw StorSimple-apparaat met behulp van Windows PowerShell tooadminister](storsimple-8000-windows-powershell-administration.md).</span><span class="sxs-lookup"><span data-stu-id="acbac-254">Learn more about [using Windows PowerShell tooadminister your StorSimple device](storsimple-8000-windows-powershell-administration.md).</span></span>
* <span data-ttu-id="acbac-255">Meer informatie over [StorSimple Apparaatbeheer service tooadminister uw StorSimple-apparaat met behulp van Hallo](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="acbac-255">Learn more about [using hello StorSimple Device Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

