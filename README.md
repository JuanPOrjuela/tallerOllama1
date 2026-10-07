# Taller Ollama - IA local en una VM Ubuntu

Taller de Sistemas Operativos (Mg. Iván Darío Méndez Aguilera).

Integrantes: Angel Arcos, Sebastian Coral, Juan Orjuela, Javier Rosero

Instalamos Ollama en una máquina virtual Ubuntu 24.04 (VirtualBox), resolvimos los ejercicios de la guía
y armamos un asistente de ciberseguridad que corre local (AsistenteIA-VM).

## Contenido

- `Informe_Taller_Ollama_VM.pdf`: el informe con cada punto de la guía, las salidas y las capturas de la VM.
- `codigo/AsistenteIA-VM/`: la interfaz web (index.html), el Modelfile del asistente y `servir.sh`.
- `codigo/scripts/`: un script por ejercicio (e01 a e10, s02 a s12), el benchmark (`bench.py`), el experimento de temperatura y los scripts de las capturas.
- `codigo/reporte_sistema.sh`: script del ejercicio 9.

Las salidas de terminal y las capturas empiezan con:

```
cloud@ubuntu-ollama:~$ echo "Angel Arcos - Sebastian Coral - Juan Orjuela - Javier Rosero"
```

## Cómo correrlo en la VM

```bash
curl -fsSL https://ollama.com/install.sh | sh
ollama pull llama3.2:3b
cd codigo/AsistenteIA-VM
ollama create asistente-ciberseguridad -f Modelfile
./servir.sh        # y abrir http://localhost:8080 en Firefox dentro de la VM
```

Los scripts de `codigo/scripts/` esperan estar en `~/taller-ollama`; `bash codigo/rehacer.sh` los corre todos en orden.

## Notas

- VM: 4 vCPU, 6 GB de RAM, 40 GB de disco, sin GPU (Ollama corre en CPU).
- En nuestro equipo VirtualBox corre encima de Hyper-V y la VM se congelaba con 4 hilos de inferencia.
  Lo arreglamos limitando Ollama a 3 CPU con un override de systemd (`AllowedCPUs=0-2`) y `num_thread 3`. Está explicado en la sección 3.1 del informe.
- Ollama y la interfaz solo escuchan en 127.0.0.1, no quedan expuestos a la red.
