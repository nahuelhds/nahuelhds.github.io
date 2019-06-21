---
lang: es
title: 'CXS — Instalación, configuración y ejecución'
description: >-
  Si todavía no sabés que es ConfigServer eXploit Scanner, básicamente es la
  salvación para la seguridad de cualquier servidor: realiza…
date: '2019-05-14T11:24:42.010Z'
categories:
  - server
keywords:
  - cxs
  - configserver-exploit-scanner
  - seguridad
---

![El logo es horrendo, como pueden apreciar](img/0__oHIO8SRbJiWq5Loa.png){: .center-block }
El logo es horrendo, como pueden apreciar
{: .img-caption }

Si todavía no sabés que es [ConfigServer eXploit Scanner](https://configserver.com/cp/cxs.html), básicamente es la salvación para la seguridad de cualquier servidor: realiza escaneos activos de cualquier archivo que sea subido al servidor. Es excepcional para hostear esos sitios WordPress gestionados por vaya a saber quién 😈

### Requisitos de instalación

Para la correcta instalación y ejecución es necesario contar con:

*   **Gestor de módulos:** App::cpanminus.
*   **Librería:** Archive::Zip
*   **Librería:** Linux::Inotify2

Básicamente, correr…

```
cpan App::cpanminuscpanm Archive::Zipcpanm Linux::Inotify2
```

### Requisitos de ejecución

* **Antivirus:** ClamAV y clamd (daemon)

Primero se instala el antivirus, se actualiza su base de datos y se lo deja corriendo como daemon.

```sh
yum install -y epel-releaseyum install -y clamav clamdfreshclamservice clamd start
```

### Requisitos del daemon

* Apache — ModSecurity

Debe procederse aún con la instalación de **ModSecurity** para poder dejar **cxs** corriendo como daemon.

### Ahora sí, la instalación

Se realizó la descarga y descompresión del archivo en /usr/tmp/cxs

```sh
cd /usr/tmpmakedir cxscd cxswget https://download.configserver.com/cxsinstaller.tgztar -xzf cxsinstaller.tgzperl cxsinstaller.plrm -fv cxsinstaller.*cd ..rmdir cxs
```

Finalmente se descargó el archivo `/etc/cxs/install.txt` para verificar temas de configuración y su posterior ejecución.

### Ejecutando CXS

Para ejecutar el CXS sobre las carpetas de los usuarios, se accede a la UI habilitada en el panel del servidor. Desde allí se accede a la opción generate command y se corre el script con las opciones por defecto.

### Fuentes

* **CXS:** [http://www.configserver.com/cp/cxsinstaller.html](http://www.configserver.com/cp/cxsinstaller.html)
* **CPAN:** [http://www.cpan.org/misc/cpan-faq.html#What\_is\_CPAN](http://www.cpan.org/misc/cpan-faq.html#What_is_CPAN)
* **CPAN — Gestiór de módulos:** [http://www.cpan.org/modules/INSTALL.html](http://www.cpan.org/modules/INSTALL.html)
* **CPAN — Librerías:** [http://www.linuxquestions.org/questions/slackware-14/ooo1-9-113-compile-error-archive-zib-pm-perl5-341538/](http://www.linuxquestions.org/questions/slackware-14/ooo1-9-113-compile-error-archive-zib-pm-perl5-341538/)
* **ClamAV:** [https://www.clamav.net/documents/installing-clamav#rhel](https://www.clamav.net/documents/installing-clamav#rhel)
