
1. Meld u aan tooyour Azure-abonnement met Hallo stappen in [tooAzure verbinding van hello Azure CLI 1.0](../articles/xplat-cli-connect.md).

2. Zorg ervoor dat u in Hallo klassieke implementatiemodus zijn als volgt:

    ```azurecli
    azure config mode asm
    ```

3. Hallo Linux installatiekopie weten dat u wilt dat tooload uit de beschikbare installatiekopieën Hallo als volgt:

   ```azurecli   
    azure vm image list | grep "Linux"
    ```
   
    Gebruik in een opdrachtpromptvenster van Windows **find** in plaats van grep.
   
4. Gebruik `azure vm create` toocreate een virtuele machine met Linux-installatiekopie Hallo van Hallo vorige lijst. In deze stap maakt u een cloudservice en een opslagaccount. U kunt ook verbinding maken met deze VM tooan bestaande cloudservice met een `-c` optie. Maken van een SSH-eindpunt toolog in toohello virtuele Linux-machine Hello `-e` optie. Hallo volgende voorbeeld wordt een virtuele machine met de naam `myVM` met Hallo `Ubuntu-14_04_4-LTS` installatiekopie in Hallo `West US` locatie, en voegt u een gebruikersnaam `ops`:
   
    ```azurecli
    azure vm create myVM \
        b39f27a8b8c64d52b05eac6a62ebad85__Ubuntu-14_04_4-LTS-amd64-server-20160516-en-us-30GB \
        -g ops -p P@ssw0rd! -z "Small" -e -l "West US"
    ```

    Hallo uitvoer is vergelijkbaar toohello volgende voorbeeld:

    ```azurecli
    info:    Executing command vm create
    + Looking up image b39f27a8b8c64d52b05eac6a62ebad85__Ubuntu-14_04_4-LTS-amd64-server-20160516-en-us-30GB
    + Looking up cloud service
    info:    cloud service myVM not found.
    + Creating cloud service
    + Retrieving storage accounts
    + Creating VM
    info:    vm create command OK
    ```
   
   > [!NOTE]
   > Voor een virtuele Linux-machine, moet u opgeven Hallo `-e` optie in `vm create`. Het is niet mogelijk tooenable SSH nadat Hallo virtuele machine is gemaakt. Lees voor meer informatie over SSH [hoe tooUse SSH met Linux op Azure](../articles/virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

5. U kunt Hallo kenmerken van Hallo VM controleren via Hallo `azure vm show` opdracht. Hallo volgende voorbeeld vindt u gegevens voor de virtuele machine met de naam Hallo `myVM`:

    ```azurecli   
    azure vm show myVM
    ```

6. Start uw virtuele machine met Hallo `azure vm start` opdracht als volgt:

    ```azurecli
    azure vm start myVM
    ```

## <a name="next-steps"></a>Volgende stappen
Lees voor meer informatie over deze opdrachten voor de virtuele machine Azure CLI 1.0 Hallo [Using hello Azure CLI 1.0 met Hallo klassieke implementatie API](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).

