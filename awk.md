% Introducción a awk 
% Joshua Haase
% 2017-02-09

# ¿Qué significa AWK?

AWK es un minilenguaje para el análisis de textos.

- Alfred **A**ho
- Peter **W**einberger
- Brian **K**ernighan

![]()hkkkj

---

# Un pseudo-programa de AWK

```
#!/usr/bin/awk -f
BEGIN { acciones antes de leer la entrada de datos }
condicion { acciones }
END { acciones al final de la lectura de datos }
```

![Portada del libro «Effective AWK»](data/curso-awk/awk-program.jpg ){align="center" width="70%"}

# El programa por defecto

La condición por defecto es `1` (verdadero).

La acción por defecto es `{ print }`.

La variable por defecto en funciones es `$0` (toda la línea).

El programa por defecto imprime todo tu archivo: `1 { print $0 }`

# Ejemplos

- ¿Cuántas lineas tiene tu archivo? `END { print NR }`

- ¿Cuántos campos tiene cada línea `{ print NF }`

- ¿Qué tiene la décima línea? `NR == 10`

- ¿El último campo de cada línea? `{print $NF}`

- ¿El último campo de la última línea? `{n = $NF} END {print n}`

- ¿Quién tiene más de 4 líneas? `NF > 4`

# Variables útiles

---------------------------------------   ---------------------------------------
**FILENAME**                              **RS**
Filename                                  Record Separator

**NF**                                    **ORS**
Number of Fields                          Output Record Separator

**NR**                                    **FS**
Number of Record                          Field Separator

**FNR**                                   **OFS**
(current) File Number of Record           Output Field Separator

**$1**
Field 1
---------------------------------------   ---------------------------------------

### Por ejemplo:

- Usar un separador diferente de campos: \
    `BEGIN {FS=":"; OFS="\t"} {$1 = $1; print}`

# Ejemplos

- ¿Cuántos campos hay en total? `'{ n = n + NF } END { print n }'`

- ¿Cuántas líneas dicen «P53»? \
    `/P53/ { n = n + 1 } END { print n }`

- ¿Cuáles líneas tienen más de 80 letras? `length($0) > 80`

- Cambiar el orden de los primeros dos campos e imprimir la línea: \
`{ temp = $1; $1 = $2; $2 = temp; print; }`


```
Print the largest first fields and the line that contains it ( assumes some $1 is positive):
$1 > max { max = $1 ; maxlines = $0 }
END { print max, maxline)
       
Print every line that has at least one field:
NF > 0
Pritn every line longer than 80 characters:
length($0) > 80
Print the numer of fields in every line, followed by the line itself:
{ print NF, $0 }
Print the first two fields, in opposite order, of every line:
{ print $2, $1 }
Exchange the first two fields of every line and then print the line:
{ temp = $1 ; $1 = $2 ; $2 = temp ; print }
Print every line witg rge first field replaced by the line number:
{ $1 = NR ; print }
Print every line after erasing the second field:
{ $2 = ""; print }
Print in reverse order the fields of every line:
{ for (i=NF ; i>0 ; i=i-1) printf( "%s ", $1)
       printf("\n")
}       
Print the sums of the fields of every line:
{ sum = 0
       for ( i=1 ; i<=NF ; i=i+1) sum = sum + $i
       print sum
}       
Ad up all fields in all lines and print the sum:
{ for ( i=1 ; i<=NF ; i=i+1 ) sum = sum + $i}
END { print sum }       
       
Print every line after replacing each field by its absolute value:
{ for (i=1 ; i<=NF ; i=i+1) if ($i<0) $i=-$i
       print
}       
```


---

https://www.debuggex.com/r/96wuvEBsdJjM5sYp

![](https://www.debuggex.com/i/qKgm7vjZYPHmDCUb.png )

# Expresiones regulares

https://www.debuggex.com/r/96wuvEBsdJjM5sYp

\
![](https://imgs.xkcd.com/comics/regular_expressions.png )

---

![](http://apps-oracle.ru/wp-content/uploads/2010/03/ancient-egyptian-regexp-300x177.jpg ){width="3cm"}

> Si tienes un problema y piensas que puedes resolverlo con expresiones regulares
> entonces tienes dos problemas
>
> []{.right}

\
![](https://bunyk.files.wordpress.com/2013/09/awk_sed.png )

# Referencias

http://orca.phys.uvic.ca/rsocs/wirth/faq/awk-oneliners.html
http://tuxgraphics.org/~guido/scripts/awk-one-liner.html
