# Inmutabilidad y Asignación en Elixir

## ¿Qué significa que todo es inmutable?

En Elixir, **una vez creado un valor, nunca cambia**. Si "modificas" una lista, un mapa o una cadena, en realidad estamos creando **una nueva copia** con los cambios aplicados. El valor original permanece intacto.

### Ejemplo práctico

```elixir
usuario = %{nombre: "Ana", edad: 25}
usuario_actualizado = %{usuario | edad: 26}