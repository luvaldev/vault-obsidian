Es un numero binario de 32 bits, se dividen en 4 bytes que cada un byte son 8 bits.

los primeros 16 bits son los de red y los últimos 16 son de host.

- Clases de Direcciones IPV4

| Tipo    | Información                         |
| ------- | ----------------------------------- |
| Clase A | Soporta redes de Internet grandes   |
| Clase B | Soporta redes de Internet moderadas |
| Clase C | Soporta redes en internet pequeñas  |
| Clase D | Soporta Redes Multicast             |
| Clase E | Sin uso. Redes experimentales       |
$Clase \_ A$ : Los primeros 8 bits representan la [Red] y los 24 sobrantes el [Host]
$Clase \_ B$ : Los primeros 16 bits representan la [Red] y los 16 sobrantes el [Host]
$Clase \_ C$ : Los primeros 24 bits representan la [Red] y los 8 sobrantes el [Host]

- Para ver una IP a que tipo de clase pertenece, debemos fijarnos en el primer octeto el cual se distribuye de la siguiente manera:

| Clase A | 0 - 127   |
| ------- | --------- |
| Clase B | 128 - 191 |
| Clase C | 192 - 223 |
| Clase D | 224 - 239 |
| Clase E | 240 - 255 |
- Conversión de IP decimal a binario:
Para convertir de decimal a binario es necesario saber que esto comienza con un $2^0$ siendo de 0 a 7 el rango para formar un [Octeto] conformado por 8 bits, en el cual para realizar la transformación tomamos el primer Octeto y verificamos el numero decimal con el del $2^7$ que es equivalente a 128, si es mayor se coloca un 1 y se resta la diferencia, luego se compara con los siguientes y así sucesivamente, en caso de ser menor el decimal que el $2^n$ este se remplaza por un 0 y así sucesivamente con los 4 Octetos.

- Conversión de IP binario a decimal:
Para convertir de binario a decimal simplemente utilizamos los valores binarios igual a 1 tanto viendo por [Octeto] la posición $2^n$ y realizamos la suma de valores en la posición del bit para tener el decimal y esto se repite para los 4 octetos.
