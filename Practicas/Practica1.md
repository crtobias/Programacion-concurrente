

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
