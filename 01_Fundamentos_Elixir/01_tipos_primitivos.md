# Tipos Primitivos en Elixir

* En Elixir, las variables se declaran asignándoles un valor.
* Todos los valores son **inmutables**, y el lenguaje proporciona varios tipos primitivos fundamentales.

## Ejemplo de uso básico

```elixir
IO.puts("=== Tipos primitivos en Elixir ===")

# Las variables se declaran asignándoles un valor.
nombre_variable = "Valor asignado"

# Enteros
entero = 42
IO.puts("Entero: #{entero} (tipo: #{is_integer(entero)})")

# Flotantes
flotante = 3.1416
IO.puts("Flotante: #{flotante} (tipo: #{is_float(flotante)})")

# Booleanos
verdadero = true
falso = false
IO.puts("Booleanos: #{verdadero}, #{falso}")

# Átomos (constantes literales)
estado = :activo
IO.puts("Átomo: #{estado} (tipo: #{is_atom(estado)})")

# Cadenas (UTF-8)
mensaje = "¡Hola, Elixir!"
IO.puts("Cadena: #{mensaje} (tipo: #{is_binary(mensaje)})")

# Nota: Elixir no tiene null; usa nil
valor_nulo = nil
IO.puts("Nil: #{valor_nulo} (tipo: #{is_nil(valor_nulo)})")
```
Resumen:
---

1. Todos los valores son inmutables.
2. Los tipos primitivos incluyen: enteros, 
3. flotantes, booleanos, átomos, cadenas.
4. Las cadenas son binarios UTF-8.
5. Usamos **IO.puts** para imprimir y **inspect** para ver estructuras.
