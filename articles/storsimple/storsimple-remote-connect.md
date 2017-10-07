---
title: aaaConnect op afstand tooyour StorSimple-apparaat | Microsoft Docs
description: Legt uit hoe tooconfigure uw apparaat voor extern beheer en hoe tooconnect tooWindows PowerShell voor StorSimple via HTTP of HTTPS.
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 923377aa-f451-4656-87de-5e95a34a6a2a
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 55ed8fcdd997901301e0adc164a302216cde0332
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-remotely-tooyour-storsimple-8000-series-device"></a><span data-ttu-id="0ad61-103">Tooyour StorSimple 8000 series apparaat op afstand verbinding maken</span><span class="sxs-lookup"><span data-stu-id="0ad61-103">Connect remotely tooyour StorSimple 8000 series device</span></span>

## <a name="overview"></a><span data-ttu-id="0ad61-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="0ad61-104">Overview</span></span>
<span data-ttu-id="0ad61-105">U kunt Windows PowerShell voor externe toegang tooconnect tooyour StorSimple-apparaat gebruiken.</span><span class="sxs-lookup"><span data-stu-id="0ad61-105">You can use Windows PowerShell remoting tooconnect tooyour StorSimple device.</span></span> <span data-ttu-id="0ad61-106">Als u op deze manier verbinding, ziet u een menu.</span><span class="sxs-lookup"><span data-stu-id="0ad61-106">When you connect this way, you will not see a menu.</span></span> <span data-ttu-id="0ad61-107">(Ziet u een menu alleen als u de seriële console Hallo op Hallo apparaat tooconnect gebruiken.) Met Windows PowerShell op afstand, moet u specifieke runspace tooa verbinden.</span><span class="sxs-lookup"><span data-stu-id="0ad61-107">(You see a menu only if you use hello serial console on hello device tooconnect.) With Windows PowerShell remoting, you connect tooa specific runspace.</span></span> <span data-ttu-id="0ad61-108">U kunt ook de weergavetaal Hallo opgeven.</span><span class="sxs-lookup"><span data-stu-id="0ad61-108">You can also specify hello display language.</span></span> 

<span data-ttu-id="0ad61-109">Voor meer informatie over het gebruik van Windows PowerShell voor externe toegang toomanage uw apparaat gaat te[gebruik Windows PowerShell voor StorSimple tooadminister uw StorSimple-apparaat](storsimple-windows-powershell-administration.md).</span><span class="sxs-lookup"><span data-stu-id="0ad61-109">For more information about using Windows PowerShell remoting toomanage your device, go too[Use Windows PowerShell for StorSimple tooadminister your StorSimple device](storsimple-windows-powershell-administration.md).</span></span>

<span data-ttu-id="0ad61-110">Deze zelfstudie wordt uitgelegd hoe tooconfigure uw apparaat voor extern beheer en klikt u vervolgens het tooconnect tooWindows PowerShell voor StorSimple.</span><span class="sxs-lookup"><span data-stu-id="0ad61-110">This tutorial explains how tooconfigure your device for remote management and then how tooconnect tooWindows PowerShell for StorSimple.</span></span> <span data-ttu-id="0ad61-111">Hier kunt u HTTP of HTTPS tooconnect via Windows PowerShell op afstand.</span><span class="sxs-lookup"><span data-stu-id="0ad61-111">You can use HTTP or HTTPS tooconnect via Windows PowerShell remoting.</span></span> <span data-ttu-id="0ad61-112">Echter, wanneer u beslist hoe tooconnect tooWindows PowerShell voor StorSimple, houd rekening met Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="0ad61-112">However, when you are deciding how tooconnect tooWindows PowerShell for StorSimple, consider hello following:</span></span> 

* <span data-ttu-id="0ad61-113">Toohello rechtstreeks verbinding maken de seriële console apparaat beveiligd is, maar verbindende toohello seriële console via netwerkswitches is niet.</span><span class="sxs-lookup"><span data-stu-id="0ad61-113">Connecting directly toohello device serial console is secure, but connecting toohello serial console over network switches is not.</span></span> <span data-ttu-id="0ad61-114">Wees voorzichtig met van Hallo beveiligingsrisico, omdat het toohello de seriële console apparaat via netwerkswitches verbinding te maken.</span><span class="sxs-lookup"><span data-stu-id="0ad61-114">Be cautious of hello security risk when connecting toohello device serial console over network switches.</span></span> 
* <span data-ttu-id="0ad61-115">Verbinding maken via een HTTP-sessie biedt meer beveiliging dan verbinding maken via de seriële console Hallo via Hallo netwerk mogelijk.</span><span class="sxs-lookup"><span data-stu-id="0ad61-115">Connecting through an HTTP session might offer more security than connecting through hello serial console over hello network.</span></span> <span data-ttu-id="0ad61-116">Hoewel dit niet de meest beveiligde methode hello, is het is acceptabel in vertrouwde netwerken.</span><span class="sxs-lookup"><span data-stu-id="0ad61-116">Although this is not hello most secure method, it is acceptable on trusted networks.</span></span> 
* <span data-ttu-id="0ad61-117">Verbinding maken via een HTTPS-sessie met een zelfondertekend certificaat is Hallo veiligste en aanbevolen optie Hallo.</span><span class="sxs-lookup"><span data-stu-id="0ad61-117">Connecting through an HTTPS session with a self-signed certificate is hello most secure and hello recommended option.</span></span>

<span data-ttu-id="0ad61-118">U kunt verbinden op afstand toohello Windows PowerShell-interface.</span><span class="sxs-lookup"><span data-stu-id="0ad61-118">You can connect remotely toohello Windows PowerShell interface.</span></span> <span data-ttu-id="0ad61-119">Externe toegang tooyour StorSimple-apparaat via Windows PowerShell-interface Hallo is echter niet standaard ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="0ad61-119">However, remote access tooyour StorSimple device via hello Windows PowerShell interface is not enabled by default.</span></span> <span data-ttu-id="0ad61-120">U moet extern beheer van de tooenable op Hallo apparaat eerst en klik vervolgens op Hallo client die wordt gebruikt tooaccess uw apparaat.</span><span class="sxs-lookup"><span data-stu-id="0ad61-120">You need tooenable remote management on hello device first, and then on hello client that is used tooaccess your device.</span></span>

<span data-ttu-id="0ad61-121">Hallo stappen in dit artikel zijn uitgevoerd op een hostsysteem met Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="0ad61-121">hello steps described in this article were performed on a host system running Windows Server 2012 R2.</span></span>

## <a name="connect-through-http"></a><span data-ttu-id="0ad61-122">Verbinding maken via HTTP</span><span class="sxs-lookup"><span data-stu-id="0ad61-122">Connect through HTTP</span></span>
<span data-ttu-id="0ad61-123">Een tooWindows PowerShell voor StorSimple verbinding via een HTTP-sessie, biedt betere beveiliging dan verbinding maken via de seriële console Hallo van uw StorSimple-apparaat.</span><span class="sxs-lookup"><span data-stu-id="0ad61-123">Connecting tooWindows PowerShell for StorSimple through an HTTP session offers more security than connecting through hello serial console of your StorSimple device.</span></span> <span data-ttu-id="0ad61-124">Hoewel dit niet de meest beveiligde methode hello, is het is acceptabel in vertrouwde netwerken.</span><span class="sxs-lookup"><span data-stu-id="0ad61-124">Although this is not hello most secure method, it is acceptable on trusted networks.</span></span>

<span data-ttu-id="0ad61-125">U kunt Hallo klassieke Azure-portal of Hallo seriële console tooconfigure extern beheer gebruiken.</span><span class="sxs-lookup"><span data-stu-id="0ad61-125">You can use either hello Azure classic portal or hello serial console tooconfigure remote management.</span></span> <span data-ttu-id="0ad61-126">Selecteer een van de Hallo procedures te volgen:</span><span class="sxs-lookup"><span data-stu-id="0ad61-126">Select from hello following procedures:</span></span>

* [<span data-ttu-id="0ad61-127">Hello Azure classic portal tooenable extern beheer via HTTP gebruiken</span><span class="sxs-lookup"><span data-stu-id="0ad61-127">Use hello Azure classic portal tooenable remote management over HTTP</span></span>](#use-the-azure-classic-portal-to-enable-remote-management-over-http)
* [<span data-ttu-id="0ad61-128">Hallo seriële console tooenable extern beheer via HTTP gebruiken</span><span class="sxs-lookup"><span data-stu-id="0ad61-128">Use hello serial console tooenable remote management over HTTP</span></span>](#use-the-serial-console-to-enable-remote-management-over-http)

<span data-ttu-id="0ad61-129">Nadat u extern beheer inschakelen, gebruikt u hello te volgen procedure tooprepare Hallo-client voor een externe verbinding.</span><span class="sxs-lookup"><span data-stu-id="0ad61-129">After you enable remote management, use hello following procedure tooprepare hello client for a remote connection.</span></span>

* [<span data-ttu-id="0ad61-130">Hallo-client voorbereiden voor externe verbinding</span><span class="sxs-lookup"><span data-stu-id="0ad61-130">Prepare hello client for remote connection</span></span>](#prepare-the-client-for-remote-connection)

### <a name="use-hello-azure-classic-portal-tooenable-remote-management-over-http"></a><span data-ttu-id="0ad61-131">Hello Azure classic portal tooenable extern beheer via HTTP gebruiken</span><span class="sxs-lookup"><span data-stu-id="0ad61-131">Use hello Azure classic portal tooenable remote management over HTTP</span></span>
<span data-ttu-id="0ad61-132">Voer Hallo stappen te volgen in hello Azure classic portal tooenable extern beheer via HTTP.</span><span class="sxs-lookup"><span data-stu-id="0ad61-132">Perform hello following steps in hello Azure classic portal tooenable remote management over HTTP.</span></span>

#### <a name="tooenable-remote-management-through-hello-azure-classic-portal"></a><span data-ttu-id="0ad61-133">extern beheer via de klassieke Azure-portal Hallo tooenable</span><span class="sxs-lookup"><span data-stu-id="0ad61-133">tooenable remote management through hello Azure classic portal</span></span>
1. <span data-ttu-id="0ad61-134">Toegang **apparaten** > **configureren** voor uw apparaat.</span><span class="sxs-lookup"><span data-stu-id="0ad61-134">Access **Devices** > **Configure** for your device.</span></span>
2. <span data-ttu-id="0ad61-135">Schuif omlaag toohello **extern beheer** sectie.</span><span class="sxs-lookup"><span data-stu-id="0ad61-135">Scroll down toohello **Remote Management** section.</span></span>
3. <span data-ttu-id="0ad61-136">Stel **extern beheer inschakelen** te**Ja**.</span><span class="sxs-lookup"><span data-stu-id="0ad61-136">Set **Enable Remote Management** too**Yes**.</span></span>
4. <span data-ttu-id="0ad61-137">U kunt nu tooconnect via HTTP.</span><span class="sxs-lookup"><span data-stu-id="0ad61-137">You can now choose tooconnect using HTTP.</span></span> <span data-ttu-id="0ad61-138">(Hallo standaardwaarde is tooconnect via HTTPS). Zorg ervoor dat HTTP is geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="0ad61-138">(hello default is tooconnect over HTTPS.) Make sure that HTTP is selected.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="0ad61-139">Verbinding maken via HTTP is alleen acceptabel in vertrouwde netwerken.</span><span class="sxs-lookup"><span data-stu-id="0ad61-139">Connecting over HTTP is acceptable only on trusted networks.</span></span>
   > 
   > 
5. <span data-ttu-id="0ad61-140">Klik op **opslaan** Hallo Hallo pagina onderaan in.</span><span class="sxs-lookup"><span data-stu-id="0ad61-140">Click **Save** at hello bottom of hello page.</span></span>

### <a name="use-hello-serial-console-tooenable-remote-management-over-http"></a><span data-ttu-id="0ad61-141">Hallo seriële console tooenable extern beheer via HTTP gebruiken</span><span class="sxs-lookup"><span data-stu-id="0ad61-141">Use hello serial console tooenable remote management over HTTP</span></span>
<span data-ttu-id="0ad61-142">Hallo volgende stappen uit op Hallo apparaat seriële console tooenable extern beheer uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="0ad61-142">Perform hello following steps on hello device serial console tooenable remote management.</span></span>

#### <a name="tooenable-remote-management-through-hello-device-serial-console"></a><span data-ttu-id="0ad61-143">extern beheer via de seriële console van Hallo apparaat tooenable</span><span class="sxs-lookup"><span data-stu-id="0ad61-143">tooenable remote management through hello device serial console</span></span>
1. <span data-ttu-id="0ad61-144">Selecteer optie 1 Hallo seriële consolemenu.</span><span class="sxs-lookup"><span data-stu-id="0ad61-144">On hello serial console menu, select option 1.</span></span> <span data-ttu-id="0ad61-145">Voor meer informatie over het gebruik van de seriële console Hallo op Hallo apparaat gaat te[tooWindows PowerShell voor StorSimple-verbinding via de seriële console apparaat](storsimple-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="0ad61-145">For more information about using hello serial console on hello device, go too[Connect tooWindows PowerShell for StorSimple via device serial console](storsimple-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).</span></span>
2. <span data-ttu-id="0ad61-146">Hallo opdrachtprompt, typt u:`Enable-HcsRemoteManagement –AllowHttp`</span><span class="sxs-lookup"><span data-stu-id="0ad61-146">At hello prompt, type: `Enable-HcsRemoteManagement –AllowHttp`</span></span>
3. <span data-ttu-id="0ad61-147">U wordt gewaarschuwd over Hallo beveiligingsproblemen van het gebruik van HTTP-tooconnect toohello apparaat.</span><span class="sxs-lookup"><span data-stu-id="0ad61-147">You will be notified about hello security vulnerabilities of using HTTP tooconnect toohello device.</span></span> <span data-ttu-id="0ad61-148">Bevestig door op te geven wanneer u wordt gevraagd, **Y**.</span><span class="sxs-lookup"><span data-stu-id="0ad61-148">When prompted, confirm by typing **Y**.</span></span>
4. <span data-ttu-id="0ad61-149">Controleer of HTTP is ingeschakeld door te typen:`Get-HcsSystem`</span><span class="sxs-lookup"><span data-stu-id="0ad61-149">Verify that HTTP is enabled by typing: `Get-HcsSystem`</span></span>
5. <span data-ttu-id="0ad61-150">Controleer of deze Hallo **RemoteManagementMode** veld bevat **HttpsAndHttpEnabled**.hello volgende afbeelding ziet u deze instellingen in de PuTTY.</span><span class="sxs-lookup"><span data-stu-id="0ad61-150">Verify that hello **RemoteManagementMode** field shows **HttpsAndHttpEnabled**.hello following illustration shows these settings in PuTTY.</span></span>
   
     ![Seriële HTTPS en HTTP-ingeschakeld](./media/storsimple-remote-connect/HCS_SerialHttpsAndHttpEnabled.png)

### <a name="prepare-hello-client-for-remote-connection"></a><span data-ttu-id="0ad61-152">Hallo-client voorbereiden voor externe verbinding</span><span class="sxs-lookup"><span data-stu-id="0ad61-152">Prepare hello client for remote connection</span></span>
<span data-ttu-id="0ad61-153">Hallo volgende stappen uit op Hallo client tooenable extern beheer uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="0ad61-153">Perform hello following steps on hello client tooenable remote management.</span></span>

#### <a name="tooprepare-hello-client-for-remote-connection"></a><span data-ttu-id="0ad61-154">tooprepare Hallo-client voor externe verbinding</span><span class="sxs-lookup"><span data-stu-id="0ad61-154">tooprepare hello client for remote connection</span></span>
1. <span data-ttu-id="0ad61-155">Start een Windows PowerShell-sessie als administrator.</span><span class="sxs-lookup"><span data-stu-id="0ad61-155">Start a Windows PowerShell session as an administrator.</span></span>
2. <span data-ttu-id="0ad61-156">Type Hallo volgende opdracht tooadd Hallo IP-adres van de lijst met vertrouwde hosts Hallo StorSimple-apparaat toohello van client:</span><span class="sxs-lookup"><span data-stu-id="0ad61-156">Type hello following command tooadd hello IP address of hello StorSimple device toohello client’s trusted hosts list:</span></span> 
   
     `Set-Item wsman:\localhost\Client\TrustedHosts <device_ip> -Concatenate -Force`
   
     <span data-ttu-id="0ad61-157">Vervang <*device_ip*> met Hallo IP-adres van uw apparaat; bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="0ad61-157">Replace <*device_ip*> with hello IP address of your device; for example:</span></span> 
   
     `Set-Item wsman:\localhost\Client\TrustedHosts 10.126.173.90 -Concatenate -Force`
3. <span data-ttu-id="0ad61-158">Type Hallo opdracht toosave Hallo apparaat referenties in een variabele te volgen:</span><span class="sxs-lookup"><span data-stu-id="0ad61-158">Type hello following command toosave hello device credentials in a variable:</span></span> 
   
    ```
    $cred = Get-Credential
    ```
    
4. <span data-ttu-id="0ad61-159">In het dialoogvenster Hallo die wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="0ad61-159">In hello dialog box that appears:</span></span>
   
   1. <span data-ttu-id="0ad61-160">Typ de gebruikersnaam in deze indeling Hallo: *device_ip\SSAdmin*.</span><span class="sxs-lookup"><span data-stu-id="0ad61-160">Type hello user name in this format: *device_ip\SSAdmin*.</span></span>
   2. <span data-ttu-id="0ad61-161">Typ beheerderswachtwoord van het Hallo-apparaat dat is ingesteld wanneer het Hallo-apparaat is geconfigureerd met de wizard setup Hallo.</span><span class="sxs-lookup"><span data-stu-id="0ad61-161">Type hello device administrator password that was set when hello device was configured with hello setup wizard.</span></span> <span data-ttu-id="0ad61-162">is het standaardwachtwoord Hallo *Wachtwoord1*.</span><span class="sxs-lookup"><span data-stu-id="0ad61-162">hello default password is *Password1*.</span></span>
5. <span data-ttu-id="0ad61-163">Start een Windows PowerShell-sessie op Hallo apparaat door deze opdracht te typen:</span><span class="sxs-lookup"><span data-stu-id="0ad61-163">Start a Windows PowerShell session on hello device by typing this command:</span></span>
   
     `Enter-PSSession -Credential $cred -ConfigurationName SSAdminConsole -ComputerName <device_ip>`
   
   > [!NOTE]
   > <span data-ttu-id="0ad61-164">toocreate een Windows PowerShell-sessie voor gebruik met Hallo virtuele StorSimple-apparaat, append Hallo `–Port` parameter en geef Hallo openbare poort die u hebt geconfigureerd in externe toegang voor virtueel StorSimple-apparaat.</span><span class="sxs-lookup"><span data-stu-id="0ad61-164">toocreate a Windows PowerShell session for use with hello StorSimple virtual device, append hello `–Port` parameter and specify hello public port that you configured in Remoting for StorSimple Virtual Appliance.</span></span>
   > 
   > 
   
     <span data-ttu-id="0ad61-165">Op dit moment hebt u een actieve externe Windows PowerShell-sessie toohello apparaat.</span><span class="sxs-lookup"><span data-stu-id="0ad61-165">At this point, you should have an active remote Windows PowerShell session toohello device.</span></span>
   
    ![Externe communicatie via HTTP met PowerShell](./media/storsimple-remote-connect/HCS_PSRemotingUsingHTTP.png)

## <a name="connect-through-https"></a><span data-ttu-id="0ad61-167">Verbinding maken via HTTPS</span><span class="sxs-lookup"><span data-stu-id="0ad61-167">Connect through HTTPS</span></span>
<span data-ttu-id="0ad61-168">Een tooWindows PowerShell voor StorSimple verbinding via een HTTPS-sessie Hallo veiligste en aanbevolen methode van Microsoft Azure StorSimple-apparaat voor op afstand verbinding tooyour.</span><span class="sxs-lookup"><span data-stu-id="0ad61-168">Connecting tooWindows PowerShell for StorSimple through an HTTPS session is hello most secure and recommended method of remotely connecting tooyour Microsoft Azure StorSimple device.</span></span> <span data-ttu-id="0ad61-169">Hallo volgen procedures wordt uitgelegd hoe tooset up Hallo seriële console en client-computers zodat u kunt HTTPS tooconnect tooWindows PowerShell voor StorSimple.</span><span class="sxs-lookup"><span data-stu-id="0ad61-169">hello following procedures explain how tooset up hello serial console and client computers so that you can use HTTPS tooconnect tooWindows PowerShell for StorSimple.</span></span>

<span data-ttu-id="0ad61-170">U kunt Hallo klassieke Azure-portal of Hallo seriële console tooconfigure extern beheer gebruiken.</span><span class="sxs-lookup"><span data-stu-id="0ad61-170">You can use either hello Azure classic portal or hello serial console tooconfigure remote management.</span></span> <span data-ttu-id="0ad61-171">Selecteer een van de Hallo procedures te volgen:</span><span class="sxs-lookup"><span data-stu-id="0ad61-171">Select from hello following procedures:</span></span>

* [<span data-ttu-id="0ad61-172">Hello Azure classic portal tooenable extern beheer via HTTPS gebruiken</span><span class="sxs-lookup"><span data-stu-id="0ad61-172">Use hello Azure classic portal tooenable remote management over HTTPS</span></span>](#use-the-azure-classic-portal-to-enable-remote-management-over-https)
* [<span data-ttu-id="0ad61-173">Hallo seriële console tooenable extern beheer via HTTPS gebruiken</span><span class="sxs-lookup"><span data-stu-id="0ad61-173">Use hello serial console tooenable remote management over HTTPS</span></span>](#use-the-serial-console-to-enable-remote-management-over-https)

<span data-ttu-id="0ad61-174">Nadat u extern beheer inschakelen, Hallo procedures tooprepare Hallo host voor een extern beheer na gebruik en toohello apparaat verbinden van de externe host Hallo.</span><span class="sxs-lookup"><span data-stu-id="0ad61-174">After you enable remote management, use hello following procedures tooprepare hello host for a remote management and connect toohello device from hello remote host.</span></span>

* [<span data-ttu-id="0ad61-175">Hallo host voorbereiden voor extern beheer</span><span class="sxs-lookup"><span data-stu-id="0ad61-175">Prepare hello host for remote management</span></span>](#prepare-the-host-for-remote-management)
* [<span data-ttu-id="0ad61-176">Verbinding maken met toohello apparaat van de externe host Hallo</span><span class="sxs-lookup"><span data-stu-id="0ad61-176">Connect toohello device from hello remote host</span></span>](#connect-to-the-device-from-the-remote-host)

### <a name="use-hello-azure-classic-portal-tooenable-remote-management-over-https"></a><span data-ttu-id="0ad61-177">Hello Azure classic portal tooenable extern beheer via HTTPS gebruiken</span><span class="sxs-lookup"><span data-stu-id="0ad61-177">Use hello Azure classic portal tooenable remote management over HTTPS</span></span>
<span data-ttu-id="0ad61-178">Voer Hallo stappen te volgen in hello Azure classic portal tooenable extern beheer via HTTPS.</span><span class="sxs-lookup"><span data-stu-id="0ad61-178">Perform hello following steps in hello Azure classic portal tooenable remote management over HTTPS.</span></span>

#### <a name="tooenable-remote-management-over-https-from-hello-azure-classic-portal"></a><span data-ttu-id="0ad61-179">tooenable remote management via HTTPS van Hallo klassieke Azure-portal</span><span class="sxs-lookup"><span data-stu-id="0ad61-179">tooenable remote management over HTTPS from hello Azure classic portal</span></span>
1. <span data-ttu-id="0ad61-180">Toegang **apparaten** > **configureren** voor uw apparaat.</span><span class="sxs-lookup"><span data-stu-id="0ad61-180">Access **Devices** > **Configure** for your device.</span></span>
2. <span data-ttu-id="0ad61-181">Schuif omlaag toohello **extern beheer** sectie.</span><span class="sxs-lookup"><span data-stu-id="0ad61-181">Scroll down toohello **Remote Management** section.</span></span>
3. <span data-ttu-id="0ad61-182">Stel **extern beheer inschakelen** te**Ja**.</span><span class="sxs-lookup"><span data-stu-id="0ad61-182">Set **Enable Remote Management** too**Yes**.</span></span>
4. <span data-ttu-id="0ad61-183">U kunt nu tooconnect via HTTPS.</span><span class="sxs-lookup"><span data-stu-id="0ad61-183">You can now choose tooconnect using HTTPS.</span></span> <span data-ttu-id="0ad61-184">(Hallo standaardwaarde is tooconnect via HTTPS). Zorg ervoor dat HTTPS is geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="0ad61-184">(hello default is tooconnect over HTTPS.) Make sure that HTTPS is selected.</span></span> 
5. <span data-ttu-id="0ad61-185">Klik op **certificaat voor extern beheer downloaden**.</span><span class="sxs-lookup"><span data-stu-id="0ad61-185">Click **Download Remote Management Certificate**.</span></span> <span data-ttu-id="0ad61-186">Geef een locatie toosave dit bestand.</span><span class="sxs-lookup"><span data-stu-id="0ad61-186">Specify a location toosave this file.</span></span> <span data-ttu-id="0ad61-187">U moet dit certificaat op de client of hostcomputer computer Hallo die u tooconnect toohello apparaat gebruikt tooinstall.</span><span class="sxs-lookup"><span data-stu-id="0ad61-187">You will need tooinstall this certificate on hello client or host computer that you will use tooconnect toohello device.</span></span>
6. <span data-ttu-id="0ad61-188">Klik op **opslaan** Hallo Hallo pagina onderaan in.</span><span class="sxs-lookup"><span data-stu-id="0ad61-188">Click **Save** at hello bottom of hello page.</span></span>

### <a name="use-hello-serial-console-tooenable-remote-management-over-https"></a><span data-ttu-id="0ad61-189">Hallo seriële console tooenable extern beheer via HTTPS gebruiken</span><span class="sxs-lookup"><span data-stu-id="0ad61-189">Use hello serial console tooenable remote management over HTTPS</span></span>
<span data-ttu-id="0ad61-190">Hallo volgende stappen uit op Hallo apparaat seriële console tooenable extern beheer uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="0ad61-190">Perform hello following steps on hello device serial console tooenable remote management.</span></span>

#### <a name="tooenable-remote-management-through-hello-device-serial-console"></a><span data-ttu-id="0ad61-191">extern beheer via de seriële console van Hallo apparaat tooenable</span><span class="sxs-lookup"><span data-stu-id="0ad61-191">tooenable remote management through hello device serial console</span></span>
1. <span data-ttu-id="0ad61-192">Selecteer optie 1 Hallo seriële consolemenu.</span><span class="sxs-lookup"><span data-stu-id="0ad61-192">On hello serial console menu, select option 1.</span></span> <span data-ttu-id="0ad61-193">Voor meer informatie over het gebruik van de seriële console Hallo op Hallo apparaat gaat te[tooWindows PowerShell voor StorSimple-verbinding via de seriële console apparaat](storsimple-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="0ad61-193">For more information about using hello serial console on hello device, go too[Connect tooWindows PowerShell for StorSimple via device serial console](storsimple-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).</span></span>
2. <span data-ttu-id="0ad61-194">Hallo opdrachtprompt, typt u:</span><span class="sxs-lookup"><span data-stu-id="0ad61-194">At hello prompt, type:</span></span> 
   
     `Enable-HcsRemoteManagement`
   
    <span data-ttu-id="0ad61-195">Dit moet HTTPS inschakelen op uw apparaat.</span><span class="sxs-lookup"><span data-stu-id="0ad61-195">This should enable HTTPS on your device.</span></span>
3. <span data-ttu-id="0ad61-196">Controleer of HTTPS is ingeschakeld door te typen:</span><span class="sxs-lookup"><span data-stu-id="0ad61-196">Verify that HTTPS has been enabled by typing:</span></span> 
   
     `Get-HcsSystem`
   
    <span data-ttu-id="0ad61-197">Zorg ervoor dat Hallo **RemoteManagementMode** veld bevat **HttpsEnabled**.hello volgende afbeelding ziet u deze instellingen in de PuTTY.</span><span class="sxs-lookup"><span data-stu-id="0ad61-197">Make sure that hello **RemoteManagementMode** field shows **HttpsEnabled**.hello following illustration shows these settings in PuTTY.</span></span>
   
     ![Seriële HTTPS-functionaliteit](./media/storsimple-remote-connect/HCS_SerialHttpsEnabled.png)
4. <span data-ttu-id="0ad61-199">Vanuit de uitvoer Hallo van `Get-HcsSystem`, serienummer Hallo Hallo apparaat kopiëren en opslaan voor later gebruik.</span><span class="sxs-lookup"><span data-stu-id="0ad61-199">From hello output of `Get-HcsSystem`, copy hello serial number of hello device and save it for later use.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="0ad61-200">Hallo serienummer maps toohello CN-naam in Hallo certificaat.</span><span class="sxs-lookup"><span data-stu-id="0ad61-200">hello serial number maps toohello CN name in hello certificate.</span></span>
   > 
   > 
5. <span data-ttu-id="0ad61-201">Een certificaat voor extern beheer verkrijgen door te typen:</span><span class="sxs-lookup"><span data-stu-id="0ad61-201">Obtain a remote management certificate by typing:</span></span> 
   
     `Get-HcsRemoteManagementCert`
   
    <span data-ttu-id="0ad61-202">Een certificaat vergelijkbare toohello volgende wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="0ad61-202">A certificate similar toohello following will appear.</span></span>
   
    ![Extern beheercertificaat ophalen](./media/storsimple-remote-connect/HCS_GetRemoteManagementCertificate.png)
6. <span data-ttu-id="0ad61-204">Hallo gegevens kopiëren in Hallo-certificaat van **---BEGIN CERTIFICATE---** te**---EINDCERTIFICAAT---** in een teksteditor zoals Kladblok en sla deze op te geven als een .cer-bestand.</span><span class="sxs-lookup"><span data-stu-id="0ad61-204">Copy hello information in hello certificate from **-----BEGIN CERTIFICATE-----** too**-----END CERTIFICATE-----** into a text editor such as Notepad, and save it as a .cer file.</span></span> <span data-ttu-id="0ad61-205">(Kopieert u dit bestand tooyour externe host wanneer u Hallo host voorbereidt.)</span><span class="sxs-lookup"><span data-stu-id="0ad61-205">(You will copy this file tooyour remote host when you prepare hello host.)</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="0ad61-206">een nieuw certificaat toogenerate gebruiken Hallo `Set-HcsRemoteManagementCert` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="0ad61-206">toogenerate a new certificate, use hello `Set-HcsRemoteManagementCert` cmdlet.</span></span>
   > 
   > 

### <a name="prepare-hello-host-for-remote-management"></a><span data-ttu-id="0ad61-207">Hallo host voorbereiden voor extern beheer</span><span class="sxs-lookup"><span data-stu-id="0ad61-207">Prepare hello host for remote management</span></span>
<span data-ttu-id="0ad61-208">het Hallo-hostcomputer tooprepare voor een externe verbinding die gebruikmaakt van een HTTPS-sessie uitvoeren Hallo procedures te volgen:</span><span class="sxs-lookup"><span data-stu-id="0ad61-208">tooprepare hello host computer for a remote connection that uses an HTTPS session, perform hello following procedures:</span></span>

* <span data-ttu-id="0ad61-209">[Importeren Hallo cer-bestand in de basisarchief Hallo van Hallo-client of de externe host](#to-import-the-certificate-on-the-remote-host).</span><span class="sxs-lookup"><span data-stu-id="0ad61-209">[Import hello .cer file into hello root store of hello client or remote host](#to-import-the-certificate-on-the-remote-host).</span></span>
* <span data-ttu-id="0ad61-210">[Hallo apparaat serienummers toohello hosts-bestand op de externe host toevoegen](#to-add-device-serial-numbers-to-the-remote-host).</span><span class="sxs-lookup"><span data-stu-id="0ad61-210">[Add hello device serial numbers toohello hosts file on your remote host](#to-add-device-serial-numbers-to-the-remote-host).</span></span>

<span data-ttu-id="0ad61-211">Elk van deze procedures wordt hieronder beschreven.</span><span class="sxs-lookup"><span data-stu-id="0ad61-211">Each of these procedures is described below.</span></span>

#### <a name="tooimport-hello-certificate-on-hello-remote-host"></a><span data-ttu-id="0ad61-212">tooimport hello certificaat op de externe host Hallo</span><span class="sxs-lookup"><span data-stu-id="0ad61-212">tooimport hello certificate on hello remote host</span></span>
1. <span data-ttu-id="0ad61-213">Met de rechtermuisknop op Hallo cer-bestand en selecteer **installeren certificaat**.</span><span class="sxs-lookup"><span data-stu-id="0ad61-213">Right-click hello .cer file and select **Install certificate**.</span></span> <span data-ttu-id="0ad61-214">Hiermee start u Hallo Wizard Certificaat importeren.</span><span class="sxs-lookup"><span data-stu-id="0ad61-214">This will start hello Certificate Import Wizard.</span></span>
   
    ![Wizard Certificaat importeren 1](./media/storsimple-remote-connect/HCS_CertificateImportWizard1.png)
2. <span data-ttu-id="0ad61-216">Voor **archieflocatie**, selecteer **lokale Machine**, en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="0ad61-216">For **Store location**, select **Local Machine**, and then click **Next**.</span></span>
3. <span data-ttu-id="0ad61-217">Selecteer **alle certificaten in Hallo volgende archief plaatsen**, en klik vervolgens op **Bladeren**.</span><span class="sxs-lookup"><span data-stu-id="0ad61-217">Select **Place all certificates in hello following store**, and then click **Browse**.</span></span> <span data-ttu-id="0ad61-218">Navigeer toohello basisarchief van de externe host, en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="0ad61-218">Navigate toohello root store of your remote host, and then click **Next**.</span></span>
   
    ![Wizard Certificaat importeren 2](./media/storsimple-remote-connect/HCS_CertificateImportWizard2.png)
4. <span data-ttu-id="0ad61-220">Klik op **Voltooien**.</span><span class="sxs-lookup"><span data-stu-id="0ad61-220">Click **Finish**.</span></span> <span data-ttu-id="0ad61-221">Er verschijnt een bericht dat aangeeft dat Hallo importeren geslaagd is.</span><span class="sxs-lookup"><span data-stu-id="0ad61-221">A message that tells you that hello import was successful appears.</span></span>
   
    ![Wizard Certificaat importeren 3](./media/storsimple-remote-connect/HCS_CertificateImportWizard3.png)

#### <a name="tooadd-device-serial-numbers-toohello-remote-host"></a><span data-ttu-id="0ad61-223">tooadd apparaat serienummers toohello externe host</span><span class="sxs-lookup"><span data-stu-id="0ad61-223">tooadd device serial numbers toohello remote host</span></span>
1. <span data-ttu-id="0ad61-224">Kladblok start als beheerder en open vervolgens Hallo hosts-bestand op \Windows\System32\Drivers\etc.</span><span class="sxs-lookup"><span data-stu-id="0ad61-224">Start Notepad as an administrator, and then open hello hosts file located at \Windows\System32\Drivers\etc.</span></span>
2. <span data-ttu-id="0ad61-225">Hallo na drie vermeldingen tooyour hosts-bestand toevoegen: **DATA 0-IP-adres**, **Controller 0 vast IP-adres**, en **Controller 1 vast IP-adres**.</span><span class="sxs-lookup"><span data-stu-id="0ad61-225">Add hello following three entries tooyour hosts file: **DATA 0 IP address**, **Controller 0 Fixed IP address**, and **Controller 1 Fixed IP address**.</span></span>
3. <span data-ttu-id="0ad61-226">Voer het serienummer van het Hallo-apparaat dat u eerder hebt opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="0ad61-226">Enter hello device serial number that you saved earlier.</span></span> <span data-ttu-id="0ad61-227">Dit toohello IP-adres toewijzen zoals weergegeven in Hallo installatiekopie te volgen.</span><span class="sxs-lookup"><span data-stu-id="0ad61-227">Map this toohello IP address as shown in hello following image.</span></span> <span data-ttu-id="0ad61-228">Voor Controller 0 en Controller 1 toevoegen **Controller0** en **Controller1** aan Hallo einde van het serienummer hello (CN-naam).</span><span class="sxs-lookup"><span data-stu-id="0ad61-228">For Controller 0 and Controller 1, append **Controller0** and **Controller1** at hello end of hello serial number (CN name).</span></span>
   
    ![CN-naam toohosts bestand toe te voegen](./media/storsimple-remote-connect/HCS_AddingCNNameToHostsFile.png)
4. <span data-ttu-id="0ad61-230">Hallo hosts-bestand opslaan.</span><span class="sxs-lookup"><span data-stu-id="0ad61-230">Save hello hosts file.</span></span>

### <a name="connect-toohello-device-from-hello-remote-host"></a><span data-ttu-id="0ad61-231">Verbinding maken met toohello apparaat van de externe host Hallo</span><span class="sxs-lookup"><span data-stu-id="0ad61-231">Connect toohello device from hello remote host</span></span>
<span data-ttu-id="0ad61-232">Gebruik Windows PowerShell- en SSL tooenter een SSAdmin-sessie op uw apparaat vanaf een externe host of de client.</span><span class="sxs-lookup"><span data-stu-id="0ad61-232">Use Windows PowerShell and SSL tooenter an SSAdmin session on your device from a remote host or client.</span></span> <span data-ttu-id="0ad61-233">Hallo SSAdmin sessie toegewezen toooption 1 in Hallo [seriële console](storsimple-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console) menu van uw apparaat.</span><span class="sxs-lookup"><span data-stu-id="0ad61-233">hello SSAdmin session maps toooption 1 in hello [serial console](storsimple-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console) menu of your device.</span></span>

<span data-ttu-id="0ad61-234">Hallo na de procedure op Hallo computer van waaruit u toomake Hallo externe Windows PowerShell verbinding wilt uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="0ad61-234">Perform hello following procedure on hello computer from which you want toomake hello remote Windows PowerShell connection.</span></span>

#### <a name="tooenter-an-ssadmin-session-on-hello-device-by-using-windows-powershell-and-ssl"></a><span data-ttu-id="0ad61-235">tooenter een SSAdmin-sessie op Hallo apparaat via Windows PowerShell- en SSL</span><span class="sxs-lookup"><span data-stu-id="0ad61-235">tooenter an SSAdmin session on hello device by using Windows PowerShell and SSL</span></span>
1. <span data-ttu-id="0ad61-236">Start een Windows PowerShell-sessie als administrator.</span><span class="sxs-lookup"><span data-stu-id="0ad61-236">Start a Windows PowerShell session as an administrator.</span></span>
2. <span data-ttu-id="0ad61-237">Hallo IP-adres toohello apparaatclient van vertrouwde hosts toevoegen door te typen:</span><span class="sxs-lookup"><span data-stu-id="0ad61-237">Add hello device IP address toohello client’s trusted hosts by typing:</span></span>
   
     `Set-Item wsman:\localhost\Client\TrustedHosts <device_ip> -Concatenate -Force`
   
    <span data-ttu-id="0ad61-238">Waarbij <*device_ip*> Hallo IP-adres van uw apparaat is; bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="0ad61-238">Where <*device_ip*> is hello IP address of your device; for example:</span></span> 
   
     `Set-Item wsman:\localhost\Client\TrustedHosts 10.126.173.90 -Concatenate -Force`
3. <span data-ttu-id="0ad61-239">Een nieuwe referentie maken door te typen:</span><span class="sxs-lookup"><span data-stu-id="0ad61-239">Create a new credential by typing:</span></span> 
   
     `$cred = New-Object pscredential @("<IP of target device>\SSAdmin", (ConvertTo-SecureString -Force -AsPlainText "<Device Administrator Password>"))`
   
    <span data-ttu-id="0ad61-240">Waarbij <*IP-adres van het doelapparaat*> Hallo IP-adres van de DATA 0 voor uw apparaat; bijvoorbeeld **10.126.173.90** zoals weergegeven in de voorafgaande aan de installatiekopie van het hosts-bestand Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="0ad61-240">Where <*IP of target device*> is hello IP address of DATA 0 for your device; for example, **10.126.173.90** as shown in hello preceding image of hello hosts file.</span></span> <span data-ttu-id="0ad61-241">Hallo beheerderswachtwoord voor uw apparaat ook opgeven.</span><span class="sxs-lookup"><span data-stu-id="0ad61-241">Also, supply hello administrator password for your device.</span></span>
4. <span data-ttu-id="0ad61-242">Een sessie maken door te typen:</span><span class="sxs-lookup"><span data-stu-id="0ad61-242">Create a session by typing:</span></span>
   
     `$session = New-PSSession -UseSSL -ComputerName <Serial number of target device> -Credential $cred -ConfigurationName "SSAdminConsole"`
   
    <span data-ttu-id="0ad61-243">Hallo - ComputerName parameter in Hallo-cmdlet, bieden Hallo <*serienummer van het doelapparaat*>.</span><span class="sxs-lookup"><span data-stu-id="0ad61-243">For hello -ComputerName parameter in hello cmdlet, provide hello <*serial number of target device*>.</span></span> <span data-ttu-id="0ad61-244">Dit serienummer is toegewezen toohello IP-adres van de DATA 0 Hallo hostbestand op de externe host; bijvoorbeeld: **SHX0991003G44MT** zoals weergegeven in Hallo installatiekopie te volgen.</span><span class="sxs-lookup"><span data-stu-id="0ad61-244">This serial number was mapped toohello IP address of DATA 0 in hello hosts file on your remote host; for example, **SHX0991003G44MT** as shown in hello following image.</span></span>
5. <span data-ttu-id="0ad61-245">Type:</span><span class="sxs-lookup"><span data-stu-id="0ad61-245">Type:</span></span> 
   
     `Enter-PSSession $session`
6. <span data-ttu-id="0ad61-246">U toowait moet een paar minuten en vervolgens kunt u zich verbonden tooyour apparaat via HTTPS via SSL.</span><span class="sxs-lookup"><span data-stu-id="0ad61-246">You will need toowait a few minutes, and then you will be connected tooyour device via HTTPS over SSL.</span></span> <span data-ttu-id="0ad61-247">U ziet een bericht waarin wordt aangegeven dat u verbonden tooyour apparaat.</span><span class="sxs-lookup"><span data-stu-id="0ad61-247">You will see a message that indicates you are connected tooyour device.</span></span>
   
    ![PowerShell voor externe toegang met behulp van HTTPS- en SSL](./media/storsimple-remote-connect/HCS_PSRemotingUsingHTTPSAndSSL.png)

## <a name="next-steps"></a><span data-ttu-id="0ad61-249">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="0ad61-249">Next steps</span></span>
* <span data-ttu-id="0ad61-250">Meer informatie over [uw StorSimple-apparaat met behulp van Windows PowerShell tooadminister](storsimple-windows-powershell-administration.md).</span><span class="sxs-lookup"><span data-stu-id="0ad61-250">Learn more about [using Windows PowerShell tooadminister your StorSimple device](storsimple-windows-powershell-administration.md).</span></span>
* <span data-ttu-id="0ad61-251">Meer informatie over [StorSimple Manager service tooadminister uw StorSimple-apparaat met behulp van Hallo](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="0ad61-251">Learn more about [using hello StorSimple Manager service tooadminister your StorSimple device](storsimple-manager-service-administration.md).</span></span>

