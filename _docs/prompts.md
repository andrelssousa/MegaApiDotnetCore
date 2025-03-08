1) CRIAÇÃO DO CÓDIGO MARKDOWN:
-----------------------------------------------------------------------------------------------------------
Você é um especialista em criar documentação utilizando markdown.
Preciso criar um README.md para documentar um projeto. Vamos utilizar markdown para isso.

contexto:
Este projeto é de uma api feito em dotnet para listar os dados dos bosses de megaman, o objetivo principal é ser um backend que fornece jsons no formato abaixo:

```
{
  Id =1,
  Code = "DLN/DRN-003",
  Name = "Cutman",
  HP = 150,
  Picture = "https://vignette.wikia.nocookie.net/megaman/images/2/22/Cutman.png"
}
```

Especificações do projeto:

```
<Project Sdk="Microsoft.NET.Sdk.Web">

  <PropertyGroup>
    <TargetFramework>netcoreapp3.1</TargetFramework>
  </PropertyGroup>

  <ItemGroup>
    <PackageReference Include="Microsoft.EntityFrameworkCore" Version="3.1.8" />
    <PackageReference Include="Microsoft.EntityFrameworkCore.Design" Version="3.1.8">
      <IncludeAssets>runtime; build; native; contentfiles; analyzers; buildtransitive</IncludeAssets>
      <PrivateAssets>all</PrivateAssets>
    </PackageReference>
    <PackageReference Include="Microsoft.EntityFrameworkCore.SqlServer" Version="3.1.8" />
    <PackageReference Include="Newtonsoft.Json" Version="12.0.2" />
  </ItemGroup>

</Project>
```

os endpoints do projeto são:
namespace Megaman.Controllers

```
{
    //api/v1/robots
    [ApiController]
    [Route("api/v1/robots")]
    public class RobotsController : ControllerBase
    {
        private readonly IRobotServices _services;
        public RobotsController(IRobotServices services)
        {
           _services = services;
        }

        //GET api/robots
        [HttpGet]
        public ActionResult<IEnumerable<RobotReadDTO>> GetAllRobots()
        {
            var robotItems = _services.SearchAll();
            return Ok(robotItems);
        }

        //GET api/v1/robots/{id}
        [HttpGet]
        [Route("{id:int}")]
        public object GetCommandById([FromRoute]int id)
        {
            var robot = _services.SearchById(id);

            if(robot != null)
                return Ok(robot);

                return NotFound(
                        new { message = "Nenhum robo encontrado" }
                );
        }

        //POST api/v1/robots
        [HttpPost]
        public ActionResult RobotSend(){
            return Ok();
        }


    }
}
```

REGRAS:

- Sempre que citar alguma dependência do projeto, deixe ela como hyperlink para a página oficial daquela dependência

- Crie uma estrutura do projeto com base na arvore de pastas abaixo, e crie uma sessão para explicitar as técnicas utilizadas.
  Utilize ícones e linhas conectando as pastas conforme modelo abaixo:


Modelo:
```
├── 📂 Controllers      [Routes for endpoints]
├── 📂 Database         [Structures related to the database]
│   ├── 📂 EntityFramework  [Files related to the ORM Entity Framework]
│   │     ├── 📂 Context         [Entity context settings]
│   ├── 📂 Repositories     [Repository pattern]
```

Minha estrutura de pastas:
```
.vs
  MegamanApi
    v15
      .suo
.vscode
  launch.json
  tasks.json
bin
  Debug
    netcoreapp3.1
      Properties
        launchSettings.json
      runtimes
        unix
          lib
            netcoreapp2.0
              System.Runtime.Caching.dll
            netcoreapp2.1
              Microsoft.Data.SqlClient.dll
        win
          lib
            netcoreapp2.0
              System.Runtime.Caching.dll
            netcoreapp2.1
              Microsoft.Data.SqlClient.dll
            netstandard2.0
              System.Security.Cryptography.ProtectedData.dll
        win-arm64
          native
            sni.dll
        win-x64
          native
            sni.dll
        win-x86
          native
            sni.dll
      appsettings.Development.json
      appsettings.json
      global.json
      MegamanApi.deps.json
      MegamanApi.dll
      MegamanApi.exe
      MegamanApi.pdb
      MegamanApi.runtimeconfig.dev.json
      MegamanApi.runtimeconfig.json
      Microsoft.Bcl.AsyncInterfaces.dll
      Microsoft.Bcl.HashCode.dll
      Microsoft.Data.SqlClient.dll
      Microsoft.EntityFrameworkCore.Abstractions.dll
      Microsoft.EntityFrameworkCore.Design.dll
      Microsoft.EntityFrameworkCore.dll
      Microsoft.EntityFrameworkCore.Relational.dll
      Microsoft.EntityFrameworkCore.SqlServer.dll
      Microsoft.Extensions.Caching.Abstractions.dll
      Microsoft.Extensions.Caching.Memory.dll
      Microsoft.Extensions.Configuration.Abstractions.dll
      Microsoft.Extensions.Configuration.Binder.dll
      Microsoft.Extensions.Configuration.dll
      Microsoft.Extensions.DependencyInjection.Abstractions.dll
      Microsoft.Extensions.DependencyInjection.dll
      Microsoft.Extensions.Logging.Abstractions.dll
      Microsoft.Extensions.Logging.dll
      Microsoft.Extensions.Options.dll
      Microsoft.Extensions.Primitives.dll
      Microsoft.Identity.Client.dll
      Microsoft.IdentityModel.JsonWebTokens.dll
      Microsoft.IdentityModel.Logging.dll
      Microsoft.IdentityModel.Protocols.dll
      Microsoft.IdentityModel.Protocols.OpenIdConnect.dll
      Microsoft.IdentityModel.Tokens.dll
      Newtonsoft.Json.dll
      System.Collections.Immutable.dll
      System.Configuration.ConfigurationManager.dll
      System.Diagnostics.DiagnosticSource.dll
      System.IdentityModel.Tokens.Jwt.dll
      System.Runtime.Caching.dll
      System.Security.Cryptography.ProtectedData.dll
Controllers
  RobotsController.cs
Database
  DTOs
    Robots
      RobotCreateDTO.cs
      RobotReadDTO.cs
  EntityFramework
    Context
      RobotsContext.cs
    Migrations
      20201010003954_InitialMigration.cs
      20201010003954_InitialMigration.Designer.cs
      RobotsContextModelSnapshot.cs
  Repositories
    Robots
      IRobotRepository.cs
      MockRobotRepository.cs
      SqlRobotRepository.cs
middlewares
  MiddlewareLog.cs
  MiddlewareLogExtesions.cs
Models
  Robot.cs
obj
  Debug
    netcoreapp3.1
      staticwebassets
        MegamanApi.StaticWebAssets.Manifest.cache
        MegamanApi.StaticWebAssets.xml
      .NETCoreApp,Version=v3.1.AssemblyAttributes.cs
      apphost.exe
      MegamanApi.AssemblyInfo.cs
      MegamanApi.AssemblyInfoInputs.cache
      MegamanApi.assets.cache
      MegamanApi.csproj.AssemblyReference.cache
      MegamanApi.csproj.CopyComplete
      MegamanApi.csproj.CoreCompileInputs.cache
      MegamanApi.csproj.FileListAbsolute.txt
      MegamanApi.csprojAssemblyReference.cache
      MegamanApi.dll
      MegamanApi.exe
      MegamanApi.GeneratedMSBuildEditorConfig.editorconfig
      MegamanApi.genruntimeconfig.cache
      MegamanApi.MvcApplicationPartsAssemblyInfo.cache
      MegamanApi.pdb
      MegamanApi.RazorTargetAssemblyInfo.cache
  MegamanApi.csproj.nuget.dgspec.json
  MegamanApi.csproj.nuget.g.props
  MegamanApi.csproj.nuget.g.targets
  project.assets.json
  project.nuget.cache
Properties
  launchSettings.json
Services
  Robots
    IRobotServices.cs
    RobotServices.cs
appsettings.Development.json
appsettings.json
global.json
MegamanApi.csproj
MegamanApi.sln
Program.cs
Startup.cs
```

2) CRIAÇÃO DA IMAGEM DO MEGAMAN:
-----------------------------------------------------------------------------------------------------------
Preciso de um prompt pra criar uma imagem similar a esta: ./_docs/assets/megaman_original.jpeg

Ilustração digital de um personagem robótico estilizado com um capacete azul futurista e um cristal vermelho no centro. O personagem tem olhos verdes expressivos e um rosto jovem e determinado. O design do capacete possui detalhes metálicos e um visual tecnológico avançado. A arte deve ter um estilo vibrante e limpo, lembrando ilustrações de jogos e animes futuristas. Adicione algo do github e simbolos de tecnologia, pois é pra ser utilizado em uma apresentação de trabalhos de programação.

Remoção de cor de fundo utilizando CANVA (por AI)

3) ALTERAÇÃO DE MARKDOWN INCLUINDO A IMAGEM
-----------------------------------------------------------------------------------------------------------
Adicione uma imagem em markdown antes do texto Megaman API	
# Megaman API
