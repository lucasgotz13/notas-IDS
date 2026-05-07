
Demostración
Para demostrar la optimalidad de este algoritmo greedy, procederemos a realizar una demostración por inversiones.

Dado que nuestro algoritmo plantea que los rivales se deben analizar en un orden decreciente de los tiempos $a_i$, diremos que una solución $S$ tiene una inversión si dentro de esta hay dos elementos $T_i$ y $T_j$ tales que $i$ < $j$ y que $a_i$  < $a_j$. Sin embargo, podríamos plantear que si $S$ contiene 2 o más tiempos $a_i$ iguales entonces podrían existir varias soluciones que no contengan inversiones. En este caso se puede demostrar que todo tipo de soluciones de este estilo tienen el mismo tiempo total:

En una solución del tipo de $S$, al no tener inversiones los únicos videos que pueden variar su orden son aquellos que tienen el mismo $a_i$, y este grupo tiene que ser consecutivos. Entonces, lo que habría que demostrar es que esta variación en el orden no afecta el tiempo total, lo cuál podemos observar en el siguiente ejemplo:  

Tendremos videos $v_1$, $v_2$ y $v_3$ donde:
- $a_1$, $a_2$ y $a_3$ tienen el mismo valor => llamemos $a$ al valor compartido
- $s_1$, $s_2$, y $s_3$ podrían o no tener el mismo valor

Entonces calculemos los tiempos de cada v:
$v_1 = s_1 + a$
$v_2 = s_1 + s_2 + a$
$v_3 = s_1 + s_2 + s_3 + a$

Como la solución no tiene inversiones y el tiempo de los ayudantes es el mismo, entonces se puede afirmar que el último video va a ser siempre el video que más se va a tardar en analizar (nuestro tiempo total). Como el tiempo que tarda Scaloni en ver la totalidad de los videos es siempre constante (es decir, no importa el orden en el que los vea siempre va a tardar lo mismo) y el tiempo que tardan los ayudantes es el mismo entonces podemos confirmar que toda solución que no tenga inversiones siempre va a tener el mismo tiempo total.

Ahora demostremos que va a existir una solución sin inversiones que sea óptima.

Postulado: Existe una solución óptima que no tiene inversiones

Demostración: 

Supongamos que tenemos una solución óptima que si tiene al menos una inversión. Entonces podemos decir que en esta solución existe al menos un par de videos v_i y v_j donde a_i < a_j y son consecutivos (viniendo el video i antes que el video j). Luego, al realizar la cantidad de inversiones necesarias para llegar a la solución sin inversiones sin alterar su optimalidad en ningún momento, se debería confirmar que el tiempo total de esta solución es la misma que la del algoritmo.

Podríamos pensar que al invertir este par de videos quizás terminemos incrementando el tiempo total. Con la siguiente demostración, se va a observar que esto no puede suceder:

Notemos T como la cantidad de tiempo que estuvo Scaloni mirando videos hasta llegar al video i, y 

Tf como la cantidad de tiempo que estuvo Scaloni mirando videos hasta llegar al video j.

Entonces:
- $t_{total_j} = T + s_i + s_j + a_j$  

Al invertir, T se convierte en la cantidad de tiempo que estuvo Scaloni mirando videos hasta llegar al video j
- $t_{total_{i'}} = T + s_j + s_i + a_i$  

Primero tenemos que determinar que tanto T como Tf no resultan alterados luego de la inversión. Esto se puede comprobar planteando sus respectivos t_total: 

Va a quedar mas claro con algún dibujo/gráfico que voy a hacer después  

Como podemos observar, el t_total de ambos no va a cambiar debido a que, como comprobamos en la anterior demostración, el orden en el que Scaloni ve los videos no afecta el t_total. Entonces, nos queda que ambos t_total dependen de sus respectivos a, los cuales son los mismos tanto antes como después de la inversión.

Por lo tanto, nos quedaría ver que si el t_total_max se encuentra en alguno de los videos invertidos, entonces debemos comprobar que este no se incrementa luego de la inversión. 

Como definimos antes que toda solución sin inversiones es la óptima, debemos comparar ambos t_total para determinar si se sigue cumpliendo la definición en este caso.

Si comparamos ambos t_total, primero podemos notar que se pueden cancelar los términos “$T$, $s_j$ y $s_i$”. Entonces, nos quedaría comparar $a_j$ con $a_i$. Como definimos antes, $a_j$ > $a_i$. Por lo tanto, la solución terminaria teniendo un tiempo total máximo igual o menor al de la solución con la inversión.
