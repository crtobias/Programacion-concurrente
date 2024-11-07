

### Examen 1

* *enunciado:* Dos robots recolectores deben transportar todos los papeles de la esquina (5, 5) a la esquina (6, 6). Los robots pueden transportar un máximo de 10 papeles en cada viaje. El trabajo entre los recolectores debe ser alternado: primero recolector 1 transporta 10 papeles, luego lo hace recolector 2, luego recolector 1, luego recolector 2 y así hasta transportar todos los papeles que estén en la esquina (5,5). Los recolectores comienzan en (1,1) y (2,2). NOTA 1: Debe maximizarse la concurrencia entre los recolectores, es decir mientras un robot está depositando todos los papeles recolectados, el otro robot puede estar llevando a cabo la tarea de recolección. NOTA 2: Piense en una solución al problema utilizando dos tipos de robots distintos

```

programa ejemplo
procesos
  proceso recolectarLote(ES x:boolean)
  comenzar
    BloquearEsquina(5,5)
    Pos(5,5)
    repetir 10
      si(HayPapelEnLaEsquina)
        tomarPapel
    si(HayPapelEnLaEsquina)
      x:=V
    sino
      x:=F   
  fin
  
  proceso deposita
  comenzar
    repetir 10
      si(HayPapelEnLaBolsa)
        depositarPapel
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
      Informar(11111)
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
