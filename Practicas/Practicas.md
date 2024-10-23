# Practica 1

#### ejercicio 2
* *code*:
* no existe riesgo de colision ya que no comparten caminos
* es la misma area para todos pero diferente posicion de inicio , aunque se deberia usar 
un area privada para cada uno pero no lo hice 
* *nota* : lo correcto seria asignar el area de cada robot , osea por asi decir su linea pero en este caso no lo hice.
```R-info

programa ejemplo

procesos
  proceso recorrer(
  E vueltas: numero;)
  variables
    papeles:numero
  comenzar
    papeles:=0
    
    repetir vueltas
      derecha
      
    repetir 20
      si (HayPapelEnLaEsquina)
        tomarPapel
        papeles := papeles+1
      mover
      si (HayPapelEnLaEsquina)
        tomarPapel
        papeles := papeles+1
        
    Informar(papeles)
  fin
  
areas
  ciudad: AreaC (10,10,30,30)
  
robots
  robot tipo1
  variables
    f:numero
  comenzar
    f:=0
    recorrer(0)
  fin
  
  robot tipo2
  variables
    f:numero
  comenzar
    f:=0
    recorrer(1)
  fin
  
  robot tipo3
  variables
	f:numero
  comenzar
    f:=0
    recorrer(2)
  fin
  
  robot tipo4
  variables
    f:numero
  comenzar
    f:=0
    recorrer(3)
  fin
  
variables
  robot1: tipo1
  robot2: tipo2
  robot3: tipo3
  robot4: tipo4
comenzar
  AsignarArea(robot1, ciudad)
  AsignarArea(robot2, ciudad)
  AsignarArea(robot3, ciudad)
  AsignarArea(robot4, ciudad)
  Iniciar(robot1, 10,10)
  Iniciar(robot2, 10,30)
  Iniciar(robot3, 30,30)
  Iniciar(robot4, 30,10)
fin
```

#### ejercicio 3
* se podria hacer con cada area para cada escalera pero es muy dificil por lo que en este caso esta permitido usar un compartida.
* *code*:
```R-info

programa ejemplo

procesos
  proceso recorrer(
  ES contador:numero;
  )
  comenzar
    repetir contador
      mover
    derecha
    repetir contador
      mover
    repetir 3
      derecha
    contador:=contador+1
  fin
  
areas
  ciudad: AreaC (1,1,100,100)
  
robots

  robot tipo1
  variables 
    contador:numero
  comenzar
    Pos(12,14)
    contador:=1
    mientras(contador < 5)
      recorrer(contador)
  fin
  robot tipo2
  variables 
    contador:numero
  comenzar
    Pos(17,10)
    contador:=1
    mientras(contador < 5)
      recorrer(contador)
  fin
  robot tipo3
  variables 
    contador:numero
  comenzar
    Pos(22,6)
    contador:=1
    mientras(contador < 5)
      recorrer(contador)
  fin
  
variables
  robot1 : tipo1
  robot2 : tipo2
  robot3 : tipo3
comenzar
  AsignarArea(robot1,ciudad)
  AsignarArea(robot2,ciudad)
  AsignarArea(robot3,ciudad)
  Iniciar(robot1,1,1)
  Iniciar(robot2,3,1)
  Iniciar(robot3,2,1)
fin
```

#### Ejercicio 4


* *code*:
```R-info
programa ejemplo

procesos
  proceso cuadrado
  comenzar
    repetir 99
      mover
    derecha
    mover
    derecha
    repetir 99
      mover
    repetir 3
      derecha
    mover
    repetir 3
      derecha
    
  fin
  proceso recorrer
  comenzar
    repetir 12
      cuadrado
    repetir 99
      mover
  fin
  
areas
  ciudad1: AreaP (1,1,25,100)
  ciudad2: AreaP (26,1,50,100)
  ciudad3: AreaP (51,1,75,100)
  ciudad4: AreaP (76,1,100,100)
  
robots

  robot tipo1
  variables 
    contador:numero
  comenzar
    Pos(1,1)
    recorrer
  fin
  
  robot tipo2
  variables 
    contador:numero
  comenzar
    Pos(26,1)
    recorrer
  fin
  
  robot tipo3
  variables 
    contador:numero
  comenzar
    Pos(51,1)
    recorrer
  fin
  
  robot tipo4
  variables 
    contador:numero
  comenzar
    Pos(76,1)
    recorrer
  fin

variables
  robot1 : tipo1
  robot2 : tipo2
  robot3 : tipo3
  robot4 : tipo4
comenzar
  AsignarArea(robot1,ciudad1)
  AsignarArea(robot2,ciudad2)
  AsignarArea(robot3,ciudad3)
  AsignarArea(robot4,ciudad4)
  Iniciar(robot1,1,1)
  Iniciar(robot2,26,1)
  Iniciar(robot3,51,1)
  Iniciar(robot4,76,1)
  
fin
```

# Practica 2
* *nota*: me aparece el robot 1 no esta en la ciudad intente usar un area compartida entre todos pero me dice el mismo error , quizas un error de comunicacion o algo asi
#### Ejercicio 1 B
```R-info


programa ejemplo
procesos
  proceso recorrerAvenida(ES cant: numero)
  comenzar
    si(HayFlorEnLaEsquina)
      tomarFlor
      cant:=cant+1
    repetir 9
      mover
      si(HayFlorEnLaEsquina)
        cant:=cant+1
        tomarFlor
  fin
areas
  ciudad3: AreaP(2,1,2,1)
  ciudad1: AreaP (1,1,1,10)
  ciudad2: AreaP (2,11,2,20)
robots

  robot RobotObrero
  variables
    quien,cant:numero
  comenzar
    cant:=0
    RecibirMensaje(quien,Robot3)
    recorrerAvenida(cant)
    EnviarMensaje(quien,Robot3)
    EnviarMensaje(cant,Robot3)
  fin
  
  robot RobotLider
  variables
    max,menor,quien,uno,dos:numero
  comenzar
    EnviarMensaje(1,Robot1)
    EnviarMensaje(2,Robot2)
    repetir 2
      RecibirMensaje(quien,*)
      si(quien = 1)
        RecibirMensaje(uno,Robot1)
      sino
        RecibirMensaje(dos,Robot2)
     
    si(uno>dos)
      menor:=dos
      dos:=max
      max:=uno
      quien:=1
    sino
      menor:=uno
      uno:=max
      max:=dos
      quien:=2
        
    
        
    Informar(max-menor)
    Informar(quien)
  fin
  
  
variables
  Robot1: RobotObrero
  Robot2: RobotObrero
  Robot3: RobotLider
comenzar
  


  AsignarArea(Robot1,ciudad1)
  AsignarArea(Robot2,ciudad2)
  AsignarArea(Robot3,ciudad3)
  
  Iniciar(Robot1, 1,1)
  Iniciar(Robot2, 2,11)
  Iniciar(Robot3, 2,1)
 
  
fin
```

