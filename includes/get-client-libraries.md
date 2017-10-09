### <a name="install-via-composer"></a><span data-ttu-id="e1f0b-101">Installeren via de Composer</span><span class="sxs-lookup"><span data-stu-id="e1f0b-101">Install via Composer</span></span>
1. <span data-ttu-id="e1f0b-102">[Installeer Git][install-git].</span><span class="sxs-lookup"><span data-stu-id="e1f0b-102">[Install Git][install-git].</span></span> <span data-ttu-id="e1f0b-103">Houd er rekening mee dat in Windows, u ook Hallo Git uitvoerbare tooyour pad-omgevingsvariabele toevoegen moet.</span><span class="sxs-lookup"><span data-stu-id="e1f0b-103">Note that on Windows, you must also add hello Git executable tooyour PATH environment variable.</span></span> 
2. <span data-ttu-id="e1f0b-104">Maak een bestand met de naam **composer.json** in Hallo hoofdmap van uw project en voeg Hallo code tooit te volgen:</span><span class="sxs-lookup"><span data-stu-id="e1f0b-104">Create a file named **composer.json** in hello root of your project and add hello following code tooit:</span></span>
   
    ```json
    {
      "require": {
        "microsoft/windowsazure": "^0.4"
      }
    }
    ```
3. <span data-ttu-id="e1f0b-105">Download  **[composer.phar] [ composer-phar]**  in de hoofdmap van uw project.</span><span class="sxs-lookup"><span data-stu-id="e1f0b-105">Download **[composer.phar][composer-phar]** in your project root.</span></span>
4. <span data-ttu-id="e1f0b-106">Open een opdrachtprompt en Hallo volgende opdracht in de hoofdmap van uw project uitvoeren</span><span class="sxs-lookup"><span data-stu-id="e1f0b-106">Open a command prompt and execute hello following command in your project root</span></span>
   
    ```
    php composer.phar install
    ```

[php-sdk-github]: http://go.microsoft.com/fwlink/?LinkId=252719
[install-git]: http://git-scm.com/book/en/Getting-Started-Installing-Git
[download-SDK-PHP]: ../articles/php-download-sdk.md
[composer-phar]: http://getcomposer.org/composer.phar
