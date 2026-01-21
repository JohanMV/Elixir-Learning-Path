# Recursión en Elixir

La recursión es el mecanismo fundamental para iterar en Elixir, reemplazando bucles imperativos tradicionales.
Una función recursiva se llama a sí misma con argumentos modificados hasta alcanzar un **caso base** que detiene la recursión.

---

## Estructura básica: caso base y caso recursivo

Toda función recursiva necesita:
1. **Caso base**: condición que detiene la recursión
2. **Caso recursivo**: la función se llama con argumentos modificados

```elixir
def factorial(0), do: 1
def factorial(n), do: n * factorial(n - 1)

IO.puts(factorial(5))   # → 120
IO.puts(factorial(0))   # → 1
```

Sin caso base, la recursión sería infinita y provocaría un desbordamiento de pila (*stack overflow*).

---

## Recursión sobre listas

El pattern matching con `[cabeza | cola]` es especialmente útil para procesar listas recursivamente.

```elixir
# Caso base: lista vacía
def sumar([]), do: 0

# Caso recursivo: suma la cabeza y continúa con la cola
def sumar([cabeza | cola]) do
  cabeza + sumar(cola)
end

IO.puts(sumar([1, 2, 3, 4, 5]))  # → 15

# Recorrer e imprimir
def imprimir([]), do: nil
def imprimir([cabeza | cola]) do
  IO.puts(cabeza)
  imprimir(cola)
end

imprimir([:a, :b, :c])
# → :a
# → :b
# → :c
```

---

## Tail Call Optimization (TCO)

Elixir optimiza automáticamente la **recursión de cola** (cuando la llamada recursiva es la última operación).
Esto reutiliza el stack frame, evitando desbordamientos incluso con miles de iteraciones.

### Sin TCO (ineficiente)

```elixir
def factorial_lento(0, acc), do: acc
def factorial_lento(n, acc) do
  acc * n  # ❌ Otra operación DESPUÉS de la recursión
  factorial_lento(n - 1, acc)
end
```

### Con TCO (eficiente)

```elixir
def factorial(0, acc), do: acc
def factorial(n, acc) do
  factorial(n - 1, n * acc)  # ✅ Última operación: la recursión
end

IO.puts(factorial(5, 1))  # → 120
IO.puts(factorial(1000, 1))  # → Sin desbordamiento
```

---

## Acumuladores

Para lograr TCO, usamos acumuladores que cargan el resultado progresivamente.

```elixir
# Sintaxis: parámetro con valor por defecto
def contar_elementos(lista, contador \\ 0)
def contar_elementos([], contador), do: contador
def contar_elementos([_cabeza | cola], contador) do
  contar_elementos(cola, contador + 1)
end

IO.puts(contar_elementos([1, 2, 3, 4]))  # → 4
```

---

## Ejemplos prácticos

**Invertir una lista:**

```elixir
def invertir(lista, resultado \\ [])
def invertir([], resultado), do: resultado
def invertir([cabeza | cola], resultado) do
  invertir(cola, [cabeza | resultado])
end

IO.puts(inspect(invertir([1, 2, 3, 4])))  # → [4, 3, 2, 1]
```

**Buscar en lista:**

```elixir
def buscar(_, []), do: nil
def buscar(objetivo, [objetivo | _]), do: true
def buscar(objetivo, [_ | cola]), do: buscar(objetivo, cola)

IO.puts(buscar(3, [1, 2, 3, 4]))  # → true
IO.puts(buscar(5, [1, 2, 3, 4]))  # → nil
```

---

## Resumen

- **Caso base** detiene la recursión; **caso recursivo** continúa
- **TCO** permite recursión eficiente sin desbordamiento de pila
- **Acumuladores** cargan el resultado incrementalmente
- El **pattern matching** con listas hace la recursión natural y legible
- La recursión sustituye los bucles imperativos tradicionales

Dominar recursión es esencial para programación funcional en Elixir.