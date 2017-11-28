### <a name="install-via-composer"></a><span data-ttu-id="500ec-101">Installeren via de Composer</span><span class="sxs-lookup"><span data-stu-id="500ec-101">Install via Composer</span></span>
1. <span data-ttu-id="500ec-102">[Installeer Git][install-git].</span><span class="sxs-lookup"><span data-stu-id="500ec-102">[Install Git][install-git].</span></span> <span data-ttu-id="500ec-103">Houd er rekening mee dat in Windows, u ook het Git uitvoerbare bestand aan de omgevingsvariabele PATH toevoegen moet.</span><span class="sxs-lookup"><span data-stu-id="500ec-103">Note that on Windows, you must also add the Git executable to your PATH environment variable.</span></span> 
2. <span data-ttu-id="500ec-104">Maak een bestand met de naam **composer.json** in de hoofdmap van uw project en voeg de volgende code toe:</span><span class="sxs-lookup"><span data-stu-id="500ec-104">Create a file named **composer.json** in the root of your project and add the following code to it:</span></span>
   
    ```json
    {
      "require": {
        "microsoft/windowsazure": "^0.4"
      }
    }
    ```
3. <span data-ttu-id="500ec-105">Download  **[composer.phar] [ composer-phar]**  in de hoofdmap van uw project.</span><span class="sxs-lookup"><span data-stu-id="500ec-105">Download **[composer.phar][composer-phar]** in your project root.</span></span>
4. <span data-ttu-id="500ec-106">Open een opdrachtprompt en voer de volgende opdracht in de hoofdmap van uw project</span><span class="sxs-lookup"><span data-stu-id="500ec-106">Open a command prompt and execute the following command in your project root</span></span>
   
    ```
    php composer.phar install
    ```

[php-sdk-github]: http://go.microsoft.com/fwlink/?LinkId=252719
[install-git]: http://git-scm.com/book/en/Getting-Started-Installing-Git
[download-SDK-PHP]: ../articles/php-download-sdk.md
[composer-phar]: http://getcomposer.org/composer.phar
