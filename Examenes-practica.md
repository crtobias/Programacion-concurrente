
### Examen 1

* *enunciado:* Dos robots recolectores deben transportar todos los papeles de la esquina (5, 5) a la esquina (6, 6). Los robots pueden transportar un máximo de 10 papeles en cada viaje. El trabajo entre los recolectores debe ser alternado: primero recolector 1 transporta 10 papeles, luego lo hace recolector 2, luego recolector 1, luego recolector 2 y así hasta transportar todos los papeles que estén en la esquina (5,5). Los recolectores comienzan en (1,1) y (2,2). 
* NOTA 1: Debe maximizarse la concurrencia entre los recolectores, es decir mientras un robot está depositando todos los papeles recolectados, el otro robot puede estar llevando a cabo la tarea de recolección.
* NOTA 2: Piense en una solución al problema utilizando dos tipos de robots distintos

```

programa ejemplo
procesos
  proceso recolectarLote(ES x:boolean)
  variables
    cont:numero
  comenzar
    cont:=0
    BloquearEsquina(5,5)
    Pos(5,5)
    
    mientras(HayPapelEnLaEsquina  & (cont<10))
      tomarPapel
      cont:=cont+1
        
    si(HayPapelEnLaEsquina)
      x:=V
    sino
      x:=F   
  fin
  
  proceso deposita
  variables
    cont:numero
  comenzar
    mientras(HayPapelEnLaBolsa  & (cont<10))
      depositarPapel
      cont:=cont+1
  fin
  
areas
  a1: AreaP(1,1,1,1)
  a2: AreaP(2,2,2,2)
  depo1: AreaC(5,5,5,5)
  depo2: AreaC(6,6,6,6)
robots

  robot recolector1
  variables
    x:boolean
  comenzar
    x:=V
    mientras(x)
      recolectarLote(x)
      BloquearEsquina(6,6)
      Pos(6,6)
      LiberarEsquina(5,5)
      EnviarMensaje(x,r2)
      deposita
      Pos(1,1)
      LiberarEsquina(6,6)
      RecibirMensaje(x,r2)
      si(x=F)
        Informar(1)
        EnviarMensaje(x,r2)

  fin
  
  robot recolector2
  variables
    x:boolean
  comenzar
    RecibirMensaje(x,r1)
    si(x=F)
      EnviarMensaje(x,r1)
      
    mientras(x)
      recolectarLote(x)
      BloquearEsquina(6,6)
      Pos(6,6)
      LiberarEsquina(5,5)
      EnviarMensaje(x,r1)
      deposita
      Pos(2,2)
      LiberarEsquina(6,6)
      RecibirMensaje(x,r1)
      si(x=F)
        Informar(2)
        EnviarMensaje(x,r1)
        
  fin
  
variables
  r1: recolector1
  r2: recolector2
comenzar


  AsignarArea(r1, a1)
  AsignarArea(r1, depo1)
  AsignarArea(r1, depo2)
  
  
  AsignarArea(r2, a2)
  AsignarArea(r2, depo1)
  AsignarArea(r2, depo2)
  
  
  Iniciar(r1, 1,1)
  Iniciar(r2, 2,2)
fin
```

### Examen 2
* *enunciado:* Tres robots recolectores deben recorrer su avenida asignada juntando flores y papeles. En una primera etapa los robots recorren su avenida juntando únicamente las flores. Cuando los tres robots finalizan esta etapa, un robot coordinador determinará cuáles son los dos robots que recolectaron más flores y que deberán realizar la segunda etapa. Estos dos robots deberán recorrer su avenida por segunda vez recolectando todos los papeles. Al finalizar, el robot coordinador informará quién finalizó primero con esta tarea. 
* Robot recolector 1 debe recorrer la avenida 5 desde 1 hasta 10. Empezando en la esquina (5,1). 
* Robot recolector 2 debe recorrer la avenida 6 desde 1 hasta 10. Empezando en la esquina (6,1).
* Robot recolector 3 debe recorrer la avenida 7 desde 1 hasta 10. Empezando en la esquina (7,1). 
* El coordinador estará en la esquina (1,1)

```

```

### Examen 3
* *enunciado:* En la ciudad existen 5 robots: hay 4 robots limpiadores y un robot jefe. El robot jefe elige un número al azar entre los 4 robots limpiadores y le avisa para que junte una flor (de ser posible) de la esquina (50,50). Este proceso lo repite 5 veces. 
* Notas: 
* El robot limpiador 1 comienza en la esquina (2,2). 
* El robot limpiador 2 comienza en la esquina (3,3).
* El robot limpiador 3 comienza en la esquina (4,4). 
* El robot limpiador 4 comienza en la esquina (5,5). 
* El robot jefe comienza en la esquina (1,1).

```

programa ejemplo
procesos
  proceso recorrido
  variables
    ca,av:numero
  comenzar
    av:=PosAv
    ca:=PosCa
    BloquearEsquina(50,50)
    Pos(50,50)
    si(HayFlorEnLaEsquina)
      tomarFlor
    Pos(av,ca)
    LiberarEsquina(50,50)  
  fin
  
  proceso enviarConfirmacion
  comenzar
    EnviarMensaje(9,rj)
  fin
  
  proceso finalizar
  comenzar
    EnviarMensaje(0,r1)
    EnviarMensaje(0,r2)
    EnviarMensaje(0,r3)
    EnviarMensaje(0,r4)
  fin
  
areas
  ciudad: AreaC (1,1,100,100)
robots

  robot limpiador
  variables
    x:numero
  comenzar
    RecibirMensaje(x,rj)
    mientras(x=1)
      recorrido {proceso}  
      enviarConfirmacion {proceso}  
      RecibirMensaje(x,rj)
    
    Informar(0000)
  fin
  
  robot jefe
  variables
    x,c:numero
  comenzar
    repetir 5
      Random(x,1,4)
      si(x=1)
        EnviarMensaje(1,r1)
        RecibirMensaje(c,r1)
      si(x=2)
        EnviarMensaje(1,r2)
        RecibirMensaje(c,r2)
      si(x=3)
        EnviarMensaje(1,r3)
        RecibirMensaje(c,r3)
      si(x=4)
        EnviarMensaje(1,r4)
        RecibirMensaje(c,r4)
    
        
    finalizar {proceso}    
  fin
  
variables
  rj: jefe
  r1: limpiador
  r2: limpiador
  r3: limpiador
  r4: limpiador
comenzar
  AsignarArea(rj, ciudad)
  AsignarArea(r1, ciudad)
  AsignarArea(r2, ciudad)
  AsignarArea(r3, ciudad)
  AsignarArea(r4, ciudad)
  Iniciar(rj, 1,1)
  Iniciar(r1, 2,2)
  Iniciar(r2, 3,3)
  Iniciar(r3, 4,4)
  Iniciar(r4, 5,5)
fin
```

