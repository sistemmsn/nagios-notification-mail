## Scripts de notificación flexibles de Nagios


Nagios Core solo viene con una estructura básica para alertas de correo electrónico basadas en texto plano. Estos scripts complementarios llevan la notificación más allá al agregar formato HTML, codificación de colores, selecciones de idioma y más. La integración con dos paquetes de gráficos populares, Nagiosgraph y PNP4Nagios, agrega visualización de problemas a las alertas.

Esto acorta el tiempo de identificación del problema, aumenta la transparencia del problema y reduce el tiempo de reparación.

Ejemplo de notificación de servicio:

### Imagen

![Ejemplo](/images/ejemplo.png)

### Requerimiento

Markdown is a lightweight and easy-to-use syntax for styling your writing. It includes conventions for

```markdown

Agregare las partes que modificaran en el plugin esto aplica para ambos de HOST y SERVICES

- Nota: la contraseña de nagios -no- de debe de llevar caracteres extraños como: $%"# ya que el plugin lo toma como otros valores y no como parte de la contraseña.



# yum install perl-MIME-tools
# yum install perl-libwww-perl
# yum install netpbm
# yum install perl-Mail-Sendmail
# yum install perl-Getopt-Long
# yum install perl-Digest
# yum install perl-LWP-Protocol-https
# yum install perl-File-Which

## Parámetros a modificar dentro de los 2 scritp (host y services)


# the sender e-mail address to be seen by recipients
`my $mail_sender  = "Nagios Monitoring <no-reply\@tuempresadecorreo.com>"; `
- Nota: aquí puedes poner un correo ficticio, obviamente al hacer eso estarían llegando a spam solo agregar ese remitente como seguro. 

## Header 2
### Header 3

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```



For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/sistemmsn/nagios-notification/settings). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact



Having trouble with Pages? Check out our [documentation](nagios.fm4dd.com) or [contact support](https://github.com/contact) and we’ll help you sort it out.
