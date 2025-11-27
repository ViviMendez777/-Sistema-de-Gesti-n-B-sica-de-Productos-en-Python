# -Sistema-de-Gestion-Basica-de-Productos-en-Python
Este proyecto consiste en el desarrollo de un programa en Python que permite gestionar un inventario básico de productos. El objetivo es demostrar el uso de listas, bucles, condicionales y validaciones de entrada para construir un sistema interactivo y funcional.  El programa está diseñado para ser simple, claro y fácil de usar.
# 🛒 Sistema de Gestión Básica de Productos

## 📌 Descripción
Este proyecto es un programa en **Python** que permite gestionar un inventario básico de productos.  
Su objetivo es demostrar el uso de listas, bucles, condicionales y validaciones de entrada para construir un sistema interactivo y funcional.  

El sistema está diseñado para ser simple, claro y fácil de usar, funcionando a través de un menú principal que ofrece distintas opciones de gestión.

---

## ⚙️ Funcionalidades
- **Agregar producto**: registra nombre, categoría y precio (entero).  
- **Mostrar productos**: lista todos los productos ingresados, numerados y ordenados.  
- **Buscar producto**: permite buscar por nombre y muestra coincidencias.  
- **Eliminar producto**: elimina un producto indicando su posición en la lista.  
- **Salir**: finaliza la ejecución del programa.  

---

## 🧰 Requisitos técnicos
- Uso de **listas** para almacenar y gestionar los datos.  
- Implementación de **bucles `while` y `for`**.  
- Validación de entradas para evitar datos vacíos o incorrectos.  
- Uso de **condicionales** para gestionar el menú y las validaciones.  

---

## 🖥️ Menú principal

# Lista inicial de productos (diccionarios)

productos = [
        {"Nombre" : "Notebook", "Precio" : 2200, "Categoria" : "Computadora" , "Cantidad": 150
        }
        ,
        {"Nombre" : "Microfono", "Precio" : 80, "Categoria" : "Audio", "Cantidad": 80
        }
        ,
        {"Nombre" : "Monitor", "Precio" : 800, "Categoria" : "Monitores", "Cantidad": 75
        }
        ,
        {"Nombre" : "Mouse", "Precio" : 30, "Categoria" : "Accesorio", "Cantidad": 80
        },
        {"Nombre" : "Impresora", "Precio" : 400, "Categoria" : "Oficina", "Cantidad": 85
        }
]
# Permite al usuario ingresar un nuevo producto y añadirlo a la lista
def agregar_producto():
    print("\nAlta de producto:\n")
    
    #Pedimos todo como texto (string) para que NO falle el input 

    nombre = input("Ingrese el Nombre del producto: ").strip()
    precio = input("Ingrese el Precio del producto: ").strip()
    categoria = input("Ingrese la Categoría del producto: ").strip()
    cantidad = input("Ingrese la cantidad del producto: ").strip() # Pedir como texto

    #Validamos campos vacíos
    #Importante: Ahora se valida que 'precio_texto' y 'cantidad_texto' NO estén vacíos.

    if nombre == "" or precio == "" or categoria == "" or cantidad == "":
        print("¡Error! Ningún campo puede estar vacío.")
        return # Salimos de la función

    #Validar que nombre y categoría no sean números
    #isdigit verifica si es un número
    if nombre.isdigit() or categoria.isdigit():   
        print("❌ El nombre y la categoría no pueden ser números.")
        return

    try:
    # Validar que precio y cantidad sean números enteros
        precio = int(precio)
        cantidad = int(cantidad)

    #Creamos un nuevo diccionario con los datos validados
        nuevo_producto = {
            "Nombre": nombre,
            "Precio": precio,
            "Categoria": categoria,
            "Cantidad": cantidad
        }
        productos.append(nuevo_producto)    #Agregar el producto a la lista existente
        print("✅ Producto agregado correctamente.")

    except ValueError:
        print("❌ El precio y la cantidad deben ser números enteros válidos.")  #Manejo de error si no son enteros


def listado_productos():
    """Muestra todos los productos en el inventario con su ID (índice + 1)."""
    print("\n--- Listado de productos ---\n")
    # enumerate() se usa para obtener el índice (i) y el producto (diccionario)
    # simultáneamente El índice 'i' actúa como el ID del producto.
    for i, producto in enumerate(productos): 
        # Acceso a los datos mediante claves de diccionario (Clase 8).
        print(f"ID: {i + 1}. Producto: {producto['Nombre']} - Precio: ${producto['Precio']} - Categoría: {producto['Categoria']} - Cantidad: {producto['Cantidad']}")


#Permite sumar o restar unidades de un producto
def Actualizar_Stock():
    print("\n--- Actualizar Stock de productos ---\n")
    listado_productos()  

    indice = int(input("Ingrese el número del producto que desea actualizar: "))
    producto = productos[indice - 1]   # Seleccionamos el producto por índice

    print(f"\nSeleccionado: {producto['Nombre']} (Stock actual: {producto['Cantidad']})")

    #Actualizamos según la opción elegida

    print("\nOpciones de actualización:")
    print("1. Sumar stock (agregar unidades)")
    print("2. Restar stock (quitar unidades)")

    opcion = input("Seleccione opción (1 o 2): ")
    cantidad = int(input("Ingrese la cantidad: "))

    if opcion == "1":
        producto["Cantidad"] += cantidad

    elif opcion == "2":
        producto["Cantidad"] -= cantidad

    print(f"✅ Stock de {producto['Nombre']} actualizado a {producto['Cantidad']} unidades.")


#Busca un producto por nombre (ignora mayúsculas/minúsculas)
def buscar_producto():
    print("\n--- Búsqueda de producto ---")
    
    producto_buscado = input("Ingrese el nombre del producto que desea buscar: ").strip()
    
    #Validación de campo vacío (ANTES del bucle)
    if not producto_buscado: # Usamos 'not producto_buscado'
        print("El nombre no puede estar vacío.")
        return # Salimos de la función si está vacío
    
    encontrado = False # Inicializamos la variable bandera

    #Iteramos correctamente sobre la lista global 'productos'
    for producto in productos: 
        #Corregimos el nombre de la variable y la clave (usamos "Nombre" original)
        if producto_buscado.lower() == producto["Nombre"].lower():
            print("\n✅ Producto encontrado:")
            print(f"- {producto['Nombre']} - ${producto['Precio']} - Categoría: {producto['Categoria']}")
            encontrado = True
            break # Es eficiente salir del bucle si ya encontramos el producto
            
    #Mensaje si no se encontró
    if not encontrado:
        print("\n❌ Producto no encontrado.")



# Elimina un producto de la lista según su número
def eliminar_producto():
        print("Baja de producto\n")

        listado_productos()  

        while True:
            indice = input("Ingrese el número del producto que desea eliminar: ")  # Bucle para asegurar una entrada válida.

            if not indice.isdigit():  # Validación si la entrada es un número 
                print("Debe ingresar un número válido.")
                continue

            indice = int(indice)

            if indice >= 1 and indice <= len(productos):     #Validación de rango: Chequea si el ID está dentro de los límites de la lista
                productos.pop(indice - 1)
                print("El producto ha sido eliminado.")
            else:
                print("Producto no encontrado.")
            break

#Genera un reporte de productos con stock igual o inferior a un límite especificado
def reporte_bajo_stock():
    print("\nReporte Bajo Stock\n")
    
    try:
        minimo_stock = int(input("Ingrese la cantidad de stock mínimo esperada: "))
    except ValueError:
        print("❌ Error: Debe ingresar un número entero para el stock mínimo.")
        return
    
    hay_minimo = False    # Bandera para controlar si se encontraron productos.
    print("-" * 35)
    print(f"PRODUCTOS CON STOCK MENOR O IGUAL A {minimo_stock}")
    print("-" * 35)

    for i, producto in enumerate(productos):
        
        if producto['Cantidad'] <= minimo_stock:
            
            print(f"ID: {i}. Nombre: {producto['Nombre']} | Stock: {producto['Cantidad']} unidades")
            hay_minimo = True
            
    if hay_minimo == False:
        print("No hay productos con bajo stock")
    
    print("-" * 35)


def menu_principal():
    print("\nSistema de Gestión Básica De Productos\n")

    print("1. Agregar producto")
    print("2. Mostrar productos")
    print("3. Actualizar stock")
    print("4. Buscar producto")
    print("5. Eliminar producto")
    print("6. Reporte de bajo stock")
    print("7. Salir\n")



opcion = "" # Inicialización de la variable opcion

while opcion != "7": 

    print("\nBienvenid@ a Tecno Mundo!\n")
    print("1. Agregar producto")
    print("2. Mostrar productos")
    print("3. Actualizar stock")
    print("4. Buscar producto")
    print("5. Eliminar producto")
    print("6. Reporte de bajo stock")
    print("7. Salir\n")

    opcion = input("\nSeleccione una opción: ")

    if opcion == "1":
        agregar_producto()

    elif opcion == "2":
        listado_productos()

    elif opcion == "3":
         Actualizar_Stock()
    
    elif opcion == "4":
        buscar_producto()

    elif opcion == "5":
        eliminar_producto()

    elif opcion == "6":
        reporte_bajo_stock()

    elif opcion == "7":
        print("\nSaliendo del programa...")
    else:
        print("\nOpción inválida")

menu_principal()

opcion = int(input("Ingrese la opción deseada: "))

print("Gracias por usar la aplicación")

