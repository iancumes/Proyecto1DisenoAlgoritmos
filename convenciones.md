# Convenciones de la Máquina de Turing de Fibonacci

1. **Representación de Entrada (Unaria):**
   Un número entero no negativo $n$ se representa colocando en la cinta una cadena de $n$ símbolos `1`.
   - Ejemplo: Para $n = 3$, la entrada inicial es `1 1 1`.
   - Ejemplo: Para $n = 0$, la cinta se encuentra vacía (compuesta solo de blancos `_`).

2. **Representación de Salida (Unaria):**
   El resultado al detenerse la máquina será la secuencia ininterrumpida de símbolos `0` más a la derecha, separada del resto de la cinta por el símbolo `#`.
   - La cantidad final de símbolos `0` será el $n$-ésimo número de Fibonacci.
   - En nuestro modelo, hemos definido que $F_0 = 0$, $F_1 = 1$, $F_2 = 1$, $F_3 = 2$, $F_4 = 3$, $F_5 = 5$, etc.

3. **Alfabeto de la Cinta y Significado Adicional:**
   - `1`: Representa las unidades pendientes de $n$ (input).
   - `0`: Representa las unidades de los números de Fibonacci que estamos calculando.
   - `X`: Marca un `1` de la entrada que ya ha sido iterado.
   - `#`: Separador físico de los bloques lógicos de ceros que guardan $F_{k-1}$ y $F_{k}$.
   - `x`, `y`: Marcadores temporales utilizados durante la copia de los bloques de `0`s (copiado hacia la derecha).
   - `_` (Blanco): Denota celdas vacías al inicio y al final de los datos en la cinta.
