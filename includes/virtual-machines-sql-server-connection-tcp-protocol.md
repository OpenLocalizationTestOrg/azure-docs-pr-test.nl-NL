1. Tijdens het verbonden toohello virtuele machine via Extern bureaublad zoekt **Configuration Manager**:

    ![SSCM openen](./media/virtual-machines-sql-server-connection-tcp-protocol/sql-server-configuration-manager.png)

1. In SQL Server Configuration Manager in het consolevenster hello, vouw **SQL Server-netwerkconfiguratie**.

1. Klik in het consolevenster hello, **protocollen voor MSSQLSERVER** (Hallo standaard exemplaarnaam.) In het deelvenster details Hallo met de rechtermuisknop op **TCP** en klik op **inschakelen** als deze nog niet is ingeschakeld.

    ![TCP inschakelen](./media/virtual-machines-sql-server-connection-tcp-protocol/enable-tcp.png)

1. Klik in het consolevenster hello, **SQL Server-Services**. In het deelvenster details Hallo met de rechtermuisknop op  **SQL Server (*exemplaarnaam*) ** (Hallo-standaardexemplaar is **SQL Server (MSSQLSERVER)**), en klik vervolgens op **opnieuw starten** , toostop en opnieuw starten Hallo-exemplaar van SQL Server.

    ![Database-engine opnieuw starten](./media/virtual-machines-sql-server-connection-tcp-protocol/restart-sql-server.png)

1. Sluit SQL Server Configuration Manager.

Zie voor meer informatie over het inschakelen van protocollen voor SQL Server Database Engine Hallo [in- of uitschakelen van een Server netwerkprotocol](http://msdn.microsoft.com/library/ms191294.aspx).
