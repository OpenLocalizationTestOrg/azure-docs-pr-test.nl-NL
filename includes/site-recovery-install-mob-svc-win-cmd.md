1. <span data-ttu-id="9e5ca-101">Het installatieprogramma kopiëren naar een lokale map (bijvoorbeeld C:\Temp) op de server die u wilt beveiligen.</span><span class="sxs-lookup"><span data-stu-id="9e5ca-101">Copy the installer to a local folder (for example, C:\Temp) on the server that you want to protect.</span></span> <span data-ttu-id="9e5ca-102">Voer de volgende opdrachten uit als beheerder bij een opdrachtprompt:</span><span class="sxs-lookup"><span data-stu-id="9e5ca-102">Run the following commands as an administrator at a command prompt:</span></span>

  ```
  cd C:\Temp
  ren Microsoft-ASR_UA*Windows*release.exe MobilityServiceInstaller.exe
  MobilityServiceInstaller.exe /q /x:C:\Temp\Extracted
  cd C:\Temp\Extracted.
  ```
2. <span data-ttu-id="9e5ca-103">Voer de volgende opdracht voor het installeren van de Mobility-Service:</span><span class="sxs-lookup"><span data-stu-id="9e5ca-103">To install Mobility Service, run the following command:</span></span>

  ```
  UnifiedAgent.exe /Role "MS" /InstallLocation "C:\Program Files (x86)\Microsoft Azure Site Recovery" /Platform "VmWare" /Silent
  ```
3. <span data-ttu-id="9e5ca-104">Nu moet de agent worden geregistreerd met de configuratieserver.</span><span class="sxs-lookup"><span data-stu-id="9e5ca-104">Now the agent needs to be registered with the Configuration Server.</span></span>

  ```
  cd C:\Program Files (x86)\Microsoft Azure Site Recovery\agent
  UnifiedAgentConfigurator.exe”  /CSEndPoint <CSIP> /PassphraseFilePath <PassphraseFilePath>
  ```

#### <a name="mobility-service-installer-command-line-arguments"></a><span data-ttu-id="9e5ca-105">Opdrachtregelargumenten van de Mobility-Service-installatieprogramma</span><span class="sxs-lookup"><span data-stu-id="9e5ca-105">Mobility Service installer command-line arguments</span></span>

```
Usage :
UnifiedAgent.exe /Role <MS|MT> /InstallLocation <Install Location> /Platform “VmWare” /Silent
```

| <span data-ttu-id="9e5ca-106">Parameter</span><span class="sxs-lookup"><span data-stu-id="9e5ca-106">Parameter</span></span>|<span data-ttu-id="9e5ca-107">Type</span><span class="sxs-lookup"><span data-stu-id="9e5ca-107">Type</span></span>|<span data-ttu-id="9e5ca-108">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="9e5ca-108">Description</span></span>|<span data-ttu-id="9e5ca-109">Mogelijke waarden</span><span class="sxs-lookup"><span data-stu-id="9e5ca-109">Possible values</span></span>|
|-|-|-|-|
|<span data-ttu-id="9e5ca-110">/ Functie</span><span class="sxs-lookup"><span data-stu-id="9e5ca-110">/Role</span></span>|<span data-ttu-id="9e5ca-111">Verplicht</span><span class="sxs-lookup"><span data-stu-id="9e5ca-111">Mandatory</span></span>|<span data-ttu-id="9e5ca-112">Geeft aan of de Mobility-Service (MS) moet worden geïnstalleerd of MasterTarget(MT) moet worden geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="9e5ca-112">Specifies whether Mobility Service (MS) should be installed or MasterTarget(MT) should be installed</span></span>|<span data-ttu-id="9e5ca-113">MS</span><span class="sxs-lookup"><span data-stu-id="9e5ca-113">MS</span></span> </br> <span data-ttu-id="9e5ca-114">MT</span><span class="sxs-lookup"><span data-stu-id="9e5ca-114">MT</span></span>|
|<span data-ttu-id="9e5ca-115">/InstallLocation</span><span class="sxs-lookup"><span data-stu-id="9e5ca-115">/InstallLocation</span></span>|<span data-ttu-id="9e5ca-116">Optioneel</span><span class="sxs-lookup"><span data-stu-id="9e5ca-116">Optional</span></span>|<span data-ttu-id="9e5ca-117">Locatie waar de Mobility-Service is geïnstalleerd</span><span class="sxs-lookup"><span data-stu-id="9e5ca-117">Location where Mobility Service is installed</span></span>|<span data-ttu-id="9e5ca-118">Een map op de computer</span><span class="sxs-lookup"><span data-stu-id="9e5ca-118">Any folder on the computer</span></span>|
|<span data-ttu-id="9e5ca-119">/ Platform</span><span class="sxs-lookup"><span data-stu-id="9e5ca-119">/Platform</span></span>|<span data-ttu-id="9e5ca-120">Verplicht</span><span class="sxs-lookup"><span data-stu-id="9e5ca-120">Mandatory</span></span>|<span data-ttu-id="9e5ca-121">Hiermee geeft u het platform waarop de Mobility-Service is ophalen geïnstalleerd</span><span class="sxs-lookup"><span data-stu-id="9e5ca-121">Specifies the platform on which the Mobility Service is getting installed</span></span> </br> </br><span data-ttu-id="9e5ca-122">- **VMware** : deze waarde wordt gebruikt als u mobility-service op een virtuele machine uitgevoerd installeert op *VMware vSphere ESXi-Hosts*, *Hyper-V-Hosts* en *Phsyical Servers*</span><span class="sxs-lookup"><span data-stu-id="9e5ca-122">- **VMware** : use this value if you are installing mobility service on a VM running on *VMware vSphere ESXi Hosts*, *Hyper-V Hosts* and *Phsyical Servers*</span></span> </br> <span data-ttu-id="9e5ca-123">- **Azure** : deze waarde wordt gebruikt als u agent op een virtuele machine van Azure IaaS installeert</span><span class="sxs-lookup"><span data-stu-id="9e5ca-123">- **Azure** : use this value if you are installing agent on a Azure IaaS VM</span></span>| <span data-ttu-id="9e5ca-124">VMware</span><span class="sxs-lookup"><span data-stu-id="9e5ca-124">VMware</span></span> </br> <span data-ttu-id="9e5ca-125">Azure</span><span class="sxs-lookup"><span data-stu-id="9e5ca-125">Azure</span></span>|
|<span data-ttu-id="9e5ca-126">/ Silent</span><span class="sxs-lookup"><span data-stu-id="9e5ca-126">/Silent</span></span>|<span data-ttu-id="9e5ca-127">Optioneel</span><span class="sxs-lookup"><span data-stu-id="9e5ca-127">Optional</span></span>|<span data-ttu-id="9e5ca-128">Hiermee geeft u het installatieprogramma uitvoeren in de stille modus</span><span class="sxs-lookup"><span data-stu-id="9e5ca-128">Specifies to run the installer in silent mode</span></span>| <span data-ttu-id="9e5ca-129">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="9e5ca-129">NA</span></span>|

>[!TIP]
> <span data-ttu-id="9e5ca-130">De installatielogboeken kunnen van %ProgramData%\ASRSetupLogs\ASRUnifiedAgentInstaller.log worden gevonden</span><span class="sxs-lookup"><span data-stu-id="9e5ca-130">The setup logs can be found under %ProgramData%\ASRSetupLogs\ASRUnifiedAgentInstaller.log</span></span>

#### <a name="mobility-service-registration-command-line-arguments"></a><span data-ttu-id="9e5ca-131">Opdrachtregelargumenten van de Mobility-Service-registratie</span><span class="sxs-lookup"><span data-stu-id="9e5ca-131">Mobility Service registration command-line arguments</span></span>

```
Usage :
UnifiedAgentConfigurator.exe”  /CSEndPoint <CSIP> /PassphraseFilePath <PassphraseFilePath>
```

  | <span data-ttu-id="9e5ca-132">Parameter</span><span class="sxs-lookup"><span data-stu-id="9e5ca-132">Parameter</span></span>|<span data-ttu-id="9e5ca-133">Type</span><span class="sxs-lookup"><span data-stu-id="9e5ca-133">Type</span></span>|<span data-ttu-id="9e5ca-134">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="9e5ca-134">Description</span></span>|<span data-ttu-id="9e5ca-135">Mogelijke waarden</span><span class="sxs-lookup"><span data-stu-id="9e5ca-135">Possible values</span></span>|
  |-|-|-|-|
  |<span data-ttu-id="9e5ca-136">/ CSEndPoint</span><span class="sxs-lookup"><span data-stu-id="9e5ca-136">/CSEndPoint</span></span> |<span data-ttu-id="9e5ca-137">Verplicht</span><span class="sxs-lookup"><span data-stu-id="9e5ca-137">Mandatory</span></span>|<span data-ttu-id="9e5ca-138">IP-adres van de configuratieserver</span><span class="sxs-lookup"><span data-stu-id="9e5ca-138">IP address of the configuration server</span></span>| <span data-ttu-id="9e5ca-139">Een geldig IP-adres</span><span class="sxs-lookup"><span data-stu-id="9e5ca-139">Any valid IP address</span></span>|
  |<span data-ttu-id="9e5ca-140">/PassphraseFilePath</span><span class="sxs-lookup"><span data-stu-id="9e5ca-140">/PassphraseFilePath</span></span>|<span data-ttu-id="9e5ca-141">Verplicht</span><span class="sxs-lookup"><span data-stu-id="9e5ca-141">Mandatory</span></span>|<span data-ttu-id="9e5ca-142">Locatie van de wachtwoordzin</span><span class="sxs-lookup"><span data-stu-id="9e5ca-142">Location of the passphrase</span></span> |<span data-ttu-id="9e5ca-143">Een geldig UNC- of lokale bestandspad</span><span class="sxs-lookup"><span data-stu-id="9e5ca-143">Any valid UNC or local file path</span></span>|


>[!TIP]
> <span data-ttu-id="9e5ca-144">De logboeken AgentConfiguration vindt u onder %ProgramData%\ASRSetupLogs\ASRUnifiedAgentConfigurator.log</span><span class="sxs-lookup"><span data-stu-id="9e5ca-144">The AgentConfiguration logs can be found under %ProgramData%\ASRSetupLogs\ASRUnifiedAgentConfigurator.log</span></span>
