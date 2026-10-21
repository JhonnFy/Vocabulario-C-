# Vocabulario-C-
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


---
## Capas de la arquitectura

| Capa | Qué hace |
|---|---|
| **Models** | Plantillas (datos) |
| **Data** | SQL y conexión |
| **Services** | Reglas de negocio |
| **Presentation** | Entrada/salida con el usuario |

### Cómo se implementa `Presentation` según la tecnología

| Tecnología | `Presentation` se implementa con... |
|---|---|
| Consola | `Menu.cs` (menú, `Console.ReadLine`) |
| Web API | `Controllers/` (`[HttpGet]`, JSON) |
| Web MVC | `Controllers/` + `Views/` |
| Escritorio | `Forms/` o `Views/` (botones, ventanas) |

**Siempre son 4 capas. Cambia la tecnología de `Presentation`, no la cantidad.**
---


