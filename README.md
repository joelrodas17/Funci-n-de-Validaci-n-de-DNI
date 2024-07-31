### Documentación de la Función `validaDni`

#### Descripción
La función `validaDni` verifica la validez de un DNI (Documento Nacional de Identidad) basado en un algoritmo que calcula un dígito de control. Dependiendo de si el DNI es numérico o alfabético, el dígito de control puede ser un número o una letra. La función retorna `true` si el DNI es válido, y `false` en caso contrario.

#### Parámetros
- **`data`**: (string) - El DNI a validar. Puede contener guiones, espacios, o letras minúsculas, los cuales serán limpiados y normalizados.

#### Retorno
- **`boolean`**: Retorna `true` si el DNI es válido según el algoritmo implementado, o `false` en caso contrario.

#### Detalles del Funcionamiento

1. **Normalización del DNI**:
   - Se eliminan los guiones (`-`), espacios en blanco, y se convierte a mayúsculas.

2. **Verificación Inicial**:
   - Si el DNI no existe (`null` o vacío) o tiene una longitud menor a 9 caracteres, la función retorna `false` inmediatamente.

3. **Cálculo del Dígito de Control**:
   - El DNI se divide en dos partes: `numdni` que contiene los dígitos (sin el dígito de control), y `dcontrol`, que es el último carácter.
   - Se multiplican los dígitos por los valores en el array `multiples`, y se suma el resultado.
   - Se calcula el valor de la llave (`key`) usando la fórmula `11 - (dsum % 11)`, donde `dsum` es la suma calculada.

4. **Verificación del Dígito de Control**:
   - Dependiendo de si el DNI es numérico o alfabético, se verifica si el dígito de control coincide con el valor esperado:
     - Si es numérico: Se compara con el valor correspondiente en el array `dcontrols.numbers`.
     - Si es alfabético: Se compara con el valor correspondiente en el array `dcontrols.letters`.

Aquí tienes algunos ejemplos de uso de la función `validaDni` basados en diferentes valores de dígito verificador, tanto numérico como alfabético.

### Ejemplos de Uso

1. **DNI con dígito verificador numérico:**

   ```javascript
   console.log(validaDni("12345678K")); // false (Ejemplo de dígito de control incorrecto)
   console.log(validaDni("123456780")); // true (Dígito de control numérico correcto)
   console.log(validaDni("87654321J")); // false (Dígito de control incorrecto)
   console.log(validaDni("876543219")); // true (Dígito de control numérico correcto)
   ```

2. **DNI con dígito verificador alfabético:**

   ```javascript
   console.log(validaDni("12345678B")); // false (Dígito de control incorrecto)
   console.log(validaDni("23456789H")); // true (Dígito de control alfabético correcto)
   console.log(validaDni("34567890A")); // true (Dígito de control alfabético correcto)
   console.log(validaDni("45678901F")); // false (Dígito de control incorrecto)
   ```

3. **Casos con formato mixto (con guiones o espacios):**

   ```javascript
   console.log(validaDni("12345678-K")); // false (Dígito de control incorrecto)
   console.log(validaDni("12345678-0")); // true (Formato con guión, dígito de control correcto)
   console.log(validaDni("1234 5678 J")); // false (Formato con espacio, dígito de control incorrecto)
   console.log(validaDni("2345 6789 H")); // true (Formato con espacio, dígito de control correcto)
   ```

### Explicación de los Ejemplos

- **Ejemplo 1**: Se muestran DNIs con un dígito verificador numérico. Solo aquellos que coinciden con el dígito de control calculado son considerados válidos (`true`).
  
- **Ejemplo 2**: Se presentan DNIs con un dígito verificador alfabético. Nuevamente, solo los DNIs con un dígito de control correcto retornan `true`.

- **Ejemplo 3**: Se incluyen DNIs que contienen guiones o espacios en su formato. La función los normaliza antes de validarlos, asegurando que solo el dígito de control determine su validez.

Estos ejemplos cubren diferentes escenarios comunes para verificar el correcto funcionamiento de la función `validaDni` según el dígito verificador proporcionado.
