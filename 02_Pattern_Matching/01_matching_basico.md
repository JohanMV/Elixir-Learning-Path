# Pattern Matching Básico en Elixir

En Elixir, el operador `=` no es de asignación tradicional, sino de **pattern matching** (coincidencia de patrones).
Su función es intentar que el lado izquierdo *encaje estructuralmente* con el lado derecho.
Si no coincide, se produce un error (`MatchError`).

Este concepto es fundamental y aparece constantemente en asignaciones, funciones, control de flujo y manejo de errores.

---

## Asignación vs Coincidencia

En Elixir, las variables se *ligan* (bind) a valores la primera vez que aparecen.

```elixir
x = 5        # x queda ligada al valor 5
5 = x        # Coincide: no hay error
6 = x        # MatchError: no puede coincidir 6 con 5
```

Esto demuestra que `=` valida coincidencias, no solo asigna valores.

---

## Desestructuración de Estructuras

El pattern matching permite extraer valores de estructuras de datos de forma clara y segura.

---

### Tuplas

Las tuplas se usan frecuentemente para representar resultados (`{:ok, valor}` / `{:error, razon}`).

```elixir
{:ok, resultado} = {:ok, "archivo leído"}
# resultado = "archivo leído"
```

Si la estructura o los valores no coinciden, el matching falla:

```elixir
# {:error, razon} = {:ok, "éxito"}
# MatchError
```

---

### Listas

Las listas pueden desestructurarse usando cabeza (*head*) y cola (*tail*).

```elixir
[primero | resto] = [1, 2, 3]
# primero = 1
# resto = [2, 3]
```

También se puede hacer matching posicional:

```elixir
[a, b, c] = [10, 20, 30]
# a = 10
# b = 20
# c = 30
```

La longitud de la lista debe coincidir exactamente.

---

### Mapas

En mapas, el pattern matching se basa en **claves**, no en el orden.

```elixir
%{nombre: nombre, edad: edad} = %{nombre: "Ana", edad: 28, ciudad: "Madrid"}
# nombre = "Ana"
# edad = 28
```

Las claves adicionales se ignoran.

✅ En mapas, el pattern matching solo exige que las claves del patrón existan.

---

## Caso Especial: Variables ya Ligadas

Cuando una variable ya está ligada, Elixir la trata como un valor fijo.

```elixir
{a, b} = {10, 20}
# a = 10
# b = 20
```

Si se vuelve a usar `a`, debe coincidir con su valor original:

```elixir
{a, c} = {10, 30}   # a ya es 10 → coincide, c = 30
{a, d} = {99, 40}   # MatchError: a es 10, no 99
```

Este comportamiento permite validaciones implícitas sin escribir lógica adicional.

---

## Importancia del Pattern Matching

El pattern matching es la base de:

- Control de flujo (`case`, `with`)
- Definición de funciones
- Recursión
- Manejo explícito de errores

Dominar este concepto es esencial para escribir código idiomático, seguro y expresivo en Elixir.
