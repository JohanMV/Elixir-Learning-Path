
# Pattern Matching en Funciones

El *pattern matching* en Elixir brilla especialmente en las **cláusulas de función**. Permite definir múltiples versiones de una función que se ejecutan según la estructura de los argumentos.

---

## Manejo de estados con tuplas

El *pattern matching* es útil para manejar diferentes estados representados por tuplas:

```elixir
def procesar_respuesta({:ok, datos}) do
  IO.puts("Éxito: #{datos}")
end

def procesar_respuesta({:error, razon}) do
  IO.puts("Error: #{razon}")
end

# Uso:
procesar_respuesta({:ok, "Usuario creado"})     # → Éxito: Usuario creado
procesar_respuesta({:error, "Email inválido"})  # → Error: Email inválido
```

---

## Recursión con listas

El *pattern matching* facilita la recursión en listas:

```elixir
# Caso base: lista vacía
def sumar([]), do: 0

# Caso recursivo: cabeza + suma del resto
def sumar([cabeza | cola]) do
  cabeza + sumar(cola)
end

sumar([1, 2, 3, 4])  # → 10
```

---

## Validación de estructura de datos

Se puede usar *pattern matching* para validar y manejar estructuras de datos como mapas:

```elixir
def saludar(%{nombre: nombre, edad: edad}) when edad >= 18 do
  "Bienvenido, #{nombre} (adulto)"
end

def saludar(%{nombre: nombre}) do
  "Hola, #{nombre} (menor de edad)"
end

# Uso:
saludar(%{nombre: "Ana", edad: 25})  # → Bienvenido, Ana (adulto)
saludar(%{nombre: "Luis"})           # → Hola, Luis (menor de edad)
```

> ✅ Las funciones se evalúan de arriba a abajo. El primer patrón que coincida se ejecuta.

---

## Ventajas

- **Código más declarativo y legible**: El *pattern matching* permite escribir código que refleja directamente la lógica del problema.
- **Elimina la necesidad de `if/else` o `switch`**: En muchos casos, se pueden evitar estructuras condicionales complejas.
- **Fuerza a manejar explícitamente distintos casos**: Esto mejora la cobertura de errores y hace el código más seguro.

El *pattern matching* en funciones es una de las herramientas más poderosas de Elixir para escribir código seguro y expresivo.
