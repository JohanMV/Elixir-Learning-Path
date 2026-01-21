# Control de Flujo en Elixir

En Elixir, el control de flujo se maneja de manera **funcional**, evitando sentencias imperativas tradicionales. 
Las estructuras principales son `if/else`, `unless`, `case` y `cond`. Todas devuelven un valor, permitiendo asignaciones directas.

---

## if/else

La estructura `if/else` evalúa una condición y ejecuta un bloque u otro según el resultado.

```elixir
edad = 20

resultado = if edad >= 18 do
  "Eres mayor de edad"
else
  "Eres menor de edad"
end

IO.puts(resultado)  # → Eres mayor de edad
```

✅ En Elixir, `if/else` **devuelve un valor** que puede ser asignado.

---

## unless

`unless` es lo opuesto a `if`. Ejecuta el bloque si la condición es **falsa**.

```elixir
usuario_activo = false

unless usuario_activo do
  IO.puts("⚠️ Cuenta inactiva, por favor actívala")
end

# Equivalente a:
# if not usuario_activo do ... end
```

---

## case

`case` realiza **pattern matching** contra múltiples patrones. Ideal para valores con estructura.

```elixir
resultado = {:ok, "Usuario creado exitosamente"}

mensaje = case resultado do
  {:ok, datos} -> 
    "✅ Éxito: #{datos}"
  
  {:error, razon} -> 
    "❌ Error: #{razon}"
  
  _ -> 
    "⚠️ Caso desconocido"
end

IO.puts(mensaje)  # → ✅ Éxito: Usuario creado exitosamente
```

> El patrón `_` (*wildcard*) coincide con cualquier valor. Se evalúa como último recurso.

---

## cond

`cond` evalúa **múltiples condiciones** en orden hasta encontrar una verdadera.

```elixir
edad = 14

clasificacion = cond do
  edad < 13 -> "Niño"
  edad < 18 -> "Adolescente"
  edad < 65 -> "Adulto"
  true -> "Jubilado"
end

IO.puts(clasificacion)  # → Adolescente
```

ℹ️ La rama con `true` actúa como `else` (siempre se ejecuta si las anteriores fallan).

---

## Combinación de estructuras

Las estructuras de control pueden combinarse para lógica más compleja:

```elixir
procesar_respuesta = fn response ->
  case response do
    {:ok, data} ->
      data
      |> String.downcase()
      |> String.trim()
    
    {:error, razon} ->
      IO.puts("Error: #{razon}")
      ""
  end
end

procesar_respuesta({:ok, "  HOLA  "})  # → "hola"
```

---

## Resumen

| Estructura | Uso | Devuelve Valor |
|---|---|---|
| `if/else` | Condición simple | ✅ Sí |
| `unless` | Negación de condición | ✅ Sí |
| `case` | Pattern matching múltiple | ✅ Sí |
| `cond` | Múltiples condiciones | ✅ Sí |
| `\|>` | Encadenamiento de funciones | ✅ Sí |

El control de flujo en Elixir es **funcional**: todo devuelve valores, permitiendo composición elegante y mantenible.