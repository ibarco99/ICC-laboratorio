import time


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



def crear():
    ID=0
    with open('alumnos.rtf') as f:
        for line in f:
            words = line.split()
            ID += 1
    lista1 = []
    alumno = []
    datos = ["Nombre: ", "Apellido Paterno: ", "Edad: ", "Teléfono: "]
    for i in datos:
        x = str(input(i))
        alumno.append(x)
    alumno.append(str(ID))
    lista1.append(alumno)
    print('El ID del alumno es ', ID)
    return alumno


def buscar(file, hola):
    lista=[]
    file = open('alumnos.rtf', 'r')
    for linea in file:
        if hola in linea:
            lista.append(linea)

    print(' '.join(lista))

    return



def editar(file, hola):
    with open('alumnos.rft', 'r+') as f:
        lineas = [linea.split('') for linea in f]
        print(lineas)
    for linea in lineas:
        if linea[4] == hola:
            print(linea)
            lista = linea
            break
    num = int(input('Si desdea cambiar el Nombre, precione 1, si desea cambiar el Apellido, precione 2, si desea cambiar la edad, presione tres, de lo contrario preciones 4 para cambiar de Telefono: '))
    ab = num - 1
    print(lista[ab])
    lista[ab] = input('Ingrese el nuevo valor')
    print(lista)
    for i in lineas:
        if i== linea:
            linea=lista
    file.close()
    file=open('alumnos.rtf', 'w')
    file.write(' '.join(lista) + '\n')

    return



def eliminar(lista, ID_Registro):
    with open('alumnos.rtf', 'r+') as f:
        lineas = [linea.split() for linea in f]
        for linea in lineas:
            if ID_Registro in linea:
                del linea

    return



def mensaje():

    lista=[]
    emisor = input("Ingrese el ID de registro del EMISOR: ")
    receptor =input("Ingrese el ID de registro del RECEPTOR: ")
    mensaje = input("Ingrese el mensaje: ")
    lista.append(emisor)
    lista.append(receptor)
    lista.append(time.strftime("%d/%m/%y"))
    lista.append(time.strftime('%H:%M:%S'))
    lista.append(mensaje)
    print(lista)
    return lista



def ver_historial():

    #Agregar un algoritmo para mostrar el historial de los mensajes en orden cronológico con la siguient estructura:
    # Nombres y apellido del emisor |  Nombres y apellido del receptor  |  Fecha y hora del mensaje  |  Contenido del Mensaje
    # El historial debe mostrarse ordenado por Emisor , Receptor y Fecha y hora del mensaje

    with open('mensajes.txt', 'r') as f:
        lineas = [linea.split(',') for linea in f]
    print('Emisor, receptor, Fecha, Hora')
    for i in lineas:
        lineas.sort(key=lambda linea:linea[3])
        for i in lineas:
            lineas.sort(key=lambda linea: linea[2])
    with open('alumnos.rtf', 'r') as f:
        lineas1 = [linea.split() for linea in f]
    for mensajes in lineas:
        for alumnos in lineas1:
            if mensajes[0]==alumnos[4]:
                mensajes[0]=alumnos[0]+' '+ alumnos[1]
    for mensajes in lineas:
        for alumnos in lineas1:
            if mensajes[1]==alumnos[4]:
                mensajes[1]=alumnos[0]+' '+alumnos[1]

    for i in lineas:
        del i[4]
        print(', '.join(i))
    f.close()



    return

file= open('alumnos.rtf','r')


opcion = 0
while not(opcion == 7):

    opcion = menu()

    if opcion == 1:
        print("Seleccionó la opción Crear")
        file1 = open('alumnos.rtf', 'a+')
        file1.write(' '.join(crear())+ '\n')
        file1.close()

    elif opcion == 2:
        print("Seleccionó la opción Buscar")
        valor_a_buscar = input("Ingrese el valor a buscar: ")
        buscar(file, valor_a_buscar)

    elif opcion == 3:
        print("Seleccionó la opción Editar")
        codigo_de_alumno = input("Ingrese el ID de registro de alumno a MODIFICAR: ")
        lista_de_alumnos = editar(file, codigo_de_alumno)

    elif opcion == 4:
        print("Seleccionó la opción Eliminar")
        codigo_de_alumno = int(input("Ingrese el ID de registro de alumnoa ELIMINAR: "))
        lista_de_alumnos = eliminar(file, codigo_de_alumno)

    elif opcion == 5:
        print("Seleccionó la opción Mensaje")
        file1 = open('mensajes.txt', 'a+')
        file1.write(','.join(mensaje()) + '\n')
        file1.close()

    elif opcion == 6:
        print("Seleccionó la opción Ver Historial")
        ver_historial()

    elif opcion == 7:
        print("Finalizó el programa")
file.close()
