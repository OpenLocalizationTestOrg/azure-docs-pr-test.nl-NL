1. <span data-ttu-id="bf14a-101">Kopieer Hallo installatieprogramma tooa lokale map (bijvoorbeeld C:\Temp) op dat u wilt dat tooprotect Hallo-server.</span><span class="sxs-lookup"><span data-stu-id="bf14a-101">Copy hello installer tooa local folder (for example, C:\Temp) on hello server that you want tooprotect.</span></span> <span data-ttu-id="bf14a-102">Voer Hallo opdrachten als beheerder bij een opdrachtprompt te volgen:</span><span class="sxs-lookup"><span data-stu-id="bf14a-102">Run hello following commands as an administrator at a command prompt:</span></span>

  ```
  cd C:\Temp
  ren Microsoft-ASR_UA*Windows*release.exe MobilityServiceInstaller.exe
  MobilityServiceInstaller.exe /q /x:C:\Temp\Extracted
  cd C:\Temp\Extracted.
  ```
2. <span data-ttu-id="bf14a-103">tooinstall Mobility-Service Hallo volgende opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="bf14a-103">tooinstall Mobility Service, run hello following command:</span></span>

  ```
  UnifiedAgent.exe /Role "MS" /InstallLocation "C:\Program Files (x86)\Microsoft Azure Site Recovery" /Platform "VmWare" /Silent
  ```
3. <span data-ttu-id="bf14a-104">Hallo-agent moet nu geregistreerd bij Hallo configuratieserver toobe.</span><span class="sxs-lookup"><span data-stu-id="bf14a-104">Now hello agent needs toobe registered with hello Configuration Server.</span></span>

  ```
  cd C:\Program Files (x86)\Microsoft Azure Site Recovery\agent
  UnifiedAgentConfigurator.exe”  /CSEndPoint <CSIP> /PassphraseFilePath <PassphraseFilePath>
  ```

#### <a name="mobility-service-installer-command-line-arguments"></a><span data-ttu-id="bf14a-105">Opdrachtregelargumenten van de Mobility-Service-installatieprogramma</span><span class="sxs-lookup"><span data-stu-id="bf14a-105">Mobility Service installer command-line arguments</span></span>

```
Usage :
UnifiedAgent.exe /Role <MS|MT> /InstallLocation <Install Location> /Platform “VmWare” /Silent
```

| <span data-ttu-id="bf14a-106">Parameter</span><span class="sxs-lookup"><span data-stu-id="bf14a-106">Parameter</span></span>|<span data-ttu-id="bf14a-107">Type</span><span class="sxs-lookup"><span data-stu-id="bf14a-107">Type</span></span>|<span data-ttu-id="bf14a-108">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="bf14a-108">Description</span></span>|<span data-ttu-id="bf14a-109">Mogelijke waarden</span><span class="sxs-lookup"><span data-stu-id="bf14a-109">Possible values</span></span>|
|-|-|-|-|
|<span data-ttu-id="bf14a-110">/ Functie</span><span class="sxs-lookup"><span data-stu-id="bf14a-110">/Role</span></span>|<span data-ttu-id="bf14a-111">Verplicht</span><span class="sxs-lookup"><span data-stu-id="bf14a-111">Mandatory</span></span>|<span data-ttu-id="bf14a-112">Geeft aan of de Mobility-Service (MS) moet worden geïnstalleerd of MasterTarget(MT) moet worden geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="bf14a-112">Specifies whether Mobility Service (MS) should be installed or MasterTarget(MT) should be installed</span></span>|<span data-ttu-id="bf14a-113">MS</span><span class="sxs-lookup"><span data-stu-id="bf14a-113">MS</span></span> </br> <span data-ttu-id="bf14a-114">MT</span><span class="sxs-lookup"><span data-stu-id="bf14a-114">MT</span></span>|
|<span data-ttu-id="bf14a-115">/InstallLocation</span><span class="sxs-lookup"><span data-stu-id="bf14a-115">/InstallLocation</span></span>|<span data-ttu-id="bf14a-116">Optioneel</span><span class="sxs-lookup"><span data-stu-id="bf14a-116">Optional</span></span>|<span data-ttu-id="bf14a-117">Locatie waar de Mobility-Service is geïnstalleerd</span><span class="sxs-lookup"><span data-stu-id="bf14a-117">Location where Mobility Service is installed</span></span>|<span data-ttu-id="bf14a-118">Een map op de computer Hallo</span><span class="sxs-lookup"><span data-stu-id="bf14a-118">Any folder on hello computer</span></span>|
|<span data-ttu-id="bf14a-119">/ Platform</span><span class="sxs-lookup"><span data-stu-id="bf14a-119">/Platform</span></span>|<span data-ttu-id="bf14a-120">Verplicht</span><span class="sxs-lookup"><span data-stu-id="bf14a-120">Mandatory</span></span>|<span data-ttu-id="bf14a-121">Hiermee geeft u op welke Hallo Mobility-Service ophalen geïnstalleerd Hallo-platform</span><span class="sxs-lookup"><span data-stu-id="bf14a-121">Specifies hello platform on which hello Mobility Service is getting installed</span></span> </br> </br><span data-ttu-id="bf14a-122">- **VMware** : deze waarde wordt gebruikt als u mobility-service op een virtuele machine uitgevoerd installeert op *VMware vSphere ESXi-Hosts*, *Hyper-V-Hosts* en *Phsyical Servers*</span><span class="sxs-lookup"><span data-stu-id="bf14a-122">- **VMware** : use this value if you are installing mobility service on a VM running on *VMware vSphere ESXi Hosts*, *Hyper-V Hosts* and *Phsyical Servers*</span></span> </br> <span data-ttu-id="bf14a-123">- **Azure** : deze waarde wordt gebruikt als u agent op een virtuele machine van Azure IaaS installeert</span><span class="sxs-lookup"><span data-stu-id="bf14a-123">- **Azure** : use this value if you are installing agent on a Azure IaaS VM</span></span>| <span data-ttu-id="bf14a-124">VMware</span><span class="sxs-lookup"><span data-stu-id="bf14a-124">VMware</span></span> </br> <span data-ttu-id="bf14a-125">Azure</span><span class="sxs-lookup"><span data-stu-id="bf14a-125">Azure</span></span>|
|<span data-ttu-id="bf14a-126">/ Silent</span><span class="sxs-lookup"><span data-stu-id="bf14a-126">/Silent</span></span>|<span data-ttu-id="bf14a-127">Optioneel</span><span class="sxs-lookup"><span data-stu-id="bf14a-127">Optional</span></span>|<span data-ttu-id="bf14a-128">Hiermee geeft u toorun Hallo installatieprogramma in stille modus</span><span class="sxs-lookup"><span data-stu-id="bf14a-128">Specifies toorun hello installer in silent mode</span></span>| <span data-ttu-id="bf14a-129">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="bf14a-129">NA</span></span>|

>[!TIP]
> <span data-ttu-id="bf14a-130">Hallo installatielogboeken kunnen van %ProgramData%\ASRSetupLogs\ASRUnifiedAgentInstaller.log worden gevonden</span><span class="sxs-lookup"><span data-stu-id="bf14a-130">hello setup logs can be found under %ProgramData%\ASRSetupLogs\ASRUnifiedAgentInstaller.log</span></span>

#### <a name="mobility-service-registration-command-line-arguments"></a><span data-ttu-id="bf14a-131">Opdrachtregelargumenten van de Mobility-Service-registratie</span><span class="sxs-lookup"><span data-stu-id="bf14a-131">Mobility Service registration command-line arguments</span></span>

```
Usage :
UnifiedAgentConfigurator.exe”  /CSEndPoint <CSIP> /PassphraseFilePath <PassphraseFilePath>
```

  | <span data-ttu-id="bf14a-132">Parameter</span><span class="sxs-lookup"><span data-stu-id="bf14a-132">Parameter</span></span>|<span data-ttu-id="bf14a-133">Type</span><span class="sxs-lookup"><span data-stu-id="bf14a-133">Type</span></span>|<span data-ttu-id="bf14a-134">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="bf14a-134">Description</span></span>|<span data-ttu-id="bf14a-135">Mogelijke waarden</span><span class="sxs-lookup"><span data-stu-id="bf14a-135">Possible values</span></span>|
  |-|-|-|-|
  |<span data-ttu-id="bf14a-136">/ CSEndPoint</span><span class="sxs-lookup"><span data-stu-id="bf14a-136">/CSEndPoint</span></span> |<span data-ttu-id="bf14a-137">Verplicht</span><span class="sxs-lookup"><span data-stu-id="bf14a-137">Mandatory</span></span>|<span data-ttu-id="bf14a-138">IP-adres van de configuratieserver Hallo</span><span class="sxs-lookup"><span data-stu-id="bf14a-138">IP address of hello configuration server</span></span>| <span data-ttu-id="bf14a-139">Een geldig IP-adres</span><span class="sxs-lookup"><span data-stu-id="bf14a-139">Any valid IP address</span></span>|
  |<span data-ttu-id="bf14a-140">/PassphraseFilePath</span><span class="sxs-lookup"><span data-stu-id="bf14a-140">/PassphraseFilePath</span></span>|<span data-ttu-id="bf14a-141">Verplicht</span><span class="sxs-lookup"><span data-stu-id="bf14a-141">Mandatory</span></span>|<span data-ttu-id="bf14a-142">Locatie van Hallo wachtwoordzin</span><span class="sxs-lookup"><span data-stu-id="bf14a-142">Location of hello passphrase</span></span> |<span data-ttu-id="bf14a-143">Een geldig UNC- of lokale bestandspad</span><span class="sxs-lookup"><span data-stu-id="bf14a-143">Any valid UNC or local file path</span></span>|


>[!TIP]
> <span data-ttu-id="bf14a-144">Hallo AgentConfiguration Logboeken vindt u onder %ProgramData%\ASRSetupLogs\ASRUnifiedAgentConfigurator.log</span><span class="sxs-lookup"><span data-stu-id="bf14a-144">hello AgentConfiguration logs can be found under %ProgramData%\ASRSetupLogs\ASRUnifiedAgentConfigurator.log</span></span>
