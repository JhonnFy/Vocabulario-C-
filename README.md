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

## Reglas de arquitectura por capas

| Regla | Cómo se garantiza |
|---|---|
| `Program` solo llama a `Services` | Disciplina: nunca `new TicketRepository()` en `Program` |
| `Services` llama a `Data` | El servicio tiene el repositorio inyectado o lo instancia |
| Nadie más toca `Data` | Si otra capa lo toca, se rompe el flujo |

---

---
static = no depende de un objeto. Se llama desde la clase directamente.
---

