# ICC-laboratorio
import datetime as dt
hours = [(i, dt.time(i).strftime('%I %p')) for i in range(24)]
def menu():

    print("=============================")
    print("==     1. Crear            ==")
    print("==     2. Buscar           ==")
    print("==     3. Editar           ==")
    print("==     4. Eliminar         ==")
    print("==     5. Mensaje          ==")
    print("==     6. Ver historial    ==")
    print("==     7. Salir            ==")
    print("=============================")
    print("Seleccione una opción del 1 al 7: ")
    opcion=int(input())

    return opcion



def crear(lista):
    lista1 = []
    alumno = []
    datos = ["Nombre: ", "Apellido Paterno: ", "Edad: ", "Teléfono: "]
    for i in datos:
        x = input(i)
        alumno.append(x)
    ID = len(lista) + 1
    alumno.append(ID)
    lista1.append(alumno)

    return alumno


def buscar(lista_donde_se_buscara_el_valor, valor_a_buscar):
    lista = []
    for i in lista_donde_se_buscara_el_valor:
        for k in i:
            if k == valor_a_buscar:
                lista.append(i)
    print(lista)

    return



def editar(lista, ID_Registro):

    for i in lista:
        if i[4] == ID_Registro:
            num=int(input('Si desdea cambiar el Nombre, precione 1, si desea cambiar el Apellido, precione 2, si desea cambiar la edad, presione tres, de lo contrario preciones 4 para cambiar de Telefono: '))
            if num==1:
                nom=input('Cual es el nuevo  numbre que desea poner?')
                i[0]=nom
            elif num == 2:
                ape=input('Cual es el apellido que desea cambiar?')
                i[1]=ape
            elif num == 3:
                edad=input('Cual es a la edad que desea remplazar?')
                i[2]=edad
            elif num==4:
                tele=input('Cual es el telefono que desea cambiar?')
                i[3]=tele
    print(i)
    return



def eliminar(lista, ID_Registro):

    for i in lista:
        if i[4]==ID_Registro:
            del i

    return lista



def mensaje(emisor, receptor, mensaje):

    lista=[]
    lista.append(emisor)
    lista.append(receptor)
    lista.append(dt)
    lista.append(mensaje)
    for i in lista_de_alumnos:
        if i[4]==emisor:
            lista[0]=i[0]+i[1]
    for i in lista_de_alumnos:
        if i[4]==receptor:
            lista[1]=i[0]+i[1]
    print(lista)
    return lista



def ver_historial(lista_de_mensaje):

    #Agregar un algoritmo para mostrar el historial de los mensajes en orden cronológico con la siguient estructura:
    # Nombres y apellido del emisor |  Nombres y apellido del receptor  |  Fecha y hora del mensaje  |  Contenido del Mensaje
    # El historial debe mostrarse ordenado por Emisor , Receptor y Fecha y hora del mensaje

    print("Funcionalidad de ver historial")


    return



lista_de_alumnos = []
lista_de_mensajes = []

opcion = 0
while not(opcion == 7):

    opcion = menu()

    if opcion == 1:
        print("Seleccionó la opción Crear")
        lista_de_alumnos.append(crear(lista_de_alumnos))

    elif opcion == 2:
        print("Seleccionó la opción Buscar")
        valor_a_buscar = input("Ingrese el valor a buscar: ")
        buscar(lista_de_alumnos, valor_a_buscar)

    elif opcion == 3:
        print("Seleccionó la opción Editar")
        codigo_de_alumno = int(input("Ingrese el ID de registro de alumno a MODIFICAR: "))
        lista_de_alumnos = editar(lista_de_alumnos, codigo_de_alumno)

    elif opcion == 4:
        print("Seleccionó la opción Eliminar")
        codigo_de_alumno = int(input("Ingrese el ID de registro de alumnoa ELIMINAR: "))
        lista_de_alumnos = eliminar(lista_de_alumnos, codigo_de_alumno)

    elif opcion == 5:
        print("Seleccionó la opción Mensaje")
        ID_registro_EMISOR   = int(input("Ingrese el ID de registro del EMISOR: "))
        ID_registro_RECEPTOR = int(input("Ingrese el ID de registro del RECEPTOR: "))
        contenido_del_mensaje = input("Ingrese el mensaje: ")
        lista_de_mensajes = mensaje(ID_registro_EMISOR, ID_registro_RECEPTOR, contenido_del_mensaje)

    elif opcion == 6:
        print("Seleccionó la opción Ver Historial")
        ver_historial(lista_de_mensajes)

    elif opcion == 7:
        print("Finalizó el programa")
