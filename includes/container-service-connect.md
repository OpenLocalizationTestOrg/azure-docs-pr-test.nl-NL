# <a name="make-a-remote-connection-tooa-kubernetes-dcos-or-docker-swarm-cluster"></a>Een verbinding met extern tooa Kubernetes, DC/OS of Docker Swarm-cluster maken
Na het maken van een Azure Container Service-cluster moet tooconnect toohello cluster toodeploy en werkbelasting moet worden beheerd. Dit artikel wordt beschreven hoe tooconnect toohello master VM Hallo-cluster van een externe computer. 

Hallo Kubernetes DC/OS en Docker Swarm-clusters bieden lokaal HTTP-eindpunten. Kubernetes, dit eindpunt is veilig zichtbaar op Hallo van internet en u toegang hebt tot het door het uitvoeren van Hallo `kubectl` opdrachtregelprogramma vanaf een willekeurige computer met internet verbonden. 

U wordt aangeraden dat u een tunnel secure shell (SSH) in uw lokale computer toohello cluster-beheersysteem maakt voor DC/OS- en Docker Swarm. Nadat het Hallo-tunnel wordt ingesteld, kunt u welke Hallo HTTP-eindpunten en weergave Hallo orchestrator webinterface (indien beschikbaar) van het lokale systeem opdrachten kunt uitvoeren. 

## <a name="prerequisites"></a>Vereisten

* Een Kubernetes-, DC/OS- of Docker Swarm-cluster, [geïmplementeerd in Azure Container Service](../articles/container-service/dcos-swarm/container-service-deployment.md).
* SSH-RSA persoonlijke sleutelbestand, toohello openbare sleutel toegevoegde toohello cluster overeenkomt tijdens de implementatie. Deze opdrachten wordt ervan uitgegaan dat Hallo persoonlijke SSH-sleutel is in `$HOME/.ssh/id_rsa` op uw computer. Zie deze instructies voor [macOS en Linux](../articles/virtual-machines/linux/mac-create-ssh-keys.md) of [Windows](../articles/virtual-machines/linux/ssh-from-windows.md) voor meer informatie. Als Hallo SSH-verbinding niet werkt, moet u mogelijk te [opnieuw instellen van uw SSH-sleutels](../articles/virtual-machines/linux/troubleshoot-ssh-connection.md).

## <a name="connect-tooa-kubernetes-cluster"></a>Verbinding maken met tooa Kubernetes cluster

Volg deze stappen tooinstall en configureer `kubectl` op uw computer.

> [!NOTE] 
> Op Linux- of Mac OS, moet u mogelijk toorun Hallo opdrachten in deze sectie met `sudo`.
> 

### <a name="install-kubectl"></a>Kubectl installeren
Eenzijdige tooinstall dit hulpprogramma is toouse hello `az acs kubernetes install-cli` Azure CLI 2.0-opdracht. toorun dit uitvoert, en zorg ervoor dat u [geïnstalleerd](/cli/azure/install-az-cli2) Hallo nieuwste Azure CLI 2.0 en vastgelegd in tooan Azure-account (`az login`).

```azurecli
# Linux or macOS
az acs kubernetes install-cli [--install-location=/some/directory/kubectl]

# Windows
az acs kubernetes install-cli [--install-location=C:\some\directory\kubectl.exe]
```

U kunt ook u recente Hallo kunt downloaden `kubectl` client rechtstreeks vanuit Hallo [Kubernetes releases pagina](https://github.com/kubernetes/kubernetes/blob/master/CHANGELOG.md). Zie [Installing and Setting up kubectl](https://kubernetes.io/docs/tasks/kubectl/install/) (kubectl installeren en instellen) voor meer informatie.

### <a name="download-cluster-credentials"></a>Clusterreferenties downloaden
Zodra u hebt `kubectl` geïnstalleerd, moet u toocopy Hallo cluster referenties tooyour machine. Eenzijdige toodo get Hallo referenties is Hello `az acs kubernetes get-credentials` opdracht. Hallo-naam van resourcegroep Hallo en Hallo-naam van Hallo container servicebron doorgeven:

```azurecli
az acs kubernetes get-credentials --resource-group=<cluster-resource-group> --name=<cluster-name>
```

Met deze opdracht downloadt Hallo cluster referenties te`$HOME/.kube/config`, waarbij `kubectl` verwacht toobe zich bevindt.

U kunt ook gebruiken `scp` toosecurely-bestand kopiëren Hallo van `$HOME/.kube/config` op Hallo master VM tooyour lokale machine. Bijvoorbeeld:

```bash
mkdir $HOME/.kube
scp azureuser@<master-dns-name>:.kube/config $HOME/.kube/config
```

Als u van Windows gebruikmaakt, kunt u Bash op Ubuntu op Windows hello PuTTy beveiligd bestand kopiëren-client of een vergelijkbaar hulpprogramma.

### <a name="use-kubectl"></a>Kubectl gebruiken

Zodra u hebt `kubectl` geconfigureerd, de testverbinding Hallo door Hallo knooppunten in het cluster te bieden:

```bash
kubectl get nodes
```

U kunt andere `kubectl`-opdrachten proberen. U kunt bijvoorbeeld Hallo Kubernetes Dashboard weergeven. Voer een proxy eerst toohello Kubernetes API-server:

```bash
kubectl proxy
```

Hallo Kubernetes UI is nu beschikbaar op: `http://localhost:8001/ui`.

Zie voor meer informatie, Hallo [Kubernetes snel starten](http://kubernetes.io/docs/user-guide/quick-start/).

## <a name="connect-tooa-dcos-or-swarm-cluster"></a>Verbinding maken met tooa DC/OS of Swarm-cluster

toouse hello DC/OS- en Docker Swarm-clusters die zijn geïmplementeerd met Azure Container Service, volgt deze instructies toocreate een SSH-tunnel in uw lokale Linux-, Mac OS- of Windows-systeem. 

> [!NOTE]
> Deze instructies zijn gericht op tunneling van TCP-verkeer via SSH. U kunt ook een interactieve SSH-sessie starten met een beheersystemen voor Hallo binnen het cluster, maar dit wordt niet aanbevolen. Wanneer er rechtstreeks in een intern systeem wordt gewerkt, ontstaat het risico dat er onbedoeld configuratiewijzigingen worden doorgevoerd.  
> 

### <a name="create-an-ssh-tunnel-on-linux-or-macos"></a>Een SSH-tunnel maken in Linux of macOS
Hallo eerste wat u doet wanneer u een SSH-tunnel maken in Linux of Mac OS is toolocate Hallo openbare DNS-naam van masters met gelijke taakverdeling Hallo. Volg deze stappen:


1. In Hallo [Azure-portal](https://portal.azure.com), bladeren toohello resourcegroep met de container service-cluster. Vouw de resourcegroep Hallo zodat elke resource wordt weergegeven. 

2. Klik op Hallo **containerservice** bron en klik op **overzicht**. Hallo **Master FQDN** Hallo cluster wordt weergegeven onder **Essentials**. Bewaar deze naam voor later gebruik. 

    ![Openbare DNS-naam](./media/container-service-connect/pubdns.png)

    Ook uitvoeren Hallo `az acs show` opdracht in de containerservice. Zoek naar Hallo **Master profiel: fqdn** eigenschap in de opdrachtuitvoer Hallo.

3. Nu een shell openen en uitvoeren van Hallo `ssh` opdracht door te geven Hallo volgende waarden: 

    **LOCAL_PORT** is TCP-poort Hallo Hallo service zijde van Hallo tunnel tooconnect aan. Voor Swarm is dit too2375 instellen Voor DC/OS, stelt u deze too80. 
    **REMOTE_PORT** Hallo-poort van het Hallo-eindpunt dat u wilt dat tooexpose. Voor Swarm gebruikt u poort 2375. Gebruik poort 80 voor DC/OS.  
    **GEBRUIKERSNAAM** Hallo-gebruikersnaam die is opgegeven tijdens de implementatie Hallo-cluster is.  
    **DNSPREFIX** Hallo DNS-voorvoegsel op dat u hebt opgegeven tijdens de implementatie Hallo-cluster is.  
    **REGIO** Hallo regio waarin uw resourcegroep zich bevindt.  
    **PATH_TO_PRIVATE_KEY** [optioneel] is Hallo pad toohello persoonlijke sleutel die overeenkomt met toohello openbare sleutel die u hebt opgegeven toen u Hallo cluster hebt gemaakt. Gebruik deze optie Hello `-i` vlag.

    ```bash
    ssh -fNL LOCAL_PORT:localhost:REMOTE_PORT -p 2200 [USERNAME]@[DNSPREFIX]mgmt.[REGION].cloudapp.azure.com
    ```
  
  > [!NOTE]
  > Hallo poort SSH-verbinding is 2200 en niet Hallo standaard poort 22. In een cluster met meer dan één master VM is dit Hallo verbinding poort toohello eerste master VM.
  > 

  Hallo-opdracht geretourneerd zonder uitvoer.

Zie Hallo voorbeelden voor DC/OS- en Swarm in Hallo uit te voeren.    

### <a name="dcos-tunnel"></a>DC/OS-tunnel
tooopen een tunnel voor DC/OS-eindpunten, een opdracht zoals Hallo volgende uitvoeren:

```bash
sudo ssh -fNL 80:localhost:80 -p 2200 azureuser@acsexamplemgmt.japaneast.cloudapp.azure.com 
```

> [!NOTE]
> Zorg ervoor dat u geen ander lokaal proces hebt dat een binding heeft met poort 80. U kunt indien nodig een andere lokale poort dan poort 80 opgeven, bijvoorbeeld poort 8080. Sommige web-UI-koppelingen werken echter niet wanneer u deze poort gebruikt.
>

U kunt nu toegang tot Hallo DC/OS-eindpunten van uw lokale systeem via Hallo volgende URL's (ervan uitgaande dat de lokale poort 80):

* DC/OS: `http://localhost:80/`
* Marathon: `http://localhost:80/marathon`
* Mesos: `http://localhost:80/mesos`

U kunt op deze manier Hallo rest API's voor elke toepassing via deze tunnel bereiken.

### <a name="swarm-tunnel"></a>Swarm-tunnel
tooopen een tunnel toohello Swarm-eindpunt een opdracht zoals Hallo volgende uitvoeren:

```bash
ssh -fNL 2375:localhost:2375 -p 2200 azureuser@acsexamplemgmt.japaneast.cloudapp.azure.com
```
> [!NOTE]
> Zorg ervoor dat u geen ander lokaal proces hebt dat een binding heeft met poort 2375. Bijvoorbeeld, als u Hallo Docker-daemon lokaal uitvoert, wordt ingesteld door toouse standaardpoort 2375. U kunt indien nodig een andere lokale poort dan poort 2375 opgeven.
>

U kunt nu toegang tot Hallo Docker Swarm-cluster met behulp van Hallo Docker-opdrachtregelinterface (Docker CLI) op het lokale systeem. Zie [Docker installeren](https://docs.docker.com/engine/installation/) voor installatie-instructies.

Stel uw DOCKER_HOST omgeving variabele toohello lokale poort die u hebt geconfigureerd voor het Hallo-tunnel. 

```bash
export DOCKER_HOST=:2375
```

Voer Docker-opdrachten die tunnel toohello Docker Swarm-cluster. Bijvoorbeeld:

```bash
docker info
```

### <a name="create-an-ssh-tunnel-on-windows"></a>Een SSH-tunnel maken in Windows
Er zijn meerdere opties voor het maken van SSH-tunnels in Windows. Als u Bash op Ubuntu op Windows of een vergelijkbaar hulpprogramma uitvoert, kunt u Hallo SSH tunneling instructies die eerder in dit artikel voor Mac OS- en Linux worden weergegeven. Als alternatief voor Windows in deze sectie wordt beschreven hoe toouse PuTTY toocreate Hallo-tunnel.

1. [Download PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) tooyour Windows-systeem.

2. Hallo-toepassing uitvoeren.

3. Voer een hostnaam die uit Hallo cluserbeheerdergebruiker en Hallo openbare DNS-naam van de eerste master Hallo in Hallo-cluster bestaat. Hallo **hostnaam** lijkt te`azureuser@PublicDNSName`. Voer 2200 voor Hallo **poort**.

    ![PuTTY-configuratie 1](./media/container-service-connect/putty1.png)

4. Selecteer **SSH > Verificatie**. Voeg een pad tooyour persoonlijke sleutelbestand (ppk-indeling) voor verificatie. U kunt een hulpprogramma zoals [PuTTYgen](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) toogenerate dit bestand van Hallo SSH-sleutel gebruikt toocreate Hallo cluster.

    ![PuTTY-configuratie 2](./media/container-service-connect/putty2.png)

5. Selecteer **SSH > Tunnels** en Hallo volgende doorgestuurde poorten te configureren:

    * **Bronpoort:** gebruik 80 voor DC/OS of 2375 voor Swarm.
    * **Doelpoort:** gebruik localhost:80 voor DC/OS of localhost:2375 voor Swarm.

    Hallo volgende voorbeeld is geconfigureerd voor DC/OS, maar ziet er ongeveer voor Docker Swarm.

    > [!NOTE]
    > Poort 80 mag niet in gebruik zijn wanneer u deze tunnel maakt.
    > 

    ![PuTTY-configuratie 3](./media/container-service-connect/putty3.png)

6. Wanneer u klaar bent, klikt u op **sessie > Opslaan** toosave Hallo verbindingsconfiguratie.

7. tooconnect toohello PuTTY-sessie, klikt u op **Open**. Wanneer u verbinding maakt, ziet u de poortconfiguratie Hallo in Hallo PuTTY-gebeurtenislogboek.

    ![PuTTY-gebeurtenislogboek](./media/container-service-connect/putty4.png)

Nadat u hebt Hallo tunnel voor DC/OS geconfigureerd, kunt u toegang tot Hallo gerelateerde eindpunten op:

* DC/OS: `http://localhost/`
* Marathon: `http://localhost/marathon`
* Mesos: `http://localhost/mesos`

Nadat u hebt Hallo tunnel voor Docker Swarm geconfigureerd, opent u uw Windows-instellingen tooconfigure een systeemomgevingsvariabele met de naam `DOCKER_HOST` met een waarde van `:2375`. Vervolgens kunt u toegang tot Hallo Swarm-cluster via Hallo Docker CLI.

## <a name="next-steps"></a>Volgende stappen
Containers in het cluster implementeren en beheren:

* [Werken met de Azure Container Service en Kubernetes](../articles/container-service/kubernetes/container-service-kubernetes-ui.md)
* [Werken met de Azure Container Service en DC/OS](../articles/container-service//dcos-swarm/container-service-mesos-marathon-rest.md)
* [Werken met hello Azure Container Service en Docker Swarm](../articles//container-service/dcos-swarm/container-service-docker-swarm.md)

