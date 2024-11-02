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
* *nota:* me olvide de que agarren los papeles y las flores pero es lo de menos porque el recorrido esta bien
```r-info
programa ejemplo
procesos

  proceso FlorerosRecorrido(E quien:numero)
  variables
    ave,calle,memoa,memoc,contador:numero
  comenzar 
    contador:=0
    Random(ave,1,5)  
    Random(calle,1,10)  
    memoa:=ave
    memoc:=calle
    BloquearEsquina(ave,calle)
    Pos(ave,calle)
    
    mientras(contador<4)    
      Random(ave,1,5)  
      Random(calle,1,10)  
      si(ave<>memoa | calle<>memoc)
        BloquearEsquina(ave,calle)
        Pos(ave,calle)
        LiberarEsquina(memoa,memoc)
        memoa:=ave
        memoc:=calle
        contador:=contador+1


    BloquearEsquina(10,10)
    Pos(10,10)
    LiberarEsquina(ave,calle)   
    si(quien=1)
      Pos(6,10)
      LiberarEsquina(10,10)
    sino
      Pos(7,10)
      LiberarEsquina(10,10)
  fin
  
  
  
  proceso PapelerosRecorrido(E quien:numero)
  variables
    ave,calle,memoa,memoc,contador:numero
  comenzar 
    contador:=0
    Random(ave,6,10)  
    Random(calle,1,9)  
    memoa:=ave
    memoc:=calle
    BloquearEsquina(ave,calle)
    Pos(ave,calle)
    
    mientras(contador<4)    
      Random(ave,6,10)  
      Random(calle,1,9)  
      si(ave<>memoa | calle<>memoc)
        BloquearEsquina(ave,calle)
        Pos(ave,calle)
        LiberarEsquina(memoa,memoc)
        memoa:=ave
        memoc:=calle
        contador:=contador+1


    BloquearEsquina(10,10)
    Pos(10,10)
    LiberarEsquina(ave,calle)   
    si(quien=3)
      Pos(8,10)
      LiberarEsquina(10,10)
    sino
      Pos(9,10)
      LiberarEsquina(10,10)
  fin
  
  
areas
  floarea: AreaPC (1,1,5,10)
  paparea: AreaPC (6,1,10,9)
  robotF1: AreaP(6,10,6,10)
  robotF2: AreaP(7,10,7,10)
  robotP1: AreaP(8,10,8,10)
  robotP2: AreaP(9,10,9,10)
  deposito: AreaC(10,10,10,10)
  alider: AreaP(11,11,11,11)
  
robots

  robot Florero
  variables
    quien:numero
  comenzar
    RecibirMensaje(quien,RobotLider)
    FlorerosRecorrido(quien)
  fin
  
  robot Papelero
  variables
    quien:numero
  comenzar
    RecibirMensaje(quien,RobotLider)
    PapelerosRecorrido(quien)
  fin
  
  robot Lider
  comenzar
    EnviarMensaje(1,Robot1)
    EnviarMensaje(2,Robot2)
    EnviarMensaje(3,Robot3)
    EnviarMensaje(4,Robot4)
  fin
  
variables

  RobotLider:Lider
  Robot1:Florero
  Robot2:Florero
  Robot3:Papelero
  Robot4:Papelero  
  
comenzar

  AsignarArea(RobotLider,alider)

  AsignarArea(Robot1,robotF1)
  AsignarArea(Robot1,floarea)
  AsignarArea(Robot1,deposito)
  AsignarArea(Robot2,robotF2)
  AsignarArea(Robot2,floarea)
  AsignarArea(Robot2,deposito)
  
  AsignarArea(Robot3,robotP1)
  AsignarArea(Robot3,paparea)
  AsignarArea(Robot3,deposito)
  AsignarArea(Robot4,robotP2)
  AsignarArea(Robot4,paparea)
  AsignarArea(Robot4,deposito)
  
  Iniciar(Robot1,6,10)
  Iniciar(Robot2,7,10)
  Iniciar(Robot3,8,10)
  Iniciar(Robot4,9,10)
  Iniciar(RobotLider,11,11)
  
fin
```
#### ejercicio 2
```
{Bienvenidos al entorno CMRE.
Lo siguiente es un código de ejemplo que implementa un
proceso que recibe un número de avenida como parámetro,
se posiciona en esa avenida y la recorre.}

programa ejemplo
procesos

  proceso GetFlores
  comenzar  
    mientras(HayFlorEnLaEsquina)
      tomarFlor
  fin
  
  proceso GetPapeles
  comenzar
    mientras(HayPapelEnLaEsquina)
      tomarPapel
  fin

  proceso izq
  comenzar
    repetir 3
      derecha
  fin
  
areas
  ciudad: AreaC (1,1,100,100)
  
robots

  robot robot1
  variables 
    contador,junto:numero
  comenzar
    contador:=5
    junto:=0
    mientras(contador>0)
      repetir contador
        mover
      derecha
      mientras(HayFlorEnLaEsquina)
        tomarFlor
        junto:=junto+1
      si(contador=1) 
        BloquearEsquina(16,16)
        EnviarMensaje(1,RobotL)
      repetir contador
        mover
      izq
      mientras(HayFlorEnLaEsquina)
        tomarFlor
        junto:=junto+1
      contador:=contador-1
    izq
    mientras(HayFlorEnLaEsquina)
      tomarFlor
      junto:=junto+1
    mover
    
    LiberarEsquina(16,16)
    
    contador:=2
    mientras(contador<6)
      repetir contador
        mover
      derecha
      mientras(HayFlorEnLaEsquina)
        tomarFlor
        junto:=junto+1
      repetir contador
        mover
      izq
      mientras(HayFlorEnLaEsquina)
        tomarFlor
        junto:=junto+1
      contador:=contador+1
    Informar(junto)
    EnviarMensaje(1,RobotL)
  fin
  
  robot robot2
  variables 
    contador,junto:numero
  comenzar
    contador:=5
    junto:=0
    
    mientras(contador>0)
      repetir contador
        mover
      izq
      mientras(HayPapelEnLaEsquina)
        tomarPapel
        junto:=junto+1
      si(contador=1) 
        BloquearEsquina(16,16)
        EnviarMensaje(2,RobotL)
      repetir contador
        mover
      derecha
      mientras(HayPapelEnLaEsquina)
        tomarPapel
        junto:=junto+1
      contador:=contador-1
    derecha
    mientras(HayPapelEnLaEsquina)
      tomarPapel
      junto:=junto+1
    mover
    
    LiberarEsquina(16,16)
    
    contador:=2
    mientras(contador<6)
      repetir contador
        mover
      izq
      mientras(HayPapelEnLaEsquina)
        tomarPapel
        junto:=junto+1
      repetir contador
        mover
      derecha
      mientras(HayPapelEnLaEsquina)
        tomarPapel
        junto:=junto+1
      contador:=contador+1
    Informar(junto)
    EnviarMensaje(1,RobotL)
  fin
  
  robot Lider
  variables
    quien,qgano,termino:numero
  comenzar
    qgano:=0        
    repetir 2
      RecibirMensaje(quien,*)
      si(qgano = 0)
        qgano:=quien
        
    repetir 2
      RecibirMensaje(termino,*)
      
          
    Informar(qgano)     
  fin
  
variables
  RobotL: Lider
  R1: robot1
  R2: robot2
comenzar
  AsignarArea(RobotL, ciudad)
  AsignarArea(R1, ciudad)
  AsignarArea(R2, ciudad)
  
  Iniciar(RobotL, 15,1)
  Iniciar(R1, 1,1)
  Iniciar(R2, 31,1)
  
fin
```
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


#### ejercicio 4
* *notas:*
  el 4-B es solamente una variante de que camina demas . no la hago porque es simplemente agregar un pos , bloquear esquina y liberar esquina extra.
```r-info

programa ejemplo
procesos
  proceso asignarId
  comenzar
    EnviarMensaje(1,Robot1)
    EnviarMensaje(2,Robot2)
    EnviarMensaje(3,Robot3)
    EnviarMensaje(4,Robot4)
  fin
areas
  compartida:AreaC(10,10,11,11)
  arL: AreaP (1,1,1,1)
  area1: AreaP(9,9,9,9)
  area2: AreaP(9,10,9,10)
  area3: AreaP(9,11,9,11)
  area4: AreaP(9,12,9,12)
robots

  robot Obrero
  variables
    id,hayFlor:numero
  comenzar
    hayFlor:=1
    RecibirMensaje(id,RobotL)
    
    mientras(hayFlor=1)
      BloquearEsquina(10,10)
      Pos(10,10)
      si(HayFlorEnLaEsquina)
        tomarFlor
      sino
        hayFlor:=0
      BloquearEsquina(11,11)
      Pos(11,11)
      si(HayFlorEnLaBolsa)
        depositarFlor
      LiberarEsquina(10,10)
      si(id=1)
        Pos(9,9)
        LiberarEsquina(11,11)
      si(id=2)
        Pos(9,10)
        LiberarEsquina(11,11)
      si(id=3)  
        Pos(9,11)
        LiberarEsquina(11,11)
      si(id=4)
        Pos(9,12)
        LiberarEsquina(11,11)  
    
    EnviarMensaje(1,RobotL)
  fin
  
  robot Lider
  variables
    listo:numero
  comenzar
    asignarId
    repetir 4
      RecibirMensaje(listo,*)
    Pos(11,11)
    mientras(HayFlorEnLaEsquina)
      tomarFlor 
    
  fin
  
variables
  RobotL:Lider
  Robot1:Obrero
  Robot2:Obrero
  Robot3:Obrero
  Robot4:Obrero
comenzar
  AsignarArea(RobotL, arL)
  AsignarArea(RobotL, compartida)
  
  AsignarArea(Robot1, area1)
  AsignarArea(Robot1, compartida)
  
  AsignarArea(Robot2, area2)
  AsignarArea(Robot2, compartida)
  
  AsignarArea(Robot3, area3)
  AsignarArea(Robot3, compartida)
  
  AsignarArea(Robot4, area4)
  AsignarArea(Robot4, compartida)


  Iniciar(Robot1,9,9)
  Iniciar(Robot2,9,10)
  Iniciar(Robot3,9,11)
  Iniciar(Robot4,9,12)
  Iniciar(RobotL, 1,1)
fin
```


#### ejercicio 5

```
programa ejemplo
procesos
  proceso asignarId
  comenzar
    EnviarMensaje(1,Robot1)
    EnviarMensaje(2,Robot2)
    EnviarMensaje(3,Robot3)
    EnviarMensaje(4,Robot4)
  fin
areas
  Area1: AreaP (4,1,4,100)
  Area2: AreaP (6,1,6,100)
  Area3: AreaP (8,1,8,100)
  Area4: AreaP (10,1,10,100)
  deposito: AreaPC(11,11,11,11)
  AreaL:AreaP(1,1,1,1)
robots

  robot Participante
  variables
    id,calle,avenida:numero
    ok:boolean
  comenzar
    RecibirMensaje(id,RobotL)
    calle:=1
    
    si(id=1)
      avenida:=4
    si(id=2)
      avenida:=6
    si(id=3)
      avenida:=8
    si(id=4)
      avenida:=10
    
    
    BloquearEsquina(11,11)
    Pos(11,11)
    si(HayFlorEnLaEsquina)
      ok:=V
      calle:=calle+1
      tomarFlor
    sino
      ok:=F
    Pos(avenida,calle)
    si(HayFlorEnLaBolsa)
      depositarFlor
    LiberarEsquina(11,11)
    
    mientras(ok)
      BloquearEsquina(11,11)
      Pos(11,11)
      si(HayFlorEnLaEsquina)
        ok:=V
        calle:=calle+1
        tomarFlor
      sino
        ok:=F
      Pos(avenida,calle)
      si(HayFlorEnLaBolsa)
        depositarFlor
      LiberarEsquina(11,11)
    
    EnviarMensaje(id,RobotL)
    EnviarMensaje(calle,RobotL)
  fin
  
  robot Lider
  variables
    Ganador,Calle,MaxG,MaxC:numero
  comenzar
    asignarId
    
    MaxG:=0
    MaxC:=0
    
    repetir 4
      RecibirMensaje(Ganador,*)
      RecibirMensaje(Calle,*)
      si(Calle>MaxC)
        MaxG:=Ganador
        MaxC:=Calle
        
    Informar(MaxG)
    Informar(MaxC)
  fin
  
  
variables
  RobotL: Lider
  Robot1: Participante
  Robot2: Participante
  Robot3: Participante
  Robot4: Participante
comenzar
  AsignarArea(RobotL, AreaL)
  
  AsignarArea(Robot1,Area1)
  AsignarArea(Robot1,deposito)
  
  AsignarArea(Robot2,Area2)
  AsignarArea(Robot2,deposito)
  
  AsignarArea(Robot3,Area3)
  AsignarArea(Robot3,deposito)
  
  AsignarArea(Robot4,Area4)
  AsignarArea(Robot4,deposito)
  
  Iniciar(RobotL,1,1)
  Iniciar(Robot1,4,1)
  Iniciar(Robot2,6,1)
  Iniciar(Robot3,8,1)
  Iniciar(Robot4,10,1)
  
fin
```

#### ejercicio 6
* *nota:* el ejercicio es muy largo y no hice los otros puntos

```R-info

programa ejemplo

procesos


  proceso cuadranteFlores(E ix:numero;E iy:numero;E x:numero;E y:numero)
  variables
    alto,largo,ave,calle:numero
  comenzar
    largo:=x
    alto:=y
    ave:=ix
    calle:=iy
    derecha
    mientras(HayFlorEnLaEsquina)
      tomarFlor
    mientras(alto>0)    
      alto:=alto-1
      repetir largo
        mientras(HayFlorEnLaEsquina)
          tomarFlor
        mover
      calle:=calle+1
      si(alto <> 0)
        Pos(ave,calle) 
  fin
  
  proceso cuadranteFloresPapeles(E ix:numero;E iy:numero;E x:numero;E y:numero)
  variables
    alto,largo,ave,calle:numero
  comenzar
    largo:=x
    alto:=y
    ave:=ix
    calle:=iy
    derecha
    mientras(HayFlorEnLaEsquina)
      tomarFlor
    mientras(HayPapelEnLaEsquina)
      tomarPapel
    mientras(alto>0)    
      alto:=alto-1
      repetir largo
        mientras(HayFlorEnLaEsquina)
          tomarFlor
        mientras(HayPapelEnLaEsquina)
          tomarPapel
        mover
      calle:=calle+1
      si(alto <> 0)
        Pos(ave,calle) 
  fin

  proceso cuadrantePapeles(E ix:numero;E iy:numero;E x:numero;E y:numero)
  variables
    alto,largo,ave,calle:numero
  comenzar
    largo:=x
    alto:=y
    ave:=ix
    calle:=iy
    derecha
    mientras(HayPapelEnLaEsquina)
      tomarPapel
    mientras(alto>0)    
      alto:=alto-1
      repetir largo
        mientras(HayPapelEnLaEsquina)
          tomarPapel
        mover
      calle:=calle+1
      si(alto <> 0)
        Pos(ave,calle) 
  fin
  
areas
  ciudad: AreaC (1,1,100,100)
robots
  robot robot1
  variables
    id,calle,cont:numero
  comenzar
    cont:=1
    RecibirMensaje(id,RobotL)
    cuadranteFlores(2,2,5,5)
    
    EnviarMensaje(1,RobotL)
    RecibirMensaje(calle,RobotL)
    Pos(1,calle)

    mientras(HayFlorEnLaBolsa & (cont<100))
      depositarFlor
      cont:=cont+1
      mover
      
    EnviarMensaje(1,RobotL)
  fin
  robot robot2
  variables
    id,calle,cont:numero
  comenzar
    cont:=1
    RecibirMensaje(id,RobotL)
    cuadranteFloresPapeles(5,5,10,10)
    
    EnviarMensaje(2,RobotL)
    RecibirMensaje(calle,RobotL)
    Pos(1,calle)
    
    mientras(HayPapelEnLaBolsa & HayFlorEnLaBolsa & (cont<100))
      depositarPapel
      depositarFlor
      cont:=cont+1
      mover
      
    EnviarMensaje(1,RobotL)
  fin
  
  robot robot3
  variables
    id,calle,cont:numero
  comenzar
    cont:=1
    RecibirMensaje(id,RobotL)
    cuadrantePapeles(9,9,7,7)
    
    EnviarMensaje(3,RobotL)
    RecibirMensaje(calle,RobotL)
    Pos(1,calle)
    
    mientras(HayPapelEnLaBolsa & (cont<100))
      depositarPapel
      cont:=cont+1
      mover
      
    EnviarMensaje(1,RobotL)
  fin
  
  robot robotL
  variables
    primero,segundo,tercero,termino:numero
  comenzar
    EnviarMensaje(1,Robot1)
    EnviarMensaje(2,Robot2)
    EnviarMensaje(3,Robot3)
    
    RecibirMensaje(primero,*)
    RecibirMensaje(segundo,*)
    RecibirMensaje(tercero,*)
    
    si(primero=1)
      EnviarMensaje(20,Robot1)
    si(primero=2)
      EnviarMensaje(20,Robot2)
    si(primero=3)
      EnviarMensaje(20,Robot3)
      
    si(segundo=1)
      EnviarMensaje(21,Robot1)
    si(segundo=2)
      EnviarMensaje(21,Robot2)
    si(segundo=3)
      EnviarMensaje(21,Robot3)  
      
    si(tercero=1)
      EnviarMensaje(22,Robot1)
    si(tercero=2)
      EnviarMensaje(22,Robot2)
    si(tercero=3)
      EnviarMensaje(22,Robot3)
       
    repetir 3
      RecibirMensaje(termino,*)
  fin
  
variables
  RobotL: robotL
  Robot1: robot1
  Robot2: robot2
  Robot3: robot3
comenzar
  AsignarArea(RobotL, ciudad)
  AsignarArea(Robot1, ciudad)
  AsignarArea(Robot2, ciudad)
  AsignarArea(Robot3, ciudad)
  
  Iniciar(Robot1,2,2)
  Iniciar(Robot2,5,5)
  Iniciar(Robot3,9,9)
  Iniciar(RobotL,1,1)
  
fin
```

#### practica 4


#### ejercicio 1

 * no lo hago porque lo que busco es aprender concurrencia no a decifrar consignas mal redactadas. (Mucho lore el enunciado)

#### ejercicio 2

```
programa ejemplo
areas
  deposito: AreaC(50,50,50,50)
  a1:AreaP(5,1,5,100)
  a2:AreaP(10,1,10,100)
  a3:AreaP(11,1,11,1)
  a4:AreaP(12,1,12,1)
robots

  robot Productor
  variables
    cont,ave,calle:numero
  comenzar
    cont:=0
    ave:=  PosAv
    calle:= PosCa
    
    mientras(calle < 100)
      mientras(cont<5)
      
        mientras(HayFlorEnLaEsquina & (cont<5))
          tomarFlor
          cont:=cont+1
        si(calle<100)
          mover
          ave:=  PosAv
          calle:= PosCa
        sino
          cont:=5
        
        
      cont:=0
      
      BloquearEsquina(50,50)
      Pos(50,50)
      repetir 5
        si(HayFlorEnLaBolsa)
          depositarFlor
      Pos(ave,calle)
      LiberarEsquina(50,50)
     
  fin
  
  robot Consumidor
  variables
    calle,ave,ran,cont:numero
    llave:boolean
  comenzar
    llave:=V
    calle:=PosCa
    ave:=PosAv
    cont:=0
    
    mientras(llave)
      Random(ran,2,5)
      BloquearEsquina(50,50)
      Pos(50,50)
      
      
      si(HayFlorEnLaEsquina)
        repetir ran
          si(HayFlorEnLaEsquina)
            tomarFlor
            cont:=0
      sino
        cont:=cont+1
        si(cont=8)
          llave:=F
      

      Pos(ave,calle)
      LiberarEsquina(50,50)
      repetir ran
        si(HayFlorEnLaBolsa)
          depositarFlor
    
  fin
  
  
variables
  R1:Productor
  R2:Productor
  R3:Consumidor
  R4:Consumidor
comenzar
  AsignarArea(R1, a1)
  AsignarArea(R1, deposito)
  AsignarArea(R2, a2)
  AsignarArea(R2, deposito)
  AsignarArea(R3, a3)
  AsignarArea(R3, deposito)
  AsignarArea(R4, a4)
  AsignarArea(R4, deposito)
  
  Iniciar(R1, 5,1)
  Iniciar(R2, 10,1)
  Iniciar(R3, 11,1)
  Iniciar(R4, 12,1)
  
fin
```

#### ejercicio 3-A
* *nota:* no asigne las areas privadas pero son 3 lineas de codigo mas , por lo tanto lo deje pasar , son 4 areas privadas 1 para cada robot.
```R-info
programa ejemplo
procesos
  proceso recorrido
  comenzar
    si(PosCa<100)
      mientras(HayFlorEnLaEsquina)
        tomarFlor
      mover
  fin
  proceso asignarId
  comenzar
    EnviarMensaje(1,r1)
    EnviarMensaje(2,r2)
    EnviarMensaje(3,r3)
  fin
  proceso enviarPermiso
  comenzar
    EnviarMensaje(1,r1)
    EnviarMensaje(2,r2)
    EnviarMensaje(3,r3)
  fin
areas
  ciudad: AreaC (1,1,100,100)
robots
  robot tipo1
  variables
    id,perm:numero
  comenzar
    RecibirMensaje(id,rj)
    mientras(PosCa<100)
      RecibirMensaje(perm,rj)
      recorrido
      si(PosCa=100)
        EnviarMensaje(0,rj)
      sino
        EnviarMensaje(1,rj)
  fin
  robot tipo2
  variables
    termino:numero
  comenzar
    termino:=1
    asignarId
    mientras(termino=1)
      enviarPermiso
      repetir 3
        RecibirMensaje(termino,*)
        
    Informar(55)
  fin
variables
  rj:tipo2
  r1:tipo1
  r2:tipo1
  r3:tipo1
comenzar
  AsignarArea(rj,ciudad)
  AsignarArea(r1,ciudad)
  AsignarArea(r2,ciudad)
  AsignarArea(r3,ciudad)
  
  Iniciar(rj,10,10)
  Iniciar(r1,1,1)
  Iniciar(r2,2,1)
  Iniciar(r3,3,1)
fin
```
#### ejercicio 3-B
* *nota:* en este ejercicio el lider solo deberia asignar el id por lo tanto lo hice mal porque lo estoy usando para acciones extras que no son asignar id (pronto lo cambiare)

```R-info
programa ejemplo
procesos
  proceso recorrido(E x:numero)
  variables
    cont:numero
  comenzar
    mientras((cont<>x) & (PosCa<100))
      si(PosCa<100)
        si(HayFlorEnLaEsquina)
          tomarFlor
          cont:=cont+1
        sino
          si(PosCa<100)
            mover
    Informar(2)
  fin
  
  proceso asignarId
  comenzar
    EnviarMensaje(1,r1)
    EnviarMensaje(2,r2)
    EnviarMensaje(3,r3)
  fin
  
  proceso RecibirMsj(ES t1:numero;ES t2:numero;ES t3:numero)
  variables
    id:numero
  comenzar
    RecibirMensaje(id,*)
    si(id=1)   
      RecibirMensaje(t1,*)
    si(id=2) 
      RecibirMensaje(t2,*) 
    si(id=3) 
      RecibirMensaje(t3,*) 
  fin
  
  
  
  
areas
  ciudad: AreaC (1,1,100,100)
robots
  robot tipo1
  variables
    id,perm,x:numero
  comenzar
    RecibirMensaje(id,rj)
    mientras(PosCa<100)
      RecibirMensaje(perm,rj)
      
      Random(x,1,5)
      recorrido(x)
      
      
      si(PosCa=100)
        EnviarMensaje(id,rj)
        EnviarMensaje(0,rj)
      sino
        EnviarMensaje(id,rj)
        EnviarMensaje(1,rj)
        
  fin
  robot tipo2
  variables
    t1,t2,t3,total:numero
    activo:boolean
  comenzar
    t1:=1
    t2:=1
    t3:=1
    activo:=V
    total:=0
    asignarId
    
    mientras(activo)
      si(t1=1)
        EnviarMensaje(1,r1)
      si(t2=1)
        EnviarMensaje(1,r2)
      si(t3=1)
        EnviarMensaje(1,r3)
        
      total:= total+t1
      total:= total+t2
      total:= total+t3
      
      
      si(total=1)
        RecibirMsj(t1,t2,t3)
      si(total=2)
        repetir 2
          RecibirMsj(t1,t2,t3)
      si(total=3)      
        repetir 3
          RecibirMsj(t1,t2,t3)
      
      si(t1=0)
        si(t2=0)
          si(t3=0)
            activo:=F
      
      total:=0 
    Informar(55)
  fin
variables
  rj:tipo2
  r1:tipo1
  r2:tipo1
  r3:tipo1
comenzar
  AsignarArea(rj,ciudad)
  AsignarArea(r1,ciudad)
  AsignarArea(r2,ciudad)
  AsignarArea(r3,ciudad) 
  
  Iniciar(rj,10,10)
  Iniciar(r1,1,1)
  Iniciar(r2,2,1)
  Iniciar(r3,3,1)
fin
```


#### ejercicio 4

```rinfo
{Bienvenidos al entorno CMRE.
Lo siguiente es un código de ejemplo que implementa un
proceso que recibe un número de avenida como parámetro,
se posiciona en esa avenida y la recorre.}

programa ejemplo

procesos
  proceso asignarId
  comenzar
    EnviarMensaje(1,r1)
    EnviarMensaje(2,r2)
  fin
  
  proceso vaciarBolsa
  comenzar
    si(HayFlorEnLaBolsa)
      mientras(HayFlorEnLaBolsa)
        depositarFlor
        
    si(HayPapelEnLaBolsa)
      mientras(HayPapelEnLaBolsa)
        depositarPapel
  fin
  
areas
  ciudad: AreaC (1,1,100,100)
  
  
robots

  robot Trabajador
  variables
    avei,callei,id,tarea,calle,ave:numero
  comenzar
    RecibirMensaje(id,rj)
    avei:=PosAv
    callei:=PosCa    
    

    RecibirMensaje(tarea,rj)
    mientras(tarea<>4)
      RecibirMensaje(ave,rj)
      RecibirMensaje(calle,rj)
      
      BloquearEsquina(ave,calle)
      Pos(ave,calle)
      si(tarea=1)
        mientras(HayFlorEnLaEsquina)
          tomarFlor
      si(tarea=2)
        mientras(HayPapelEnLaEsquina)
          tomarPapel
      si(tarea=3)
        vaciarBolsa
        
      Pos(avei,callei)
      LiberarEsquina(ave,calle)
      
      RecibirMensaje(tarea,rj)
  fin
  
  robot Jefe
  variables
    ave,calle,tarea,rb:numero
  comenzar
    
    asignarId
    
    repetir 10
      Random(ave,2,100)
      Random(calle,2,100)
      Random(tarea,1,4)
      Random(rb,1,2)
      
      si(rb=1)
        EnviarMensaje(tarea,r1)
        EnviarMensaje(ave,r1)
        EnviarMensaje(calle,r1)
      si(rb=2)
        EnviarMensaje(tarea,r2)
        EnviarMensaje(ave,r2)
        EnviarMensaje(calle,r2)
      
    EnviarMensaje(4,r1) 
    EnviarMensaje(4,r2) 
      
  fin
  
  
variables
  r1:Trabajador
  r2:Trabajador
  rj:Jefe
comenzar
  AsignarArea(r1,ciudad)
  AsignarArea(r2,ciudad)
  AsignarArea(rj,ciudad)
  Iniciar(rj,1,1)
  Iniciar(r1,2,1)
  Iniciar(r2,3,1)
fin
```

### preguntas :
* siempre tienen que tener id los trabajadores o los robots repetidos?
* si no dice que se tiene que usar un robot fiscalizador lo puedo usar igual o asumo que no deberia usarlo?
