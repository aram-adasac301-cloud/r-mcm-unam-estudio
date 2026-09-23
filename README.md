## 0. SINTAXIS GENERAL DE R

```
```

```
# comentario                      # Todo lo situado después de # no se ejecuta.

objeto <- valor                   # <- asigna/guarda un valor en un objeto. Forma recomendada.
objeto = valor                    # = también puede asignar, pero se reserva sobre todo para argumentos.

funcion()                         # () indica llamada a una función.
funcion(argumento = valor)        # = dentro de () asigna valor a un argumento, NO crea un objeto.

"texto"                           # Cadena de caracteres.
'texto'                           # También cadena de caracteres.

;                                 # Separa dos instrucciones en una misma línea.
{ }                               # Agrupa varias instrucciones.

objeto                            # Escribir el nombre imprime/muestra su contenido.
print(objeto)                     # Imprime explícitamente un objeto.

TRUE                              # Valor lógico verdadero.
FALSE                             # Valor lógico falso.

NA                                # Valor faltante: existe la posición, pero falta el dato.
NULL                              # Ausencia de objeto/elemento. Muy importante en listas.

Inf                               # Infinito positivo. Útil como límite abierto, por ejemplo en cut().

1L                                # La L fuerza que 1 se almacene como integer.
2e3                               # Notación científica: 2 × 10^3 = 2000.

Ctrl + Enter                      # Ejecuta desde el script la línea/selección actual.
Alt + -                           # Atajo de RStudio para escribir <-.
↑ / ↓                             # Recorre historial de la consola.
Tab                               # Autocompleta objetos, funciones y rutas.
```

El manual recomienda `<-` para asignar y usa `=` dentro de las llamadas a funciones; también distingue `NA` de `NULL`. 

---

# 1. AYUDA Y DOCUMENTACIÓN

```
```

```
?mean                             # Abre ayuda cuando conoces el nombre exacto de la función.
??mean                            # Busca funciones/documentación relacionada con un término.

help.search("data input")         # Busca documentación por tema o frase.
apropos("mean")                   # Busca nombres de funciones que contengan ese texto.
find("lowess")                    # Indica en qué paquete está una función.
help.start()                      # Abre el sistema general de ayuda de R.
example(sum)                      # Ejecuta los ejemplos oficiales de una función.

?round                            # Consulta ayuda de round().
example(round)                    # Ejecuta sus ejemplos.
```

```
```

```
Description                       # Qué hace la función.
Usage                             # Cómo se escribe.
Arguments                         # Qué significa cada argumento.
Value                             # Qué devuelve.
Examples                          # Ejemplos ejecutables.
```

Regla del curso: `?` si conoces el nombre y `??` si necesitas buscarlo. 

---

# 2. PAQUETES

```
```

```
install.packages("paquete")       # Instala el paquete. Normalmente una sola vez.
library(paquete)                  # Carga el paquete en la sesión actual.

paquete::objeto                   # Usa un objeto/función de un paquete sin cargar todo el paquete.

MASS::birthwt                     # Accede directamente al dataset birthwt de MASS.
```

```
```

```
# install.packages("ggplot2")     # En un script compartido suele dejarse comentado.
library(ggplot2)                  # Se carga en cada nueva sesión.
```

Instalar y cargar son operaciones diferentes. 

---

# 3. OPERADORES ARITMÉTICOS

```
```

```
x + y                             # Suma.
x - y                             # Resta.
x * y                             # Multiplicación.
x / y                             # División.
x ^ y                             # Potencia.

x %/% y                           # División entera. Devuelve el cociente entero.
x %% y                            # Módulo/residuo de la división.

x %% 2 == 0                       # Comprueba si x es par.

( )                               # Controla el orden de las operaciones.
```

---

# 4. OPERADORES DE COMPARACIÓN

```
```

```
x == y                            # Igual a.
x != y                            # Diferente de.

x > y                             # Mayor que.
x < y                             # Menor que.

x >= y                            # Mayor o igual.
x <= y                            # Menor o igual.
```

```
```

```
x > 10                            # Devuelve TRUE o FALSE.
```

Una comparación genera datos **lógicos**. 

---

# 5. OPERADORES LÓGICOS

```
```

```
A & B                             # Y. Ambas condiciones deben ser TRUE.
A | B                             # O inclusivo. Basta con una condición TRUE.
!A                                # NO. Invierte TRUE ↔ FALSE.

A && B                            # Y escalar: evalúa un solo valor lógico.
A || B                            # O escalar: evalúa un solo valor lógico.
```

### Para filtrar datos:

```
```

```
&                                 # USAR éste para vectores/filas.
|                                 # USAR éste para vectores/filas.
!                                 # Negar condición.

&&                                # NO usar para filtrado vectorizado.
||                                # NO usar para filtrado vectorizado.
```

### Precedencia:

```
```

```
!                                 # Se evalúa primero.
&
|
```

```
```

```
(A | B) & C                       # Los paréntesis dejan explícito el orden.
```

Para selección de filas, el manual indica utilizar `&` y `|` vectorizados. 

---

# 6. TIPOS BÁSICOS DE DATOS

```
```

```
5                                 # numeric.
3.14                              # numeric.
2e3                               # numeric en notación científica.

1L                                # integer.

TRUE                              # logical.
FALSE                             # logical.

"hola"                            # character.
'hola'                            # character.
```

### Identificación

```
```

```
class(x)                          # Clase con la que R trata al objeto.
typeof(x)                         # Tipo interno de almacenamiento.
str(x)                            # Estructura completa y compacta del objeto.
```

### Conversión explícita

```
```

```
as.numeric(x)                     # Convierte a numérico.
as.character(x)                   # Convierte a texto.
as.logical(x)                     # Convierte a lógico.
as.factor(x)                      # Convierte a factor.
```

### Coerción automática en vectores

```
```

```
logical → numeric → character     # Jerarquía simplificada de coerción.
```

```
```

```
TRUE                              # Puede convertirse a 1.
FALSE                             # Puede convertirse a 0.
```

`class()` y la familia `as.*()` son centrales en el tema. 

---

# 7. VALORES FALTANTES

```
```

```
NA                                # Dato faltante.

sum(x)                            # Si x contiene NA, normalmente devuelve NA.
sum(x, na.rm = TRUE)              # Ignora los NA al calcular.

mean(x, na.rm = TRUE)             # Media ignorando NA.
```

```
```

```
which(condicion)                  # Devuelve únicamente posiciones TRUE; elimina FALSE y NA.
```

`which()` es especialmente útil cuando una condición de filtrado puede contener `NA`. 

---

# 8. VECTORES

## Constructor principal

```
```

```
c(...)                            # c = combine. Combina valores en UN VECTOR.
```

```
```

```
c(1, 2, 3)                        # Vector numérico.
c(TRUE, FALSE)                    # Vector lógico.
c("a", "b")                       # Vector character.
```

**Regla:** un vector tiene **una dimensión y un solo tipo**. Si mezclas tipos, R hace coerción. 

---

## 8.1 Otras formas de crear vectores

```
```

```
1:10                              # Secuencia de 1 a 10 con paso 1.
10:1                              # Secuencia descendente.

seq(from = 0, to = 1, by = 0.25) # Secuencia controlando inicio, final y paso.

rep(0, times = 5)                 # Repite un valor un número determinado de veces.
```

`:` es el atajo para secuencias sencillas; `seq()` permite controlar el paso y `rep()` repetir valores. 

---

# 9. FUNCIONES PARA VECTORES

```
```

```
length(x)                         # Número de elementos del vector.

names(x)                          # Consulta nombres asociados a sus elementos.
names(x) <- c(...)                # Asigna nombres a sus elementos.

class(x)                          # Clase.
typeof(x)                         # Tipo interno.
str(x)                            # Estructura.

sum(x)                            # Suma todos los elementos.
mean(x)                           # Media.
min(x)                            # Valor mínimo.
max(x)                            # Valor máximo.

which.max(x)                      # Posición/nombre del valor máximo.
which(condicion)                  # Posiciones donde la condición es TRUE.

unique(x)                         # Valores únicos/distintos.

sort(x)                           # Ordena valores.
```

`names()` añade un atributo al vector; no crea otra columna. 

---

# 10. `[ ]` EN VECTORES

Ésta es la sintaxis fundamental:

```
```

```
vector[indice]                    # Selecciona elementos del vector.
```

### Por posición

```
```

```
x[1]                              # Primer elemento.
x[3]                              # Tercer elemento.
```

### Varias posiciones

```
```

```
x[c(1, 3, 5)]                     # c() crea EL VECTOR DE ÍNDICES 1, 3 y 5.
```

Aquí:

```
```

```
[ ]                               # Hace la selección.
c()                               # Agrupa las posiciones que quieres seleccionar.
```

### Excluir

```
```

```
x[-1]                             # Todos excepto el primero.
x[-c(1, 3)]                       # Todos excepto posiciones 1 y 3.
```

### Por nombre

```
```

```
x["nombre"]                       # Elemento con ese nombre.
x[c("nombre1", "nombre2")]        # Varios elementos por nombre.
```

### Por condición

```
```

```
x[x > 10]                         # Conserva elementos >10.
x[x == 10]                        # Conserva elementos iguales a 10.
x[x != 10]                        # Conserva elementos diferentes de 10.
```

R comienza a contar desde **1**, y un índice negativo excluye posiciones. 

---

# 11. CONDICIONES Y VECTORES

```
```

```
x > 10                            # Produce vector TRUE/FALSE.
x[x > 10]                         # Usa ese vector lógico como índice.

sum(x > 10)                       # Cuenta cuántos elementos cumplen condición.
```

```
```

```
TRUE  = 1                         # En operaciones numéricas.
FALSE = 0
```

---

# 12. VECTORIZACIÓN

```
```

```
x + y                             # Suma elemento por elemento.
x - y                             # Resta elemento por elemento.
x * y                             # Multiplica elemento por elemento.
x / y                             # Divide elemento por elemento.

x > y                             # Comparación elemento por elemento.
```

### Funciones agregadoras

```
```

```
sum(x)                            # Muchos elementos → un resultado.
mean(x)                           # Muchos elementos → una media.
min(x)                            # Muchos elementos → mínimo.
max(x)                            # Muchos elementos → máximo.
```

Diferencia fundamental: los operadores vectorizados suelen producir otro vector; las funciones de agregación resumen el vector. 

---

# 13. RECICLADO DE VECTORES

```
```

```
x * 2                             # El 2 se recicla para cada elemento de x.

x + y                             # Si tienen longitudes diferentes, R puede reciclar el más corto.

length(x)                         # Revisar longitud.
length(y)                         # Revisar antes de combinar vectores relacionados.
```

```
```

```
longitud mayor múltiplo de menor
→ puede reciclar SIN advertencia.

longitud mayor NO múltiplo de menor
→ R suele producir Warning.
```

Ésta es una de las trampas importantes del tema. 

---

# 14. MATRICES

## Constructor

```
```

```
matrix(datos)                     # Crea una matriz.
```

```
```

```
matrix(datos,
       nrow = n,                  # Número de filas.
       ncol = n)                  # Número de columnas.
```

```
```

```
matrix(datos,
       nrow = n,
       byrow = TRUE)              # Llena la matriz por filas.
```

```
```

```
byrow = FALSE                     # Comportamiento predeterminado: llena por columnas.
byrow = TRUE                      # Llena por filas.
```

Una matriz tiene **dos dimensiones y todos sus elementos son del mismo tipo**. 

---

# 15. FUNCIONES DE MATRICES

```
```

```
matrix()                          # Crear matriz.

dim(m)                            # Dimensiones: filas × columnas.
nrow(m)                           # Número de filas.
ncol(m)                           # Número de columnas.

rownames(m)                       # Consultar nombres de filas.
rownames(m) <- c(...)             # Asignar nombres de filas.

colnames(m)                       # Consultar nombres de columnas.
colnames(m) <- c(...)             # Asignar nombres de columnas.

rbind(...)                        # Une/agrega objetos por FILAS.
cbind(...)                        # Une/agrega objetos por COLUMNAS.

class(m)                          # Clase.
str(m)                            # Estructura.
summary(m)                        # Resumen estadístico si es numérica.

is.matrix(m)                      # TRUE si el objeto sigue siendo matriz.

colSums(m)                        # Suma cada columna.
colMeans(m)                       # Media de cada columna.
rowSums(m)                        # Suma cada fila.

which.max(x)                      # Localiza el máximo de un resultado/vector.
which(condicion)                  # Posiciones TRUE.
```

En matrices se usan `rownames()` y `colnames()`, no `names()` para representar las dos dimensiones. 

---

# 16. `[fila, columna]` EN MATRICES

Regla que debes memorizar:

```
```

```
m[fila, columna]                  # MATRIZ = [FILA, COLUMNA].
```

### Una celda

```
```

```
m[2, 3]                           # Fila 2, columna 3.
```

### Una fila

```
```

```
m[2, ]                            # Fila 2, TODAS las columnas.
```

### Una columna

```
```

```
m[, 3]                            # TODAS las filas, columna 3.
```

### Varias filas

```
```

```
m[c(1, 3), ]                      # Filas 1 y 3.
```

### Varias columnas

```
```

```
m[, c(1, 3)]                      # Columnas 1 y 3.
```

### Varias filas y columnas

```
```

```
m[c(1, 3), c(2, 4)]              # Filas 1 y 3; columnas 2 y 4.
```

### Por nombres

```
```

```
m["Paciente1", "Glucosa"]         # Fila y columna por nombre.

m[, c("Glucosa", "Plaquetas")]   # Todas las filas y columnas indicadas.
```

### Por condición

```
```

```
m[m[, "Glucosa"] > 100, ]         # Filtra FILAS según una columna.

m[condicion, ]                    # Condición aplicada a filas.
```

La coma es esencial porque separa **filas de columnas**. 

---

# 17. `c()` DENTRO DE UNA MATRIZ

No significa que la matriz se convierta en vector.

```
```

```
m[c(1, 3), ]                      # c() crea el VECTOR de filas que quieres.
m[, c(2, 4)]                      # c() crea el VECTOR de columnas que quieres.
```

```
```

```
m[ , ]                            # Selección de matriz.
c()                               # Sólo agrupa índices/nombres.
```

---

# 18. EVITAR QUE UNA MATRIZ SE CONVIERTA EN VECTOR

Una matriz con una única fila o columna seleccionada puede simplificarse.

```
```

```
m[1, ]                            # Puede devolver vector.

m[1, , drop = FALSE]              # Conserva estructura de matriz.

m[, 1, drop = FALSE]              # Conserva matriz de una columna.
```

---

# 19. FILTRADO DE MATRICES CON `NA`

```
```

```
condicion <- m[, "variable"] > valor        # Puede generar TRUE/FALSE/NA.

m[which(condicion), ]                       # which() conserva sólo TRUE reales.
```

---

# 20. DATA FRAME

## Constructor

```
```

```
data.frame(...)                    # Crea un data frame.
```

Conceptualmente:

```
```

```
data frame                         # Lista de vectores.
cada columna                       # Un vector.
todas las columnas                 # Deben tener el mismo largo.
cada columna                       # Puede tener distinto tipo.
filas                              # Observaciones.
columnas                           # Variables.
```

---

# 21. FUNCIONES PARA INSPECCIONAR UN DATA FRAME

```
```

```
str(df)                            # PRIMERA función: estructura y tipo de cada columna.

summary(df)                        # Resumen de cada variable.

head(df)                           # Primeras 6 filas.
head(df, n = 3)                    # Primeras 3 filas.

tail(df)                           # Últimas 6 filas.
tail(df, n = 1)                    # Última fila.

dim(df)                            # Número de filas y columnas.
nrow(df)                           # Número de filas/observaciones.
ncol(df)                           # Número de columnas/variables.

names(df)                          # Nombres de columnas.
colnames(df)                       # Nombres de columnas.

class(df)                          # "data.frame".
typeof(df)                         # Internamente un data frame es una "list".
```

El manual señala `str()` como la primera inspección del data frame. 

---

# 22. `$` EN DATA FRAME

```
```

```
df$variable                       # Extrae una columna POR NOMBRE.
```

```
```

```
$                                 # "Entra al objeto y dame este componente por nombre".
```

```
```

```
df$edad                           # Devuelve el vector almacenado en edad.

df$nueva_variable <- vector       # Crea una nueva columna.

df$variable <- nuevo_vector       # Reemplaza/modifica una columna existente.
```

La longitud del vector asignado debe corresponder con las filas; puede aparecer reciclado si el largo es compatible. 

---

# 23. `[[ ]]` EN DATA FRAME

```
```

```
df[["variable"]]                  # Extrae UNA columna como vector.
```

Especialmente útil cuando el nombre está guardado en otro objeto:

```
```

```
nombre <- "edad"
df[[nombre]]                      # Busca la columna cuyo nombre está almacenado en nombre.
```

Mientras:

```
```

```
df$nombre                         # Busca literalmente una columna llamada "nombre".
```

---

# 24. `[ ]` EN DATA FRAME

El data frame también utiliza:

```
```

```
df[filas, columnas]
```

### Filas

```
```

```
df[1, ]                           # Primera fila.
df[c(1, 3), ]                     # Filas 1 y 3.
```

### Columnas

```
```

```
df[, 2]                           # Segunda columna.
df[, c(1, 3)]                     # Columnas 1 y 3.

df[, c("edad", "sexo")]           # Columnas por nombre.
```

### Filas y columnas simultáneamente

```
```

```
df[c(1, 3), c("edad", "sexo")]    # Filas 1 y 3 + columnas edad y sexo.
```

---

# 25. DIFERENCIA CRÍTICA EN DATA FRAME

```
```

```
df$edad                           # Vector edad.
df[["edad"]]                      # Vector edad.
df[, "edad"]                      # Normalmente simplifica a vector.

df["edad"]                        # DATA FRAME de una sola columna.
```

Regla mental:

```
```

```
$                                 # Extraer contenido por nombre.
[[ ]]                             # Extraer contenido.
[ ]                               # Seleccionar/conservar contenedor.
```

El comportamiento se entiende porque un data frame es internamente una lista de columnas. 

---

# 26. FILTRAR FILAS DE UN DATA FRAME

Patrón fundamental:

```
```

```
df[condicion, ]
```

```
```

```
df[df$edad > 40, ]                # Filas con edad >40.

df[df$edad > 40 &
   df$sexo == "M", ]              # Ambas condiciones.

df[df$edad > 40 |
   df$sexo == "M", ]              # Al menos una condición.

df[!df$hospitalizado, ]           # Hospitalizado == FALSE.
```

La condición produce primero un vector lógico; éste se introduce en la posición de las filas. 

---

# 27. COMPROBAR UN FILTRO

```
```

```
nrow(df_filtrado)                 # Cuántas filas quedaron.

str(df_filtrado)                  # Comprobar estructura.
```

Si quedan 0 filas o todas cuando no debería, revisar la condición. 

---

# 28. FACTORES

## Constructor

```
```

```
factor(x)                         # Convierte/crea una variable categórica.

as.factor(x)                      # Conversión directa a factor.
```

Conceptualmente:

```
```

```
factor                            # Vector categórico.
por dentro                        # integer.
atributos                         # levels + class.
```

---

# 29. FUNCIONES PARA FACTORES

```
```

```
factor(x)                         # Crear factor.
as.factor(x)                      # Convertir a factor.

levels(f)                         # Consultar niveles/categorías.
nlevels(f)                        # Número de niveles.

length(f)                         # Número de observaciones, NO número de niveles.

table(f)                          # Frecuencias por categoría.
summary(f)                        # Frecuencias por categoría.

unique(x)                         # Valores que realmente aparecen en los datos.

relevel(f, ref = "categoria")     # Cambiar categoría de referencia.

droplevels(f)                     # Eliminar niveles vacíos.

sort(f)                           # Ordena respetando el orden de levels.

class(f)                          # "factor".
typeof(f)                         # "integer".
str(f)                            # Muestra levels y códigos internos.

attributes(f)                     # Todos los atributos.
names(attributes(f))             # Nombres de los atributos, p. ej. levels y class.
```

Un factor conoce tanto los datos observados como el catálogo de categorías posibles. 

---

# 30. `levels` EN FACTORES

```
```

```
factor(x,
       levels = c("leve",
                  "moderado",
                  "grave"))
```

```
```

```
levels = c(...)                   # Define catálogo Y orden de las categorías.
```

```
```

```
levels(f)                         # Consulta ese orden.
```

Si no declaras `levels`, R suele ordenarlos alfabéticamente. 

---

# 31. `labels` EN FACTORES

```
```

```
factor(x,
       levels = c(0, 1),
       labels = c("no", "sí"))
```

```
```

```
levels                            # Valores originales permitidos.
labels                            # Etiquetas con las que quieres mostrarlos.
```

---

# 32. FACTORES ORDENADOS

```
```

```
factor(x,
       levels = c("leve", "moderado", "grave"),
       ordered = TRUE)
```

```
```

```
levels = c(...)                   # Define el ORDEN.
ordered = TRUE                    # Declara que ese orden tiene jerarquía.
```

Entonces:

```
```

```
f[1] > f[2]                       # Comparación ordinal permitida.
f[1] < f[2]                       # Comparación ordinal permitida.

min(f)                            # Puede utilizarse en factor ordenado.
max(f)                            # Puede utilizarse en factor ordenado.
```

Sin `ordered = TRUE`, `<` y `>` no tienen significado para un factor nominal. 

---

# 33. CATEGORÍA DE REFERENCIA

```
```

```
relevel(f, ref = "control")       # Coloca "control" como primer nivel/referencia.
```

```
```

```
primer level                      # Normalmente categoría de referencia en modelos.
```

---

# 34. FRECUENCIAS Y TABLAS DE CONTINGENCIA

```
```

```
table(f)                          # Frecuencias de una variable categórica.

table(f1, f2)                     # Tabla cruzada/contingencia de dos variables.
```

```
```

```
prop.table(tabla)                 # Convierte conteos en proporciones globales.

prop.table(tabla, margin = 1)     # Proporciones POR FILA.

prop.table(tabla, margin = 2)     # Proporciones POR COLUMNA.
```

```
```

```
round(x, 2)                       # Redondea a 2 decimales.
```

`prop.table(..., margin = 1)` aparece en el manual para porcentajes por fila. 

---

# 35. DE VARIABLE CONTINUA A CATEGÓRICA: `cut()`

```
```

```
cut(x,
    breaks = c(...),              # Puntos de corte.
    labels = c(...),              # Nombres de los intervalos.
    right = FALSE)                # Decide inclusión del límite derecho.
```

```
```

```
breaks                            # Límites/puntos de corte.
labels                            # Etiquetas para cada intervalo.
right = TRUE                      # Intervalos cerrados por la derecha.
right = FALSE                     # Intervalos cerrados por la izquierda.
Inf                               # Límite superior infinito.
```

```
```

```
cut(x,
    breaks = c(0, 18, 65, Inf),
    labels = c("grupo1", "grupo2", "grupo3"),
    right = FALSE)
```

`cut()` devuelve un factor categórico. 

---

# 36. TRAMPA FACTOR → NUMÉRICO

```
```

```
as.numeric(f)                     # PELIGRO: devuelve códigos internos del factor.

as.character(f)                   # Primero recupera las etiquetas.
as.numeric(as.character(f))       # Conversión correcta si las etiquetas representan números.
```

---

# 37. NIVELES VACÍOS

Después de filtrar:

```
```

```
table(f)                          # Puede mostrar categorías con frecuencia 0.

droplevels(f)                     # Elimina niveles que ya no están presentes.
```

---

# 38. LISTAS

## Constructor

```
```

```
list(...)                         # Crea una lista.
```

```
```

```
list(
  nombre1 = objeto1,
  nombre2 = objeto2
)
```

Una lista puede contener:

```
```

```
numeric
character
logical
vector
factor
matrix
data.frame
list
modelo
```

sin necesidad de que tengan la misma longitud o tipo. 

---

# 39. FUNCIONES PARA LISTAS

```
```

```
list(...)                         # Crear lista.

length(lista)                     # Número de ELEMENTOS/COMPARTIMENTOS de la lista.

lengths(lista)                    # Longitud de CADA elemento interno.

names(lista)                      # Nombres de los elementos.

str(lista)                        # Estructura completa de la lista.

unlist(lista)                     # Aplana la lista y la convierte en vector.

class(lista)                      # Clase.
typeof(lista)                     # Tipo interno.
```

`length()` cuenta compartimentos; `lengths()` mide cada compartimento. 

---

# 40. `[ ]` EN LISTAS

```
```

```
lista["elemento"]                 # Devuelve una SUBLISTA.
lista[1]                          # Devuelve una SUBLISTA.
```

```
```

```
[ ]                               # Conserva el contenedor lista.
```

Si haces:

```
```

```
class(lista["elemento"])          # "list"
```

---

# 41. `[[ ]]` EN LISTAS

```
```

```
lista[["elemento"]]               # EXTRAE el objeto contenido.
lista[[1]]                        # Extrae el primer objeto.
```

```
```

```
[[ ]]                             # Abre el compartimento y saca su contenido.
```

```
```

```
nombre <- "elemento"
lista[[nombre]]                   # Permite que el nombre esté guardado en otra variable.
```

---

# 42. `$` EN LISTAS

```
```

```
lista$elemento                    # Extrae objeto por nombre.
```

Conceptualmente:

```
```

```
lista$elemento                    # Similar a:
lista[["elemento"]]
```

Pero:

```
```

```
nombre <- "elemento"

lista[[nombre]]                   # CORRECTO: usa el contenido de nombre.
lista$nombre                      # Busca literalmente algo llamado "nombre".
```

En scripts conviene escribir el nombre completo después de `$`; la coincidencia parcial puede ser peligrosa. 

---

# 43. REGLA DEFINITIVA DE LOS CORCHETES

```
```

```
lista["x"]                        # Devuelve LISTA.
lista[["x"]]                      # Devuelve CONTENIDO.
lista$x                           # Devuelve CONTENIDO por nombre.
```

```
```

```
[ ]                               # Seleccionar/conservar contenedor.
[[ ]]                             # Extraer.
$                                 # Extraer por nombre.
```

---

# 44. OBJETOS DENTRO DE LISTAS

Se lee de izquierda a derecha:

```
```

```
lista$df$edad                     # Lista → data frame → columna.

lista$df$edad[2]                  # Lista → data frame → vector → segundo elemento.

lista$matriz[2, 3]                # Lista → matriz → fila 2, columna 3.

lista[["df"]][["edad"]][2]        # Lo mismo usando [[ ]].
```

Cada estructura conserva sus propias reglas aunque esté dentro de una lista. 

---

# 45. MODIFICAR LISTAS

```
```

```
lista$nuevo <- objeto             # Añade nuevo elemento.

lista$existente <- objeto         # Reemplaza elemento existente.

lista$elemento <- NULL            # ELIMINA ese elemento.

lista$elemento <- NA              # Mantiene el elemento pero con valor faltante.
```

---

# 46. `unlist()`

```
```

```
unlist(lista)                     # Aplana una lista y produce un vector.
```

Como un vector exige un solo tipo:

```
```

```
logical → numeric → character
```

puede ocurrir coerción al hacer `unlist()`. 

---

# 47. DATA FRAME = LISTA ESPECIAL

Esto conecta todo:

```
```

```
typeof(df)                        # "list".

length(df)                        # Número de columnas.

df["edad"]                        # Sublista especial → data.frame.
df[["edad"]]                      # Contenido → vector.
df$edad                           # Contenido → vector.
```

```
```

```
data frame
    ├── columna 1 = vector
    ├── columna 2 = vector
    ├── columna 3 = vector
    └── todos tienen igual longitud
```

---

# 48. TABLA DEFINITIVA DE SELECCIÓN

| EstructuraSintaxisSignificado |                    |                             |
| ----------------------------- | ------------------ | --------------------------- |
| Vector                        | `x[i]`             | elemento(s)                 |
| Vector                        | `x[c(i,j)]`        | varias posiciones           |
| Vector                        | `x[-i]`            | excluir posición            |
| Vector                        | `x[condicion]`     | filtrar                     |
| Matriz                        | `m[fila,columna]`  | celda/submatriz             |
| Matriz                        | `m[fila, ]`        | fila                        |
| Matriz                        | `m[, columna]`     | columna                     |
| Matriz                        | `m[c(...),c(...)]` | varias filas/columnas       |
| Data frame                    | `df[fila,columna]` | tabla/subtabla              |
| Data frame                    | `df$var`           | columna como vector         |
| Data frame                    | `df[["var"]]`      | columna como vector         |
| Data frame                    | `df["var"]`        | data frame de una columna   |
| Lista                         | `l["x"]`           | sublista                    |
| Lista                         | `l[["x"]]`         | objeto contenido            |
| Lista                         | `l$x`              | objeto contenido por nombre |

---

# 49. TABLA DEFINITIVA DE CONSTRUCTORES

```
```

```
c(...)                            # VECTOR.
1:10                              # VECTOR secuencial.
seq(...)                          # VECTOR secuencial.
rep(...)                          # VECTOR repetido.

matrix(...)                       # MATRIZ.

data.frame(...)                   # DATA FRAME.

factor(...)                       # FACTOR.

list(...)                         # LISTA.
```

---

# 50. FUNCIONES GENERALES DE INSPECCIÓN

```
```

```
class(x)                          # Cómo se comporta/clase.

typeof(x)                         # Cómo está almacenado internamente.

str(x)                            # Estructura completa. FUNCIÓN CLAVE.

length(x)                         # Longitud:
                                   # vector → elementos.
                                   # factor → observaciones.
                                   # lista → compartimentos.
                                   # data frame → columnas.

dim(x)                            # Dimensiones filas × columnas.

nrow(x)                           # Número de filas.
ncol(x)                           # Número de columnas.

names(x)                          # Nombres de elementos/columnas.

rownames(x)                       # Nombres de filas.
colnames(x)                       # Nombres de columnas.

head(x)                           # Primeras observaciones.
tail(x)                           # Últimas observaciones.

summary(x)                        # Resumen dependiente de la clase.
```

`summary()` cambia su comportamiento según la clase del objeto, por eso `class()` y `str()` son tan importantes. 

---

# 51. QUÉ HACE `summary()` SEGÚN EL OBJETO

```
```

```
summary(vector_numerico)          # Mínimo, Q1, mediana, media, Q3, máximo.

summary(matriz_numerica)          # Resúmenes numéricos.

summary(data_frame)               # Resumen columna por columna.

summary(factor)                   # Frecuencia de cada nivel.

summary(modelo)                   # Objeto resumen del modelo.
```

---

# 52. FÓRMULAS EPIDEMIOLÓGICAS DEL TEMA 01

## Tasa de incidencia

```math
TI=\frac{C}{N}\times k
```

```
```

```
tasa_incidencia <- (casos_nuevos / poblacion_riesgo) * k
# C = casos nuevos.
# N = población en riesgo.
# k = constante de escala: 1000, 100000, etc.
```

## Prevalencia

```math
P=\frac{C}{N}\times100
```

```
```

```
prevalencia <- (casos_totales / poblacion) * 100
# C = casos existentes/totales.
# N = población.
```

## Letalidad

```math
L=\frac{D}{C}\times100
```

```
```

```
letalidad <- (muertes / casos_totales) * 100
# D = defunciones por la enfermedad.
# C = casos de la enfermedad.
```

La diferencia fundamental está en el **denominador**; R ejecutará cualquier división aunque conceptualmente sea incorrecta. 

---

# 53. FÓRMULAS EN MODELOS DE R

```
```

```
y ~ x                              # Fórmula: y se modela/explica en función de x.

lm(y ~ x, data = df)               # Ajusta modelo lineal.

modelo <- lm(y ~ x, data = df)     # Guarda el modelo.

coef(modelo)                       # Extrae coeficientes.

modelo$coefficients                # Extrae coeficientes directamente de la lista.

summary(modelo)                    # Resumen del modelo.

summary(modelo)$r.squared          # Extrae R² desde la lista producida por summary().
```

```
```

```
~                                  # "en función de" / relación fórmula.
data = df                          # Indica de qué data frame salen las variables.
```

Los modelos aparecen en el tema para demostrar que los resultados de R suelen ser listas y que una variable categórica debe codificarse correctamente como factor. 

---

# 54. `::`

```
```

```
paquete::objeto                   # Busca objeto específicamente dentro de un paquete.

MASS::birthwt                     # Dataset birthwt del paquete MASS.
```

---

# 55. `round()`

```
```

```
round(x)                          # Redondea.
round(x, digits = 2)              # Redondea a 2 decimales.
```

---

# 56. `table()` + `prop.table()` + `round()`

Secuencia típica para categóricas:

```
```

```
tabla <- table(df$grupo, df$evento)          # Conteos.

prop.table(tabla, margin = 1)                # Proporciones por fila.

round(prop.table(tabla, margin = 1), 2)      # Proporciones por fila a 2 decimales.
```

---

# 57. SÍMBOLOS QUE DEBES RECONOCER AL INSTANTE

```
```

```
<-                                # Asignar.
=                                 # Argumento = valor; también puede asignar.

#                                 # Comentario.

()                                # Función / agrupación matemática.

[]                                # Selección/subconjunto.

[[]]                              # Extracción de contenido de lista/data frame.

$                                 # Extraer componente por nombre.

,                                 # En [fila,columna], separa dimensiones.

c()                               # combine → crear vector/combinar valores.

:                                 # Secuencia.

-                                 # Resta O índice negativo para excluir.

+                                 # Suma.

*                                 # Multiplicación.

/                                 # División.

^                                 # Potencia.

%/%                               # División entera.

%%                                # Residuo.

==                                # Igual.

!=                                # Diferente.

>                                 # Mayor.

<                                 # Menor.

>=                                # Mayor o igual.

<=                                # Menor o igual.

&                                 # Y vectorizado.

|                                 # O vectorizado.

!                                 # Negación.

&&                                # Y escalar.

||                                # O escalar.

~                                 # Fórmula de modelo: respuesta ~ predictor.

::                                # objeto perteneciente a un paquete.

TRUE                              # Verdadero.

FALSE                             # Falso.

NA                                # Dato faltante.

NULL                              # Ausencia de objeto.

Inf                               # Infinito.

L                                 # Sufijo para integer.

e                                 # Notación científica.
```

---

# 58. LA REGLA MÁS IMPORTANTE PARA NO CONFUNDIRTE

```
```

```
VECTOR
x[ ]                              # selecciona elementos.
x[c()]                            # selecciona varios elementos.

MATRIZ
m[fila, columna]                  # SIEMPRE pensar fila, columna.
m[c(...), c(...)]                 # varias filas y varias columnas.

DATA FRAME
df[fila, columna]                 # seleccionar tabla.
df$variable                       # sacar columna por nombre.
df[["variable"]]                  # sacar columna/contenido.
df["variable"]                    # conservar data frame.

FACTOR
f[ ]                              # se comporta como vector para seleccionar.
levels(f)                         # catálogo de categorías.
factor()                          # crear/configurar categorías.

LISTA
l["x"]                            # conservar lista.
l[["x"]]                          # sacar contenido.
l$x                               # sacar contenido por nombre.
```

Y la secuencia práctica que te conviene automatizar es:

```
```

```
str(x)                            # 1. ¿Qué estructura tengo?
class(x)                          # 2. ¿Qué clase tiene?
typeof(x)                         # 3. ¿Cómo está almacenado?

length(x)                         # 4. Si es 1D/lista: ¿cuánto mide?
dim(x)                            # 4. Si es tabla/matriz: ¿qué dimensiones tiene?

# Después seleccionas según estructura:

x[i]                              # Vector/factor.
m[fila, columna]                  # Matriz.
df[fila, columna]                 # Data frame.
df$variable                       # Columna de data frame.
l[["elemento"]]                   # Contenido de lista.
```

Eso cubre el **código, operadores, constructores, selección, inspección, factores, listas y fórmulas que aparecen como contenido de los dos temas**. 