---
title:  'CXS - Instalación, configuración y ejecución'
categories: cxs
tags: server, firewall, cxs, exploit
---


## Prerrequisitos
Para la correcta instalación y ejecución es necesario contar con:

### De instalación
- Gestor de módulos: App::cpanminus.
- Librería: Archive::Zip
- Librería: Linux::Inotify2

Comandos

```sh
cpan App::cpanminus
cpanm Archive::Zip
cpanm Linux::Inotify2
```

### De ejecución

- Antivirus: ClamAV y clamd (daemon)

Primero se instala el antivirus, se actualiza su base de datos y se lo deja corriendo como daemon.

```bash
yum install -y epel-release
yum install -y clamav clamd
freshclam
service clamd start
```

### Del daemon

- Apache - ModSecurity

Debe procederse aún con la instalación de **ModSecurity** para poder dejar cxs corriendo como daemon.

## Instalación

Se realizó la descarga y descompresión del archivo en /usr/tmp/cxs

```sh
cd /usr/tmp
makedir cxs
cd cxs
wget https://download.configserver.com/cxsinstaller.tgz
tar -xzf cxsinstaller.tgz
perl cxsinstaller.pl
rm -fv cxsinstaller.*
cd ..
rmdir cxs
```

Finalmente se descargó el archivo `/etc/cxs/install.txt` para verificar temas de configuración y su posterior ejecución.

## Ejecución

Para ejecutar el CXS sobre las carpetas de los usuarios, se accede a la UI habilitada en el panel del servidor. Desde allí se accede a la opción generate command y se corre el script con las opciones por defecto.

## Fuentes

- **CXS:** [http://www.configserver.com/cp/cxsinstaller.html](http://www.configserver.com/cp/cxsinstaller.html)
- **CPAN:** [http://www.cpan.org/misc/cpan-faq.html#What_is_CPAN](http://www.cpan.org/misc/cpan-faq.html#What_is_CPAN)
- **CPAN - Gestiór de módulos:** [http://www.cpan.org/modules/INSTALL.html](http://www.cpan.org/modules/INSTALL.html)
- **CPAN - Librerías:** [http://www.linuxquestions.org/questions/slackware-14/ooo1-9-113-compile-error-archive-zib-pm-perl5-341538/](http://www.linuxquestions.org/questions/slackware-14/ooo1-9-113-compile-error-archive-zib-pm-perl5-341538/)
- **ClamAV:** [https://www.clamav.net/documents/installing-clamav#rhel](https://www.clamav.net/documents/installing-clamav#rhel)
