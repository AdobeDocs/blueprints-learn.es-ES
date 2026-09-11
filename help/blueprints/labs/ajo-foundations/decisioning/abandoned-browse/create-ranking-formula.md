---
hold: true
title: Crear fórmula de clasificación
description: Cree una fórmula de clasificación que aumente dinámicamente las puntuaciones de prioridad de oferta en función de atributos de perfil como la edad.
doc-type: article
solution: Experience Platform
exl-id: 67aaca7f-366c-4db4-a5d5-017f52fbd15b
source-git-commit: 2b2b9b9c359c4cc6757ac62ad502ece9a4923095
workflow-type: tm+mt
source-wordcount: '1761'
ht-degree: 0%

---


# Crear fórmula de clasificación

## Objetivo

Ahora que todos los elementos de la oferta se han creado, priorizado, se han aplicado los requisitos y se han organizado en una colección, podemos centrar nuestra atención en determinar cómo se clasificarán para un perfil determinado. Esto se hace creando una fórmula de clasificación.

Una fórmula de clasificación aumenta dinámicamente las prioridades de oferta específicas para que &quot;suban a la parte superior&quot;, en función de los criterios del perfil que interactúa con la propiedad web/móvil o el propio evento de experiencia.

En este escenario de laboratorio, pretenderemos que el equipo de marketing de investigación para Connection 5G mostró que los menores de 39 años serían atraídos a los niveles Ultra o Pro y los de 40-59 serían atraídos a los niveles base y pro. Y como Connection 5G preferiría vender teléfonos de nivel superior, siendo todo igual, el modelo ultra se presentaría primero para los menores de 39 años, con el modelo pro presentándose primero para los 40-59. Esta sección le mostrará cómo crear una fórmula de clasificación para satisfacer esos requisitos comerciales.

## Crear una fórmula de clasificación y una expresión predeterminada

1. Si es necesario, expanda **Decisioning** en el carril izquierdo y haga clic en **Configuración de estrategia**. Aterriza en la página &quot;Reglas de toma de decisiones&quot; y ve la regla de decisión &quot;Planes de nivel superior&quot; que creó anteriormente y que utilizó como requisitos de elegibilidad para los elementos de oferta de teléfono de nivel superior.
2. Haga clic en **Fórmulas de clasificación** en el menú &#39;Métodos de clasificación&#39;. Se abrirá una página vacía, ya que aún no tiene ninguna fórmula de clasificación.

![Vaciar la página de fórmulas de clasificación antes de crear una fórmula](assets/create-ranking-formula-empty-ranking-formulas-page.png)

3. Haga clic en el botón azul **Crear fórmula** para comenzar a crear una nueva fórmula de clasificación
4. Asigne un nombre a la fórmula de clasificación **iPhone 17 Ranking Formula**

>[!NOTE]
>
>Cuando se envía un evento de experiencia a la recopilación de datos de Edge con los parámetros necesarios para solicitar una oferta de un paquete de Decisioning activo, todas las ofertas de ese paquete se evalúan mediante la fórmula de clasificación. Cada oferta mantendrá su prioridad original o la ajustará dinámicamente en función del perfil que activó el evento de experiencia.

5. Desplácese hasta la parte inferior de la sección &quot;Criterios&quot;, haga clic en el icono **\&lt;/>** del cuadro de texto inferior y seleccione la variable **Puntuación de prioridad de oferta**.

![Variable de puntuación de prioridad de oferta seleccionada en los criterios de fórmula de clasificación](assets/create-ranking-formula-select-offer-priority-score.png)

La expresión predeterminada ahora está configurada de esta manera:

![Expresión predeterminada establecida en la variable de puntuación de prioridad de oferta](assets/create-ranking-formula-default-expression-set.png)

>[!NOTE]
>
>Este cuadro de texto inferior es la expresión predeterminada aplicada a cualquier elemento de oferta que no cumpla ningún criterio de ajuste de prioridad. En este caso, simplemente es la prioridad asignada a la oferta cuando se creó. Si no se asigna ninguna puntuación de prioridad predeterminada a la colección en la que se ejecutará esta fórmula de clasificación, le interesa asignar una puntuación predeterminada

## Creación de reglas de ajuste de prioridad

Ahora que hay una expresión predeterminada, puede empezar a agregar reglas que ajusten dinámicamente la prioridad en función de la edad del usuario.

Una forma de pensar en las reglas de ajuste de prioridad es tratarlas como instrucciones estándar que solo se aplican a determinadas ofertas. Si la prueba resulta verdadera, ajuste la prioridad de las ofertas que cumplen un criterio determinado. La interfaz de usuario los organiza en un orden ligeramente diferente, como se indica en esta captura de pantalla.

![Orden de IU de las secciones if, then y where en una regla de ajuste de prioridad](assets/create-ranking-formula-if-then-where-rule-order.png "Orden de IU de if, then y where en una regla de ajuste de prioridad")

>[!NOTE]
>
>El valor &quot;if&quot; es opcional porque se puede aplicar una regla de ajuste de prioridad cuando una oferta cumple un criterio específico sin una declaración condicional primero. Si ampliamos el ejemplo de esta guía, imaginemos que tenemos varias ofertas con un atributo de sistema operativo del teléfono (Android frente a iOS). Se puede aumentar la prioridad de todas las ofertas de iPhone donde el sistema operativo preferido del perfil sea iOS. No hay un &quot;if&quot;. Solo &quot;ajustar la puntuación donde atributo de oferta = atributo de perfil&quot;. A continuación se muestra una imagen similar a la anterior que describe esta idea sin una declaración condicional.
>
>![Regla de ajuste de prioridad aplicada sin una instrucción if condicional](assets/create-ranking-formula-rule-without-conditional.png "Regla de ajuste de prioridad aplicada sin una instrucción if condicional")

## Crear criterio 1: regla de ajuste para menores de 39 años

1. Comience creando la regla de clasificación para el elemento de oferta de capa Ultra. Haga clic en el primer cuadro de texto de la sección **Criterio 1** y, a continuación, haga clic en el botón **Seleccionar atributo** cuando aparezca.

![Seleccionar opción de atributo mostrada para el criterio 1](assets/create-ranking-formula-criterion-one-select-attribute.png)

2. Cuando se abra el cuadro de diálogo &quot;Seleccionar un atributo&quot;, haga clic en **Nombre de oferta**. Una vez seleccionado, haga clic en **Guardar.**

>[!NOTE]
>
>El &quot;atributo Decisión&quot; hace referencia a elementos del elemento de oferta. Dado que aquí es donde se describe a qué artículos de oferta se aplican los criterios, las únicas opciones disponibles son los atributos del artículo de oferta.
>

3. Deje el operador establecido en &quot;Es igual que&quot; y, en el cuadro de texto restante, escriba el nombre del elemento de oferta de ultra nivel, que es **iphone:17\:ultra**. Después de escribir el texto, la interfaz de usuario se actualiza y refleja que se ha aceptado la condición coincidente.
4. Haga clic en **+Agregar condición** y, a continuación, haga clic en el **cuadro de texto nuevo que aparece** (tiene el texto &#39;*Haga clic para crear un elemento de decisión...*&#39; en él
5. Haga clic en la opción **Seleccionar atributo** ahora disponible**.**
6. Cuando se abra el cuadro de diálogo &quot;Seleccionar un atributo&quot;, haga clic en **Atributos de perfil > Persona** (probablemente necesite desplazarse hacia abajo) **> Año de nacimiento**. Una vez seleccionado, haga clic en **Guardar.**

>[!NOTE]
>
> &quot;Atributos de perfil&quot; hace referencia al usuario o perfil que envió el evento de experiencia y &quot;Datos de contexto&quot; hace referencia a elementos en el propio evento de experiencia, como la URL, el nombre de página u otros atributos de la carga útil del evento de experiencia.

7. Cambie el operador a **Greater than** e introduzca el año de nacimiento **1986** (la interfaz de usuario coloca una coma en el año, que se espera). Después de entrar, la interfaz de usuario se actualiza para reflejar que la condición se ha aceptado. Dado que el caso de uso comercial es ofrecer el nivel Ultra a cualquier persona menor de 40 años, la prioridad se ajusta para cualquier persona nacida después de 1986.

>[!NOTE]
>
>Como se mencionó anteriormente, la interfaz de usuario indica que estas condiciones adicionales son &quot;opcionales&quot;. Esto se debe a que es posible que se desee ajustar dinámicamente la prioridad de un conjunto de elementos de oferta sin ningún criterio adicional. Puede ser que los mismos elementos de oferta se puedan usar en una colección diferente y se clasifiquen con un conjunto diferente de reglas de clasificación. Dado que este laboratorio utiliza un único conjunto de elementos de oferta, se utilizan condiciones adicionales para ajustar la prioridad.

8. La prioridad original para el artículo de oferta de nivel Ultra es 4. Para aumentar la prioridad, multiplíquelo por 100. Para ello, haga clic en el icono **\&lt;/>** junto al último cuadro de texto y seleccione la variable **Puntuación de prioridad de oferta**. Agregue un **\*100** después del texto introducido automáticamente. Esta expresión multiplica la prioridad original (4) por 100 y le da una nueva prioridad de 400.

   La regla debería tener un aspecto similar al siguiente:

![Criterio 1 que aumenta la puntuación de prioridad de ofertas de nivel Ultra en 100](assets/create-ranking-formula-criterion-one-ultra-boost.png)

>[!NOTE]
>
>¿Por qué multiplicar por 100? La idea es que si quieres asegurarte de que tus prioridades se ajusten muy por encima de las otras prioridades, 100 es solo una manera de hacer matemáticas simples para que eso suceda. Las fórmulas de clasificación pueden ser complicadas, como verá en la siguiente sección, por lo que es útil tener una matemática simple.
>
>Además, aunque se utilizó la multiplicación para aumentar la puntuación de prioridad, se podrían haber utilizado otras expresiones matemáticas para disminuir la puntuación de prioridad. En términos generales, sin embargo, es más fácil hacer que las ofertas deseadas &quot;floten hasta la parte superior&quot; de lo que es hacer ofertas que no quieres &quot;hundirse hasta la parte inferior&quot;.



## Crear criterio 2: regla de ajuste para los 40-59

1. Justo debajo de la regla de ajuste que acaba de crear, haga clic en el botón **+ Agregar criterio**.
2. Cree una condición coincidente para donde el **nombre de la oferta** NO sea igual a **iphone:17\:ultra**.

>[!WARNING]
>
>Esta regla está pensada para aplicarse a todos los demás elementos de oferta. Más detalles sobre por qué están más adelante en esta página, pero debe tener cuidado con utilizar este tipo de lógica en la práctica, ya que se aplicaría a todas las ofertas de la colección que no tengan este valor. En nuestro caso, está bien, pero puede que no sea en otros casos de uso.

3. Agregue la condición de que esta regla se aplique a todas las personas cuyo año de nacimiento sea mayor que **1966** (todas las menores de 60 años).
4. Al igual que la regla anterior, multiplique la puntuación de prioridad predeterminada del elemento de oferta por 100. Cuando termine, la regla &quot;Criterio 2&quot; tendrá este aspecto:

![Regla de criterio 2 que ajusta la prioridad de los perfiles nacidos después de 1966](assets/create-ranking-formula-criterion-two-rule.png)

>[!NOTE]
>
>El uso conjunto de fórmulas de clasificación y reglas de idoneidad puede parecer complejo, pero esta es la idea central:
>
>- **Las fórmulas de clasificación** ajustan dinámicamente las puntuaciones de prioridad y, por lo tanto, el orden de las ofertas.
>- **Las reglas de aceptación** (como las reglas de decisión y los límites de frecuencia) eliminan ofertas de la lista ordenada si el usuario no tiene permiso para verlas.
>
>A continuación, se muestra cómo se ordenarían las ofertas dados estos ejemplos y la fórmula de clasificación que acaba de crear:
>
>**Año de nacimiento = 1990**
>
>- La prioridad ultra se convierte en **400**
>- Pro = **3**, Base = **2**, Genérico = **1**
>  Resultado: Ultra se muestra primero (hasta 3 veces), luego Pro, Base y finalmente Genérico.
>
>**Año de nacimiento = 1970**
>
>- La prioridad ultra permanece en **4**
>- Pro se convierte en **300**, Base = **200** y Genérico = **100**
>  Resultado: Pro se muestra primero (3 veces), luego Base y luego Genérico. Ultra se ordena en último lugar porque su prioridad (4) es menor que Generic (100).
>
>Cuando la idoneidad se aplica mediante reglas de decisión y un límite de frecuencia,
>
>- A los usuarios nacidos en 1990 con un **ID de plan = 1** se les eliminarán las ofertas Ultra y Pro, a pesar de que ocupen el puesto más alto. El usuario solo ve las ofertas básicas y genéricas porque los niveles Ultra y Pro tienen una condición adicional: solo los usuarios con **ID de plan 2 o 3** pueden verlas.
>- Dado que la oferta genérica no tiene reglas de límite de frecuencia, el usuario **1970** del año de nacimiento nunca verá la oferta Ultra, ya que su puntuación de prioridad es inferior a la puntuación aumentada del genérico.

5. Con todas las reglas y la puntuación de prioridad predeterminada en su lugar, desplácese hacia atrás hasta la parte superior y haga clic en el botón azul **Crear** en la esquina superior derecha.

>[!TIP]
>
>Ahora volverá a la página &quot;Configuración de estrategia&quot; y verá la fórmula de clasificación única que acaba de crear.

> [!NOTE]
>
>¿Qué sucede si dos ofertas resultan en la misma prioridad? Las ofertas con la misma puntuación de prioridad se eligen al azar para volver al sistema solicitante.

## Resumen

En esta página, se ha creado una fórmula de clasificación que determina cómo se ordenan dinámicamente los elementos de oferta para cada perfil. También ha definido una expresión predeterminada (la puntuación de prioridad original) y, a continuación, ha añadido reglas de ajuste de prioridad que aumentan las prioridades de oferta en función de criterios de perfil (como la edad). Esta lógica de clasificación garantiza que las ofertas relevantes (como los niveles Ultra o Pro para intervalos de edad específicos) suban a la cima cuando se evalúan.
