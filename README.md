Para el *script*, se recomienda realizar modificaciones únicamente en las siguientes secciones:

1. En la línea `#SBATCH -n 16`, se sugiere experimentar con múltiplos de 2 hasta alcanzar la utilización de los 16 núcleos. Es importante evitar el uso de núcleos adicionales a los requeridos por el código, ya que esto podría ocasionar una desaceleración en el tiempo de ejecución del mismo código, fenómeno conocido como *oversubscription*, información al respecto se puede encontrar en [Tosini2015](referencia1), [Jimenez-Gonzalez](referencia2).

2. En la línea 7, es posible explorar la opción de ejecución en el otro núcleo secundario del clúster `#SBATCH -w compute-0-2`.

3. Por último, se recomienda reemplazar `S_F.in` con el código principal que se ejecuta junto con el archivo correspondiente a su extensión.

### Descripción de *script* de trabajo para Ansys

- Linea 1: Esto se conoce como *shebang* y establece que el *script* debe ser interpretado por el *shell bash*.

- Linea 2: Define el nombre del trabajo como `Example`.

- Linea 3: Establece el nombre del archivo de error de salida, donde `%j` se reemplazará automáticamente con el número del trabajo.

- Linea 4: Establece el nombre del archivo de salida estándar, donde `%j` se reemplazará con el número del trabajo.

- Linea 5: Establece el límite de tiempo del trabajo en 1 día, 10 horas y 10 minutos.

- Linea 6: Solicita 16 núcleos (procesadores) para la ejecución del trabajo.

- Linea 7: Indica que el trabajo debe ejecutarse en el nodo `compute-0-1`.

- Linea 10: Define la variable de entorno `Project` con el valor `Example`.

- Linea 12: Carga de módulo necesario para la ejecución del software ANSYS versión 21.2.

- Linea 13: Define la variable de entorno `WORKDIR` con el valor de la variable de entorno `SLURM_SUBMIT_DIR`, que generalmente representa el directorio desde el cual se envió el trabajo.

- Linea 15: Cambia el directorio actual al directorio de trabajo definido anteriormente.

- Linea 16. Aquí se ejecuta el comando ANSYS Mechanical con los siguientes parámetros:
    - `-np 16`: Utiliza 16 procesadores para la ejecución.
    - `-mpi=intelmpi`: Utiliza el entorno de ejecución de Intel MPI.
    - `-b`: Ejecuta ANSYS en modo por lotes (batch).
    - `-dir $WORKDIR`: Especifica el directorio de trabajo.
    - `-i S_F.in`: Indica el archivo de entrada de la simulación.
    - `-o Example.txt`: Establece el nombre del archivo de salida de la simulación.

[referencia1]: https://users.exa.unicen.edu.ar/catedras/arqui2/arqui2/filminas/Introduccion%20a%20las%20arquitecturas%20Paralelas.pdf
[referencia2]: https://openaccess.uoc.edu/bitstream/10609/79549/3/Arquitecturas%20de%20computadores%20avanzadas_M%C3%B3dulo%201_Introducci%C3%B3n%20a%20las%20arquitecturas%20paralelas.pdf


