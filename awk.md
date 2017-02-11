% Introducción a awk 
% Joshua Haase
% 2017-02-09

# ¿Qué significa AWK?

AWK es un minilenguaje para el análisis de textos.

- Alfred **A**ho
- Peter **W**einberger
- Brian **K**ernighan

---

# Un pseudo-programa de AWK

```
#!/usr/bin/awk -f
BEGIN { acciones antes de leer la entrada de datos }
condicion { acciones }
END { acciones al final de la lectura de datos }
```

![Portada del libro «Effective AWK»](data/curso-awk/awk-program.jpg ){align="center" width="70%"}

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

## Por ejemplo:

- Usar un separador diferente de campos: \
    `BEGIN {FS=":"; OFS="\t"} {$1 = $1; print}`

# El programa por defecto

La condición por defecto es `1` (verdadero).

La acción por defecto es `{ print }`.

La variable por defecto en funciones es `$0` (toda la línea).

El programa más corto, imprime todo tu archivo: `1`

# Ejemplos

- ¿Cuántas lineas tiene tu archivo? `END { print NR }`

- ¿Cuántos campos tiene cada línea `{ print NF }`

- ¿Qué tiene la décima línea? `NR == 10`

- ¿El último campo de cada línea? `{print $NF}`

- ¿El último campo de la última línea? `{n = $NF} END {print n}`

- ¿Quién tiene más de 4 líneas? `NF > 4`

- ¿Cuántas líneas dicen «P53»? \
    `/P53/ { n = n + 1 } END { print n }`

# Expresiones regulares

> Si tienes un problema y piensas que puedes resolverlo con expresiones regulares
> entonces tienes dos problemas

![](data/curso-awk/xkcd.png )

# Expresiones regulares

Las expresiones regulares (regexp) son un lenguaje para expresar patrones.

![](data/curso-awk/regexp_1.png ){align="center" width="70%"}
![](data/curso-awk/regexp_2.png ){align="center" width="70%"}

# Referencias

- [Ejemplos de awk](http://tuxgraphics.org/~guido/scripts/awk-one-liner.html ).

- [Más ejemplos](http://orca.phys.uvic.ca/rsocs/wirth/faq/awk-oneliners.html ).

- [Un sitio para mostrar gráficamente expresiones regulares](https://www.debuggex.com/ ).

- [Un libro explicando expresiones regulares](https://www.lunametrics.com/regex-book/Regular-Expressions-Google-Analytics.pdf ).

- [De aquí salen las imágenes que explican las expresiones regulares.](http://www.visibone.com/regular-expressions/ ).
