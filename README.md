# The-code-for-Airline
This problem is to solve a plane airline, I hope that all the steps work are posted in each repository. Python language, MySQL database

#"""""""""""""""""""THE CODE STARTS HERE"""""""""""""""""""""""""""#

import mysql.connector
import datetime
import threading
import time
from datetime import datetime, timedelta

mydb = mysql.connector.connect(
    host="localhost",
    user="root",
    passwd="Root",
    database="aeropuerto"
)

mycursor = mydb.cursor()


# Clase cliente

class Pais:
    def __init__(self, id_pais, nombre_pais, region_pais):
        self.id_pais = id_pais
        self.nombre_pais = nombre_pais
        self.region_pais = region_pais

    def get_id_pais(self):
        return self.id_pais

    def set_id_pais(self, id_pais):
        self.id_pais = id_pais

    def get_nombre_pais(self):
        return self.nombre_pais

    def set_nombre_pais(self, nombre_pais):
        self.nombre_pais = nombre_pais

    def get_region_pais(self):
        return self.region_pais

    def set_region_pais(self, region_pais):
        self.region_pais = region_pais


class Aeropuerto:
    def __init__(self, id_aeropuerto, nombre, id_pais):
        self.id_aeropuerto = id_aeropuerto
        self.nombre = nombre
        self.id_pais = id_pais

    def get_id_aeropuerto(self):
        return self.id_aeropuerto

    def set_id_aeropuerto(self, id_aeropuerto):
        self.id_aeropuerto = id_aeropuerto

    def get_nombre(self):
        return self.nombre

    def set_nombre(self, nombre):
        self.nombre = nombre

    def get_id_pais(self):
        return self.id_pais

    def set_id_pais(self, id_pais):
        self.id_pais = id_pais


class Cliente:
    def __init__(self, cedula, nombre, apellido, fecha_nac, direccion, telefono, correo, id_pais):
        self.cedula = cedula
        self.nombre = nombre
        self.apellido = apellido
        self.fecha_nac = fecha_nac
        self.direccion = direccion
        self.telefono = telefono
        self.correo = correo
        self.id_pais = id_pais

    def get_cedula(self):
        return self.cedula

    def set_cedula(self, cedula):
        self.cedula = cedula

    def get_nombre(self):
        return self.nombre

    def set_nombre(self, nombre):
        self.nombre = nombre

    def get_apellido(self):
        return self.apellido

    def set_apellido(self, apellido):
        self.apellido = apellido

    def get_fecha_nac(self):
        return self.fecha_nac

    def set_fecha_nac(self, fecha_nac):
        self.fecha_nac = fecha_nac

    def get_direccion(self):
        return self.direccion

    def set_direccion(self, direccion):
        self.direccion = direccion

    def get_telefono(self):
        return self.telefono

    def set_telefono(self, telefono):
        self.telefono = telefono

    def get_correo(self):
        return self.correo

    def set_correo(self, correo):
        self.correo = correo

    def get_id_pais(self):
        return self.id_pais

    def set_id_pais(self, id_pais):
        self.id_pais = id_pais


class Avion:
    def __init__(self, id_avion, numero_de_serie, nombre, tipo, marca, modelo, capacidad, horas_vuelo):
        self.id_avion = id_avion
        self.numero_de_serie = numero_de_serie
        self.nombre = nombre
        self.tipo = tipo
        self.marca = marca
        self.modelo = modelo
        self.capacidad = capacidad
        self.horas_vuelo = horas_vuelo

    def get_id_avion(self):
        return self.id_avion

    def set_id_avion(self, id_avion):
        self.id_avion = id_avion

    def get_numero_de_serie(self):
        return self.numero_de_serie

    def set_numero_de_serie(self, numero_de_serie):
        self.numero_de_serie = numero_de_serie

    def get_nombre(self):
        return self.nombre

    def set_nombre(self, nombre):
        self.nombre = nombre

    def get_tipo(self):
        return self.tipo

    def set_tipo(self, tipo):
        self.tipo = tipo

    def get_marca(self):
        return self.marca

    def set_marca(self, marca):
        self.marca = marca

    def get_modelo(self):
        return self.modelo

    def set_modelo(self, modelo):
        self.modelo = modelo

    def get_capacidad(self):
        return self.capacidad

    def set_capacidad(self, capacidad):
        self.capacidad = capacidad

    def get_horas_vuelo(self):
        return self.horas_vuelo

    def set_horas_vuelo(self, horas_vuelo):
        self.horas_vuelo = horas_vuelo


class Silla:
    def __init__(self, id_silla, estado, id_avion):
        self.id_silla = id_silla
        self.estado = estado
        self.id_avion = id_avion

    def get_id_silla(self):
        return self.id_silla

    def set_id_silla(self, id_silla):
        self.id_silla = id_silla

    def get_estado(self):
        return self.estado

    def set_estado(self, estado):
        self.estado = estado

    def get_id_avion(self):
        return self.id_avion

    def set_id_avion(self, id_avion):
        self.id_avion = id_avion


class Estado:
    def __init__(self, id_estado, estado):
        self.id_estado = id_estado
        self.estado = estado

    def get_id_estado(self):
        return self.id_estado

    def set_id_estado(self, id_estado):
        self.id_estado = id_estado

    def get_estado(self):
        return self.estado

    def set_estado(self, estado):
        self.estado = estado


class Vuelo:
    def __init__(self, id_vuelo, fecha, horaSalida, horaLlegada, numero_Pista, comentarios, id_avion,
                 id_aeropuerto_origen, id_aeropuerto_destino, id_estado):
        self.id_vuelo = id_vuelo
        self.fecha = fecha
        self.horaSalida = horaSalida
        self.horaLlegada = horaLlegada
        self.numero_Pista = numero_Pista
        self.comentarios = comentarios
        self.id_avion = id_avion
        self.id_aeropuerto_origen = id_aeropuerto_origen
        self.id_aeropuerto_destino = id_aeropuerto_destino
        self.id_estado = id_estado

    def get_id_vuelo(self):
        return self.id_vuelo

    def set_id_vuelo(self, id_vuelo):
        self.id_vuelo = id_vuelo

    def get_fecha(self):
        return self.fecha

    def set_fecha(self, fecha):
        self.fecha = fecha

    def get_horaSalida(self):
        return self.horaSalida

    def set_horaSalida(self, horaSalida):
        self.horaSalida = horaSalida

    def get_horaLlegada(self):
        return self.horaLlegada

    def set_horaLlegada(self, horaLlegada):
        self.horaLlegada = horaLlegada

    def get_numero_Pista(self):
        return self.numero_Pista

    def set_numero_Pista(self, numero_Pista):
        self.numero_Pista = numero_Pista

    def get_comentarios(self):
        return self.comentarios

    def set_comentarios(self, comentarios):
        self.comentarios = comentarios

    def get_id_avion(self):
        return self.id_avion

    def set_id_avion(self, id_avion):
        self.id_avion = id_avion

    def get_id_aeropuerto_origen(self):
        return self.id_aeropuerto_origen

    def set_id_aeropuerto_origen(self, id_aeropuerto_origen):
        self.id_aeropuerto_origen = id_aeropuerto_origen

    def get_id_aeropuerto_destino(self):
        return self.id_aeropuerto_destino

    def set_id_aeropuerto_destino(self, id_aeropuerto_destino):
        self.id_aeropuerto_destino = id_aeropuerto_destino

    def get_id_estado(self):
        return self.id_estado

    def set_id_estado(self, id_estado):
        self.id_estado = id_estado


class Horario_dia:
    def __init__(self, id_horariodia, dias_disponibles, id_vuelo):
        self.id_horariodia = id_horariodia
        self.dias_disponibles = dias_disponibles
        self.id_vuelo = id_vuelo

    def get_id_horariodia(self):
        return self.id_horariodia

    def set_id_horariodia(self, id_horariodia):
        self.id_horariodia = id_horariodia

    def get_dias_disponibles(self):
        return self.dias_disponibles

    def set_dias_disponibles(self, dias_disponibles):
        self.dias_disponibles = dias_disponibles

    def get_id_vuelo(self):
        return self.id_vuelo

    def set_id_vuelo(self, id_vuelo):
        self.id_vuelo = id_vuelo


class Horario_hora:
    def __init__(self, id_horariohora, hora_disponibles, id_dia):
        self.id_horariohora = id_horariohora
        self.hora_disponibles = hora_disponibles
        self.id_dia = id_dia

    def get_id_horariohora(self):
        return self.id_horariohora

    def set_id_horariohora(self, id_horariohora):
        self.id_horariohora = id_horariohora

    def get_hora_disponibles(self):
        return self.hora_disponibles

    def set_hora_disponibles(self, hora_disponibles):
        self.hora_disponibles = hora_disponibles

    def get_id_dia(self):
        return self.id_dia

    def set_id_dia(self, id_dia):
        self.id_dia = id_dia


class Tiquete:
    def __init__(self, id_tiquete, id_cliente, id_vuelo, tipo):
        self.id_tiquete = id_tiquete
        self.id_cliente = id_cliente
        self.id_vuelo = id_vuelo
        self.tipo = tipo

    def get_id_tiquete(self):
        return self.id_tiquete

    def set_id_tiquete(self, id_tiquete):
        self.id_tiquete = id_tiquete

    def get_id_cliente(self):
        return self.id_cliente

    def set_id_cliente(self, id_cliente):
        self.id_cliente = id_cliente

    def get_id_vuelo(self):
        return self.id_vuelo

    def set_id_vuelo(self, id_vuelo):
        self.id_vuelo = id_vuelo

    def get_tipo(self):
        return self.tipo

    def set_tipo(self, tipo):
        self.tipo = tipo


def registrar_cliente(self):
    sql = "INSERT INTO cliente (cedula, nombre, apellido, fecha_nac, direccion, telefono, correo, id_pais) " \
          "VALUES (%s, %s, %s, %s, %s, %s, %s, %s)"
    val = (
    self.cedula, self.nombre, self.apellido, self.fecha_nac, self.direccion, self.telefono, self.correo, self.id_pais)
    time.sleep(2)
    mycursor.execute(sql, val)
    mydb.commit()
    print(mycursor.rowcount, "record inserted.")
    print("Se ha registrado satisfactoriamente")


def registrar_avion(self):
    sql = "INSERT INTO avion (id_avion,numero_de_serie, nombre, tipo, marca, modelo, capacidad, horas_vuelo) VALUES (%s, %s, %s, %s, %s,%s,%s,%s)"
    val = (self.id_avion, self.numero_de_serie, self.nombre, self.tipo, self.marca, self.modelo, self.capacidad,
           self.horas_vuelo)
    time.sleep(1)
    mycursor.execute(sql, val)
    mydb.commit()
    mycursor.execute("select max(id_silla) from silla")
    myresult = mycursor.fetchall()
    cap = self.capacidad
    cap = int(cap)
    numerosilla = 1
    num = myresult[0][0] + 1
    for i in range(cap):
        sql2 = "INSERT INTO silla (id_silla, id_avion, estado, numero_silla) VALUES (%s, %s, %s, %s)"
        val2 = (num, self.id_avion, "Disponible", numerosilla)
        mycursor.execute(sql2, val2)
        mydb.commit()
        num += 1
        numerosilla += 1
    print(mycursor.rowcount, "record inserted.")
    print("Se ha registrado el avion satisfactoriamente")


# Metodos de validacion. Estos metodos verifican que los datos ingresados por el usuario cumplan con los requisitos de la base de datos


# Cliente

# Se valida que la cedula del cliente sea unica
def registrarPersona():
    cedula = input("Ingrese la cedula del cliente: ")
    existe = True
    while existe:
        mycursor.execute("SELECT * FROM cliente")
        myresult = mycursor.fetchall()
        for x in myresult:
            if x[0] == cedula:
                print("La cedula del cliente ya existe")
                cedula = input("Ingrese nuevamente la cedula del cliente: ")
            else:
                existe = False
    nombre = input("Ingrese el nombre del cliente: ")
    apellido = input("Ingrese el apellido del cliente: ")
    fecha = input("Ingrese la fecha de nacimiento del cliente: ")
    direccion = input("Ingrese la direccion del cliente: ")
    telefono = input("Ingrese el telefono del cliente: ")
    correo = input("Ingrese el correo del cliente: ")
    id_pais = input("Ingrese el id del pais del cliente: ")
    cliente = Cliente(cedula, nombre, apellido, fecha, direccion, telefono, correo, id_pais)

    registrar_cliente(cliente)


# Avion

def registrarAvion():
    # Se valida que el numero de serie de avion no exista
    id_avion = input("Ingrese el id del avion: ")
    existe = True
    while existe:
        mycursor.execute("SELECT id_avion FROM avion")
        myresult = mycursor.fetchall()
        for x in myresult:
            if x[0] == id_avion:
                print("El id_avion del avion ya existe")
                id_avion = input("Ingrese nuevamente el numero de serie del avion: ")
            else:
                existe = False
    numero_serie = input("Ingrese el numero de serie de avion: ")
    nombre = input("Ingrese el nombre de avion: ")
    tipo = input("Ingrese el tipo de avion: ")
    marca = input("Ingrese la marca del avion: ")
    modelo = input("Ingrese el modelo del avion: ")
    capacidad = input("Ingrese la capacidad del avion: ")
    horas = input("Ingrese la horas de vuelo del avion: ")
    avion = Avion(id_avion, numero_serie, nombre, tipo, marca, modelo, capacidad, horas)
    registrar_avion(avion)


# Vuelo


def registrar_vuelo(self):
    sql = "INSERT INTO vuelo values (%s,%s,%s,%s,%s,%s,%s,%s,%s,%s)"
    val = (
        self.id_vuelo, self.fecha, self.horaSalida, self.horaLlegada, self.numero_Pista, self.comentarios,
        self.id_avion, self.id_aeropuerto_origen, self.id_aeropuerto_destino, self.id_estado)
    time.sleep(2)
    mycursor.execute(sql, val)
    mydb.commit()
    print(mycursor.rowcount, "Vuelo creado exitosamente")


def validarNumeroVuelo(numero_de_vuelo):
    existe = True
    while existe:
        mycursor.execute("SELECT id_vuelo FROM vuelo")
        myresult = mycursor.fetchall()
        for x in myresult:
            if x[0] == numero_de_vuelo:
                print("El numero de vuelo ya existe")
                numero_de_vuelo = input("Ingrese nuevamente el numero de vuelo: ")
            else:
                existe = False
    return numero_de_vuelo


def validarNumeroAvion(numero_de_avion):
    existe = True
    while existe:
        mycursor.execute("SELECT * FROM avion")
        myresult = mycursor.fetchall()
        for x in myresult:
            if str(x[0]) == str(numero_de_avion):
                return numero_de_avion
            else:
                numero_de_avion = input("Ingrese nuevamente el numero de avion: ")
    return numero_de_avion


def registrarVuelo():
    # Se valida que el numero de vuelo no exista
    id_vuelo = input("Ingrese el numero de vuelo: ")
    numero_de_vuelo = validarNumeroVuelo(id_vuelo)
    # Se valida que el numero de avion exista
    fecha = input("Ingrese el fecha: ")
    # numero_de_avion = validarNumeroAvion(numero_de_avion)
    horaS = input("Ingrese la hora de salida: ")
    numero_p = input("Ingrese el numero de pista: ")
    comentarios = input("Ingrese los comentarios del vuelo: ")
    id_avion = input("Ingrese el id del avion: ")
    id_ao = input("Ingrese el id del aeropuerto de origen: ")
    id_ad = input("Ingrese el id del aeropuerto del destino: ")
    vuelo = Vuelo(id_vuelo, fecha, horaS, '00:00:00', numero_p, comentarios,
                  id_avion, id_ao, id_ad, 1)
    registrar_vuelo(vuelo)


# Ticket

def registrar_tiquete(self):
    # print("Se registrara el tiquete con la siguiente informacion:", self.numero_de_tiquete_id, self.cedula, self.numero_de_vuelo_id, self.numero_de_asiento)
    sql = "INSERT INTO tiquete (id_tiquete,id_cliente,id_vuelo,tipo) values (%s,%s,%s,%s);"
    val = (self.id_tiquete, self.id_cliente, self.id_vuelo, self.tipo)
    time.sleep(2)
    mycursor.execute(sql, val)
    mydb.commit()
    print(mycursor.rowcount, "Tiquete creado exitosamente")


def validarNumeroTiquete(numero_de_tiquete_id):
    existe = True
    while existe:
        mycursor.execute("SELECT * FROM tiquete")
        myresult = mycursor.fetchall()
        for x in myresult:
            if str(x[0]) == str(numero_de_tiquete_id):
                print("El numero de tiquete ya existe")
                numero_de_tiquete_id = input("Ingrese nuevamente el numero de tiquete: ")
            else:
                existe = False
    return numero_de_tiquete_id


def validarCedula(cedula):
    existe = True
    while existe:
        mycursor.execute("SELECT * FROM cliente")
        myresult = mycursor.fetchall()
        for x in myresult:
            if str(x[0]) == str(cedula):
                return cedula
        cedula = input("Ingrese nuevamente la cedula: ")
    return cedula


def mostrarAsientosOcupados(numero_de_vuelo_id):
    mycursor.execute(
        "SELECT s.id_silla FROM vuelo v join avion a on a.id_avion = v.id_avion join silla s on s.id_avion = a.id_avion WHERE v.id_vuelo  = " + numero_de_vuelo_id + " and  s.estado = 'Ocupado'")
    myresult = mycursor.fetchall()
    asientos = []
    for x in myresult:
        x[0]
        asientos.append(x[0])
    return asientos


def mostrarAsientosDisponibles(numero_de_vuelo_id):
    # select numero_silla from silla where id_avion = 1 and estado= 'Disponible'
    mycursor.execute(
        "select numero_silla from silla where id_avion =" + str(numero_de_vuelo_id) + " and estado= 'Disponible'")
    myresult = mycursor.fetchall()
    asientos = []
    for x in myresult:
        x[0]
        asientos.append(x[0])
    return asientos


def validar_asiento(numero_de_asiento, asientos, iD_avion):
    existe = True
    while existe:
        for x in asientos:
            if int(asientos[x]) == int(numero_de_asiento):
                # update silla set estado = 'Ocupado' where numero_silla = '8' and id_avion = '3'
                sql = "update silla set estado = 'Ocupado' where numero_silla =" + str(
                    numero_de_asiento) + " and id_avion = " + str(iD_avion)
                mycursor.execute(sql)
                mydb.commit()
                existe = False
                print("Asiento otorgado satisfactoriamente")
                break
        if existe:
            print("El numero de asiento ya esta ocupado")
            numero_de_asiento = input("Ingrese nuevamente el asiento: ")
    return numero_de_asiento


def cantidad_asientos_vuelo_actual(numero_de_vuelo_id):
    mycursor.execute(
        "select capacidad from avion a join vuelo v on a.id_avion = v.id_avion where v.id_vuelo = " + numero_de_vuelo_id)
    myresult = mycursor.fetchall()
    asientos = 0
    for x in myresult:
        asientos = x[0]
    return asientos


def validarEstadoVuelo(numero_de_vuelo_id):
    mycursor.execute(
        "SELECT e.estado FROM vuelo v join estado e on e.id_estado = v.id_estado WHERE v.id_vuelo = " + numero_de_vuelo_id)
    myresult = mycursor.fetchall()
    estado = ""
    for x in myresult:
        estado = x[0]
    return estado


def registrarTiquete():
    # Se valida que el numero de vuelo exista
    id_tiquete = input("Ingrese el numero de tiquete: ")
    numero_de_tiquete_id = validarNumeroTiquete(id_tiquete)
    # Se valida que la cedula exista
    id_cliente = input("Ingrese la cedula: ")
    cedula = validarCedula(id_cliente)
    # Se valida que el numero de vuelo exista
    id_vuelo = input("Ingrese el numero de vuelo: ")
    numero_de_vuelo_id = validarNumeroVuelo(id_vuelo)

    mycursor.execute("select id_avion from vuelo where id_vuelo =" + id_vuelo)
    myresult = mycursor.fetchall()
    print("El numero del avion es " + str(myresult[0][0]))
    numeroavion = int(myresult[0][0])

    salida_vuelo = validarEstadoVuelo(numero_de_vuelo_id)
    if (salida_vuelo != "Activo"):
        print("El vuelo no se encuentra disponible ya que no esta activo, no es posible registrar el tiquete")
        return
    # Se valida que el asiento no este ocupado
    print("Asientos Ocupados: ")
    asientos = mostrarAsientosOcupados(id_vuelo)
    cantidad_asientos = len(asientos)

    print(cantidad_asientos)

    asientos_vuelo = mostrarAsientosDisponibles(numeroavion)
    asientos_disponibles = int(len(asientos_vuelo))
    print("el numero de asientos es", asientos_disponibles)
    # select id_avion from vuelo where id_vuelo = 901

    var = int(myresult[0][0])
    print("Asientos disponibles: ", asientos_disponibles)
    if (asientos_disponibles) >= int(0):
        numero_de_asiento = input("Ingrese el numero de asiento: ")
        validar_asiento(numero_de_asiento, asientos_vuelo, var)
        tipo = input("Ingrese el tipo de tiquete: ")
        tiquete = Tiquete(id_tiquete, id_cliente, id_vuelo, tipo)
        registrar_tiquete(tiquete)
    else:
        print("No hay asientos disponibles")


###SALIDA VUELOS

def salidaVuelos():
    horaActual = datetime.now().time()
    horaActual = horaActual.strftime('%H:%M:%S')
    print(horaActual)
    mycursor.execute(
        "SELECT id_vuelo,id_estado FROM vuelo where id_estado = 1 or id_estado = 6 or id_estado =7 or id_estado = 8 and id_estado = 10")
    myresult = mycursor.fetchall()
    for x in myresult:
        print(x[0])
        if (len(myresult) != 0):
            mycursor.execute(
                "UPDATE vuelo SET id_estado = 11,horaSalida = NOW(), comentarios='El vuelo en vuelo' WHERE id_vuelo =" + str(
                    x[0]))
            mydb.commit()
            print(mycursor.rowcount, "record(s) affected")
            print("EL vuelo identificado " + str(x[0]) + " esta en vuelo y salio a las: ", horaActual)
        else:
            print("El no hay vuelos listos")
        print(mycursor.rowcount, "record(s) affected")


def cambioEstadoVuelo(numero_de_vuelo_id, comentrario):
    sql = "UPDATE vuelo SET id_estado = 3,comentarios = %s WHERE id_vuelo = %s"
    val = (comentrario, numero_de_vuelo_id)
    time.sleep(2)
    mycursor.execute(sql, val)
    mydb.commit()
    print(mycursor.rowcount, "record(s) affected")


def RetrasoArreglado(numero_de_vuelo_id):
    # Pedirle al usuario que ingrese el numero de vuelo
    estadoSiguiente = input("Digite el nuevo estado del vuelo: 1. En espera 2. En vuelo 3. Retraso")
    estadovuelo = "Retraso"
    if (estadoSiguiente == str(1)):
        estadovuelo = "En espera"
    if (estadoSiguiente == str(2)):
        estadovuelo = "En vuelo"
    comentrario = "Retraso arreglado"
    sql = "UPDATE vuelo SET estado = %s WHERE numero_de_vuelo = %s"
    val = (estadovuelo, numero_de_vuelo_id)
    time.sleep(2)
    mycursor.execute(sql, val)
    mydb.commit()
    print(mycursor.rowcount, "record(s) affected")
    # cambio comentario
    sqll = "UPDATE vuelo SET comentarios = %s WHERE numero_de_vuelo = %s"
    vall = (comentrario, numero_de_vuelo_id)
    time.sleep(2)
    mycursor.execute(sqll, vall)
    mydb.commit()


# Menu
def retrasoVuelo():
    numero_de_vuelo_id = input("Ingrese el numero de vuelo: ")
    existe = False
    while not existe:
        mycursor.execute("SELECT id_estado FROM vuelo where id_vuelo=" + numero_de_vuelo_id)

        myresult = mycursor.fetchall()
        if (len(myresult) != 0):
            existe = True
        for x in myresult:
            print(x[0])
            if (int(x[0]) != 1 and x[0] != 7 and x[0] != 8):
                print("No se le puede cambiar el estado al vuelo :", numero_de_vuelo_id)
                menu()
                break
        if existe == False:
            print("El numero de vuelo no existe")
            menu()
            break
        comentarios = input("Ingrese los comentarios del vuelo: ")
        cambioEstadoVuelo(numero_de_vuelo_id, comentarios)


def llegadaVuelo(id_vuelo):
    print("El id es : ", id_vuelo)
    horaActual = datetime.now().time()
    horaActual = horaActual.strftime('%H:%M:%S')
    print(horaActual)
    mycursor.execute("SELECT id_estado FROM vuelo where id_vuelo=" + id_vuelo)
    myresult = mycursor.fetchall()
    print(str(myresult[0][0]))
    if (len(myresult) != 0):
        if (myresult[0][0] == 11):
            time.sleep(2)
            mycursor.execute(
                "UPDATE vuelo SET id_estado = 5,horaLlegada = NOW(), comentarios='El vuelo finalizado' WHERE id_vuelo =" + id_vuelo)
            mydb.commit()
            print(mycursor.rowcount, "record(s) affected")
            print("EL vuelo ha finalizado a las: ", horaActual)
        else:
            print("El vuelo no esta en vuelo")
    else:
        print("El vuelo no existe")


def listarClientesVuelo():
    mycursor.execute(
        "SELECT c.cedula, concat(c.nombre,' ',c.apellido) as cliente, v.id_vuelo, v.fecha, v.horaSalida, v.horaLlegada, v.comentarios FROM vuelo v join tiquete t on t.id_vuelo = v.id_vuelo join cliente c on c.cedula = t.id_cliente")
    myresult = mycursor.fetchall()
    for x in myresult:
        print("cedula: ", x[0], ", cliente: ", x[1], ", id_vuelo: ", x[2], " ,fecha: ", x[3], ", hora salida: ", x[4],
              ", hora llegada: ", x[5], ", comentario de vuelo: ", x[6])


def listarAvionesListosPartir():
    mycursor.execute(
        "select a.id_avion, a.nombre, v.id_vuelo, v.fecha, e.estado , a.capacidad from vuelo v join estado e on e.id_estado = v.id_estado join avion a on a.id_avion = v.id_avion where e.id_estado = 1 or e.id_estado = 6 or e.id_estado =7 or e.id_estado = 8 and e.id_estado = 10")
    myresult = mycursor.fetchall()
    for x in myresult:
        print("id_avion: ", x[0], ", nombre avión: ", x[1], ", id_vuelo: ", x[2], " ,fecha: ", x[3], ", estado: ", x[4],
              " cantidad de sillas: ", x[5])


##Pendiente

def listarAvionesLlegaronDestino():
    sql = "select a.id_avion, a.nombre,v.id_vuelo, hour(timediff(v.horaLlegada, v.horaSalida)), e.estado from vuelo v join estado e on e.id_estado = v.id_estado join avion a on a.id_avion = v.id_avion where e.id_estado = 5;"
    mycursor.execute(sql)
    myresult = mycursor.fetchall()
    for x in myresult:
        print("id_avion: ", x[0], ", nombre avión: ", x[1], ", id_vuelo: ", x[2], " ,hora de vuelo: ", x[3],
              ", estado: ", x[4])


def listarAvionesRetrasados():
    mycursor.execute(
        "select a.id_avion, a.nombre, v.id_vuelo, v.fecha, e.estado, v.comentarios from vuelo v join estado e on e.id_estado = v.id_estado join avion a on a.id_avion = v.id_avion where e.id_estado = 3")
    myresult = mycursor.fetchall()
    for x in myresult:
        print("id_avion: ", x[0], ", nombre avión: ", x[1], ", id_vuelo: ", x[2], " ,fecha: ", x[3], ", estado: ", x[4],
              ", comentario de retraso: ", x[5])


def menuInformes():
    print("1. Listado de clientes por vuelo.")
    print(
        "2. Listado de aviones que se encuentran listos para partir asi como la cantidad de clientes que trasportan.(Se recomienda esperar 60s a que termine el hilo)")
    print("3. Listado de aviones que han llegado a su destino y el tiempo que tardaron en llegar.")
    print("4. Listado de aviones que se han retrasado y el motivo del retraso de su partida.")
    print("5. Volver a menu principal.")
    opcionMenu = int(input("Ingrese una opcion del menu: "))
    if opcionMenu == 5:
        menu()
    while opcionMenu < 5 and opcionMenu > 0:
        if opcionMenu == 1:
            listarClientesVuelo()
            menuInformes()
            break
        if opcionMenu == 2:
            listarAvionesListosPartir()
            menuInformes()
            break
        if opcionMenu == 3:
            listarAvionesLlegaronDestino()
            menuInformes()
            break
        if opcionMenu == 4:
            listarAvionesRetrasados()
            menuInformes()
            break


def modificarEstadoRetraso():
    id_vuelo = input("Ingrese el numero de vuelo: ")
    mycursor.execute("SELECT id_estado FROM vuelo where id_vuelo=" + id_vuelo)
    myresult = mycursor.fetchall()
    print(myresult[0][0])
    if (len(myresult) != 0):
        if (myresult[0][0] == 3):
            time.sleep(2)
            mycursor.execute(
                "UPDATE vuelo SET id_estado = 1, comentarios='Se reactivo el vuelo' WHERE id_vuelo =" + id_vuelo)
            mydb.commit()
            print(mycursor.rowcount, "record(s) affected")
            print("EL vuelo se ha reactivado")
        else:
            print("El vuelo no esta en retraso")
    else:
        print("El vuelo no existe")


def get_difference_in_seconds(time1, time2):
    # convertimos las dos horas a segundos
    t1_seconds = time1[3] * 3600 + time1[4] * 60 + time1[5]
    t2_seconds = time.localtime(time2)[3] * 3600 + time.localtime(time2)[4] * 60 + time.localtime(time2)[5]
    # restamos los dos valores
    diff = t1_seconds - t2_seconds
    return diff


def get_current_time():
    return time.localtime()


def thread_function():
    while True:
        # aqui se ejecutaran las acciones del hilo
        main()
        time.sleep(1)


start_time = time.time()


def main():
    # obtenemos la hora actual
    current_time = get_current_time()
    # obtenemos la hora en la que se ejecutó el programa

    # calculamos la diferencia entre las dos horas
    mycursor.execute("SELECT id_estado,id_vuelo FROM vuelo")
    myresult = mycursor.fetchall()
    for x in myresult:
        diff = get_difference_in_seconds(current_time, start_time)
        if (len(myresult) != 0):
            if (x[0] == 1 and diff > 2):
                mycursor.execute(
                    "UPDATE vuelo SET id_estado = 10, comentarios='El vuelo despego' WHERE id_vuelo =" + str(x[1]))
                mydb.commit()
            if (x[0] == 10 and diff > 4):
                mycursor.execute(
                    "UPDATE vuelo SET id_estado = 11, comentarios='El vuelo este en vuelo' WHERE id_vuelo =" + str(
                        x[1]))
                mydb.commit()
            if (x[0] == 11 and diff > 6):
                mycursor.execute(
                    "UPDATE vuelo SET id_estado = 9, comentarios='El vuelo esta aterrizando' WHERE id_vuelo =" + str(
                        x[1]))
                mydb.commit()
            if (x[0] == 9 and diff > 8):
                mycursor.execute(
                    "UPDATE vuelo SET id_estado = 5, comentarios='El vuelo ha finalizado' WHERE id_vuelo =" + str(x[1]))
                mydb.commit()
                time.sleep(100000)


if __name__ == "__main__":
    x = threading.Thread(target=thread_function)
    x.start()


########################################
def menu():
    print("MENU")
    print("1. Registrar Cliente")
    print("2. Registrar Avion")
    print("3. Registrar Vuelo")
    print("4. Registrar Tiquete")
    print("5. Registrar Retraso")
    print("6. Registrar Llegada")
    print("7. Modificar Estado de Retraso")
    print("8. Informes")
    print("9. Salida vuelos")
    print("10. Salir")


menu()

opcionMenu = int(input("Digite una opcion: "))

while opcionMenu != 10:
    if opcionMenu == 1:
        registrarPersona()
    elif opcionMenu == 2:
        registrarAvion()
    elif opcionMenu == 3:
        registrarVuelo()
    elif opcionMenu == 4:
        registrarTiquete()
    elif opcionMenu == 5:
        # Se valida que el numero de vuelo exista en la base de datos
        retrasoVuelo()
    elif opcionMenu == 6:
        id_vuelo = input("Digite el id del vuelo: ")
        llegadaVuelo(id_vuelo)
    elif opcionMenu == 7:
        modificarEstadoRetraso()
    elif opcionMenu == 8:
        menuInformes()
    elif opcionMenu == 9:
        print("Saliendo los vuelos")
        salidaVuelos()
    else:
        print("No existe esa opcion")
    menu()
    opcionMenu = int(input("Digite una opcion: "))

print("Ha salido del programa")
