Wanneer u een gegevensschijf die is aangesloten tooa virtuele machine niet meer nodig hebt, kunt u deze eenvoudig loskoppelen. Een schijf wordt losgekoppeld Hallo schijf verwijdert uit Hallo virtuele machine, maar niet Hallo schijf verwijderen uit hello Azure storage-account.

Als u toouse Hallo bestaande gegevens op Hallo schijf opnieuw wilt, u kunt opnieuw het toohello dezelfde virtuele machine of een andere naam.  

> [!NOTE]
> toodetach schijf van een besturingssysteem, moet u eerst toodelete Hallo virtuele machine.
>

## <a name="find-hello-disk"></a>Hallo schijf gevonden
Als u de naam van de Hallo van schijf Hallo of tooverify wilt niet weet het voordat u deze loskoppelen, als volgt te werk.

1. Meld u aan toohello [Azure-portal](https://portal.azure.com).

2. Klik op **virtuele Machines**, en vervolgens selecteert Hallo juiste VM.

3. Klik op **schijven** langs Hallo de linkerrand van dashboard van de virtuele machine hello, onder **instellingen**.

 Hallo virtuele machine dashboard geeft een lijst Hallo naam en type van alle gekoppelde schijven. Op dit scherm wordt bijvoorbeeld een virtuele machine weergegeven met een besturingssysteemschijf en een gegevensschijf:

    ![Gegevensschijf vinden](./media/howto-detach-disk-windows-linux/vmwithdisklist.png)

## <a name="detach-hello-disk"></a>Ontkoppel de schijf Hallo
1. Hallo Azure-portal, klik op **virtuele Machines**, en klik vervolgens op Hallo-naam van Hallo virtuele machine die Hallo gegevensschijf gewenste toodetach heeft.

2. Klik op **schijven** langs Hallo de linkerrand van dashboard van de virtuele machine hello, onder **instellingen**.

3. Klik op de gewenste toodetach Hallo-schijf.

  ![Hallo schijf toodetach identificeren](./media/howto-detach-disk-windows-linux/disklist.png)

4. Hallo opdrachtbalk en klik op **Detach**.

  ![Zoek Hallo loskoppelen van de opdracht](./media/howto-detach-disk-windows-linux/diskdetachcommand.png)

5. Klik in het bevestigingsvenster hello, **Ja** toodetach Hallo schijf.

  ![Loskoppelen Hallo schijf bevestigen](./media/howto-detach-disk-windows-linux/confirmdetach.png)

Hallo schijf blijft in de opslag, maar is niet langer gekoppelde tooa virtuele machine.
