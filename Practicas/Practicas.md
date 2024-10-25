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

#### ejercicio 1
```R-info

programa ejemplo
procesos
  proceso RandomFlorero(ES a:numero;ES c:numero)
  variables
    ave,calle,aveV,calleV:numero
  comenzar
    Random(ave,1,5)
    Random(calle,1,10)
    BloquearEsquina(ave,calle)
    Pos(ave,calle)
    mientras(HayFlorEnLaEsquina)
      tomarFlor
    aveV:=ave
    calleV:=calle
    repetir 4
      Random(ave,1,5)
      Random(calle,1,10)
      BloquearEsquina(ave,calle)
      Pos(ave,calle)
      mientras(HayFlorEnLaEsquina)
        tomarFlor
      LiberarEsquina(aveV,calleV)
      aveV:=ave
      calleV:=calle
    a:=ave
    c:=calle
  fin
  
  proceso RandomPapelero(ES a:numero;ES c:numero)
  variables
    ave,calle,aveV,calleV:numero
  comenzar
    Random(ave,6,10)
    Random(calle,1,9)
    BloquearEsquina(ave,calle)
    Pos(ave,calle)
    mientras(HayPapelEnLaEsquina)
      tomarPapel
    aveV:=ave
    calleV:=calle
    repetir 4
      Random(ave,6,10)
      Random(calle,1,9)
      BloquearEsquina(ave,calle)
      Pos(ave,calle)
      mientras(HayPapelEnLaEsquina)
        tomarPapel
      LiberarEsquina(aveV,calleV)
      aveV:=ave
      calleV:=calle
    a:=ave
    c:=calle
  fin
  
  
areas
  inicioFloreros: AreaPC(6,10,7,10)
  inicioPapeleros: AreaPC(8,10,9,10)
  areaFloreros: AreaPC (1,1,5,10)
  areaPapeleros: AreaPC (6,1,10,9)
  areaLider: AreaP(11,1,11,1)
  deposito:AreaC(10,10,10,10)
robots
  robot floreros
  variables
    ave,calle,quien:numero
  comenzar
    RecibirMensaje(quien,robot3)
    
    RandomFlorero(ave,calle)

    BloquearEsquina(10,10)
    Pos(10,10)
    LiberarEsquina(ave,calle)
   
    mientras(HayFlorEnLaBolsa)
      depositarFlor
    si(quien = 1)
      Pos(6,10)
    sino
      Pos(7,10)  
    LiberarEsquina(10,10)
  fin
  
  robot papeleros
  variables
    ave,calle,quien:numero
  comenzar
    RecibirMensaje(quien,robot3)
 
    RandomPapelero(ave,calle)
      
    BloquearEsquina(10,10)
    Pos(10,10)
    LiberarEsquina(ave,calle)
    
    mientras(HayPapelEnLaBolsa)
      depositarPapel
    si(quien = 4)
      Pos(8,10)
    sino
      Pos(9,10)  
    LiberarEsquina(10,10)
  fin
  
  robot lider
  comenzar
    EnviarMensaje(1,robot1)
    EnviarMensaje(2,robot2)
    EnviarMensaje(4,robot4)
    EnviarMensaje(5,robot5)
  fin
variables
  robot1: floreros
  robot2: floreros
  robot3: lider
  robot4: papeleros
  robot5: papeleros
comenzar
  AsignarArea(robot4,inicioPapeleros)
  AsignarArea(robot5,inicioPapeleros)
  
  AsignarArea(robot4,areaPapeleros)
  AsignarArea(robot5,areaPapeleros)
  
  AsignarArea(robot4,deposito)
  AsignarArea(robot5,deposito)
  
  AsignarArea(robot1,areaFloreros)
  AsignarArea(robot2,areaFloreros)
  
  AsignarArea(robot1,deposito)
  AsignarArea(robot2,deposito)
  
  AsignarArea(robot1,inicioFloreros)
  AsignarArea(robot2,inicioFloreros)
  
  AsignarArea(robot3,areaLider)
  
  
  Iniciar(robot3,11,1)
  Iniciar(robot1,6,10)
  Iniciar(robot2,7,10)
  Iniciar(robot4,8,10)
  Iniciar(robot5,9,10)
fin
```
#### ejercicio 3

```R-info

programa ejemplo
areas
  ciudad: AreaC (1,1,100,100)
robots
  robot Obrero
  variables
    Quien,Ave,Calle,Final:numero
    Hay,:boolean
  comenzar
    Hay:=V
    RecibirMensaje(Final,RobotL)
    si(Final=1)
      RecibirMensaje(Quien,RobotL)
      RecibirMensaje(Ave,RobotL)
      RecibirMensaje(Calle,RobotL)
      BloquearEsquina(Ave,Calle)
      Pos(Ave,Calle)
      si(HayFlorEnLaEsquina)
        tomarFlor
      si(~HayFlorEnLaEsquina)
        Hay:=F
      si(Quien=1)   
        Pos(2,1)
        LiberarEsquina(Ave,Calle)
        EnviarMensaje(Hay,RobotL)
      si(Quien=2)
        Pos(3,1)
        LiberarEsquina(Ave,Calle)
        EnviarMensaje(Hay,RobotL)
      si(Quien=3)
        Pos(4,1)
        LiberarEsquina(Ave,Calle)
        EnviarMensaje(Hay,RobotL)
      si(Quien=4)
        Pos(5,1)
        LiberarEsquina(Ave,Calle)
        EnviarMensaje(Hay,RobotL)
        
    sino
      EnviarMensaje(Hay,RobotL)
  fin
  
  robot Lider
  variables
    Hay:boolean
    r1,r2,r3,r4,Ave,Calle,A,Max,Rmax,Final:numero
  comenzar
    Max:=0
    r1:=0
    r2:=0
    r3:=0
    r4:=0
    Hay:=V
    Final:=1
    Random(Ave,2,10)
    Random(Calle,2,10)
    mientras(Hay)
      Random(A,1,4)
      si(A=1)
        EnviarMensaje(Final,Robot1)
        EnviarMensaje(1,Robot1)
        EnviarMensaje(Ave,Robot1)
        EnviarMensaje(Calle,Robot1)
        RecibirMensaje(Hay,Robot1)
        r1:=r1+1
      si(A=2)
        EnviarMensaje(Final,Robot2)    
        EnviarMensaje(2,Robot2)
        EnviarMensaje(Ave,Robot2)
        EnviarMensaje(Calle,Robot2)
        RecibirMensaje(Hay,Robot2)
        r2:=r2+1
      si(A=3)
        EnviarMensaje(Final,Robot3)
        EnviarMensaje(3,Robot3)
        EnviarMensaje(Ave,Robot3)
        EnviarMensaje(Calle,Robot3)
        RecibirMensaje(Hay,Robot3)      
        r3:=r3+1    
      sino
        EnviarMensaje(Final,Robot4)
        EnviarMensaje(4,Robot4)
        EnviarMensaje(Ave,Robot4)
        EnviarMensaje(Calle,Robot4)
        RecibirMensaje(Hay,Robot4)  
        r4:=r4+1
    si(r1>Max)
      Max:=r1
      Rmax:=1
    si(r2>Max)
      Max:=r2
      Rmax:=2
    si(r3>Max)
      Max:=r3   
      Rmax:=3
    si(r4>Max)
      Max:=r4   
      Rmax:=4
      
    Informar(Max)
    Informar(Rmax)
    
    {Finalizo}
    Final:=0
    

    EnviarMensaje(Final,Robot1)
    EnviarMensaje(Final,Robot2)
    EnviarMensaje(Final,Robot3)
    EnviarMensaje(Final,Robot4)

  fin
  
  
variables
  RobotL : Lider
  Robot1 : Obrero
  Robot2 : Obrero
  Robot3 : Obrero
  Robot4 : Obrero
comenzar

  AsignarArea(RobotL, ciudad)
  AsignarArea(Robot1, ciudad)
  AsignarArea(Robot2, ciudad)
  AsignarArea(Robot3, ciudad)
  AsignarArea(Robot4, ciudad)
  

  Iniciar(Robot1, 2,1)
  Iniciar(Robot2, 3,1)
  Iniciar(Robot3, 4,1)
  Iniciar(Robot4, 5,1)
  Iniciar(RobotL, 1,1)
fin
```
