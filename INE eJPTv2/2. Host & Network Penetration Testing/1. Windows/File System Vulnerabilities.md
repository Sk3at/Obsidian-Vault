Alternate Data Streams (ADS)
El flujo alternativo de datos es un NTFS (New Technology File System o Nueva Tecnología de Archivos del Sistema) y fueron diseñados para proveer compatibilidad con el HFS (Hierarchical File System) de MacOS,
Todos los archivos creados con un formato NTFS van a tener dos tipos de flujo de datos:
- Flujo de datos: contiene los datos del archivo.
- Flujo de recursos: contiene los metadatos del archivos.
Un atacante puede utilizar ADS para esconder código malicioso o ejecutables en archivos legítimos con el objetivo de evadir la detección. 
Esto se logra almacenando el código malicioso en la metadata de un archivo legitimo.
Esta técnica es utilizada para evadir antivirus y herramientas de análisis estático.

