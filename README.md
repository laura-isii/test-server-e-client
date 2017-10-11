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
