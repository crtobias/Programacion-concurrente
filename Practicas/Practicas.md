* *nota:* practicas que faltan porque me parecen repetitivas y son muy similares a otras que hice :
* practica 1  el ejercicio 1 y 5
* practica 2 el ejercicio 3
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
* *nota:* el 1 c y d es lo mismo pero copiar y pegar robots

* el E , se puede hacer sin robot fiscalizador pero seria mucho quilombo ya que nesecitarias
muchos tipos de robots y comunicarlos entre si para ver quien fue el ganador y seria mucho
lio

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
#### ejercicio 2
Random (var,1,5) usar esto al pasar los parametros de la escalera m yo le puse 3 pero se cambia por eso y listo para que sea random entre 1 y 5

```R-info


programa ejemplo
procesos
  proceso recorrerEscalera(ES Esc: numero;ES Cant:numero)
  variables
    escF,escP:numero
  comenzar
    escF:=0
    escP:=0
    repetir Esc
      mover
      si(HayFlorEnLaEsquina)
        escF:=escF+1
      si(HayPapelEnLaEsquina)
        escP:=escP+1
    derecha
    mover
    si(HayFlorEnLaEsquina)
      escF:=escF+1
    si(HayPapelEnLaEsquina)
      escP:=escP+1
    repetir 3
      derecha
    si(escF>escP)
      Cant:=Cant+1
    
  fin
areas
  ciudad : AreaC(1,1,100,100)
robots
  robot RobotObrero
  variables
    Quien,Esc,Cant:numero
  comenzar
    RecibirMensaje(Quien,RobotL)
    RecibirMensaje(Esc,RobotL)
    repetir 4
      recorrerEscalera(Esc,Cant)
    EnviarMensaje(Cant,RobotL)
  fin
  
  robot RobotLider
  variables
    Rcant,Cant:numero
  comenzar
    Cant:=0
    EnviarMensaje(1,Robot1)
    EnviarMensaje(3,Robot1)
    EnviarMensaje(2,Robot2)
    EnviarMensaje(3,Robot2)
    EnviarMensaje(3,Robot3)
    EnviarMensaje(3,Robot3)
    repetir 3  
      RecibirMensaje(Rcant,*)
      Cant:=Cant+Rcant
    Informar(Cant)
  fin
  
variables
  Robot1: RobotObrero
  Robot2: RobotObrero
  Robot3: RobotObrero
  RobotL: RobotLider
comenzar
  
  AsignarArea(Robot1,ciudad)
  AsignarArea(Robot2,ciudad)
  AsignarArea(Robot3,ciudad)
  AsignarArea(RobotL,ciudad) 
  
  Iniciar(Robot1,2,1)
  Iniciar(Robot2,7,1)
  Iniciar(Robot3,12,1)
  Iniciar(RobotL,1,1)
fin
```
# practica 3

#### ejercicio 3

```R-info

programa ejemplo
procesos
  proceso AsignarId
  variables
    HayF:numero
  comenzar
    HayF:=3
    EnviarMensaje(1,Robot1)
    EnviarMensaje(2,Robot2)
    EnviarMensaje(3,Robot3)
    EnviarMensaje(4,Robot4)
  fin
  proceso volver(E id:numero)
  comenzar
    si(id=1)
      Pos(2,1)
    si(id=2)
      Pos(3,1)
    si(id=3)    
      Pos(4,1)
    si(id=4)
      Pos(5,1)
  fin
areas
  ciudad: AreaC (1,1,100,100)
robots

  robot Obrero
  variables
    id,HayF,Ave,Calle,Cant:numero
  comenzar
    Cant:=0
    RecibirMensaje(id,RobotL)
    RecibirMensaje(HayF,RobotL)
    
    mientras(HayF=1)
      RecibirMensaje(Ave,RobotL)
      RecibirMensaje(Calle,RobotL)
      BloquearEsquina(Ave,Calle)
      Pos(Ave,Calle)
      si(HayFlorEnLaEsquina)
        Cant:=Cant+1
        tomarFlor
      si(HayFlorEnLaEsquina)
        HayF:=1
      sino
        HayF:=0     
      EnviarMensaje(HayF,RobotL)  
      volver(id)
      LiberarEsquina(Ave,Calle)
      RecibirMensaje(HayF,RobotL)
    
    EnviarMensaje(Cant,RobotL)
  fin
    
  robot Lider
  variables
    HayF,max,maxr,Ave,Calle,r,r1,r2,r3,r4:numero
  comenzar
    max:=0
    HayF:=1
    AsignarId
    Random(Ave,2,10)
    Random(Calle,2,10)
    mientras(HayF=1) 
      Random(r,1,4)
      si(r=1)
        EnviarMensaje(HayF,Robot1)    
        EnviarMensaje(Ave,Robot1)    
        EnviarMensaje(Calle,Robot1)    
        RecibirMensaje(HayF,Robot1)

      si(r=2)   
        EnviarMensaje(HayF,Robot2)    
        EnviarMensaje(Ave,Robot2)    
        EnviarMensaje(Calle,Robot2)    
        RecibirMensaje(HayF,Robot2)  

      si(r=3)
        EnviarMensaje(HayF,Robot3)    
        EnviarMensaje(Ave,Robot3)    
        EnviarMensaje(Calle,Robot3)    
        RecibirMensaje(HayF,Robot3)

      si(r=4)  
        EnviarMensaje(HayF,Robot4)    
        EnviarMensaje(Ave,Robot4)    
        EnviarMensaje(Calle,Robot4)    
        RecibirMensaje(HayF,Robot4)

        
    HayF:=0
    EnviarMensaje(HayF,Robot1)
    RecibirMensaje(r1,Robot1)
    EnviarMensaje(HayF,Robot2)
    RecibirMensaje(r2,Robot2)
    EnviarMensaje(HayF,Robot3)
    RecibirMensaje(r3,Robot3)
    EnviarMensaje(HayF,Robot4)
    RecibirMensaje(r4,Robot4)
 

    si(r1>max)
      max:=r1
      maxr:=1
    si(r2>max)
      max:=r2
      maxr:=2
    si(r3>max)
      max:=r3
      maxr:=3
    si(r4>max)
      max:=r4
      maxr:=4
      
    Informar(max)
    Informar(maxr)
  fin
  
  
variables
  RobotL: Lider
  Robot1: Obrero
  Robot2: Obrero
  Robot3: Obrero
  Robot4: Obrero
comenzar
  AsignarArea(RobotL, ciudad)
  AsignarArea(Robot1, ciudad)
  AsignarArea(Robot2, ciudad)
  AsignarArea(Robot3, ciudad)
  AsignarArea(Robot4, ciudad)
  
  Iniciar(RobotL, 1,1)
  Iniciar(Robot1, 2,1)
  Iniciar(Robot2, 3,1)
  Iniciar(Robot3, 4,1)
  Iniciar(Robot4, 5,1)
fin
```
