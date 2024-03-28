Alternate Data Streams (ADS)
El flujo alternativo de datos es un NTFS (New Technology File System o Nueva Tecnología de Archivos del Sistema) y fueron diseñados para proveer compatibilidad con el HFS (Hierarchical File System) de MacOS,
Todos los archivos creados con un formato NTFS van a tener dos tipos de flujo de datos:
- Flujo de datos: contiene los datos del archivo.
- Flujo de recursos: contiene los metadatos del archivos.
Un atacante puede utilizar ADS para esconder código malicioso o ejecutables en archivos legítimos con el objetivo de evadir la detección. 
Esto se logra almacenando el código malicioso en la metadata de un archivo legitimo.
Esta técnica es utilizada para evadir antivirus y herramientas de análisis estático.

Para realizar esto debemos dirigirnos al directorio temp C:\\Windows\\Temp
![[../../../Images/Pasted image 20231112204634.png]]
Abrimos un cmd y podemos crear un txt secreto dentro de otro txt
![[../../../Images/Pasted image 20231112205330.png]]
![[../../../Images/Pasted image 20231112205337.png]]
![[../../../Images/Pasted image 20231112205354.png]]
Pero si abrimos el test del escritorio no vemos ese mensaje vemos
![[../../../Images/Pasted image 20231112205420.png]]
Por lo que para abrir ese secreto debemos recurrir al comando 
![[../../../Images/Pasted image 20231112205446.png]]
Por ejemplo, si tuvieramos un WinPeas64 (sirve para escalar privilegios en windows) deberiamos ocultarlo, por lo que lo ponemos dentro de la carpeta Temp. 
Ahora podemos meter el archivo dentro de uno que sea legitimo
![[../../../Images/Pasted image 20231112205857.png]]
![[../../../Images/Pasted image 20231112205912.png]]
Luego debemos modificar ese windowslog para que parezca legitimo
![[../../../Images/Pasted image 20231112205958.png]]
![[../../../Images/Pasted image 20231112210007.png]]
Eliminamos el exe que quedo en Temp ya que quedo asignado dentro de los recursos del txt
![[../../../Images/Pasted image 20231112210104.png]]
Por ultimo para ejecutar nuestro payload
![[../../../Images/Pasted image 20231112210217.png]]
![[../../../Images/Pasted image 20231112210303.png]]
![[../../../Images/Pasted image 20231112210321.png]]
Por lo que ahora cada vez que llamemos a nuestro payload deberia ejecutarse
