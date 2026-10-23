# portafolio_ccna2
# Topología de Red: Router-on-a-Stick con VLANs
<img width="759" height="548" alt="1-topologia" src="https://github.com/user-attachments/assets/2ba7cf93-6bd3-4012-965d-7ac227af366b" />

## 1. Diagrama de la topología

```bash
                 [ R1-Core-LuisMGL (Router) ]
                          |
                          | Gi0/0
                          | Trunk 802.1Q
                          | Router-on-a-Stick
                          | VLANs 10, 20, 30, 99
                          | VLAN 111 nativa
                          |
                     [ SW-Core-LuisMGL ]
                       /       \
              (Trunk) /         \ (Trunk)
          VLAN 111 nativa     VLAN 111 nativa
                    /             \
             [ SW-Lab1-LuisMGL ]       [ SW-Lab2-LuisMGL ]
             Edificio A        Edificio B

     Dispositivos en SW-Lab1-LuisMGL:       Dispositivos en SW-Lab2-LuisMGL:

     ├── VLAN 10: 3 PCs Admin       ├── VLAN 10: 3 PCs Admin
     │   Fa0/1 - Fa0/3              │   Fa0/1 - Fa0/3
     │                              │
     ├── VLAN 20: 3 PCs Alumnos     ├── VLAN 20: 3 PCs Alumnos
     │   Fa0/4 - Fa0/6              │   Fa0/4 - Fa0/6
     │                              │
     └── VLAN 30: 1 PC Dirección   └── VLAN 30: 1 PC Dirección
         Fa0/7                          Fa0/7


     Conexión local de SW-Core-LuisMGL:

     └── VLAN 99: 1 PC Gestión
         Puerto Fa0/9
```

## 2. Diagrama gráfico mermaid

```mermaid
%%{init: {'theme': 'dark'}}%%
flowchart TB
    R1["R1-Core-LuisMGL<br/>Router Central<br/>G0/0/0<br/>Router-on-a-Stick"]

    CORE["SW-Core-LuisMGL<br/>Switch Núcleo"]

    PCG["PC Gestión<br/>VLAN 99<br/>Fa0/9"]

    LAB1["SW-Lab1-LuisMGL<br/>Edificio A"]
    LAB2["SW-Lab2-LuisMGL<br/>Edificio B"]

    R1 <-->|"Trunk 802.1Q<br/>VLAN 10, 20, 30, 99<br/>VLAN 111 nativa"| CORE

    CORE <-->|"Trunk<br/>VLAN 10, 20, 30<br/>VLAN 111 nativa"| LAB1
    CORE <-->|"Trunk<br/>VLAN 10, 20, 30<br/>VLAN 111 nativa"| LAB2

    CORE --- PCG

    subgraph A["Edificio A - SW-Lab1"]
        A10["VLAN 10<br/>3 PCs Administrativos<br/>Fa0/1 - Fa0/3"]
        A20["VLAN 20<br/>3 PCs Alumnos<br/>Fa0/4 - Fa0/6"]
        A30["VLAN 30<br/>1 PC Dirección<br/>Fa0/7"]

        LAB1 --- A10
        LAB1 --- A20
        LAB1 --- A30
    end

    subgraph B["Edificio B - SW-Lab2"]
        B10["VLAN 10<br/>3 PCs Administrativos<br/>Fa0/1 - Fa0/3"]
        B20["VLAN 20<br/>3 PCs Alumnos<br/>Fa0/4 - Fa0/6"]
        B30["VLAN 30<br/>1 PC Dirección<br/>Fa0/7"]

        LAB2 --- B10
        LAB2 --- B20
        LAB2 --- B30
    end

    classDef router fill:#2563eb,color:#ffffff,stroke:#1e40af
    classDef core fill:#0f766e,color:#ffffff,stroke:#115e59
    classDef access fill:#dbeafe,color:#1e3a8a,stroke:#2563eb
    classDef pc fill:#f3f4f6,color:#111827,stroke:#6b7280

    class R1 router
    class CORE core
    class LAB1,LAB2 access
    class PCG,A10,A20,A30,B10,B20,B30 pc no me aparece elflowchart TB
    R1["R1-Core-LuisMGL<br/>Router Central<br/>G0/0/0<br/>Router-on-a-Stick"]

    CORE["SW-Core-LuisMGL<br/>Switch Núcleo"]

    PCG["PC Gestión<br/>VLAN 99<br/>Fa0/9"]

    LAB1["SW-Lab1-LuisMGL<br/>Edificio A"]
    LAB2["SW-Lab2-LuisMGL<br/>Edificio B"]

    R1 <-->|"Trunk 802.1Q<br/>VLAN 10, 20, 30, 99<br/>VLAN 111 nativa"| CORE

    CORE <-->|"Trunk<br/>VLAN 10, 20, 30<br/>VLAN 111 nativa"| LAB1
    CORE <-->|"Trunk<br/>VLAN 10, 20, 30<br/>VLAN 111 nativa"| LAB2

    CORE --- PCG

    subgraph A["Edificio A - SW-Lab1"]
        A10["VLAN 10<br/>3 PCs Administrativos<br/>Fa0/1 - Fa0/3"]
        A20["VLAN 20<br/>3 PCs Alumnos<br/>Fa0/4 - Fa0/6"]
        A30["VLAN 30<br/>1 PC Dirección<br/>Fa0/7"]

        LAB1 --- A10
        LAB1 --- A20
        LAB1 --- A30
    end

    subgraph B["Edificio B - SW-Lab2"]
        B10["VLAN 10<br/>3 PCs Administrativos<br/>Fa0/1 - Fa0/3"]
        B20["VLAN 20<br/>3 PCs Alumnos<br/>Fa0/4 - Fa0/6"]
        B30["VLAN 30<br/>1 PC Dirección<br/>Fa0/7"]

        LAB2 --- B10
        LAB2 --- B20
        LAB2 --- B30
    end

    classDef router fill:#2563eb,color:#ffffff,stroke:#1e40af
    classDef core fill:#0f766e,color:#ffffff,stroke:#115e59
    classDef access fill:#dbeafe,color:#1e3a8a,stroke:#2563eb
    classDef pc fill:#f3f4f6,color:#111827,stroke:#6b7280

    class R1 router
    class CORE core
    class LAB1,LAB2 access
    class PCG,A10,A20,A30,B10,B20,B30 pc no me aparece el

```

## 3. Tabla de direccionamiento

Todas las subredes indicadas para las VLAN 10, 20, 30 y 99 usan máscara
`/24` (`255.255.255.0`). En cada subred, la primera dirección utilizable
es `.1` y la última es `.254`.

### 3.1 Tabla A. Infraestructura

  ### 3.1 Tabla de Direccionamiento de Segmentos / VLANs

| Segmento | VLAN | Red/CIDR | Máscara | Primera IP utilizable | Última IP utilizable | Gateway |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: |
| Administración | 10 | `192.168.10.0/24` | `255.255.255.0` | `192.168.10.1` | `192.168.10.254` | `192.168.10.254` |
| Laboratorios | 20 | `192.168.20.0/24` | `255.255.255.0` | `192.168.20.1` | `192.168.20.254` | `192.168.20.254` |
| Dirección | 30 | `192.168.30.0/24` | `255.255.255.0` | `192.168.30.1` | `192.168.30.254` | `192.168.30.254` |
| Gestión | 99 | `192.168.99.0/24` | `255.255.255.0` | `192.168.99.1` | `192.168.99.254` | `192.168.99.254` |
| VLAN nativa | 111 | No especificada en el documento | No especificada | No asignada | No asignada | No asignado |
| Blackhole / puertos inactivos | 999 | No se especifica una subred | No especificada | No asignada | No asignada | No asignado |

*Las puertas de enlace de las VLAN 10, 20, 30 y 99 se configuran con la última IP utilizable de cada subred en las subinterfaces del router.*

---

### 3.2 Direcciones SVI de los switches

| Dispositivo | Interfaz VLAN | Dirección IP/CIDR | Gateway predeterminado |
| :--- | :---: | :---: | :---: |
| `SW-Core-LuisMGL` | `Vlan99` | `192.168.99.1/24` | `192.168.99.254` |
| `SW-Lab1-LuisMGL` | `Vlan99` | `192.168.99.2/24` | `192.168.99.254` |
| `SW-Lab2-LuisMGL` | `Vlan99` | `192.168.99.3/24` | `192.168.99.254` |

---

### 3.4 Tabla B. Hosts

Se asignan direcciones estáticas consecutivas dentro de cada VLAN. La PC de gestión usa `192.168.99.4`, porque las direcciones `.1`, `.2` y `.3` se reservan para las SVI de los tres switches.

| Dispositivo | VLAN | Dirección IP/CIDR | Máscara | Gateway predeterminado |
| :--- | :---: | :---: | :---: | :---: |
| PC-Admin-Lab1-1 | 10 | `192.168.10.1/24` | `255.255.255.0` | `192.168.10.254` |
| PC-Admin-Lab1-2 | 10 | `192.168.10.2/24` | `255.255.255.0` | `192.168.10.254` |
| PC-Admin-Lab1-3 | 10 | `192.168.10.3/24` | `255.255.255.0` | `192.168.10.254` |
| PC-Admin-Lab2-1 | 10 | `192.168.10.4/24` | `255.255.255.0` | `192.168.10.254` |
| PC-Admin-Lab2-2 | 10 | `192.168.10.5/24` | `255.255.255.0` | `192.168.10.254` |
| PC-Admin-Lab2-3 | 10 | `192.168.10.6/24` | `255.255.255.0` | `192.168.10.254` |
| PC-Alumno-Lab1-1 | 20 | `192.168.20.1/24` | `255.255.255.0` | `192.168.20.254` |
| PC-Alumno-Lab1-2 | 20 | `192.168.20.2/24` | `255.255.255.0` | `192.168.20.254` |
| PC-Alumno-Lab1-3 | 20 | `192.168.20.3/24` | `255.255.255.0` | `192.168.20.254` |
| PC-Alumno-Lab2-1 | 20 | `192.168.20.4/24` | `255.255.255.0` | `192.168.20.254` |
| PC-Alumno-Lab2-2 | 20 | `192.168.20.5/24` | `255.255.255.0` | `192.168.20.254` |
| PC-Alumno-Lab2-3 | 20 | `192.168.20.6/24` | `255.255.255.0` | `192.168.20.254` |
| PC-Direccion-Lab1 | 30 | `192.168.30.1/24` | `255.255.255.0` | `192.168.30.254` |
| PC-Direccion-Lab2 | 30 | `192.168.30.2/24` | `255.255.255.0` | `192.168.30.254` |
| PC-Gestion | 99 | `192.168.99.4/24` | `255.255.255.0` | `192.168.99.254` |

>  **Tip de Packet Tracer:** En cada PC ve a **Desktop → IP Configuration → Static**. Introduce la dirección IP, la máscara y el gateway indicados en la tabla para habilitar el tráfico.


------------------------------------------------------------------------

## 4. Asignar nombre a los dispositivos con las iniciales LuisMGL

Ejecuta en cada dispositivo, en modo privilegiado y luego en
configuración global:

### Router --- `R1-Core-LuisMGL`
```bash
Router>enable
Router#configure terminal
Enter configuration commands, one per line.  End with CNTL/Z.
Router(config)#hostname R1-Core-LuisMGL
R1-Core-LuisMGL(config)#
```
<img width="446" height="80" alt="4 1-asig-nom-R1-core" src="https://github.com/user-attachments/assets/503e28ea-f431-457f-a70e-e0f770f73dad" />

### Switch central --- `SW-Core-LuisMGL`
```bash
Switch>enable
Switch#configure terminal
Enter configuration commands, one per line.  End with CNTL/Z.
Switch(config)#hostname SW-Core-LuisMGL
SW-Core-LuisMGL(config)#
```
<img width="430" height="71" alt="4 2-asig_nom_SW_Core" src="https://github.com/user-attachments/assets/ffef3c61-43e8-4d24-a1e4-a11c92ca3f8e" />

### Switch de acceso 1 --- `SW-Lab1-LuisMGL`

```bash
Switch>enable
Switch#configure terminal
Enter configuration commands, one per line.  End with CNTL/Z.
Switch(config)#hostname SW-Lab1-LuisMGL
SW-Lab1-LuisMGL(config)#
```
<img width="453" height="67" alt="4 3-asig_nom_SW_lab_1" src="https://github.com/user-attachments/assets/72f1d816-860f-47e6-b111-5d6eb5b023c1" />

### Switch de acceso 2 --- `SW-Lab2-LuisMGL`
```bash
Switch>enable
Switch#configure terminal
Enter configuration commands, one per line.  End with CNTL/Z.
Switch(config)#hostname SW-Lab2-LuisMGL
SW-Lab2-LuisMGL(config)#
```
<img width="445" height="63" alt="4 4-asig_nom_SW_lab_2" src="https://github.com/user-attachments/assets/2b22a326-7159-4413-bea9-fe948e296597" />

## 5. Configuración básica de seguridad en router y switches
Ejecuta en **router y switchS**, después de establecer el
`hostname`:

```bash
enable
config
enable secret MODULO_PREFERIDO_MANEJOTE
service password-encryption
banner motd #ACCESO RESTRINGIDO: solo personal autorizado#
```
<img width="583" height="97" alt="5 3-CONTRASEÑA-SW-CORE" src="https://github.com/user-attachments/assets/a7789afa-4beb-4101-87d2-90a571965904" />

Para configurar una contraseña en la consola:

```bash
line console 0
password MODULO_PREFERIDO_MANEJOTE
login
exit
```
Para la línea VTY, destinada al acceso remoto por terminal:
```bash
Para la línea VTY, destinada al acceso remoto por terminal:
```bash
line vty 0 4
password MODULO_PREFERIDO_MANEJOTE
login
exit
```

```bash

Guarda la configuración al terminar el equipo:
```bash
end
copy running-config startup-config
```

Cuando Packet Tracer pregunte por el nombre del archivo de destino,
pulsa **Enter** para aceptar el valor predeterminado.

------------------------------------------------------------------------
## 5.5 Crear las VLAN 10, 20, 30, 99, 111 y 999

Crea las VLAN en **los tres switches** (`SW-Core-LuisMGL`, `SW-Lab1-LuisMGL` y
`SW-Lab2-LuisMGL`).

```bash
configure terminal
vlan 10
 name Administracion
exit
vlan 20
 name Laboratorios
exit
vlan 30
 name Direccion
exit
vlan 99
 name Gestion
exit
vlan 111
 name Nativa
exit
vlan 999
 name Blackhole
exit
end
```
<img width="476" height="349" alt="5 5VLANS-SW" src="https://github.com/user-attachments/assets/651b02e2-5d4d-47ae-8a6b-31f3ce86bcd8" />

Verifica la creación:

```bash
show vlan brief
```
<img width="618" height="304" alt="SH-VLAN-BRIEF-SWITCHS" src="https://github.com/user-attachments/assets/c706e9be-e2c5-43c8-84d3-cdca67d483f8" />

Comprueba que aparezcan las seis VLAN. La VLAN 999 se usará para los
puertos que no estén en uso; no asignes a ella los puertos conectados a
PCs ni los enlaces troncales.

------------------------------------------------------------------------

## 6. Asignar los puertos a las VLAN

### 6.1 SW-Lab1-LuisMGL

IRAN A:

-   `Fa0/1` a `Fa0/3`: Administración, VLAN 10.
-   `Fa0/4` a `Fa0/6`: Laboratorios/Alumnos, VLAN 20.
-   `Fa0/7`: Dirección, VLAN 30.

```bash
SW-Lab1-LuisMGL#configure terminal
Enter configuration commands, one per line.  End with CNTL/Z.
SW-Lab1-LuisMGL(config)#interface range fastEthernet 0/1-3
SW-Lab1-LuisMGL(config-if-range)# switchport mode access
SW-Lab1-LuisMGL(config-if-range)# switchport access vlan 10
SW-Lab1-LuisMGL(config-if-range)#exit
SW-Lab1-LuisMGL(config)#interface range fastEthernet 0/4-6
SW-Lab1-LuisMGL(config-if-range)# switchport mode access
SW-Lab1-LuisMGL(config-if-range)# switchport access vlan 20
SW-Lab1-LuisMGL(config-if-range)#exit
SW-Lab1-LuisMGL(config)#interface fastEthernet 0/7
SW-Lab1-LuisMGL(config-if)# switchport mode access
SW-Lab1-LuisMGL(config-if)# switchport access vlan 30
SW-Lab1-LuisMGL(config-if)#exit
SW-Lab1-LuisMGL(config)#end
```
<img width="467" height="194" alt="6 1-ASIGNAR-PUERTOS-SW-LAB1" src="https://github.com/user-attachments/assets/07eb93d5-ea74-4021-b48d-ab2457ae1df8" />

### 6.2 SW-Lab2-LuisMGL

```bash
SW-Lab2-LuisMGL#configure terminal
Enter configuration commands, one per line.  End with CNTL/Z.
SW-Lab2-LuisMGL(config)#interface range fastEthernet 0/1-3
SW-Lab2-LuisMGL(config-if-range)# switchport mode access
SW-Lab2-LuisMGL(config-if-range)# switchport access vlan 10
SW-Lab2-LuisMGL(config-if-range)#exit
SW-Lab2-LuisMGL(config)#interface range fastEthernet 0/4-6
SW-Lab2-LuisMGL(config-if-range)# switchport mode access
SW-Lab2-LuisMGL(config-if-range)# switchport access vlan 20
SW-Lab2-LuisMGL(config-if-range)#exit
SW-Lab2-LuisMGL(config)#interface fastEthernet 0/7
SW-Lab2-LuisMGL(config-if)# switchport mode access
SW-Lab2-LuisMGL(config-if)# switchport access vlan 30
SW-Lab2-LuisMGL(config-if)#exit
SW-Lab2-LuisMGL(config)#end
SW-Lab2-LuisMGL#
%SYS-5-CONFIG_I: Configured from console by console
```
<img width="475" height="229" alt="6 2-ASIGNAR-PUERTOS-SW-LAB2" src="https://github.com/user-attachments/assets/66c293a6-dd5d-4c3a-9c40-ee7e5221a6b5" />

### 6.3 SW-Core-LuisMGL: PC de gestión

Coloca la PC de gestión en `Fa0/9`, VLAN 99.

```bash
SW-Core-LuisMGL#configure terminal
Enter configuration commands, one per line.  End with CNTL/Z.
SW-Core-LuisMGL(config)#interface fastEthernet 0/9
SW-Core-LuisMGL(config-if)# switchport mode access
SW-Core-LuisMGL(config-if)# switchport access vlan 99
SW-Core-LuisMGL(config-if)# no shutdown
SW-Core-LuisMGL(config-if)#exit
SW-Core-LuisMGL(config)#end
```
<img width="453" height="108" alt="6 3-ASIGNAR-PUERTOS-SW-CORE" src="https://github.com/user-attachments/assets/fd112989-440a-48d4-a71e-cace471d08a7" />
# Quedaria de la siguiente manera
<img width="892" height="670" alt="5 6-VLANS" src="https://github.com/user-attachments/assets/1234d0ed-2a6d-478d-bfa8-19467b244b0f" />

**No asignes otros puertos de acceso del SW-Core a una VLAN de usuario
sin que corresponda a un dispositivo del diagrama.** Los puertos del
núcleo que conectan con el router y con los switches de laboratorio se
configurarán como troncales en el siguiente apartado.

### 6.4 Verificar la pertenencia a VLAN

En cada switch:

```bash
show vlan brief
```

<img width="564" height="295" alt="6 4 1-VERIFICACION-DE-PERTENECIA-DE-VLANS-SW-CORE" src="https://github.com/user-attachments/assets/aed0edf5-fd74-4c70-935f-8997373eef2b" />
<img width="586" height="268" alt="6 4 2-VERIFICACION-DE-PERTENECIA-DE-VLANS-SW-LAB1" src="https://github.com/user-attachments/assets/7b23a6ac-ce6a-4d9f-a721-5395a4252a63" />
<img width="610" height="269" alt="6 4 3-VERIFICACION-DE-PERTENECIA-DE-VLANS-SW-LAB2" src="https://github.com/user-attachments/assets/0abf5210-3dab-4894-a699-09e0e7426a5c" />

Comprueba que `Fa0/1-Fa0/3`, `Fa0/4-Fa0/6` y `Fa0/7` estén en las VLAN
indicadas en cada switch de laboratorio, y que `SW-Core-luismgl Fa0/9` esté
en VLAN 99.

------------------------------------------------------------------------
## 7. Habilitar los enlaces troncales

La VLAN nativa requerida es la **VLAN 111**. Configura los puertos que
conectan switch con switch y el puerto del SW-Core que conecta al router
como troncales, permitiendo las VLAN 10, 20, 30, 99 y 111.

### 7.1 SW-Core-LuisMGL

```bash
SW-Core-LuisMGL(config)#interface Gig0/1
SW-Core-LuisMGL(config-if)#switchport mode trunk
SW-Core-LuisMGL(config-if)# switchport trunk native vlan 111
SW-Core-LuisMGL(config-if)# switchport trunk allowed vlan 10,20,30,99,111
SW-Core-LuisMGL(config-if)# no shutdown
SW-Core-LuisMGL(config-if)#exit
SW-Core-LuisMGL(config)#interface f0/24
SW-Core-LuisMGL(config-if)# switchport mode trunk

SW-Core-LuisMGL(config-if)# switchport trunk native vlan 111
SW-Core-LuisMGL(config-if)# switchport trunk allowed vlan 10,20,30,99,111
SW-Core-LuisMGL(config-if)# no shutdown
SW-Core-LuisMGL(config-if)#exit
SW-Core-LuisMGL(config)#interface f0/23
SW-Core-LuisMGL(config-if)# switchport mode trunk

SW-Core-LuisMGL(config-if)# switchport trunk native vlan 111
SW-Core-LuisMGL(config-if)# switchport trunk allowed vlan 10,20,30,99,111
SW-Core-LuisMGL(config-if)# no shutdown
SW-Core-LuisMGL(config-if)#exit
SW-Core-LuisMGL(config)#end
%LINEPROTO-5-UPDOWN: Line protocol on Interface FastEthernet0/24, changed state to down

%LINEPROTO-5-UPDOWN: Line protocol on Interface FastEthernet0/24, changed state to up

%LINEPROTO-5-UPDOWN: Line protocol on Interface FastEthernet0/23, changed state to down

%LINEPROTO-5-UPDOWN: Line protocol on Interface FastEthernet0/23, changed state to up

SW-Core-LuisMGL#
%SYS-5-CONFIG_I: Configured from console by console
```
<img width="627" height="273" alt="7 1-enloace-troncal-sw-core" src="https://github.com/user-attachments/assets/aabd54b2-076a-4026-a464-a76608c679ec" />

Ejemplo de sustitución: si el cable hacia SW-Lab1 está conectado a
`GigabitEthernet0/1`, escribe `interface gigabitEthernet 0/1` en lugar
de `interface <INTERFAZ_LAB1>`. **No copies literalmente los marcadores
`<...>` en la CLI.**

### 7.2 SW-Lab1-LuisMGL

Por el puerto que conecta al SW-Core.

```bash
SW-Lab1-LuisMGL#configure terminal
Enter configuration commands, one per line.  End with CNTL/Z.
SW-Lab1-LuisMGL(config)#interface fa0/24
SW-Lab1-LuisMGL(config-if)# switchport mode trunk
SW-Lab1-LuisMGL(config-if)# switchport trunk native vlan 111
SW-Lab1-LuisMGL(config-if)# switchport trunk allowed vlan 10,20,30,99,111
SW-Lab1-LuisMGL(config-if)# no shutdown
SW-Lab1-LuisMGL(config-if)#exit
SW-Lab1-LuisMGL(config)#end
SW-Lab1-LuisMGL#
%SYS-5-CONFIG_I: Configured from console by console
```
<img width="538" height="175" alt="7 2-enlace-troncal-sw-lab1" src="https://github.com/user-attachments/assets/5953991a-2306-4e81-b8a8-1ca8d3b49587" />

### 7.3 SW-Lab2-LuisMGL
Por el puerto que conecta al SW-Core.

```bash
SW-Lab2-LuisMGL#configure terminal
Enter configuration commands, one per line.  End with CNTL/Z.
SW-Lab2-LuisMGL(config)#interface fa0/23
SW-Lab2-LuisMGL(config-if)# switchport mode trunk
SW-Lab2-LuisMGL(config-if)# switchport trunk native vlan 111
SW-Lab2-LuisMGL(config-if)# switchport trunk allowed vlan 10,20,30,99,111
SW-Lab2-LuisMGL(config-if)# no shutdown
SW-Lab2-LuisMGL(config-if)#exit
SW-Lab2-LuisMGL(config)#end
SW-Lab2-LuisMGL#
%SYS-5-CONFIG_I: Configured from console by console

```
<img width="554" height="152" alt="7 3-enlace-troncal-sw-lab2" src="https://github.com/user-attachments/assets/92b41d8c-6844-41bb-b27c-888eb918822d" />

> Si el modelo de switch seleccionado no admite alguno de los comandos
> `switchport` mostrados, verifica el modelo y las capacidades de la
> interfaz en Packet Tracer. No cambies la topología para ocultar el
> error.

### 7.4 Verificar los troncales
En cada switch:

```bash
show interfaces trunk
show interfaces <PUERTO_TRONCAL> switchport
```
<img width="610" height="485" alt="7 4-verificacion-trocal-lab2" src="https://github.com/user-attachments/assets/182062fe-e06c-4941-8964-9216572af692" />
<img width="469" height="319" alt="7 4-verificacion-trocal-lab1" src="https://github.com/user-attachments/assets/5c168ae2-92a9-4e3b-8b7d-8cd4a3956718" />
<img width="542" height="470" alt="7 4-verificacion-trocal-core" src="https://github.com/user-attachments/assets/24689cc4-8a8f-432c-bd6a-14acc6124e26" />

Comprueba que los enlaces aparezcan como troncales, que la VLAN nativa
sea 111 y que la lista permitida incluya `10,20,30,99,111`.

------------------------------------------------------------------------
## 8. Configurar las SVI de administración y el gateway de los switches

La VLAN 99 se usa para administrar los switches. Configura las
siguientes direcciones.

### 8.1 SW-Core-LuisMGL --- primera IP utilizable

```bash
SW-Core-LuisMGL#configure terminal
Enter configuration commands, one per line.  End with CNTL/Z.
SW-Core-LuisMGL(config)#interface vlan 99
SW-Core-LuisMGL(config-if)# ip address 192.168.99.1 255.255.255.0
SW-Core-LuisMGL(config-if)# no shutdown
SW-Core-LuisMGL(config-if)#exit
SW-Core-LuisMGL(config)#ip default-gateway 192.168.99.254
SW-Core-LuisMGL(config)#end
```
<img width="590" height="108" alt="8 1-SW-CORE-PRIMERA-IP-UTILIZABLE" src="https://github.com/user-attachments/assets/b973e602-c50b-43c9-a1a9-c97a8461983b" />

### 8.2 SW-Lab1-LuisMGL --- segunda IP utilizable

```bash
SW-Lab1-LuisMGL#configure terminal
Enter configuration commands, one per line.  End with CNTL/Z.
SW-Lab1-LuisMGL(config)#interface vlan 99
SW-Lab1-LuisMGL(config-if)# ip address 192.168.99.2 255.255.255.0
SW-Lab1-LuisMGL(config-if)# no shutdown
SW-Lab1-LuisMGL(config-if)#exit
SW-Lab1-LuisMGL(config)#ip default-gateway 192.168.99.254
SW-Lab1-LuisMGL(config)#end
```
<img width="519" height="152" alt="8 2-SW-LAB1-SEGUNDA-IP-UTILIZABLE" src="https://github.com/user-attachments/assets/a34b2fb8-bfef-4af1-9ff5-3db5c75e3665" />

### 8.3 SW-Lab2-LuisMGL --- tercera IP utilizable

```bash
SW-Lab2-LuisMGL#configure terminal
Enter configuration commands, one per line.  End with CNTL/Z.
SW-Lab2-LuisMGL(config)#interface vlan 99
SW-Lab2-LuisMGL(config-if)# ip address 192.168.99.3 255.255.255.0
SW-Lab2-LuisMGL(config-if)# no shutdown
SW-Lab2-LuisMGL(config-if)#exit
SW-Lab2-LuisMGL(config)#ip default-gateway 192.168.99.254
SW-Lab2-LuisMGL(config)#end
%LINK-5-CHANGED: Interface Vlan99, changed state to up
```
<img width="639" height="187" alt="8 3-SW-LAB2-TERCERA-IP-UTILIZABLE" src="https://github.com/user-attachments/assets/900c98b4-da3b-4ccf-9fa4-52548d6afdb8" />

## 8.4 Verifica en cada switch:

```bash
show ip interface brief
show running-config
```
### SW-Core-LuisMGL
<img width="462" height="467" alt="8 4 2-SW-CORE-SH-RUNNIG-CONFIG" src="https://github.com/user-attachments/assets/4ef3f079-0f1a-406a-a88c-fbcefcc5caed" />
<img width="571" height="314" alt="8 4 1-SW-CORE-SH-IPINTERFACE-BRIEF" src="https://github.com/user-attachments/assets/27d95c10-46df-489c-acdc-bb6b04297b9b" />
### SW-LAB1-LuisMGL
<img width="583" height="311" alt="8 4 4-SW-LAB1-SH-IPINTERFACE-BRIEF" src="https://github.com/user-attachments/assets/7bfecfc6-5808-47d0-905d-bcff7d4d74bb" />
<img width="481" height="432" alt="8 4 3-SW-LAB1-SH-RUNNIG-CONFIG" src="https://github.com/user-attachments/assets/e6d7a9a0-7402-45f1-a18c-5526954f1c6f" />
### SW-LAB2-LuisMGL
<img width="580" height="451" alt="8 4 6-SW-LAB2-SH-RUNNIG-CONFIG" src="https://github.com/user-attachments/assets/2d4ed750-af61-4765-9629-341b46cc310d" />
<img width="603" height="309" alt="8 4 5-SW-LAB2-SH-IPINTERFACE-BRIEF" src="https://github.com/user-attachments/assets/071563e6-ada5-4ab0-834a-b8bb536a8677" />

INVESTIGAR SHOW RUNNING-CONFIG

La SVI puede permanecer `down` hasta que la VLAN exista y haya al menos
un puerto activo que transporte esa VLAN. Comprueba también los enlaces
y la VLAN 99 antes de diagnosticar una dirección IP.

------------------------------------------------------------------------
## 9. Configurar los puertos inactivos en VLAN 999 y apagarlos
Usar VLAN 999 para puertos inactivos y apagarlos.
Aplica este procedimiento en cada switch **solo a los puertos que
confirmes que no están conectados a equipos ni se usan como enlaces**.
No incluyas puertos de PCs, el puerto `Fa0/9` del PC de gestión ni los
enlaces troncales.

### 9.1 SW-Core-LuisMGL
```bash
SW-Core-LuisMGL#configure terminal
SW-Core-LuisMGL(config)#interface range fa0/1-8,fa0/10-22,gi0/2
SW-Core-LuisMGL(config-if-range)#switchport mode access
SW-Core-LuisMGL(config-if-range)#switchport access vlan 999
SW-Core-LuisMGL(config-if-range)#shutdown
SW-Core-LuisMGL(config-if-range)#exit
SW-Core-LuisMGL(config)#end
```
<img width="1045" height="792" alt="9 1 1 1-SW-CORE-CERRANDO-PUERTOS" src="https://github.com/user-attachments/assets/38451b7b-8547-4766-b27d-f69dd1ef0d33" />


### 9.2 SW-Lab1-LuisMGL
```bash
SW-Lab1-LuisMGL#configure terminal
Enter configuration commands, one per line.  End with CNTL/Z.
SW-Lab1-LuisMGL(config)#interface range fa0/8-23,gi0/1,gi0/2
SW-Lab1-LuisMGL(config-if-range)#switchport mode access
SW-Lab1-LuisMGL(config-if-range)#switchport access vlan 999
SW-Lab1-LuisMGL(config-if-range)#shutdown
SW-Lab1-LuisMGL(config-if-range)#exit
SW-Lab1-LuisMGL(config)#end
SW-Lab1-LuisMGL#
```
<img width="848" height="690" alt="9 2 1 1-SW-LAB1-CERRANDO-PUERTOS" src="https://github.com/user-attachments/assets/72c82fed-4a30-4780-8f6e-2f27528033e5" />


### 9.3 SW-Lab2-LuisMGL
```bash
SW-Lab2-LuisMGL#configure terminal
Enter configuration commands, one per line.  End with CNTL/Z.
SW-Lab2-LuisMGL(config)#interface range fa0/8-22,fa0/24,gi0/1,gi0/2
SW-Lab2-LuisMGL(config-if-range)#switchport mode access
SW-Lab2-LuisMGL(config-if-range)#switchport access vlan 999
SW-Lab2-LuisMGL(config-if-range)#shutdown
SW-Lab2-LuisMGL(config-if-range)#exit
SW-Lab2-LuisMGL(config)#end
```
<img width="735" height="687" alt="9 3 1 1-SW-LAB2-CERRANDO-PUERTOS" src="https://github.com/user-attachments/assets/c99abebc-9871-4e36-9835-5123d133504f" />

## 9.4 Verifica:

```bash
show vlan brief
show interfaces status
```
# SW-Core-LuisMGL
<img width="730" height="732" alt="9 4 2 1-SW-CORE-VERIFICACION-PUERTOS" src="https://github.com/user-attachments/assets/dd5927c6-7b00-444f-985a-c2680bdcb80b" />

# SW-Lab1-LuisMGL
<img width="722" height="730" alt="9 4 2 2-SW-LAB1-VERIFICACION-PUERTOS" src="https://github.com/user-attachments/assets/8ca265ab-4b97-4d5b-a5e4-e1d9f1dbef4a" />

# SW-Lab2-LuisMGL
<img width="658" height="722" alt="9 4 2 3-SW-LAB2-VERIFICACION-PUERTOS" src="https://github.com/user-attachments/assets/3f018550-d4e9-4606-9feb-bdc2e36f59db" />

------------------------------------------------------------------------

# 10. Configurar las subinterfaces en R1-Core-LMGL

El router usa la interfaz física `GigabitEthernet0/0/0` hacia el
SW-Core. El método solicitado es **Router-on-a-Stick**: una subinterfaz
por VLAN en la misma interfaz física, con encapsulamiento IEEE 802.1Q.

Las últimas IP utilizables de las subredes asignadas son las puertas de
enlace: `192.168.10.254`, `192.168.20.254`, `192.168.30.254` y
`192.168.99.254`.

```bash

R1-Core-LuisMGL>ENABLE
Password: 
Password: 
R1-Core-LuisMGL#configure terminal
Enter configuration commands, one per line.  End with CNTL/Z.
R1-Core-LuisMGL(config)#interface gi 0/0
R1-Core-LuisMGL(config-if)#no shutdown

R1-Core-LuisMGL(config-if)#exit
R1-Core-LuisMGL(config)#
R1-Core-LuisMGL(config)#interface gi 0/0.10
R1-Core-LuisMGL(config-subif)#encapsulation dot1Q 10
R1-Core-LuisMGL(config-subif)#ip address 192.168.10.254 255.255.255.0
R1-Core-LuisMGL(config-subif)#exit
R1-Core-LuisMGL(config)#
R1-Core-LuisMGL(config)#interface gi 0/0.20
R1-Core-LuisMGL(config-subif)#encapsulation dot1Q 20
R1-Core-LuisMGL(config-subif)#ip address 192.168.20.254 255.255.255.0
R1-Core-LuisMGL(config-subif)#exit
R1-Core-LuisMGL(config)#
R1-Core-LuisMGL(config)#interface gi 0/0.30
R1-Core-LuisMGL(config-subif)#encapsulation dot1Q 30
R1-Core-LuisMGL(config-subif)#ip address 192.168.30.254 255.255.255.0
R1-Core-LuisMGL(config-subif)#exit
R1-Core-LuisMGL(config)#
R1-Core-LuisMGL(config)#interface gi 0/0.99
R1-Core-LuisMGL(config-subif)#encapsulation dot1Q 99
R1-Core-LuisMGL(config-subif)#ip address 192.168.99.254 255.255.255.0
R1-Core-LuisMGL(config-subif)#exit
R1-Core-LuisMGL(config)#
R1-Core-LuisMGL(config)#interface gi 0/0.111
R1-Core-LuisMGL(config-subif)#encapsulation dot1Q 111 native
R1-Core-LuisMGL(config-subif)#no ip address
R1-Core-LuisMGL(config-subif)#exit
R1-Core-LuisMGL(config)#end
```

La subinterfaz `.111`. No se le asigna dirección IP
porque no tiene una subred para VLAN 111, no se usa
como gateway de hosts en esta práctica.

Verifica las interfaces:

``` text
show ip interface brief
show running-config
```
<img width="443" height="808" alt="10 1 2-verificacion" src="https://github.com/user-attachments/assets/f07803eb-1538-4827-955a-64cce50270f1" />
<img width="706" height="182" alt="10 1 1-verificacion-show-ip-interface-bief" src="https://github.com/user-attachments/assets/120dc8ed-0f3a-4a86-b588-987b7127f2d6" />

Las subinterfaces deben quedar habilitadas cuando la interfaz física
esté activa y el enlace troncal esté correctamente configurado.

------------------------------------------------------------------------
## 11. Asignar direccionamiento estático a los hosts

En cada PC, abre **Desktop → IP Configuration → Static** e introduce la
IP, la máscara y el gateway de la Tabla B.

<img width="217" height="230" alt="11 1 1-ingreso-a-la-pc" src="https://github.com/user-attachments/assets/36ae8a2b-7b5e-471f-bc29-8d3c66fbba6c" />



Ejemplo para una PC de Administración:

-   IPv4 Address: `192.168.10.1`
-   Subnet Mask: `255.255.255.0`
-   Default Gateway: `192.168.10.254`
<img width="895" height="275" alt="11 1 2-ingreso-ip-gatwey-mascara" src="https://github.com/user-attachments/assets/f1e2a0e1-c12a-4c23-b601-b43f92b45fed" />

Ejemplo para la PC de gestión:

-   IPv4 Address: `192.168.99.4`
-   Subnet Mask: `255.255.255.0`
-   Default Gateway: `192.168.99.254`

Repite con la dirección correspondiente a cada PC en la tabla. No
dupliques direcciones IP.

------------------------------------------------------------------------

## 12. Verificar la configuración de VLAN y enlaces

Ejecuta los siguientes comandos en los switches:

``` text
show vlan brief
show interfaces trunk
show ip interface brief
```
<img width="677" height="607" alt="12 1 -VERIFICACIÓN-SW-CORE" src="https://github.com/user-attachments/assets/4c64397c-cd6b-4d8a-8517-98b668a36077" />
<img width="651" height="473" alt="12 1 2-VERIFICACIÓN-SW-CORE" src="https://github.com/user-attachments/assets/cce64fc0-415c-43e0-adad-94a461bba380" />

Ejecuta en el router:

``` text
show ip interface brief
```
<img width="713" height="197" alt="12 1 2-VERIFICACIÓN-ROUTER-CORE" src="https://github.com/user-attachments/assets/d644980f-227d-480b-9c20-0e9118662be7" />

Verifica lo siguiente:

-   Las VLAN 10, 20, 30, 99, 111 y 999 existen en los tres switches.
-   Los puertos de acceso están en la VLAN correspondiente.
-   Los enlaces troncales permiten las VLAN 10, 20, 30, 99 y 111.
-   La VLAN nativa de cada troncal es 111.
-   Las SVI de gestión usan `192.168.99.1`, `.2` y `.3`.
-   Las subinterfaces del router tienen las direcciones indicadas en la
    Tabla A.

------------------------------------------------------------------------

## 13. Verificar conectividad con Ping

Las pruebas de conectividad se pueden verificar mediante la consola tradicional o a través de la interfaz gráfica de Packet Tracer utilizando el sistema de simulación de paquetes.

### 13.1 Métodos de Validación en Tiempo Real

#### Método A: Consola CLI (Command Prompt)
Desde el entorno de escritorio de cualquier Host origen, se puede ejecutar la herramienta estándar ICMP hacia las puertas de enlace o equipos remotos:

```bash
# Ejemplo de prueba hacia los gateways desde hosts respectivos
ping 192.168.10.254
ping 192.168.20.254
ping 192.168.30.254
ping 192.168.99.254
```
# O

Para verificar la conectividad y el enrutamiento entre tus VLANs sin usar la terminal de los equipos, puedes usar la herramienta del **sobrecito** (**Simple PDU**). Sigue estos pasos:

### 🛠️ Pasos para realizar la prueba en Tiempo Real:

1. **Selecciona la herramienta:** Presiona la tecla **`P`** en tu teclado o haz clic en el icono del **sobre cerrado** en la barra de herramientas lateral derecha.
2. **Elige el origen:** Haz clic sobre la computadora desde la cual quieres mandar el ping (por ejemplo, `PC-1`).
3. **Elige el destino:** Haz clic sobre la computadora de la misma vlan (por ejemplo, `PC-2`).
4. **Verifica el resultado:** Revisa la esquina inferior derecha de Packet Tracer en la ventana **Ventas / Escenarios**:
   * Si dice **`Successful`**, ¡tu enrutamiento entre VLANs funciona perfectamente!
   * Si dice **`Failed`**, revisa que las subinterfaces del router y el enlace troncal del switch estén bien configurados.
Ejecuta solamente el ping correspondiente a la VLAN configurada en esa
PC.
<img width="778" height="40" alt="13 1 2-VERIFICACIÓN-ping" src="https://github.com/user-attachments/assets/ab20c583-57ed-45e5-9234-c8c6ccb64f6e" />

### 13.2 Pruebas inter-VLAN
Esta prueba verifica que el **Router-on-a-Stick** está funcionando. El paquete sale de una VLAN, sube al router a través del enlace troncal por una subinterfaz, el router lo cambia de red y lo baja por otra subinterfaz hacia la VLAN de destino.

Desde una PC de Administración (por ejemplo `192.168.10.1`), prueba una
PC de Laboratorios y otra de Dirección:

``` text
ping 192.168.20.1
ping 192.168.30.1
```

Desde la PC de gestión (`192.168.99.4`), prueba el gateway y una PC de
otra VLAN:

``` text
ping 192.168.99.254
ping 192.168.10.1
```
# o
### 🛠️ Pasos para realizar la prueba en Tiempo Real:

1. **Selecciona la herramienta:** Presiona la tecla **`P`** en tu teclado o haz clic en el icono del **sobre cerrado** en la barra de herramientas lateral derecha.
2. **Origen:** Una computadora en una VLAN (ej. `PC-VLAN10`).
3. **Destino:** Una computadora en una VLAN **diferente** (ej. `PC-VLAN20`).**Resultado esperado:** 
4. **1er intento:** **`Failed`** (Normal, debido al proceso de ARP entre el router y las PCs).
5 **2do intento:** **`Successful`** (Obligatorio para dar por buena la configuración).
6 **Qué demuestra:** Que el enlace troncal (`trunk`), la encapsulación `dot1Q` y las direcciones IP de las subinterfaces del router están operando al 100%.
Si el primer ping falla, repítelo una vez: Packet Tracer puede necesitar
resolver ARP inicialmente. Registra los resultados reales; no marques
como exitosas pruebas que no hayas realizado.
<img width="772" height="43" alt="13 1 2-VERIFICACIÓN-ping-inter-vlan" src="https://github.com/user-attachments/assets/e8d38eb3-75ec-48fe-b3e1-27a832d98ae8" />

## Si un ping falla

1.  Confirma que la PC tiene IP, máscara y gateway correctos.
2.  Ejecuta `show vlan brief` para verificar la VLAN del puerto.
3.  Ejecuta `show interfaces trunk` para comprobar los enlaces
    troncales, las VLAN permitidas y la VLAN nativa.
4.  Ejecuta `show ip interface brief` en el router para revisar la
    interfaz física y las subinterfaces.
5.  Revisa que cada subinterfaz tenga `encapsulation dot1Q` con el ID de
    VLAN correcto.
6.  Vuelve a probar el ping y registra qué corregiste.

------------------------------------------------------------------------

## 14. Guardar la configuración

En el router y en cada switch, ejecuta:

```bash
R1-Core-LuisMGL#wr(que significa write memory)
Building configuration...
[OK]
R1-Core-LuisMGL#

```

Guarda el archivo de Packet Tracer mediante **File → Save As** con un
nombre claro, por ejemplo:

`Etapa1_Infraestructura_LMGL.pkt`

------------------------------------------------------------------------

## 15. Glosario de comandos de Cisco IOS

A continuación se detalla una investigación y resumen de cada uno de los comandos utilizados a lo largo de este proyecto en la CLI de Cisco, clasificados por su función operativa:

### ⚙️ Modos de Acceso y Configuración
*   **`enable`:** Cambia el entorno operativo del modo Usuario ("`>`") al modo Privilegiado o modo Root ("`#`"), solicitando contraseña si está configurada.
*   **`configure terminal`:** Permite el ingreso desde el modo Privilegiado al modo de Configuración Global (`(config)#`), el cual es obligatorio para realizar modificaciones en el sistema.
*   **`interface <tipo/número>`:** Cambia el prompt al modo de configuración de interfaz (`(config-if)#`) para aplicar parámetros físicos o lógicos a un puerto específico (Ej: `interface fastEthernet 0/7`).
*   **`interface range <tipo/rango>`:** Permite agrupar múltiples puertos físicos para configurarlos de forma simultánea, optimizando el tiempo de despliegue (Ej: `interface range fa0/1-3`).
*   **`exit`:** Retrocede un nivel exacto en la jerarquía de menús de la CLI de Cisco IOS.
*   **`end`:** Cancela inmediatamente cualquier modo de configuración profunda y regresa al prompt raíz del modo Privilegiado (`#`).

### 🔒 Comandos de Seguridad Básica
*   **`hostname <nombre>`:** Asigna un nombre de identificación único al dispositivo en la red.
*   **`enable secret <contraseña>`:** Configura una contraseña cifrada con un algoritmo fuerte para proteger el acceso al modo Privilegiado.
*   **`service password-encryption`:** Cifra en texto plano todas las contraseñas guardadas en el archivo de configuración (como las de consola y VTY) para que no sean visibles al ejecutar un `show running-config`.
*   **`banner motd #<mensaje>#`:** Configura un aviso legal visible de "Mensaje del Día" que se despliega inmediatamente antes de que cualquier usuario intente iniciar sesión en el equipo.
*   **`line console 0`:** Permite ingresar al modo de configuración del puerto físico de consola para establecer directivas de acceso local.
*   **`line vty 0 4`:** Permite ingresar al modo de configuración de las líneas de terminal virtuales (Virtual Teletype) para administrar el acceso remoto por Telnet o SSH.
*   **`password <contraseña>`:** Asigna la clave que se solicitará al intentar ingresar por la línea física o virtual seleccionada.
*   **`login`:** Instruye explícitamente al dispositivo a solicitar y validar la contraseña configurada en la línea de acceso antes de permitir la entrada al sistema.

### 🌐 Configuración de VLANs y Conectividad (Capa 2 y Capa 3)
*   **`vlan <id>`:** Accede a la base de datos de VLANs del switch y crea o edita el identificador numérico seleccionado.
*   **`name <nombre>`:** Asigna una etiqueta de texto descriptiva a la VLAN seleccionada para facilitar la administración de la red.
*   **`switchport mode access`:** Define un puerto del switch en modo de acceso estático, configurándolo para conectar exclusivamente dispositivos finales (como PCs).
*   **`switchport access vlan <id>`:** Asigna y amarra el puerto de acceso a una VLAN específica para aislar su tráfico.
*   **`switchport mode trunk`:** Establece la interfaz en modo troncal para permitir que el puerto transmita y reciba tráfico de múltiples VLANs simultáneamente.
*   **`switchport trunk native vlan <id>`:** Define qué VLAN procesará el puerto troncal como tráfico nativo (tráfico sin etiquetar), mitigando vulnerabilidades de salto de VLAN.
*   **`switchport trunk allowed vlan <lista>`:** Aplica un filtro estricto de seguridad en el enlace troncal para especificar únicamente qué IDs de VLAN tienen autorización de cruzar por dicho puerto.
*   **`no shutdown`:** Enciende de forma lógica una interfaz física o subinterfaz, cambiando su estado administrativo a activo (*up*).
*   **`shutdown`:** Deshabilita de forma lógica y apaga un puerto, una SVI o un rango de interfaces, como medida de protección para puertos inactivos.
*   **`encapsulation dot1Q <vlan> [native]`:** Habilita el protocolo de etiquetado estándar de la industria IEEE 802.1Q en una subinterfaz de router, enlazándola a un ID de VLAN y definiendo si operará como nativa.
*   **`ip address <dirección> <máscara>`:** Asigna de forma estática una dirección IPv4 y su correspondiente máscara de subred a una interfaz lógica, subinterfaz o SVI de gestión.
*   **`ip default-gateway <dirección>`:** Configura la puerta de enlace predeterminada en un switch de Capa 2 para permitir su administración IP desde subredes externas.

### 📊 Comandos de Diagnóstico, Verificación y Almacenamiento
*   **`show running-config`:** Extrae y despliega en pantalla la configuración actual guardada en la memoria RAM volátil del dispositivo.
*   **`show vlan brief`:** Genera un resumen conciso de la tabla de VLANs del switch, mostrando los nombres de las redes activas y sus puertos de acceso asociados.
*   **`show interfaces trunk`:** Muestra detalladamente los puertos troncales operativos, el protocolo de encapsulación utilizado, la VLAN nativa y los IDs permitidos en el enlace.
*   **`show ip interface brief`:** Despliega una tabla compacta con el estado físico y operativo de todas las interfaces y subinterfaces del equipo, junto con sus direcciones IP configuradas.
*   **`show interfaces status`:** Muestra de forma rápida el estado de conexión de todos los puertos físicos del switch, especificando su velocidad, modo dúplex y VLAN actual.
*   **`ping <dirección>`:** Envía paquetes de solicitud de eco ICMP hacia una IP destino para verificar la conectividad de extremo a extremo y medir los tiempos de respuesta.
*   **`copy running-config startup-config` / `wr`:** Guarda de forma permanente la configuración activa de la memoria RAM a la memoria NVRAM no volátil, evitando que se borren los datos al reiniciar el equipo.

------------------------------------------------------------------------

### 15.1 Archivo `.pkt`

[📂 Descargar Archivo Packet Tracer (1-proyecto.pkt)](./1-proyecto.pkt)

### 15.2 Diario de aprendizaje y troubleshooting

**¿Cuál fue el mayor reto técnico que enfrentaste en esta unidad?**

> El mayor reto técnico fue el diseño e implementación de las tablas de direccionamiento A y B. Aunque los errores de sintaxis en los comandos se corrigen fácilmente y sirven como aprendizaje, un solo error en el esquema de direcciones IP provoca que toda la topología y el enrutamiento dejen de funcionar por completo.

**Bitácora de errores**

*   **Error 1:** No documentar ni registrar la contraseña asignada para acceder al modo privilegiado (`MODULO_PREFERIDO_MANEJOTE`) del router.
*   **Solución 1:** Se tuvo que reiniciar el router para volver a aplicar la configuración inicial desde cero, asegurando esta vez registrar la contraseña de manera correcta.
*   **Error 2:** Copiar y pegar una contraseña en el switch que incluía por error los caracteres `< >` (los cuales comúnmente delimitan variables en las guías, pero no deben escribirse).
*   **Solución 2:** Reconfigurar la contraseña en la línea de comandos utilizando una cadena de texto limpia sin los caracteres `< >`.
*   **Error 3:** Olvidar ingresar al modo de configuración global mediante el comando `configure terminal` antes de ejecutar las instrucciones de las interfaces.
*   **Solución 3:** Revisé detalladamente la guía de pasos a seguir e identifiqué que omitir este comando impedía que el switch reconociera las configuraciones de rango, por lo que se aplicó primero para corregir el problema.


------------------------------------------------------------------------

