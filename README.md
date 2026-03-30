# UTN-TUPaDProgramacion1

#ejercicio 1:

while True:
    nombre = input("Cliente: ").strip()
    if nombre.isalpha():
        break
    print("Error: Ingrese solo letras")

while True:
    cantidad_str = input("Cantidad de productos: ")
    if cantidad_str.isdigit() and int(cantidad_str) > 0:
        cantidad = int(cantidad_str)
        break
    print("Error: Ingrese un número entero positivo")

total_sin_descuento = 0
total_con_descuento = 0

for i in range(1, cantidad + 1):
    while True:
        precio_str = input(f"Producto {i} - Precio: ")
        if precio_str.isdigit():
            precio = int(precio_str)
            break
        print("Error: Ingrese un numero entero valido")
    
    while True:
        descuento_respuesta = input(f"Descuento (S/N): ").strip().lower()
        if descuento_respuesta in ['s', 'n']:
            break
        print("Error: Ingrese S o N")
    
    if descuento_respuesta == 's':
        precio_final = precio * 0.9
    else:
        precio_final = precio
    
    total_sin_descuento += precio
    total_con_descuento += precio_final

ahorro = total_sin_descuento - total_con_descuento
promedio = total_con_descuento / cantidad

print(f"Total sin descuentos: ${total_sin_descuento}")
print(f"Total con descuentos: ${total_con_descuento:.2f}")
print(f"Ahorro: ${ahorro:.2f}")
print(f"Promedio por producto: ${promedio:.2f}")



#Ejercicio 2:

usuario_correcto = "alumno"
clave_correcta = "python123"
clave_actual = clave_correcta
intentos = 0
max_intentos = 3

while intentos < max_intentos:
    intentos += 1
    print(f"Intento {intentos}/{max_intentos} - Usuario: ", end="")
    usuario = input()
    print("Clave: ", end="")
    clave = input()
    
    if usuario == usuario_correcto and clave == clave_actual:
        print("Acceso concedido.\n")
        break
    else:
        print("Error: credenciales invalidas.\n")
else:
    print("Cuenta bloqueada.")
    exit()

while True:
    print("1) Estado  2) Cambiar clave  3) Mensaje  4) Salir")
    print("Opcion: ", end="")
    opcion = input()
    
    if not opcion.isdigit():
        print("Error: ingrese un numero valido.\n")
        continue
    
    opcion = int(opcion)
    
    if opcion < 1 or opcion > 4:
        print("Error: opción fuera de rango.\n")
        continue
    
    if opcion == 1:
        print("Inscripto\n")
    
    elif opcion == 2:
        print("Nueva clave: ", end="")
        nueva_clave = input()
        
        if len(nueva_clave) < 6:
            print("Error: mínimo 6 caracteres.\n")
        else:
            print("Confirmación: ", end="")
            confirmacion = input()
            
            if nueva_clave == confirmacion:
                clave_actual = nueva_clave
                print("Clave actualizada.\n")
            else:
                print("Error: las claves no coinciden.\n")
    
    elif opcion == 3:
        print("Sigue adelante, estas en el camino correcto\n")
    
    elif opcion == 4:
        print("Hasta luego.")
        break



#Ejercicio 3:

def validar_nombre(mensaje):
    while True:
        nombre = input(mensaje).strip()
        if nombre.isalpha():
            return nombre
        print("Error: Solo se permiten letras.")

def validar_opcion(mensaje, minimo, maximo):
    while True:
        opcion = input(mensaje).strip()
        if opcion.isdigit() and minimo <= int(opcion) <= maximo:
            return int(opcion)
        print(f"Error: Ingrese un numero entre {minimo} y {maximo}.")

lunes1, lunes2, lunes3, lunes4 = "", "", "", ""
martes1, martes2, martes3 = "", "", ""

nombre_operador = validar_nombre("Ingrese nombre del operador: ")

while True:
    print(f"\n SISTEMA DE AGENDA (Operador: {nombre_operador}) ")
    print("1. Reservar turno")
    print("2. Cancelar turno")
    print("3. Ver agenda del dia")
    print("4. Ver resumen general")
    print("5. Cerrar sistema")
    
    opcion = validar_opcion("Seleccione opción: ", 1, 5)
    
    if opcion == 1:
        dia = validar_opcion("¿Que dia? (1=Lunes, 2=Martes): ", 1, 2)
        nombre_paciente = validar_nombre("Nombre del paciente: ")
        
        if dia == 1:
            if nombre_paciente in (lunes1, lunes2, lunes3, lunes4):
                print("Error: Paciente ya tiene turno el lunes.")
            else:
                if lunes1 == "":
                    lunes1 = nombre_paciente
                    print(f"Turno reservado: {nombre_paciente} - Lunes, Turno 1")
                elif lunes2 == "":
                    lunes2 = nombre_paciente
                    print(f"Turno reservado: {nombre_paciente} - Lunes, Turno 2")
                elif lunes3 == "":
                    lunes3 = nombre_paciente
                    print(f"Turno reservado: {nombre_paciente} - Lunes, Turno 3")
                elif lunes4 == "":
                    lunes4 = nombre_paciente
                    print(f"Turno reservado: {nombre_paciente} - Lunes, Turno 4")
                else:
                    print("Error: No hay turnos disponibles el lunes.")
        else:
            if nombre_paciente in (martes1, martes2, martes3):
                print("Error: Paciente ya tiene turno el martes.")
            else:
                if martes1 == "":
                    martes1 = nombre_paciente
                    print(f"Turno reservado: {nombre_paciente} - Martes, Turno 1")
                elif martes2 == "":
                    martes2 = nombre_paciente
                    print(f"Turno reservado: {nombre_paciente} - Martes, Turno 2")
                elif martes3 == "":
                    martes3 = nombre_paciente
                    print(f"Turno reservado: {nombre_paciente} - Martes, Turno 3")
                else:
                    print("Error: No hay turnos disponibles el martes.")
    
    elif opcion == 2:  
        dia = validar_opcion("¿Que dia? (1=Lunes, 2=Martes): ", 1, 2)
        nombre_paciente = validar_nombre("Nombre del paciente a cancelar: ")
        
        if dia == 1:
            if lunes1 == nombre_paciente:
                lunes1 = ""
                print(f"Turno cancelado: {nombre_paciente} - Lunes, Turno 1")
            elif lunes2 == nombre_paciente:
                lunes2 = ""
                print(f"Turno cancelado: {nombre_paciente} - Lunes, Turno 2")
            elif lunes3 == nombre_paciente:
                lunes3 = ""
                print(f"Turno cancelado: {nombre_paciente} - Lunes, Turno 3")
            elif lunes4 == nombre_paciente:
                lunes4 = ""
                print(f"Turno cancelado: {nombre_paciente} - Lunes, Turno 4")
            else:
                print("Error: Paciente no encontrado el lunes.")
        else:
            if martes1 == nombre_paciente:
                martes1 = ""
                print(f"Turno cancelado: {nombre_paciente} - Martes, Turno 1")
            elif martes2 == nombre_paciente:
                martes2 = ""
                print(f"Turno cancelado: {nombre_paciente} - Martes, Turno 2")
            elif martes3 == nombre_paciente:
                martes3 = ""
                print(f"Turno cancelado: {nombre_paciente} - Martes, Turno 3")
            else:
                print("Error: Paciente no encontrado el martes.")
    
    elif opcion == 3:
        dia = validar_opcion("¿Que dia? (1=Lunes, 2=Martes): ", 1, 2)
        if dia == 1:
            print("\n--- AGENDA LUNES ---")
            print(f"Turno 1: {lunes1 if lunes1 else '(libre)'}")
            print(f"Turno 2: {lunes2 if lunes2 else '(libre)'}")
            print(f"Turno 3: {lunes3 if lunes3 else '(libre)'}")
            print(f"Turno 4: {lunes4 if lunes4 else '(libre)'}")
        else:
            print("\n--- AGENDA MARTES ---")
            print(f"Turno 1: {martes1 if martes1 else '(libre)'}")
            print(f"Turno 2: {martes2 if martes2 else '(libre)'}")
            print(f"Turno 3: {martes3 if martes3 else '(libre)'}")
    
    elif opcion == 4: 
        ocupados_lunes = (1 if lunes1 else 0) + (1 if lunes2 else 0) + (1 if lunes3 else 0) + (1 if lunes4 else 0)
        ocupados_martes = (1 if martes1 else 0) + (1 if martes2 else 0) + (1 if martes3 else 0)
        disponibles_lunes = 4 - ocupados_lunes
        disponibles_martes = 3 - ocupados_martes
        
        print("\n--- RESUMEN GENERAL ---")
        print(f"Lunes: {ocupados_lunes} ocupados, {disponibles_lunes} disponibles")
        print(f"Martes: {ocupados_martes} ocupados, {disponibles_martes} disponibles")
        
        if ocupados_lunes > ocupados_martes:
            print("Dia con mas turnos: Lunes")
        elif ocupados_martes > ocupados_lunes:
            print("Dia con mas turnos: Martes")
        else:
            print("Dias con igual cantidad de turnos: Lunes y Martes")
    
    elif opcion == 5: 
        print("\nSistema cerrado.")
        break



#Ejercicio 4:

energia = 100
tiempo = 12
cerraduras_abiertas = 0
alarma = False
codigo_parcial = ""
forzar_consecutivas = 0

while True:
    nombre = input("Ingresa tu nombre de agente: ")
    if nombre.isalpha():
        break
    print("Error: El nombre debe contener solo letras.")

print(f"\nBienvenido, agente {nombre} Tienes 3 cerraduras para abrir.")
print("=" * 50)

while energia > 0 and tiempo > 0 and cerraduras_abiertas < 3:
    if alarma and tiempo <= 3:
        print("\nSistema bloqueado. La alarma se activo y el tiempo se agoto.")
        print("DERROTA - Bloqueo del sistema")
        break
    
    print(f"\n--- ESTADO ---")
    print(f"Energia: {energia} | Tiempo: {tiempo} min | Cerraduras: {cerraduras_abiertas}/3")
    print(f"Alarma: {'ACTIVA' if alarma else 'Desactiva'}")
    if codigo_parcial:
        print(f"Código: {codigo_parcial}")
    
    print("\n--- MENU ---")
    print("1. Forzar cerradura (-20 energia, -2 tiempo)")
    print("2. Hackear panel (-10 energia, -3 tiempo)")
    print("3. Descansar (+15 energia, -1 tiempo)")
    
    while True:
        opcion = input("Elige opcion (1-3): ")
        if opcion.isdigit() and opcion in ["1", "2", "3"]:
            opcion = int(opcion)
            break
        print("Error: Debes ingresar 1, 2 o 3.")
    
    if opcion == 1:
        energia -= 20
        tiempo -= 2
        forzar_consecutivas += 1
        
        if energia < 40:
            print("\n riesgo de alarma - Tu energia es baja")
            while True:
                numero = input("Elige un numero (1-3) para continuar: ")
                if numero.isdigit() and numero in ["1", "2", "3"]:
                    numero = int(numero)
                    break
                print("Error: Debes ingresar 1, 2 o 3.")
            
            if numero == 3:
                alarma = True
                print("La alarma se activo")
        
        if forzar_consecutivas >= 3:
            alarma = True
            print("La cerradura se trabo, se activo la alarma")
            forzar_consecutivas = 0
        elif not alarma:
            cerraduras_abiertas += 1
            print(f"Cerradura abierta. Total: {cerraduras_abiertas}/3")
            forzar_consecutivas = 0
    
    elif opcion == 2:
        energia -= 10
        tiempo -= 3
        forzar_consecutivas = 0
        
        print("\nHackeando panel...")
        for paso in range(1, 5):
            codigo_parcial += chr(65 + paso - 1)  # A, B, C, D
            print(f"Paso {paso}/4: {codigo_parcial}")
        
        if len(codigo_parcial) >= 8 and cerraduras_abiertas < 3:
            cerraduras_abiertas += 1
            print(f"Panel hackeado, cerradura abierta. Total: {cerraduras_abiertas}/3")
            codigo_parcial = ""
    
    elif opcion == 3:
        tiempo -= 1
        forzar_consecutivas = 0
        
        if alarma:
            energia -= 10
            print("La alarma consume energia extra (-10 adicional)")
        
        energia = min(energia + 15, 100)
        print(f"Descansaste. Energia recuperada: {energia}")

print("\n" + "=" * 50)
if cerraduras_abiertas == 3:
    print(f"¡Victoria! Agente {nombre}, abriste la boveda.")
elif energia <= 0:
    print("DERROTA - Se acabo la energia.")
elif tiempo <= 0:
    print("DERROTA - Se acabo el tiempo.")
else:
    print("DERROTA - Sistema bloqueado por alarma.")

print("=" * 50)



#Ejercicio 5:

print("--- BIENVENIDO A LA ARENA ---")
nombre_valido = False
while not nombre_valido:
    nombre_gladiador = input("Nombre del Gladiador: ")
    if nombre_gladiador.isalpha():
        nombre_valido = True
    else:
        print("Error: Solo se permiten letras.")

vida_gladiador = 100
vida_enemigo = 100
pociones = 3
daño_pesado = 15
daño_enemigo = 12
turno_gladiador = True

print("\n=== INICIO DEL COMBATE ===")
juego_activo = True

while juego_activo and vida_gladiador > 0 and vida_enemigo > 0:
    print(f"{nombre_gladiador} (HP: {vida_gladiador}) vs Enemigo (HP: {vida_enemigo}) | Pociones: {pociones}")
    
    opcion_valida = False
    while not opcion_valida:
        print("Elige accion:")
        print("1. Ataque Pesado")
        print("2. Rafaga Veloz")
        print("3. Curar")
        opcion = input("Opcion: ")
        
        if opcion.isdigit() and opcion in ["1", "2", "3"]:
            opcion_valida = True
        else:
            print("Error: Ingrese un numero valido.")
    
    if opcion == "1":
        if vida_enemigo < 20:
            daño_final = daño_pesado * 1.5
            print(f"¡Golpe Critico! ¡Atacaste al enemigo por {daño_final} puntos de daño!")
        else:
            daño_final = daño_pesado
            print(f"¡Atacaste al enemigo por {daño_final} puntos de daño!")
        vida_enemigo -= daño_final
    
    elif opcion == "2":
        print(">> ¡Iniciaste una rafaga de golpes!")
        for i in range(3):
            print("> Golpe conectado por 5 de daño")
            vida_enemigo -= 5
    
    elif opcion == "3": 
        if pociones > 0:
            vida_gladiador += 30
            pociones -= 1
            print(f"Usaste una pocion +30 HP. Pociones restantes: {pociones}")
        else:
            print("No quedan pociones")
    
    if vida_enemigo <= 0:
        juego_activo = False
        break
    
    print(f">> El enemigo te ataco por {daño_enemigo} puntos de daño")
    vida_gladiador -= daño_enemigo
    
    if vida_gladiador <= 0:
        juego_activo = False
        break
    
    print(f"\n=== NUEVO TURNO ===")

if vida_gladiador > 0:
    print(f"\n¡VICTORIA! {nombre_gladiador} ganaste la batalla.")
else:
    print("\nDERROTA. Caiste en combate.")