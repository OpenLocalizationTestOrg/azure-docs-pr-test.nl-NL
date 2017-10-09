# <a name="scale-agent-nodes-in-a-container-service-cluster"></a>Agentknooppunten schalen in een Container Service-cluster
Na [een Azure Container Service-cluster implementeren](../articles/container-service/dcos-swarm/container-service-deployment.md), moet u mogelijk toochange Hallo aantal knooppunten van de agent. U hebt mogelijk meer agents nodig zodat u meer containertoepassingen of -exemplaren kunt uitvoeren. 

U kunt het aantal knooppunten in een cluster DC/OS, Docker Swarm of Kubernetes agent Hallo wijzigen met behulp van hello Azure-portal of hello Azure CLI 2.0. 

## <a name="scale-with-hello-azure-portal"></a>Schalen Hello Azure-portal

1. In Hallo [Azure-portal](https://portal.azure.com), zoeken naar **containerservices**, en klik vervolgens op Hallo containerservice die u toomodify wilt.
2. In Hallo **containerservice** blade, klikt u op **Agents**.
3. In **aantal VM's**, Voer Hallo gewenst aantal agents knooppunten.

    ![Een groep in de portal Hallo schalen](./media/container-service-scale/container-service-scale-portal.png)

4. toosave hello configuratie, klikt u op **opslaan**.

## <a name="scale-with-hello-azure-cli-20"></a>Schalen Hello Azure CLI 2.0

Zorg ervoor dat u [geïnstalleerd](/cli/azure/install-az-cli2) Hallo nieuwste Azure CLI 2.0 en vastgelegd in tooan azure-account (`az login`).

### <a name="see-hello-current-agent-count"></a>Zie het huidige agent aantal Hallo
toosee hello aantal agents dat momenteel in Hallo-cluster, voert u Hallo `az acs show` opdracht. Dit betekent dat de clusterconfiguratie Hallo. Bijvoorbeeld, Hallo volgende opdracht geeft de configuratie van Hallo containerservice met de naam Hallo `containerservice-myACSName` in de resourcegroep Hallo `myResourceGroup`:

```azurecli
az acs show -g myResourceGroup -n containerservice-myACSName
```

Hallo opdracht retourneert het aantal agents Hallo in Hallo `Count` waarde onder `AgentPoolProfiles`.

### <a name="use-hello-az-acs-scale-command"></a>Gebruik Hallo az acs scale opdracht
toochange hello aantal knooppunten van de agent, Hallo uitvoeren `az acs scale` opdracht en leveringen Hallo **resourcegroep**, **service containernaam**, en Hallo gewenst **aantal nieuwe agent**. Door een kleiner of groter getal te gebruiken kunt u omlaag of omhoog schalen.

Typ bijvoorbeeld toochange Hallo aantal agents in de vorige cluster too10 hello, Hallo volgende opdracht:

```azurecli
az acs scale -g myResourceGroup -n containerservice-myACSName --new-agent-count 10
```

Hello Azure CLI 2.0 retourneert een JSON-tekenreeks voor van Hallo nieuwe configuratie van Hallo containerservice, inclusief Hallo nieuwe agent count.

Voer `az acs scale --help` uit voor meer opdrachtopties.

## <a name="scaling-considerations"></a>Overwegingen voor schalen

* het aantal knooppunten dat agent Hallo moet liggen tussen 1 en 100 liggen. 

* Het quotum voor kernen kunt Hallo aantal knooppunten in een cluster agent beperken.

* Agent knooppunt vergroten/verkleinen bewerkingen zijn toegepaste tooan Azure virtuele-machineschaalset weergeven die Hallo agent toepassingen bevat. In een DC/OS-cluster, worden alleen agent knooppunten in het persoonlijke groep Hallo geschaald Hallo bewerkingen worden weergegeven in dit artikel.

* Afhankelijk van de orchestrator Hallo die u in uw cluster implementeert, kunt u afzonderlijk Hallo aantal exemplaren van een container op Hallo cluster schalen. Bijvoorbeeld in een DC/OS-cluster gebruiken Hallo [Marathon-gebruikersinterface](../articles/container-service/dcos-swarm/container-service-mesos-marathon-ui.md) toochange Hallo aantal exemplaren van een containertoepassing.

* Automatisch schalen van agentknooppunten in een containerservicecluster wordt momenteel niet ondersteund.

## <a name="next-steps"></a>Volgende stappen
* Bekijk [meer voorbeelden](../articles/container-service/dcos-swarm/container-service-create-acs-cluster-cli.md) van de toepassing van Azure CLI 2.0-opdrachten met Azure Container Service.
* Meer informatie over [DC/OS-agentpools](../articles/container-service/dcos-swarm/container-service-dcos-agents.md) in Azure Container Service.

