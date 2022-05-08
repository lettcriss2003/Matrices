# Matrices
Suma de Matrices 
/**
 * @file SumaMatrices.c
 * @author lettcriss
 * @brief 
 * @version 0.1
 * @date 2022-02-10
 * 
 * @copyright Copyright (c) 2022
 * 
 * El programa debe permitir:
 * - Ingresar 2 matrices desde el teclado.
 * - Sumar las matrices 
 * - Presnetar las matrices originales y las respuestas
 * 
 * ANALISIS 
 * ============
 * DATOS DE ENTRADA                        INFORMACION DE SALIDA
 * --------------------------------------------------------------
 * - 2 matrices                              - Matriz RTA
 * - la dimension de cada una                                 
 * 
 * 
 * ESQUEMAS ADICIONALES 
 * ========================
 * Sumar Matrices: Sumar cada elemento de las matrices iniciales posicion por posicion 
 * Las matrices iniciales deben ser cuadradas, de la misma dimension 
 * M1[a,b] + M2[a,b] = RTAM[a,b] 
 * 
 * REUQERIMINETOS 
 * ===============
 * - Ingrresar las dimensiones de las matrices
 * - Ingresar las matrices que se desea sumar 
 * - Calcular la suma de las matrices 
 * - Presentar el resultado de forma agradable al ususario 
 * 
 */

#include<stdio.h>
#include<stdlib.h>

int ingresarOrden(char * mensaje);
void ingresarMatriz(char * etiqueta, int filas, int cols, float matriz[filas][cols]);
void presentarMatriz(char * etiqueta, int filas, int cols, float matriz[filas][cols]);
float ** sumarMatriz(int filas, int cols, float matriz1[filas][cols], float matriz2[filas][cols]);
void presentarMatrizRTA(char * etiqueta, int filas, int cols, float **matrizRTA);

int main(int argc, char const *argv[])
{
    system("@cls||clear");

    int numFilas = ingresarOrden("Ingrese el numero de filas para la Matrices a sumar:");
    int numCols = ingresarOrden("Ingrese el numero de cols para la Matrices a sumar:");

    float m1[numFilas][numCols];
    float m2[numFilas][numCols];

    ingresarMatriz("M1", numFilas, numCols, m1);
    ingresarMatriz("M2", numFilas, numCols, m2);

    float **rta = sumarMatriz(numFilas, numCols, m1, m2);

    printf("*************************************\n");
    presentarMatriz("[M1]", numFilas, numCols, m1);
    printf("+\n");
    presentarMatriz("[M2]", numFilas, numCols, m2);
    printf("=====================================\n");
    presentarMatrizRTA("[RTA]", numFilas, numCols, rta);
    printf("=====================================\n");
    
    return 0;
}

// FUNCION QUE ME DEVUELVA UN ENTERO COMO NUMERO DE FILAS 
/*int ingresarOrden(char * mensaje){
    int numFilas, numCols;
    printf("Ingrese el numero de filas para las matrices a operar: \n");
    scanf("%d", &numFilas);
    printf("Ingrese el numero de columnas para las matrices a operar: \n");
    scanf("%d", &numCols);
    
}*/

int ingresarOrden(char * mensaje){
    int orden;
    printf("%s",mensaje);  // ->>> se presenta el mensaje del int main
    scanf("%d", &orden);
    getchar();
    return orden;
    }


void ingresarMatriz(char * etiqueta, int filas, int cols, float matriz[filas][cols]){
  printf("INGRESANDO LA MATRIZ %s, DE ORDEN: [%d][%d]: ", etiqueta, filas, cols);
    for (int i = 0; i < filas; i++)
    {
        for (int j = 0; j < cols; j++)
        {
         printf("Ingrese el elemento de la posicion [%d][%d]: ", i, j);
            scanf("%f", &matriz[i][j]); 
        }   
    }
}

void presentarMatriz(char * etiqueta, int filas, int cols, float matriz[filas][cols]){
    printf("PRESENTANDO MATRIZ DE ORDEN [%d][%d]\n", filas, cols);
    for (int i = 0; i < filas; i++) // recorremos las filas (arreglos apilados)
    {
        // recorremos las columnas (por cada arreglo apilado debemos recorrer sus elementos)
        for (int j = 0; j < cols; j++)
        {
            //printf("[%d][%d]: %d\n", i, j, arregloBidimensional[i][j]);  // presentar las posiciones ->> [%d][%d]
            printf("%f\t", matriz [i][j]);
        }  
        printf("\n"); 
    }   
}

float ** sumarMatriz(int filas, int cols, float matriz1[filas][cols], float matriz2[filas][cols]){
    float **matrizRTA = malloc(filas);  // ->> Se traba con puenteros hay que reservar el espacio de memoria para las filas
    for (int i = 0; i < filas; i++)
    {
        matrizRTA[i] = (float *)malloc(sizeof(float) * cols);
        for (int j = 0; j < cols; j++)
        {
         int rta;
         rta = matriz1[i][j] + matriz2[i][j];
         matrizRTA[i][j] = rta;
        }
    }
    return matrizRTA;
}


void presentarMatrizRTA(char * etiqueta, int filas, int cols, float **matrizRTA){
    printf("PRESENTANDO MATRIZ RESULTADO [%d][%d]\n", filas, cols);
    for (int i = 0; i < filas; i++) // recorremos las filas (arreglos apilados)
    {
        // recorremos las columnas (por cada arreglo apilado debemos recorrer sus elementos)
        for (int j = 0; j < cols; j++)
        {
            //printf("[%d][%d]: %d\n", i, j, arregloBidimensional[i][j]);  // presentar las posiciones ->> [%d][%d]
            printf("%2.f\t", matrizRTA [i][j]);
        }  
        printf("\n"); 
    }   
}

