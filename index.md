## Scripts de notificación flexibles de Nagios


Nagios Core solo viene con una estructura básica para alertas de correo electrónico basadas en texto plano. Estos scripts complementarios llevan la notificación más allá al agregar formato HTML, codificación de colores, selecciones de idioma y más. La integración con dos paquetes de gráficos populares, Nagiosgraph y PNP4Nagios, agrega visualización de problemas a las alertas.

Esto acorta el tiempo de identificación del problema, aumenta la transparencia del problema y reduce el tiempo de reparación.

Ejemplo de notificación de servicio:

### Imagen

![Ejemplo](/images/ejemplo.png)

- Nota: la contraseña de nagios `no` de debe de llevar caracteres extraños como: $%"# ya que el plugin lo toma como otros valores y no como parte de la contraseña.

### Requerimiento

```markdown
 yum install perl-MIME-tools
 yum install perl-libwww-perl
 yum install netpbm
 yum install perl-Mail-Sendmail
 yum install perl-Getopt-Long
 yum install perl-Digest
 yum install perl-LWP-Protocol-https
 yum install perl-File-Which
```

### Agregare las partes ha modificar en el plugin esto aplica para ambos (HOST y SERVICES).

```markdown
# the sender e-mail address to be seen by recipients
my $mail_sender  = "Nagios Monitoring <no-reply\@tuempresadecorreo.com>";
```
- Nota: aquí puedes poner un correo ficticio, obviamente al hacer eso estarían llegando a spam solo hay que agregar ese remitente como seguro.
`ojo` este servicio no depende de spotfix o smtp-cli.

```markdown
# The Nagios CGI URL for integrated service links
my $nagios_cgiurl      = "http://192.168.1.1/nagios/cgi-bin";
```

```markdown
# ########################################################################
# Here we set the URL to pick up the RRD data files for the optional graph
# image generation. Modified by Robert Becht for use with PNP4Nagios.
# The PNP4Nagios URL : if not used we can set $pnp4nagios_url = undef;
# ########################################################################
my $pnp4nagios_url     = "http://192.168.1.1/pnp4nagios";
my $graph_history      = 48; # in hours, a good range is between 12...48
``` 

```markdown
# ########################################################################
# If web authentication is needed, configure the access parameters below:
# ########################################################################
my $pnp4nagios_auth   = "true";
my $server_port       = "192.168.1.1:80";
my $auth_name         = "Nagios Access";  en el auth name lo puedes ver en cat/etc/httpd/conf.d/pnp4nagios.conf (AuthName "Nagios Access")

my $web_user          = "nagiosadmin"; el usuario de nagios con el que accedes a la web
my $web_pass          = "123456789"; y la contraseña de nagiosadmin
```  


```markdown
# ########################################################################
# SMTP related data: If the commandline argument -H/--smtphost was not
# given, we use the provided value in $o_smtphost below as the default.
# If the mailserver requires auth, an example is further down the code.
# ########################################################################
my $domain            = "\@tuempresadecorreo.com";
```

- Nota aquí puedes poner un correo ficticio, obviamente al hacer eso estarían llegando a spam solo agregar ese remitente como seguro.


-- Aqui iria su logo de la empresa.

```markdown
# ########################################################################
# This is the logo image file, the path must point to a valid JPG, GIF or
# PNG file, i.e. the nagios logo. Best size is rectangular up to 160x80px.
# example: [nagioshome]/share/images/NagiosEnterprises-whitebg-112x46.png
# ########################################################################
my $logofile = "/srv/www/std-root/nagios.fm4dd.com/images/nagios-mail.gif";
```

### Parametros en el command.cfg

```markdown
# ###########################################################
# 'service-email-pnp4n-int-en' command definition, sends
# multipart HTML e-mails, English with Nagios URL's + graph
# ##########################################################
define command{
command_name    service-email-pnp4n-int
command_line    $USER1$/pnp4n_send_service_mail.pl  -p "Nombre de la empresa, o lo que quieras poner."  -r "$CONTACTEMAIL$"  -c "$CONTACTADDRESS1$" -f graph -u -l es  
 }
```
- Nota opcional: este parámetro es para agregar a personas con en la parte "cc" ósea con copia ( -c "$CONTACTADDRESS1$")

 ```markdown
define command{
command_name    host-email-pnp4n-int
command_line    $USER1$/pnp4n_send_host_mail.pl  -p "Nombre de la empresa, o lo que quieras poner."  -r "$CONTACTEMAIL$"  -c "$CONTACTADDRESS1$" -f graph -u -l es 
}
```


### Parametros en el template.cfg


 ```markdown
define contact {

    name                            generic-contact         
    service_notification_period     24x7                    
    host_notification_period        24x7                    
    service_notification_options    w,u,c,r,f,s             
    host_notification_options       d,u,r,f,s               
    service_notification_commands   service-email-pnp4n-int 
    host_notification_commands      host-email-pnp4n-int
    register                        0                       
}
```

### Parametros en el contacs.cfg

-- Crearemos un nuevo contact name 

 ```markdown
define contact{
  contact_name                    Support                     
  use                             generic-contact             
  alias                           Business support team
  email                           soporte@empresa.com                 
  address1                        soporte1@empresa.com,soporte2@empresa.com
  service_notification_commands   service-email-pnp4n-int
  host_notification_commands      host-email-pnp4n-int
}
```
- Nota una vez creado el contact name lo agregamos a nuesto contactgroup



<h2>Referencias</h2>

-- Para obtener más detalles, consulte [GitHub fm4dd](https://github.com/fm4dd/nagios4dd).

