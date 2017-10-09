1. <span data-ttu-id="ad59e-101">Hallo installatieprogramma tooa lokale map (bijvoorbeeld map) op Hallo server die u tooprotect wilt kopiëren.</span><span class="sxs-lookup"><span data-stu-id="ad59e-101">Copy hello installer tooa local folder (for example, /tmp) on hello server that you want tooprotect.</span></span> <span data-ttu-id="ad59e-102">Voer in een terminal Hallo volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="ad59e-102">In a terminal, run hello following commands:</span></span>
  ```
  cd /tmp
  tar -xvzf Microsoft-ASR_UA*release.tar.gz
  ```
2. <span data-ttu-id="ad59e-103">tooinstall Mobility-Service Hallo volgende opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="ad59e-103">tooinstall Mobility Service, run hello following command:</span></span>

  ```
  sudo ./install -d <Install Location> -r MS -v VmWare -q
  ```
3. <span data-ttu-id="ad59e-104">Zodra de installatie is voltooid, moet Hallo Mobility-Service tooget geregistreerde toohello configuratieserver.</span><span class="sxs-lookup"><span data-stu-id="ad59e-104">Once installation is complete, hello Mobility Service needs tooget registered toohello configuration server.</span></span> <span data-ttu-id="ad59e-105">Hallo na de opdracht tooregister Hallo Mobility-Service met de configuratieserver worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="ad59e-105">Run hello following command tooregister hello Mobility Service with Configuration server.</span></span>

  ```
  /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i <CSIP> -P /var/passphrase.txt
  ```

#### <a name="mobility-service-installer-command-line"></a><span data-ttu-id="ad59e-106">Mobility-Service installatieprogramma vanaf de opdrachtregel</span><span class="sxs-lookup"><span data-stu-id="ad59e-106">Mobility Service installer command-line</span></span>

```
Usage:
./install -d <Install Location> -r <MS|MT> -v VmWare -q
```

|<span data-ttu-id="ad59e-107">Parameter</span><span class="sxs-lookup"><span data-stu-id="ad59e-107">Parameter</span></span>|<span data-ttu-id="ad59e-108">Type</span><span class="sxs-lookup"><span data-stu-id="ad59e-108">Type</span></span>|<span data-ttu-id="ad59e-109">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="ad59e-109">Description</span></span>|<span data-ttu-id="ad59e-110">Mogelijke waarden</span><span class="sxs-lookup"><span data-stu-id="ad59e-110">Possible values</span></span>|
|-|-|-|-|
|<span data-ttu-id="ad59e-111">-r</span><span class="sxs-lookup"><span data-stu-id="ad59e-111">-r</span></span> |<span data-ttu-id="ad59e-112">Verplicht</span><span class="sxs-lookup"><span data-stu-id="ad59e-112">Mandatory</span></span>|<span data-ttu-id="ad59e-113">Geeft aan of de Mobility-Service (MS) moet worden geïnstalleerd of MasterTarget(MT) moet worden geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="ad59e-113">Specifies whether Mobility Service (MS) should be installed or MasterTarget(MT) should be installed</span></span>|<span data-ttu-id="ad59e-114">MS</span><span class="sxs-lookup"><span data-stu-id="ad59e-114">MS</span></span> </br> <span data-ttu-id="ad59e-115">MT</span><span class="sxs-lookup"><span data-stu-id="ad59e-115">MT</span></span>|
|<span data-ttu-id="ad59e-116">-d</span><span class="sxs-lookup"><span data-stu-id="ad59e-116">-d</span></span> |<span data-ttu-id="ad59e-117">Optioneel</span><span class="sxs-lookup"><span data-stu-id="ad59e-117">Optional</span></span>|<span data-ttu-id="ad59e-118">Locatie waar de Mobility-Service moet worden geïnstalleerd</span><span class="sxs-lookup"><span data-stu-id="ad59e-118">Location where Mobility Service will be installed</span></span>|<span data-ttu-id="ad59e-119">/usr/local/ASR</span><span class="sxs-lookup"><span data-stu-id="ad59e-119">/usr/local/ASR</span></span>|
|<span data-ttu-id="ad59e-120">-v</span><span class="sxs-lookup"><span data-stu-id="ad59e-120">-v</span></span>|<span data-ttu-id="ad59e-121">Verplicht</span><span class="sxs-lookup"><span data-stu-id="ad59e-121">Mandatory</span></span>|<span data-ttu-id="ad59e-122">Hiermee geeft u op welke Hallo Mobility-Service ophalen geïnstalleerd Hallo-platform</span><span class="sxs-lookup"><span data-stu-id="ad59e-122">Specifies hello platform on which hello Mobility Service is getting installed</span></span> </br> </br><span data-ttu-id="ad59e-123">- **VMware** : deze waarde wordt gebruikt als u mobility-service op een virtuele machine uitgevoerd installeert op *VMware vSphere ESXi-Hosts*, *Hyper-V-Hosts* en *Phsyical Servers*</span><span class="sxs-lookup"><span data-stu-id="ad59e-123">- **VMware** : use this value if you are installing mobility service on a VM running on *VMware vSphere ESXi Hosts*, *Hyper-V Hosts* and *Phsyical Servers*</span></span> </br> <span data-ttu-id="ad59e-124">- **Azure** : deze waarde wordt gebruikt als u agent op een virtuele machine van Azure IaaS installeert</span><span class="sxs-lookup"><span data-stu-id="ad59e-124">- **Azure** : use this value if you are installing agent on a Azure IaaS VM</span></span>| <span data-ttu-id="ad59e-125">VMware</span><span class="sxs-lookup"><span data-stu-id="ad59e-125">VMware</span></span> </br> <span data-ttu-id="ad59e-126">Azure</span><span class="sxs-lookup"><span data-stu-id="ad59e-126">Azure</span></span>|
|<span data-ttu-id="ad59e-127">-q</span><span class="sxs-lookup"><span data-stu-id="ad59e-127">-q</span></span>|<span data-ttu-id="ad59e-128">Optioneel</span><span class="sxs-lookup"><span data-stu-id="ad59e-128">Optional</span></span>|<span data-ttu-id="ad59e-129">Hiermee geeft u toorun installatieprogramma in stille modus</span><span class="sxs-lookup"><span data-stu-id="ad59e-129">Specifies toorun installer in silent mode</span></span>| <span data-ttu-id="ad59e-130">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="ad59e-130">N/A</span></span>|


#### <a name="mobility-service-configuration-command-line"></a><span data-ttu-id="ad59e-131">Configuratie van Mobility-Service vanaf de opdrachtregel</span><span class="sxs-lookup"><span data-stu-id="ad59e-131">Mobility Service configuration command-line</span></span>

```
Usage:
cd /usr/local/ASR/Vx/bin
UnifiedAgentConfigurator.sh -i <CSIP> -P <PassphraseFilePath>
```

|<span data-ttu-id="ad59e-132">Parameter</span><span class="sxs-lookup"><span data-stu-id="ad59e-132">Parameter</span></span>|<span data-ttu-id="ad59e-133">Type</span><span class="sxs-lookup"><span data-stu-id="ad59e-133">Type</span></span>|<span data-ttu-id="ad59e-134">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="ad59e-134">Description</span></span>|<span data-ttu-id="ad59e-135">Mogelijke waarden</span><span class="sxs-lookup"><span data-stu-id="ad59e-135">Possible values</span></span>|
|-|-|-|-|
|<span data-ttu-id="ad59e-136">-i</span><span class="sxs-lookup"><span data-stu-id="ad59e-136">-i</span></span> |<span data-ttu-id="ad59e-137">Verplicht</span><span class="sxs-lookup"><span data-stu-id="ad59e-137">Mandatory</span></span>|<span data-ttu-id="ad59e-138">IP-adres van de configuratieserver Hallo</span><span class="sxs-lookup"><span data-stu-id="ad59e-138">IP of hello Configuration Server</span></span>|<span data-ttu-id="ad59e-139">Een geldig IP-adres</span><span class="sxs-lookup"><span data-stu-id="ad59e-139">Any valid IP Address</span></span>|
|<span data-ttu-id="ad59e-140">-P</span><span class="sxs-lookup"><span data-stu-id="ad59e-140">-P</span></span> |<span data-ttu-id="ad59e-141">Verplicht</span><span class="sxs-lookup"><span data-stu-id="ad59e-141">Mandatory</span></span>|<span data-ttu-id="ad59e-142">Volledig pad Hallo bestand waarin Hallo verbinding wachtwoordzin is opgeslagen</span><span class="sxs-lookup"><span data-stu-id="ad59e-142">Full file path hello file where hello connection passphrase is saved</span></span>|<span data-ttu-id="ad59e-143">Een geldige map</span><span class="sxs-lookup"><span data-stu-id="ad59e-143">Any valid folder</span></span>|
