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
    file = open('alumnos.txt', 'r+')
    lineas = [linea.split(',') for linea in file]
    ID=1
    for i in lineas:
        ID=int(i[4])+1
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
    file = open('alumnos.txt', 'r')
    for linea in file:
        if hola in linea:
            lista.append(linea)
    print(' '.join(lista))

    return



def editar(hola):
    with open('alumnos.txt', 'r') as file:
        lineas = [linea.split(',') for linea in file]
    for i in lineas:
        if int(i[4]) == int(hola):
            print(','.join(i))
            lista = i
            lista1=i
            break
    file.close()
    num = int(input('Si desdea cambiar el Nombre, precione 1, si desea cambiar el Apellido, precione 2, si desea cambiar la edad, presione 3, de lo contrario preciones 4 para cambiar de Telefono: '))
    ab = num - 1
    print(lista[ab])
    lista[ab] = input('Ingrese el nuevo valor: ')
    print(lista)
    for i in lineas:
        if i==lista1:
            i=lista
    file=open('alumnos.txt', 'w+')
    for i in lineas:
        file.write(','.join(i))
    file.close()
    return



def eliminar(ID_Registro):
    file=open('alumnos.txt', 'r')
    lineas = [linea.split(',') for linea in file]
    for j in lineas:
        if ID_Registro + '\n' in j:
            lineas.remove(j)
    file.close()
    file = open('alumnos.txt', 'w+')
    for i in lineas:
        file.write(','.join(i))
    file.close()



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


    with open('mensajes.txt', 'r+') as f:
        lineas = [linea.split(',') for linea in f]
    print('Emisor, receptor, Fecha, Hora, Mensaje')
    for i in lineas:
        lineas.sort(key=lambda linea:linea[3])
        for i in lineas:
            lineas.sort(key=lambda linea: linea[2])
    with open('alumnos.txt', 'r+') as f:
        lineas1 = [linea.split(',') for linea in f]
    for alumnos in lineas1:
        for mensajes in lineas:
            if mensajes[0] + '\n' in alumnos:
                mensajes[0]=alumnos[0]+' '+ alumnos[1]
    for mensajes1 in lineas:
        for alumnos1 in lineas1:
            if mensajes1[1]  + '\n' in alumnos1:
                mensajes1[1]=alumnos1[0]+' '+alumnos1[1]

    for i in lineas:
        print(', '.join(i))
    f.close()


    return

file= open('alumnos.txt','w')
file1= open('mensajes.txt','w')


opcion = 0
while not(opcion == 7):

    opcion = menu()

    if opcion == 1:
        print("Seleccionó la opción Crear")
        file1 = open('alumnos.txt', 'a+')
        file1.write(','.join(crear())+ '\n')
        file1.close()

    elif opcion == 2:
        print("Seleccionó la opción Buscar")
        valor_a_buscar = input("Ingrese el valor a buscar: ")
        buscar(file, valor_a_buscar)

    elif opcion == 3:
        print("Seleccionó la opción Editar")
        codigo_de_alumno = str(input("Ingrese el ID de registro de alumno a MODIFICAR: "))
        lista_de_alumnos = editar( codigo_de_alumno)

    elif opcion == 4:
        print("Seleccionó la opción Eliminar")
        codigo_de_alumno = input("Ingrese el ID de registro de alumno a ELIMINAR: ")
        lista_de_alumnos = eliminar(codigo_de_alumno)

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
file1.close()
