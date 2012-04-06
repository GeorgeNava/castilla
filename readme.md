# Castilla 1.0

## Lenguaje de programación en español

* * * * *

**Castilla** es un lenguaje de programación que trata de llenar un vacío
en el mundo de habla hispana donde los lenguajes son muy escasos y con
poca aceptación. La primera pregunta que encontraremos es: por qué un
lenguaje de programación en español? Y la respuesta simplemente es
porque nos da la gana. Con más de 300 millones de hispano parlantes en
el mundo creo que existe la posibilidad de llenar ese vacío.

Conjuntamente con Castilla, se desarrollará un compilador en inglés
llamado London y un traductor llamado Babel, para poder traducir los
programas de Español a Inglés y viceversa, sin pérdida de fidelidad.

Veamos a continuación la sintaxis del lenguaje:


### Mostrar información en cónsola

    di 'Hola'

    nombre = 'Camila'
    di 'Hola {nombre}, como estás?'             -- reemplazo de variables en contexto
    di 'Mi nombre es '+ nombre +' y el tuyo?'   -- concatenación
    di 'Hasta luego'


### Comentarios

    -- Comentarios al inicio de la linea
    di 'Hola'
    di 'Como estás?'   -- Comentarios al final de la linea

    ---- 
    Comentarios de lineas multiples
    Usar cuadruple guión al inicio y al final
    Buenos para encabezados de programa, clase o función
    ----
    di 'Hola'
    di 'Me encanta este lenguaje'
    di 'Es muy fácil de aprender!'

    ----------------------------------------------------------------------
    El comando 'di' agrega separador de lineas al final del texto
    a menos que se especifique continuación de linea con +
    ----------------------------------------------------------------------
    di 'Esto va '+
    di 'en la misma '+
    di 'linea'


### Definición y asignación de variables

    nombre = 'Carolina'             -- Texto
    altura = 178                    -- Entero
    peso   = 54.25                  -- Decimal
    fecha  = 20101231.235959F       -- Fecha: Año nuevo 2011
    color  = 0x0022CC               -- Hexadecimal

    di 'Hola {nombre}, nacistes el {fecha|dia dd/mm/yy}'
    di 'Tu altura es {altura|num 3} y tu peso es {peso|num 3.2} kgs'

    -- Conversiones de tipo
    edad  = 15.texto                     -- convierte entero a texto
    area  = '123.45'.entero              -- convierte texto a entero
    peso  = '123.4567'.real(2)           -- convierte texto a real con dos decimales
    largo = 123.45.texto                 -- convierte real a texto
    ancho = (456/123).texto              -- convierte resultado real a texto
    alto  = (456/123).entero.texto       -- convierte resultado real a entero y texto
    ayer  = '2012/12/31'.fecha           -- convierte texto a fecha
    hoy   = '2012/12/31 23:59:59'.fecha  -- convierte texto a fecha


### Listas y Diccionarios

    -- Las listas son agrupaciones de elementos simples
    lista = ['Lunes','Martes','Miércoles']
    di lista[1]                     -- Lunes
    di lista.último                 -- Miércoles, último elemento
    di lista.cuantos                -- 3
    lista.agregar('Jueves')
    lista.eliminar.primero
    lista.eliminar.último
    lista.eliminar.todos

    lista+['Viernes','Sábado']      -- agregar elementos al final de la lista
    lista-['Lunes']                 -- eliminar elemento de la lista 

    -- Los diccionarios son listas de elementos dobles
    -- donde el primer elemento es el indice y el segundo el contenido
    paises = ['españa':'madrid', 'italia':'roma', 'francia':'paris']
    paises.agregar('alemania':'berlin','inglaterra':'londres')
    paises+['portugal':'lisboa']    -- agregar al diccionario
    paises-['inglaterra']           -- eliminar elemento por indice

    -- Algunas funciones de lista:
    autos = ['toyota','mazda','fiat','seat','ford']
    autos.cuantos           -- 5
    autos.contiene('mazda') -- si
    autos.menor             -- fiat
    autos.mayor             -- toyota
    autos.primero           -- toyota
    autos.ultimo            -- ford
    -- asi como ordenar, sumar, promediar, agregar, eliminar, etc


### Objetos complejos

    Sexo := [Femenino:0, Masculino:1]  -- Enumeración constante

    persona = [
        nombre: 'Julieta'
        edad  : 18
        sexo  : Sexo.Femenino
        teléfonos : [
            casa    : '555-1234'
            oficina : '666-1234'
            móvil   : '777-1234'
        ]
        mascotas: ['chicle','gatico','caramelo']
    ]

    -- elementos separados por lineas son separados por comas por el compilador
    -- mucho mas fácil de agregar o reordenar elementos en una lista

    di persona.nombre
    di persona.telefonos.móvil
    di persona.mascotas.1
    di persona.mascotas[1]

    -- En castilla usamos corchetes [] para denotar listas y diccionarios, 
    -- pero pueden ser intercambiados por llaves para hacerlos mas parecidos a JSON


### Ciclos y repeticiones

    de 10:
        di 'Hola'

    de 1 a 10:
        di 'Hola'

    de 1 a 10 en n:
        di 'Número {n}'

    de 10 a 1 en n:
        di 'En reverso {n}'

    de 1 a 10 por 2 en n:
        di 'Número par: {n}'

    colores = ['amarillo','azul','rojo']
    de colores en color:
        di 'Color primario: {color}'

    paises = ['españa':'madrid','italia':'roma','francia':'paris']
    de paises en pais,capital:
        di 'La capital de {pais} es {capital}'

    -- diccionarios pueden accesar indice, valor y contador en ese orden
    paises = ['españa':'madrid','italia':'roma','francia':'paris']
    de paises en pais,capital,n:
        di 'Pais #{n} es {pais} y su capital es {capital}'


### Condiciones y Casos

    marca  = 'Ford'
    modelo = 'Pinto'
    precio = €1500
    año    = 1998

    es año>2000 y precio<€9000 o marca='Mercedes'?
    si:
        di 'Ese auto si es lindo'
    no:
        di 'Auto muy viejo o caro, no me gusta'

    -- podemos suprimir el 'si' despues de la condicion, depende de los gustos:
    es año>2000 y precio<€9000 o marca='Mercedes'?
        di 'Ese auto si es lindo'
    no:
        di 'Auto muy viejo o caro, no me gusta'

    -- Condición ternaria
    marca = es modelo='Corola' ? 'Toyota' no: 'Otro' 
    di marca        -- Otro

    -- Casos múltiples
    edad = 18

    caso edad<10:
        di 'Niño'
    caso edad<20:
        di 'Joven'
    caso edad<80:
        di 'Adulto'
    otro:
        di 'Anciano'


### Funciones

    saludar(nombre):
        di 'Hola {nombre}'

    saludar('Camila')   -- Hola Camila

    sumar(lista):
        total = 0
        de lista en num:
            total+num
        da total

    suma = sumar([1,2,3,4,5,6])
    di suma      -- 21


### Tipos y Clases

    -- Podemos definir el tipo de un objeto con anterioridad
    autos tipo lista[T]     -- T:texto E:entero R:Real F:fecha B:binario H:hex V:variado
    autos = ['toyota','mazda','fiat','seat','ford']

    -- Clases son definidas con atributos y verbos como metodos
    -- Preferiblemente en mayúsculas y denotando sujetos o cosas
    Auto:
        marca  := 'Toyota'      -- constante
        modelo := 'Corola'      -- constante
        color  :  'Rojo'        -- variable
        sucio- :   no           -- variable privada
        ruedas :   4
        prender:
            di 'run ruuun'
        manejar:
            mi.sucio = si
        lavar:
            mi.sucio = no
            di 'estoy limpio'
        pintar(color):
            mi.color = color

    auto = Auto.nuevo
    auto.prender.manejar        -- podemos concatenar métodos
    auto.lavar                  -- métodos sin argumentos no requieren paréntesis
    auto.pintar('azul')

    -- Extensibilidad
    Camión tipo Auto:
        capacidad := 5ton
        largo := 10mt
        lleno-: no
        cargar:
            mi.lleno = si
            di 'Camión lleno'
        vaciar:
            mi.lleno = no
            di 'Camión vacio'
        nuevo(ruedas):
            mis.ruedas = ruedas

    camión = Camión.nuevo(6)
    camión.cargar               -- Camión lleno
    camión.vaciar               -- Camión vacio


### Módulos y Librerías

    -- archivos de librerías internas y externas pueden ser incluidos
    usa matemáticas en global
    di seno(10) * coseno(20) + tangente(50)
    di hipotenusa(20,30)    -- 36.06

    usa sistema, cifrado y azar
    di sistema.nombre       -- linux
    di cifrado.MD5('mi clave secreta')
    di azar.entero(100)     -- 42     cualquier numero entre 0 y 100
    di azar.decimal(4)      -- 0.1234 cualquier numero entre 0 y 1 con N decimales


### Errores y Excepciones

    -- Hay dos formas de detectar problemas: con captura de errores o con bloques de excepciones

    -- Captura de errores
    saludar(nombre):
        di 'Hola ' + nombre.mayúscula   |  error 'Nombre debe ser texto'

    saludar(123)                        |  di error

    sumar(a,b):
        total = a+b                     | error 'montos deben ser numericos'
        da total

    num = sumar(123,'abc')              |  num = 0
    di num                              -- num es 0 debido al error

    -- Bloques de excepción
    sumar(a,b):
        da a+b

    hacer:
        c = sumar(1,2)
        d = sumar('a',4)
    error:
        di 'No se puede sumar texto'
    salir:
        c = 0
        d = 0


### Desarrollo Web

    usa web y modelos

    inicio(sol,pag):        -- métodos web reciben solicitud y respuesta como parámetros
        pag.mostrar('<h1>Hola web</h1>')

    verClientes(sol,pag):
        lista  = modelos.listaClientes   -- lista de clientes desde la base de datos
        pag.mostrar('{% de lista en cliente %}<li>{cliente}</li>{% fin %}')

    noExiste(sol,pag):
        pag.mostrar('<pre>404 - La página {sol.ruta} no existe</pre>')

    web.rutas = [
        '/'         : inicio 
        '/clientes' : verClientes 
        '*'         : noExiste
    ]

    web.servir()

Todavía hay algunos detalles y ambiguedades que resolver pero en general esta es la idea y sus conceptos principales.

Eso es todo. Esperamos que les haya gustado el lenguaje de programación **Castilla**.

Gracias por su atención