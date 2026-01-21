# Enumerables en Elixir

El módulo `Enum` proporciona un conjunto de funciones para trabajar con colecciones (**listas, mapas, rangos**) de forma **funcional y declarativa**. 
Estas funciones transforman datos sin mutar la colección original.

---

## Ejemplo de uso básico

```elixir
IO.puts("=== Enumerables en Elixir ===\n")

# ── map ──────────────────────────────────────────
# Transforma cada elemento aplicando una función
numeros = [1, 2, 3, 4, 5]
duplicados = Enum.map(numeros, fn x -> x * 2 end)
IO.puts("map: Enum.map([1,2,3], &(&1*2)) = #{inspect(duplicados)}")

# ── filter ───────────────────────────────────────
# Retorna solo elementos que cumplen la condición
pares = Enum.filter(numeros, fn x -> rem(x, 2) == 0 end)
IO.puts("filter: Enum.filter([1,2,3,4,5], pares) = #{inspect(pares)}")

# ── reduce ───────────────────────────────────────
# Acumula un valor iterando sobre la colección
suma = Enum.reduce(numeros, 0, fn x, acc -> acc + x end)
IO.puts("reduce: Enum.reduce([1,2,3,4,5], suma) = #{suma}")

# ── each ─────────────────────────────────────────
# Ejecuta un efecto secundario (impresión, I/O, etc)
IO.puts("each: imprimiendo elementos:")
Enum.each([1, 2, 3], fn x -> IO.puts("  → #{x}") end)

# ── find ─────────────────────────────────────────
# Retorna el PRIMER elemento que cumple la condición
primero_mayor_tres = Enum.find(numeros, fn x -> x > 3 end)
IO.puts("find: primer número > 3: #{primero_mayor_tres}")

# ── sort ─────────────────────────────────────────
# Ordena elementos (ascendente por defecto)
desordenados = [5, 2, 8, 1, 9]
ordenados = Enum.sort(desordenados)
IO.puts("sort: #{inspect(desordenados)} → #{inspect(ordenados)}")
```

---

## map

Transforma **cada elemento** aplicando una función. Retorna una nueva colección del mismo tamaño.

```elixir
usuarios = ["ana", "luis", "carlos"]

# Convertir a mayúsculas
mayusculas = Enum.map(usuarios, fn nombre -> String.upcase(nombre) end)
IO.puts("#{inspect(mayusculas)}")  # → ["ANA", "LUIS", "CARLOS"]

# Sintaxis corta con &
el_cuadrado = Enum.map([1, 2, 3], &(&1 * &1))
IO.puts("#{inspect(el_cuadrado)}")  # → [1, 4, 9]
```

---

## filter

Retorna una nueva colección con solo los elementos que **satisfacen la condición**.

```elixir
numeros = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

# Números mayores a 5
mayores = Enum.filter(numeros, fn x -> x > 5 end)
IO.puts("#{inspect(mayores)}")  # → [6, 7, 8, 9, 10]

# Palabras que comienzan con 'a'
palabras = ["apple", "banana", "apricot", "cherry"]
con_a = Enum.filter(palabras, fn p -> String.starts_with?(p, "a") end)
IO.puts("#{inspect(con_a)}")  # → ["apple", "apricot"]
```

---

## reduce

Acumula un valor iterando sobre la colección. Útil para cálculos agregados.

```elixir
numeros = [1, 2, 3, 4, 5]

# Suma
suma = Enum.reduce(numeros, 0, fn x, acc -> acc + x end)
IO.puts("Suma: #{suma}")  # → 15

# Producto
producto = Enum.reduce(numeros, 1, fn x, acc -> acc * x end)
IO.puts("Producto: #{producto}")  # → 120

# Agrupar en un mapa (contador de frecuencias)
palabras = ["gato", "perro", "gato", "gato", "perro"]
frecuencias = Enum.reduce(palabras, %{}, fn palabra, acc ->
  Map.update(acc, palabra, 1, &(&1 + 1))
end)
IO.puts("Frecuencias: #{inspect(frecuencias)}")  
# → %{"gato" => 3, "perro" => 2}
```

---

## each

Ejecuta un **efecto secundario** (impresión, modificación de estado externo, I/O) sin transformar datos.
Retorna siempre `:ok`.

```elixir
tareas = ["tarea 1", "tarea 2", "tarea 3"]

Enum.each(tareas, fn tarea -> IO.puts("Ejecutando: #{tarea}") end)
# → Ejecutando: tarea 1
# → Ejecutando: tarea 2
# → Ejecutando: tarea 3
```

✅ Úsalo cuando necesites efectos secundarios, no transformación de datos.

---

## find

Retorna el **primer elemento** que cumple la condición, o `nil` si no hay coincidencia.

```elixir
numeros = [1, 2, 3, 4, 5, 6]

primero_par = Enum.find(numeros, fn x -> rem(x, 2) == 0 end)
IO.puts("Primer par: #{primero_par}")  # → 2

inexistente = Enum.find(numeros, fn x -> x > 100 end)
IO.puts("Inexistente: #{inspect(inexistente)}")  # → nil

# Con valor por defecto
con_defecto = Enum.find(numeros, -1, fn x -> x > 100 end)
IO.puts("Con defecto: #{con_defecto}")  # → -1
```

---

## sort

Ordena los elementos. Por defecto, en orden **ascendente**.

```elixir
numeros = [5, 2, 8, 1, 9, 3]
ordenados = Enum.sort(numeros)
IO.puts("Ascendente: #{inspect(ordenados)}")  # → [1, 2, 3, 5, 8, 9]

# Descendente
descendente = Enum.sort(numeros, :desc)
IO.puts("Descendente: #{inspect(descendente)}")  # → [9, 8, 5, 3, 2, 1]

# Ordenar mapas por valor
personas = [
  %{nombre: "Ana", edad: 25},
  %{nombre: "Luis", edad: 20},
  %{nombre: "Carlos", edad: 30}
]

por_edad = Enum.sort(personas, fn a, b -> a.edad <= b.edad end)
# por_edad = Enum.sort(personas, fn a, b -> a.edad < b.edad end)
# por_edad = Enum.sort_by(personas, &(&1.edad))
IO.puts("Por edad: #{inspect(por_edad)}")
# → [%{nombre: "Luis", edad: 20}, %{nombre: "Ana", edad: 25}, %{nombre: "Carlos", edad: 30}]
```

---

## Otros Enumerables Útiles

```elixir
# count: cantidad de elementos
IO.puts("Cantidad: #{Enum.count([1, 2, 3, 4])}")  # → 4

# reverse: invierte el orden
IO.puts("Invertido: #{inspect(Enum.reverse([1, 2, 3]))}")  # → [3, 2, 1]

# uniq: elimina duplicados
IO.puts("Únicos: #{inspect(Enum.uniq([1, 2, 2, 3, 3, 3]))}")  # → [1, 2, 3]

# chunk_every: agrupa en sublistas
IO.puts("Chunks: #{inspect(Enum.chunk_every([1, 2, 3, 4, 5], 2))}")  
# → [[1, 2], [3, 4], [5]]

# any?: verifica si ALGUNO cumple
IO.puts("¿Alguno > 5? #{Enum.any?([1, 2, 3, 6], &(&1 > 5))}")  # → true

# all?: verifica si TODOS cumplen
IO.puts("¿Todos > 0? #{Enum.all?([1, 2, 3, 4], &(&1 > 0))}")  # → true

# join: une elementos en cadena
IO.puts("Unidos: #{Enum.join([1, 2, 3], ", ")}")  # → 1, 2, 3
```

---

## Resumen

| Función | Propósito | Retorna |
|---|---|---|
| `map` | Transformar cada elemento | Nueva colección |
| `filter` | Seleccionar elementos | Nueva colección (menor) |
| `reduce` | Acumular un valor | Valor único |
| `each` | Efecto secundario | `:ok` |
| `find` | Buscar primer elemento | Elemento o `nil` |
| `sort` | Ordenar colección | Nueva colección ordenada |

El módulo `Enum` es el corazón de la programación funcional en Elixir. Dominarla permite escribir código declarativo, conciso y expresivo.