# Guía de instalación y configuración IOQuake

Instalación rápida en linux:

```bash
# Ubuntu / Linux mint:
$ sudo apt install ioquake
```

Compilación desde el repositorio:

```bash
sudo apt install libsdl2-2.0-0 \
  libsdl2-gfx-dev \
  libsdl2-mixer-2.0-0 \
  libsdl2-image-2.0-0 \
  libsdl2-net-2.0-0 \
  libsdl2-ttf-2.0-0

git clone git@github.com:ioquake/ioq3.git
cd ioq3
make
make copyfiles
```

**Preparación del directorio del juego**

Descargar los paquetes de extensión incluidos en: https://aao.cr/dwnld/q3/pk3s.7z


Asegurarse que los archivos pk3 de la última versión estén instalados, se pueden descargar aquí: https://ioquake3.org/extras/patch-data/

Crear la siguiente estructura en el directorio $HOME:
```
.q3a
├── baseq3
│   ├── autoexec.cfg
│   ├── pak0.pk3  >> Debe copiarse del instalador original <<
│   ├── pak1.pk3
│   ├── pak2.pk3
│   ├── pak3.pk3
│   ├── pak4.pk3
│   ├── pak5.pk3
│   ├── pak6.pk3
│   ├── pak7.pk3
│   ├── pak8.pk3
│   ├── pak9hqq36.pk3
│   ├── q3config.cfg
│   ├── q3dm17++.pk3
│   ├── settings.cfg
│   └── xcsv_bq3hi-res.pk3
└── missionpack
    ├── pak1.pk3
    ├── pak2.pk3
    └── pak3.pk3
```
**Notas**:
* En el directorio .q3a/baseq3 deben copiarse los archivos originales .pk3 y se debe ingresar un código de licencia al iniciar el juego.
* El archivo autoexec.cfg contiene la configuración de alta calidad para jugar en una resolución de 1920x1080, puede cambiar los parámetros según su configuración.

**Referencias**:
* Sitio oficinal del proyecto: https://ioquake3.org/
* Repositorio de github: https://github.com/ioquake/ioq3