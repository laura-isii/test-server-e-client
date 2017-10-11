# Prerequisiti
- Visual Studio Code ([ultima disponibile](https://code.visualstudio.com/download))
    - Git For Windows è incluso
- [Node 8+](https://www.nodejs.org)
- [.NET Core 2.0+](https://www.microsoft.com/net/core#windowscmd)

1. Installare `@angular/cli` (da terminale)
```cmd
npm install -g @angular/cli
```

# Creazione della soluzione
1. Creare una cartella con il nome della soluzione
1. Aprire un terminale entro quest'ultima
    * Un modo semplice è `SHIFT + Click-destro` e quindi *Apri Powershell*
1. Creare il progetto Angular:
    ```
    ng new web
    ```
1. Creare la WebAPI ASP.NET Core:
    ```
    dotnet new webapi -o myapi
    ```
1. Lanciare Visual Studio Code
    ```
    code .
    ```

# Avviare la soluzione
1. Dentro VS Code, aprire un primo terminale (`CTRL + ò`)
    ```
    cd web
    ng serve
    ```
1. Aprire un secondo terminale, tramite il tasto "+" nel terminale già aperto.
1. Lanciare anche la Web API
    ```
    cd myapi
    dotnet run
    ```

# Altre configurazioni

## CORS

E' necessario attivare il **Cross-Origin Resource Sharing** per consentire al frontend Angular (in esecuzione, di default, su http://localhost:4200) di accedere alla Web API (di default http://localhost:5000).

1. Aprire `ValueController.cs` in *myapi/Controllers*
1. Modificare come segue:
    ```csharp
    [Route("api/[controller]")]
    [EnableCors("*")] // Aggiungere
    public class ValuesController : Controller
    ```

**NOTA**: se l'applicazione è già in esecuzione, è necessario riavviarla.

## dotnet watch

Un utile ausilio allo sviluppo di progetti .NET Core è il comando `dotnet watch`, che riavvia automaticamente il server Web API quando si modificano i sorgenti. La procedura è descritta nella [documentazione ufficiale](https://github.com/aspnet/Docs/blob/master/aspnetcore/tutorials/dotnet-watch.md) ed è qui riportata:

1. Aprire il file `.csproj` in *myapi*
1. Modificarlo come segue:
    ```xml
      <ItemGroup>
        <!--Altro se presente-->      
        <DotNetCliToolReference Include="Microsoft.DotNet.Watcher.Tools" Version="2.0.0" />
    </ItemGroup>
    ```
1. Aprire il terminale
    ```
    cd myapi
    dotnet restore
    dotnet watch run
    ```
1. E' ora possibile vedere le modifiche applicate al codice senza riavvare *myapi*.

# Pubblicazione su Github

## Creazione del repository

1. Accedere a [github.com](https://github.com)
1. Selezionare *Start a project*
1. Immettere semplicemente un nome, ed opzionalmente una descrizione. Lasciare gli altri campi intatti.
1. Seguire le istruzioni per *"...add existing repository"*. Eseguire i comandi nel terminale di VS Code, a livello di root. Se necessario, immettere le proprie credenziali per il comando `git push`.

## Aggiunta di collaboratori

1. Dalla pagina del repository appena creato, individuare il tab *Settings*
1. Selezionare la sotto voce *Collaborators* e invitare gli altri utenti tramite email o nickname. Devono già essere registrati.

## Clonare il repository

Per iniziare a sviluppare, i nuovi utenti devono eseguire il *clone* del repository.

1. Dalla homepage del repository, tab *Code*, individuare e cliccare il pulsante verde *Clone or download*
1. Cliccare l'icona accanto all'URL (*Copy to clipboard*)
1. In una cartella adatta, aprire un terminale e quindi:
    ```cmd
    git clone <URL COPIATO>
    ```
    Questo clonerà il codice nella cartella corrente. In alternativa:
    ```cmd
    git clone <URL COPIATO> <cartella soluzione>
    ```
    Creerà la cartella indicata e vi copierà i file.

## Pushare le modifiche su Github
Di base, Git è uno strumento **locale**, che opera quindi sul PC dell'utente. Procedere normalmente con i vari *commit*. Per condividere gli sviluppi fatti, poi, è sufficiente:

1. In VS Code, aprire il tab *Controllo del codice sorgente* (icona simile ad una forbice)
1. Andare sui "..." e cliccare "Esegui Push".

Per ricevere le modifiche altrui, cliccare invece *Esegui pull*.

**NOTA**: In modo compatto, è presente un'icona "ricircolo" nella status bar di VS Code, a sinistra. Questo comando esegue prima un pull e quindi un push. Di norma, presenta due numeri, i commit in arrivo e quelli in uscita.