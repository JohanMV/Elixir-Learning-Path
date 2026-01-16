# Colecciones en Elixir

Elixir ofrece varias estructuras de colección, todas inmutables. Las más comunes son listas, tuplas, mapas y keywords. Cada una tiene un propósito y rendimiento específicos.

## Ejemplo de uso básico

```elixir
IO.puts("=== Colecciones en Elixir ===")

# ── Listas ───────────────────────────────────────
# - Almacenadas como listas enlazadas.
# - Óptimas para agregar/quitar por la cabeza (O(1)).
# - Acceso por índice es lento (O(n)).

lista = [1, 2, 3, "hola", :ok]
IO.puts("Lista: #{inspect(lista)}")
IO.puts("Primer elemento (head): #{hd(lista)}")
IO.puts("Resto (tail): #{inspect(tl(lista))}")
IO.puts("Concatenación: [1,2] ++ [3] = #{inspect([1,2] ++ [3])}")
IO.puts("Diferencia: [1,2,3] -- [2] = #{inspect([1,2,3] -- [2])}")

# ── Tuplas ───────────────────────────────────────
# - Almacenadas contiguamente en memoria.
# - Acceso por índice rápido (O(1)).
# - Usadas para devolver múltiples valores o estados.

tupla = {:ok, "archivo leído", 200}
IO.puts("\nTupla: #{inspect(tupla)}")
IO.puts("Segundo elemento: #{elem(tupla, 1)}")
IO.puts("Tamaño: #{tuple_size(tupla)}")

# ── Mapas ────────────────────────────────────────
# - Colección clave-valor más común.
# - Claves pueden ser de cualquier tipo.
# - Acceso eficiente incluso con miles de claves.

mapa = %{
  "nombre" => "María",
  :edad => 28,
  true => "valor con clave booleana"
}
IO.puts("\nMapa: #{inspect(mapa)}")
IO.puts("Acceso por string: #{mapa["nombre"]}")
IO.puts("Acceso por átomo: #{mapa[:edad]}")
IO.puts("Actualizar edad: #{inspect(Map.put(mapa, :edad, 29))}")

# ── Keywords ─────────────────────────────────────
# - Lista de tuplas donde la clave es un átomo.
# - Útiles para opciones de funciones (legibles y orden preservado).

keywords = [nombre: "Carlos", rol: :admin, activo: true]
IO.puts("\nKeywords: #{inspect(keywords)}")
IO.puts("Acceso: keywords[:nombre] = #{keywords[:nombre]}")
IO.puts("Equivalente explícito: #{inspect([{:nombre, "Carlos"}, {:rol, :admin}])}")