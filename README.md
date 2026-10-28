# VocabularioC
Vocabulario

# Anatomía de un método en C#

```csharp
public bool Validar(Categoria c)
  ↑     ↑      ↑         ↑
  │     │      │         └── Parámetro (tipo + nombre)
  │     │      └──────────── Nombre del método
  │     └─────────────────── Tipo de retorno
  └───────────────────────── Modificador de acceso
```

---
## Metodos Para Una Capa Datos CRUD

ObtenerTodos, ObtenerPorId, Crear, Actualizar, Eliminar

---

---

## Reglas de arquitectura por capas

| Regla | Cómo se garantiza |
|---|---|
| `Program` solo llama a `Services` | Disciplina: nunca `new TicketRepository()` en `Program` |
| `Services` llama a `Data` | El servicio tiene el repositorio inyectado o lo instancia |
| Nadie más toca `Data` | Si otra capa lo toca, se rompe el flujo |

---

---
## static
Puntualmente static es un modificador de acceso; Pertenece a la clase no a los objetos creados de ella

**Qué es:** modificador de pertenencia. **No es modificador de acceso.**

**Qué hace:** indica que el método/propiedad/clase **pertenece a la clase**, no a los objetos creados de ella.

**Consecuencia:** se llama **desde la clase directamente**, **sin crear objeto**.

### Sin static

```csharp
public string ConvertirMayuscula(string cadena) { ... }

// Uso:
var r = new Rules();              // ← creas objeto
r.ConvertirMayuscula("zul");      // ← usas el objeto
---



## Capas de la arquitectura

| Capa | Qué hace |
|---|---|
| Models | Plantillas (datos) |
| Data | SQL y conexión |
| Services | Reglas de negocio |
| Presentation | Entrada/salida con el usuario |

### Cómo se implementa `Presentation` según la tecnología

| Tecnología | `Presentation` se implementa con... |
|---|---|
| Consola | `Menu.cs` (menú, `Console.ReadLine`) |
| Web API | `Controllers/` (`[HttpGet]`, JSON) |
| Web MVC | `Controllers/` + `Views/` |
| Escritorio | `Forms/` o `Views/` (botones, ventanas) |

**Siempre son 4 capas. Cambia la tecnología de `Presentation`, no la cantidad.**
---

## Estándar de nombres por capa

| Capa | Convención | Ejemplo |
| :--- | :--- | :--- |
| **Models** | Sin sufijo | `Categoria`, `Ticket`, `Usuario` |
| **Data (repositorios)** | Sufijo `Repository` | `CategoriaRepository`, `TicketRepository` |
| **Data (conexión)** | Descriptivo | `Conexion` |
| **Services** | Sufijo `Service` (singular) | `CategoriaService`, `TicketService` |
| **Presentation (consola)** | Descriptivo | `Menu` |
| **Presentation (web)** | Sufijo `Controller` | `TicketController` |



Cuando la DB usa snake_case y C# usa PascalCase, el SP (o el SELECT) pone los alias para que coincidan





## Inyección de dependencias (DI)

**Frase clave:**
> "Recibir lo que necesitas por constructor, en vez de crearlo adentro."

**Qué significa:**
La clase NO crea sus dependencias con `new`. Las recibe desde afuera (por el constructor) y las guarda en un campo privado `readonly`.

**Ejemplo del proyecto:**
- `Conexion(IConfiguration config)` → recibe la configuración.
- `CategoriaRepository(Conexion conexion)` → recibe la conexión.
- `CategoriaService(CategoriaRepository repo)` → recibe el repositorio.

**Por qué:**
- Desacopla: cada clase no sabe cómo se construye su dependencia.
- Testeable: puedes pasar un mock.
- Flexible: cambiar la implementación no rompe la clase.

**No es herencia ni polimorfismo.** Es otro concepto.




## readonly

**Qué es:** modificador de campo que garantiza que el valor solo se puede asignar **una vez**, en el constructor.

**Qué garantiza:**
- El constructor **sí** puede asignarlo.
- Después del constructor, **nadie** puede reasignarlo (ni métodos, ni propiedades).
- El campo queda fijo con ese objeto durante toda la vida del objeto.

**Dónde se usa en el proyecto:**
```csharp
private readonly Conexion _conexion;
private readonly IConfiguration _iConfiguration;
private readonly UsuarioRepository _repository;
