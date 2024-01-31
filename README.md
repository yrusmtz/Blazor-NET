Stacks de tecnologias utilizadas
Microsotf Entity Framework como orm
Minimals Api
Docker como contenedor
ASP.NET 8
C#
MYSQL Server

![image](https://github.com/yrusmtz/Blazor-NET/assets/79479231/12bc35c8-48e2-45dd-911d-f64526d34743)

# Login y Manejo de estado en Blazor
![Captura de pantalla 2024-01-31 141325](https://github.com/yrusmtz/Blazor-NET/assets/79479231/b726f8ad-9520-4c07-911c-8085b5ddba63)

![Captura de pantalla 2024-01-31 142101](https://github.com/yrusmtz/Blazor-NET/assets/79479231/2bd615eb-198d-4f50-9b29-3efe45bb686d)
![Captura de pantalla 2024-01-31 141151](https://github.com/yrusmtz/Blazor-NET/assets/79479231/1310894a-9a24-4e78-b8b9-8e67c38ca3ba)
![Captura de pantalla 2024-01-31 142952](https://github.com/yrusmtz/Blazor-NET/assets/79479231/b5c7c367-01de-4cba-b7be-d326eb7466cc)
![Captura de pantalla 2024-01-31 143253](https://github.com/yrusmtz/Blazor-NET/assets/79479231/bb3925c8-a095-4ea9-849a-211094949cd8)



## Manejo de estado en Blazor
El manejo de estado en Blazor se refiere a la forma en que tu aplicación maneja y mantiene la información del usuario y de la aplicación entre las solicitudes del usuario. Esto es especialmente importante en las aplicaciones de una sola página (SPA), como las aplicaciones Blazor, donde la aplicación se ejecuta en el navegador del cliente.

En Blazor, hay varias formas de manejar el estado:

1. **Estado del componente**: El estado del componente se mantiene dentro del componente y se pierde cuando el componente se destruye. Este es el tipo de estado más simple y se puede manejar simplemente con variables en el componente.

2. **Servicios Singleton**: Los servicios Singleton son servicios que se crean una vez por aplicación y se pueden usar para mantener el estado que se comparte entre varios componentes.

3. **LocalStorage y SessionStorage**: Estos son mecanismos proporcionados por el navegador que permiten almacenar el estado entre sesiones de usuario. LocalStorage mantiene la información incluso después de cerrar y abrir el navegador, mientras que SessionStorage mantiene la información solo mientras el navegador está abierto.

4. **Blazored.LocalStorage**: Es una biblioteca que proporciona una forma fácil de usar LocalStorage y SessionStorage en Blazor.

5. **Server-side state management**: En las aplicaciones Blazor Server, el estado se puede mantener en el servidor entre las solicitudes del usuario. Esto se puede hacer usando SignalR para mantener una conexión en tiempo real entre el cliente y el servidor.

~~~mermaid
graph TB
    A[Aplicación Blazor] --> B[Estado del Componente]
    A --> C[Servicios Singleton]
    A --> D[LocalStorage y SessionStorage]
    A --> E[Blazored.LocalStorage]
    A --> F[Server-side state management]
    B --> G[Variables en el componente]
    C --> H[Servicio creado una vez por aplicación]
    D --> I[Almacenamiento entre sesiones de usuario]
    E --> J[Biblioteca para usar LocalStorage y SessionStorage]
    F --> K[Estado mantenido en el servidor entre solicitudes]
~~~


## Local Storage, Browser Storage y Memory Storage in Blazor
Claro, puedo proporcionar más detalles sobre estos tres tipos de almacenamiento en Blazor.

1. **Local Storage**: Local Storage es una característica del navegador web que permite a las aplicaciones web almacenar datos en el lado del cliente. Los datos almacenados en Local Storage son persistentes, lo que significa que los datos se mantienen incluso después de cerrar y abrir el navegador. En Blazor, puedes usar Local Storage para almacenar datos que necesitas mantener entre las sesiones del usuario, como la información de autenticación del usuario. Para usar Local Storage en Blazor, puedes usar la API de JavaScript Interop para interactuar con Local Storage directamente, o puedes usar una biblioteca como Blazored.LocalStorage que proporciona una interfaz .NET para Local Storage.

2. **Browser Storage (Session Storage)**: Session Storage es similar a Local Storage en que permite a las aplicaciones web almacenar datos en el lado del cliente. Sin embargo, a diferencia de Local Storage, los datos almacenados en Session Storage se pierden cuando se cierra la sesión del navegador. Esto lo hace útil para almacenar datos que solo necesitas mantener mientras el usuario está navegando en tu aplicación, como el estado de la interfaz de usuario. Al igual que con Local Storage, puedes usar la API de JavaScript Interop para interactuar con Session Storage directamente, o puedes usar una biblioteca como Blazored.SessionStorage.

3. **Memory Storage**: En Blazor, el almacenamiento en memoria se refiere a los datos que se almacenan en la memoria del servidor o del cliente mientras la aplicación está en ejecución. Los datos almacenados en la memoria se pierden cuando se cierra la aplicación o cuando se recicla el proceso del servidor. En Blazor Server, puedes usar el almacenamiento en memoria para mantener los datos entre las solicitudes del usuario mientras mantienes una conexión en tiempo real entre el cliente y el servidor con SignalR. En Blazor WebAssembly, el almacenamiento en memoria se limita a la vida útil de la aplicación en el navegador del cliente.

Es importante tener en cuenta que cada uno de estos métodos de almacenamiento tiene sus propias limitaciones y consideraciones de seguridad. Por ejemplo, tanto Local Storage como Session Storage están limitados en tamaño (generalmente a unos pocos MB), y los datos almacenados en ellos son accesibles para cualquier código JavaScript que se ejecute en la misma página, lo que puede ser un problema de seguridad si estás almacenando datos sensibles. Por otro lado, el almacenamiento en memoria puede ser más seguro ya que los datos se mantienen en el servidor, pero también puede ser más costoso en términos de uso de la memoria.

### localstorage para guardar el token de acceso
LocalStorage es conveniente en este caso de uso por varias razones:

1. **Persistencia**: LocalStorage permite almacenar datos de manera persistente en el navegador del cliente. Esto significa que los datos, como el token de acceso y la información del usuario, se mantendrán incluso después de cerrar y abrir el navegador. Esto es útil para mantener al usuario autenticado entre sesiones.

2. **Facilidad de uso**: Con la biblioteca Blazored.LocalStorage, es fácil interactuar con LocalStorage desde Blazor. Puedes almacenar y recuperar datos con simples llamadas a métodos.

3. **Almacenamiento en el lado del cliente**: Al almacenar los datos en el navegador del cliente, reduces la carga en tu servidor y evitas tener que transmitir estos datos entre el cliente y el servidor.

4. **Compatibilidad**: LocalStorage es compatible con todos los navegadores modernos, lo que significa que tu aplicación funcionará para la mayoría de los usuarios.

Sin embargo, es importante tener en cuenta que LocalStorage tiene sus limitaciones y consideraciones de seguridad. Los datos almacenados en LocalStorage son accesibles para cualquier código JavaScript que se ejecute en la misma página, lo que puede ser un problema de seguridad si estás almacenando datos sensibles. Además, LocalStorage está limitado en tamaño (generalmente a unos pocos MB), por lo que no es adecuado para almacenar grandes cantidades de datos.

### Uso de Local Storage, Session Storage y Memory Storage en Blazor

1. **Local Storage**: Para usar Local Storage en Blazor, puedes usar la biblioteca Blazored.LocalStorage. Primero, necesitas instalarla en tu proyecto con el siguiente comando:

```bash
dotnet add package Blazored.LocalStorage
```

Luego, puedes usarla en tu componente de la siguiente manera:

```csharp
@page "/localstorage"
@inject Blazored.LocalStorage.ILocalStorageService localStorage

<button @onclick="SaveData">Save Data</button>

@code {
    private async Task SaveData()
    {
        await localStorage.SetItemAsync("key", "value");
    }
}
```

2. **Session Storage**: Para usar Session Storage en Blazor, puedes usar la biblioteca Blazored.SessionStorage. Primero, necesitas instalarla en tu proyecto con el siguiente comando:

```bash
dotnet add package Blazored.SessionStorage
```

Luego, puedes usarla en tu componente de la siguiente manera:

```csharp
@page "/sessionstorage"
@inject Blazored.SessionStorage.ISessionStorageService sessionStorage

<button @onclick="SaveData">Save Data</button>

@code {
    private async Task SaveData()
    {
        await sessionStorage.SetItemAsync("key", "value");
    }
}
```

3. **Memory Storage**: Para el almacenamiento en memoria, puedes usar una variable en tu componente que mantendrá los datos mientras el componente esté en ejecución. Aquí hay un ejemplo:

```csharp
@page "/memorystorage"

<button @onclick="SaveData">Save Data</button>

@code {
    private string data;

    private void SaveData()
    {
        data = "value";
    }
}
```

Para agregar estos componentes a tu aplicación Blazor, simplemente necesitas crear los archivos `.razor` correspondientes en la carpeta `Pages` de tu proyecto y pegar el código correspondiente. Recuerda que también necesitas registrar los servicios de Blazored.LocalStorage y Blazored.SessionStorage en tu método `Startup.ConfigureServices`:

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddBlazoredLocalStorage();
    services.AddBlazoredSessionStorage();
}
```

Por último, asegúrate de tener las siguientes directivas `@using` en tu archivo `_Imports.razor`:

```csharp
@using Blazored.LocalStorage
@using Blazored.SessionStorage
```

Estos ejemplos son muy básicos y solo almacenan una cadena estática. En una aplicación real, probablemente querrías almacenar datos más complejos y manejar errores y casos límite.

### Ejemplo de uso de Local Storage en una aplicación Blazor para el login

Para loguearte y almacenar el token en LocalStorage, necesitarás utilizar la biblioteca Blazored.LocalStorage. Asegúrate de haberla instalado en tu proyecto con el comando `dotnet add package Blazored.LocalStorage`.

Primero, inyecta el servicio `ILocalStorageService` en tu componente `Login.razor`:

```csharp
@inject Blazored.LocalStorage.ILocalStorageService localStorage
```

Luego, después de obtener el token de acceso en tu método `HandleValidSubmit`, puedes almacenarlo en LocalStorage de la siguiente manera:

```csharp
await localStorage.SetItemAsync("accessToken", token);
```

Para almacenar la información del usuario logeado, puedes crear un objeto con la información que deseas almacenar y luego convertirlo a JSON para almacenarlo en LocalStorage. Por ejemplo, si tienes un objeto `User` con las propiedades `Email` y `Name`, puedes hacer lo siguiente:

```csharp
var user = new { Email = loginForm.Email, Name = "User Name" };
var userJson = JsonSerializer.Serialize(user);
await localStorage.SetItemAsync("user", userJson);
```

Aquí está el código completo de cómo podrías hacerlo en tu método `HandleValidSubmit`:

```csharp
private async Task HandleValidSubmit()
{
    var loginRequest = new { Email = loginForm.Email, Password = loginForm.Password };
    var data = new StringContent(JsonSerializer.Serialize(loginRequest), Encoding.UTF8, "application/json");

    var response = await Http.PostAsync("/auth/login", data);

    if (response.IsSuccessStatusCode)
    {
        var responseContent = await response.Content.ReadAsStringAsync();
        var responseBody = JsonSerializer.Deserialize<Dictionary<string, string>>(responseContent);

        if (responseBody.TryGetValue("AccessToken", out string token))
        {
            jwtToken = new JwtSecurityToken(token);

            // Almacenar el token en LocalStorage
            await localStorage.SetItemAsync("accessToken", token);

            // Almacenar la información del usuario en LocalStorage
            var user = new { Email = loginForm.Email, Name = "User Name" };
            var userJson = JsonSerializer.Serialize(user);
            await localStorage.SetItemAsync("user", userJson);

            // Navegar a la página de usuarios
            NavigationManager.NavigateTo("/users");
        }
        else
        {
            // Mostrar algún error en caso de no poder obtener el token
        }
    }
    else
    {
        // Mostrar un error al usuario en caso de que las credenciales sean incorrectas, etc.
    }
}
```

~~~mermaid
sequenceDiagram
    participant U as Usuario
    participant F as Formulario Login (Blazor)
    participant S as Servidor (API o servicio de autenticación)
    participant LS as LocalStorage (navegador)
    participant N as Navegador (Chrome, Firefox, etc.)

    U->>F: Ingresa credenciales
    F->>S: Envía solicitud POST con credenciales
    S-->>F: Responde con token o error
    Note over F,S: Si la respuesta es exitosa
    F->>LS: Almacena token en LocalStorage
    F->>LS: Almacena información del usuario en LocalStorage
    F->>N: Navega a la página de usuarios
    Note over F,S: Si la respuesta no es exitosa
    F->>U: Muestra error
~~~

Recuerda que este es un ejemplo básico y que deberías manejar los errores y los casos límite adecuadamente en tu aplicación. Además, asegúrate de que la información del usuario que estás almacenando en LocalStorage no es sensible, ya que LocalStorage es accesible para cualquier código JavaScript que se ejecute en la misma página.


servicio de seguridad 
![Captura de pantalla 2024-01-31 142138](https://github.com/yrusmtz/Blazor-NET/assets/79479231/1f47fd77-9281-482e-8f5a-0db97cddeef4)

Microservicios 
![Captura de pantalla 2024-01-31 142147](https://github.com/yrusmtz/Blazor-NET/assets/79479231/f5d75e67-3ef7-4614-90e7-318fa23c39ad)

Usuario 
![Captura de pantalla 2024-01-31 142153](https://github.com/yrusmtz/Blazor-NET/assets/79479231/08ae084a-fd5b-4805-b891-17b9e55de9f1)

![Captura de pantalla 2024-01-31 142221](https://github.com/yrusmtz/Blazor-NET/assets/79479231/4511a549-67b3-449f-b3c4-80fea2f59e72)

![Captura de pantalla 2024-01-31 142456](https://github.com/yrusmtz/Blazor-NET/assets/79479231/4bda97cf-caa4-47f9-a532-ac4ae802611f)

![Captura de pantalla 2024-01-31 142811](https://github.com/yrusmtz/Blazor-NET/assets/79479231/0c8813be-5fe9-4c93-9460-4cced4fd3539)


# Funcionamiento de JWT y Users

## JWT

### ¿Qué es JWT?
JWT (por sus siglas en inglés JSON Web Token) es un estándar que define una manera segura de transmitir información entre dos partes a través de JSON. Los JWT son especialmente populares en los procesos de autentificación.

### Estructura JSON Web Token
Un JWT firmado consta de 3 partes separadas por puntos.

![Estructura JWT](https://res.cloudinary.com/practicaldev/image/fetch/s--MTT2QHbt--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/uploads/articles/04bibz8lka7qdx5f33oh.png)


- HEADER
Consta generalmente de dos valores y proporciona información importante sobre el token. Contiene el tipo de token y el algoritmo de la firma.

- PAYLOAD
Contiene la información real que se transmitirá a la aplicación. Aquí se definen algunos estándares que determinan qué datos se transmiten y cómo. La información se proporciona como pares Key/Value (Clave/Valor). Las claves se denominan claims en JWT. Hay tres tipos diferentes de claims (registrados, públicos, privados).

- SIGNATURE
La firma de un JSON Web Token se crea utilizando la codificación Base64 del header y del payload, así como el método de firma o cifrado especificado.


### Flujo basico de JWT
![Flujo JWt](https://res.cloudinary.com/practicaldev/image/fetch/s--7Hk1iVWA--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/uploads/articles/04ttxv7nmisvs5gnd0i9.png)

https://dev.to/gdcodev/introduccion-a-json-web-token-3mjf

___
## Login y JWT en la API
La generación de JWT (JSON Web Tokens) en este archivo se realiza en el endpoint de inicio de sesión ("/auth/login"). Aquí están los pasos detallados:

1. Primero, se obtiene el usuario de la base de datos utilizando el correo electrónico proporcionado en la solicitud de inicio de sesión.

```csharp
var user = userService.GetUser(request.Email);
```

2. Luego, se verifica si el usuario existe y si la contraseña proporcionada coincide con la del usuario.

```csharp
if (user != null && request.Password == user.Password)
```

3. Si la verificación es exitosa, se procede a la generación del JWT. Primero, se crean las reclamaciones (claims) que se incluirán en el token. En este caso, se está incluyendo el correo electrónico del usuario.

```csharp
var claims = new List<Claim>() { new(ClaimTypes.Name, request.Email), };
```

4. Luego, se crea una clave de seguridad utilizando la clave secreta proporcionada. Esta clave se utilizará para firmar el token.

```csharp
var securityKey = new SymmetricSecurityKey(
                        Encoding.UTF8.GetBytes(
                                "aopsjfp0aoisjf[poajsf[poajsp[fojasp[foja[psojf[paosjfp[aojsfpaojsfp[ojasf"));
var credentials = new SigningCredentials(securityKey, SecurityAlgorithms.HmacSha256);
```

5. A continuación, se crea el token JWT utilizando el emisor, el público, las reclamaciones, la fecha de vencimiento y las credenciales de firma.

```csharp
var jwtSecurityToken = new JwtSecurityToken(
                        issuer: "https://www.surymartinez.com",
                        audience: "Minimal APIs Client",
                        claims: claims,
                        expires: DateTime.UtcNow.AddHours(1),
                        signingCredentials: credentials);
```

6. Finalmente, se escribe el token JWT en una cadena y se devuelve como parte de la respuesta.

```csharp
var accessToken = new JwtSecurityTokenHandler().WriteToken(jwtSecurityToken);

return Results.Ok(new { AccessToken = accessToken });
```

Si la verificación del usuario falla, se devuelve un error 400 (BadRequest).

```csharp
return Results.BadRequest();
```

___
### Configuración de JWT en la API
La declaración de servicios para la generación de JWT en el archivo `Program.cs` se realiza en varias partes:

1. Primero, se configura el servicio de autenticación para usar JWT (JSON Web Tokens) como el esquema de autenticación predeterminado. Esto se hace utilizando `AddAuthentication(JwtBearerDefaults.AuthenticationScheme)`.

```csharp
builder.Services.AddAuthentication(JwtBearerDefaults.AuthenticationScheme)
```

2. Luego, se configura el servicio JWT Bearer. Aquí es donde se establecen los parámetros de validación del token. Se valida el emisor del token (`ValidateIssuer = true`), se establece la clave de firma del token (`IssuerSigningKey`) y se definen el emisor válido (`ValidIssuer`) y la audiencia válida (`ValidAudience`).

```csharp
.AddJwtBearer(options =>
{
    options.TokenValidationParameters = new TokenValidationParameters
    {
        ValidateIssuer = true, 
        IssuerSigningKey = new SymmetricSecurityKey(Encoding.UTF8.GetBytes("aopsjfp0aoisjf[poajsf[poajsp[fojasp[foja[psojf[paosjfp[aojsfpaojsfp[ojasf")),
        ValidIssuer = "https://www.surymartinez.com", 
        ValidAudience = "Minimal APIs Client" 
    };
})
```

3. Después de configurar la autenticación, se agrega el servicio de autorización con `AddAuthorization()`.

```csharp
builder.Services.AddAuthorization();
```

4. Finalmente, se configura Swagger para usar JWT. Se agrega una definición de seguridad para JWT y se agrega un requisito de seguridad que hace referencia a esa definición.

```csharp
builder.Services.AddSwaggerGen(options =>
{
    options.AddSecurityDefinition(JwtBearerDefaults.AuthenticationScheme,
        new OpenApiSecurityScheme
        { 
            Type = SecuritySchemeType.ApiKey, 
            In = ParameterLocation.Header, 
            Name = HeaderNames.Authorization, 
            Description = "Insert the token with the 'Bearer ' prefix", 
        });

    options.AddSecurityRequirement(new OpenApiSecurityRequirement
    {
        { 
            new OpenApiSecurityScheme 
            { 
                Reference = new OpenApiReference 
                { 
                    Type = ReferenceType.SecurityScheme, 
                    Id = JwtBearerDefaults.AuthenticationScheme 
                } 
            },
            new string[] { } 
        } 
    });
});
```

Estas configuraciones permiten que la aplicación genere y valide JWT para la autenticación de usuarios.


## Users

### Declaracion de la clase o record User
El `UserDto` es un `record` en C#, introducido en C# 9.0. Un `record` es un tipo de referencia que tiene características de inmutabilidad y comportamiento de valor. Esto significa que una vez que un `record` es creado, no puede ser modificado. Cualquier modificación resultará en la creación de un nuevo `record`.

Aquí está el `UserDto`:

```csharp
public record UserDto(string Email, string Password);
```

Este `record` tiene dos propiedades, `Email` y `Password`, que son inmutables. Esto significa que una vez que se crea una instancia de `UserDto`, no puedes cambiar el `Email` o `Password`.

La principal diferencia entre un `record` y una clase es que un `record` es inmutable y tiene comportamiento de valor. Esto significa que dos `records` con los mismos valores serán considerados iguales. En contraste, dos instancias de una clase con los mismos valores no son iguales a menos que se sobrescriba el método `Equals`.

Además, los `records` proporcionan funcionalidades incorporadas para copiar y comparar objetos. Por ejemplo, puedes crear una copia de un `record` con algunas propiedades modificadas utilizando la sintaxis `with`.

En resumen, debes usar `records` cuando quieras modelos inmutables con comportamiento de valor, y clases cuando necesites objetos con estado mutable.

___
### Servicio de usuarios
El archivo `UserService.cs` contiene una clase llamada `UserService` que se utiliza para manejar las operaciones relacionadas con los usuarios en la aplicación. Aquí está un desglose de su funcionamiento:

1. La clase `UserService` se inicializa con una lista de `UserDto`. Esta lista se utiliza como una base de datos en memoria para almacenar los usuarios.

```csharp
public class UserService(List<UserDto> users)
{
    private readonly List<UserDto> _users = users;
}
```

2. La función `CreateUser` toma un `UserDto` como argumento, lo agrega a la lista de usuarios y luego lo devuelve.

```csharp
public UserDto CreateUser(UserDto newUser)
{
    _users.Add(newUser);
    return newUser;
}
```

3. La función `GetAllUsers` devuelve todos los usuarios en la lista.

```csharp
public List<UserDto> GetAllUsers()
{
    return _users;
}
```

4. La función `GetUser` toma un `userId` como argumento, busca un usuario con ese ID en la lista y lo devuelve. Si no se encuentra ningún usuario, devuelve `null`.

```csharp
public UserDto? GetUser(string userId)
{
    return _users.Find(u => u.Email == userId);
}
```

5. La función `UpdateUserPassword` toma un `userId` y un `UserDto` como argumentos. Busca un usuario con ese ID en la lista y, si lo encuentra, actualiza su contraseña con la del `UserDto` proporcionado y lo devuelve. Si no se encuentra ningún usuario, devuelve `null`.

```csharp
public UserDto? UpdateUserPassword(string userId, UserDto updatedUser)
{
    var user = _users.Find(u => u.Email == userId);
    if (user != null)
    {
        user = updatedUser;
        return user;
    }
    return null;
}
```

En resumen, `UserService` es una clase simple que proporciona funcionalidades para crear, obtener y actualizar usuarios en una base de datos en memoria.

___
### Endpoints de usuarios
Los endpoints `/users` en el archivo `Program.cs` interactúan con la clase `UserService` para realizar operaciones CRUD (Crear, Leer, Actualizar, Eliminar) en los usuarios.

1. `app.MapPost("/users", (UserDto newUser) => {...})`: Este es un endpoint POST que se utiliza para crear un nuevo usuario. Toma un `UserDto` como cuerpo de la solicitud, lo pasa al método `CreateUser` de `UserService`, y luego devuelve el usuario creado. Si la creación es exitosa, devuelve un estado 201 (Created) con la ubicación del nuevo recurso y el recurso creado.

```csharp
app.MapPost("/users", (UserDto newUser) =>
{
    var createdUser = userService.CreateUser(newUser);
    return Results.Created($"/users/{createdUser.Email}", createdUser);
}).WithName("CreateUser").WithOpenApi();
```

2. `app.MapGet("/users", () => {...})`: Este es un endpoint GET que se utiliza para obtener todos los usuarios. Llama al método `GetAllUsers` de `UserService` y devuelve la lista de todos los usuarios.

```csharp
app.MapGet("/users", () => userService.GetAllUsers()).WithName("GetAllUsers").WithOpenApi();
```

3. `app.MapGet("/users/{userId}", (string userId) => {...})`: Este es un endpoint GET que se utiliza para obtener un usuario específico por su ID (en este caso, el correo electrónico). Toma un `userId` como parámetro de ruta, lo pasa al método `GetUser` de `UserService`, y luego devuelve el usuario si se encuentra. Si no se encuentra el usuario, devuelve un estado 404 (Not Found).

```csharp
app.MapGet("/users/{userId}", (string userId) =>
{
    var user = userService.GetUser(userId);
    if (user == null)
    {
        return Results.NotFound($"User with ID {userId} not found.");
    }
    return Results.Ok(user);
});
```

4. `app.MapPut("/users/{userId}", (string userId, UserDto updatedUser) => {...})`: Este es un endpoint PUT que se utiliza para actualizar la contraseña de un usuario específico. Toma un `userId` como parámetro de ruta y un `UserDto` como cuerpo de la solicitud, los pasa al método `UpdateUserPassword` de `UserService`, y luego devuelve el usuario actualizado si se encuentra. Si no se encuentra el usuario, devuelve un estado 404 (Not Found).

```csharp
app.MapPut("/users/{userId}", (string userId, UserDto updatedUser) =>
{
    var user = userService.UpdateUserPassword(userId, updatedUser);
    if (user == null)
    {
        return Results.NotFound($"User with ID {userId} not found.");
    }
    return Results.Ok(user);
}).WithName("UpdateUserPassword").WithOpenApi();
```

En resumen, estos endpoints proporcionan una interfaz HTTP para interactuar con la clase `UserService`, permitiendo a los clientes de la API realizar operaciones CRUD en los usuarios.

___
### Funcionamiento de los endpoints de la API
~~~mermaid
sequenceDiagram
    participant Cliente
    participant Login as API: /auth/login
    participant Users as API: /users
    participant UserService

    Cliente->>Login: POST (email, password)
    Login->>UserService: GetUser(email)
    UserService-->>Login: UserDto (email, password)
    Login->>Login: Verificar contraseña
    Login->>Login: Generar JWT
    Login-->>Cliente: JWT

    Cliente->>Users: POST (UserDto)
    Users->>UserService: CreateUser(UserDto)
    UserService-->>Users: UserDto (email, password)
    Users-->>Cliente: UserDto (email, password)

    Cliente->>Users: GET
    Users->>UserService: GetAllUsers()
    UserService-->>Users: List<UserDto>
    Users-->>Cliente: List<UserDto>

    Cliente->>Users: GET (userId)
    Users->>UserService: GetUser(userId)
    UserService-->>Users: UserDto (email, password)
    Users-->>Cliente: UserDto (email, password)

    Cliente->>Users: PUT (userId, UserDto)
    Users->>UserService: UpdateUserPassword(userId, UserDto)
    UserService-->>Users: UserDto (email, password)
    Users-->>Cliente: UserDto (email, password)
~~~
___
### Diagrama de clases API
~~~mermaid
classDiagram
    WebApplication --|> WebApplicationBuilder: Creates
    WebApplicationBuilder --> UserService: Adds to services
    WebApplication --> UserService: Uses
    UserService --> UserDto: Manages
    class WebApplication {
        +CreateBuilder(args: string[]): WebApplicationBuilder
        +Build(): WebApplication
    }
    class WebApplicationBuilder {
        +Services: IServiceCollection
        +Build(): WebApplication
    }
    class WebApplication {
        +Services: IServiceProvider
        +UseSwagger(): WebApplication
        +UseSwaggerUI(): WebApplication
        +UseHttpsRedirection(): WebApplication
        +UseAuthentication(): WebApplication
        +UseAuthorization(): WebApplication
        +MapGet(pattern: string, handler: Delegate): WebApplication
        +MapPost(pattern: string, handler: Delegate): WebApplication
        +MapPut(pattern: string, handler: Delegate): WebApplication
        +Run(): void
    }
    class UserService {
        +CreateUser(newUser: UserDto): UserDto
        +GetAllUsers(): List<UserDto>
        +GetUser(userId: string): UserDto?
        +UpdateUserPassword(userId: string, updatedUser: UserDto): UserDto?
    }
    class UserDto {
        +Email: string
        +Password: string
    }
~~~
