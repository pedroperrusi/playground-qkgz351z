# Exercício mapa Gaussiano

O mapa gaussiano é definido por:
```
x_next = exp(-b * pow(x, 2)) + c
```
onde b e c são parâmetros constantes. Como no caso do mapa logı́stico ele
pode apresentar comportamento regulare ou caótico. Para b = 7.5 pode ser
caótico dependendo do valor do parâmetro c.

>> O objeto deste exercı́cio é obter o diagrama de bifurcação desse mapa para b = 7.5 e com c variando no intervalo [−1, 1]. Tome como valor inicial x = 0 e proceda como no caso dos mapas logı́stico e do seno.


```C++ runnable
#include <math.h>
#include <stdio.h>

double mapaGaussiano(double x, double b, double c) {
    return exp(-b * pow(x, 2)) + c;
}

int main() {
    // Declaração das variáveis
    unsigned int num_points;            // variáveis de número natural (em C: inteiro e sem sinal)
    double x, b, c, c_min, c_max, d_c;  // variáveis de número real (em C: precisão dupla)
    FILE *entrada, *saida;               // variáveis de leitura de arquivos (em C: ponteiro de arquivo)

    // Leitura do arquivo de entrada
    entrada = fopen("uploads/bifurcacao.in", "r");  // abertura
    fscanf(entrada, "%lf", &c_min);                 // leitura de c_min
    fscanf(entrada, "%lf", &c_max);                 // leitura de c_max
    fscanf(entrada, "%i", &num_points);            // leitura de num_points
    fclose(entrada);                              // fim da leitura

    // Cálculo da variaçăo de C entre dois pontos do intervalo
    d_c = (c_max - c_min) / (num_points - 1);

    // Imprime valores lidos para confirmar os parametros do problema
    printf("Leitura do arquivo bifurcacao.in:\n");
    printf("\t c_min= %lf  c_max = %lf   num_points= %i\n", c_min, c_max, num_points);
    printf("\t  variaçăo de C entre dois pontos da amostra d_c = %f \n", d_c);

    saida = fopen("myfiles/bifurcacao.dat", "w");  // abertura do arquivo de saída

    // Parâmetros do mapa Gaussiano
    x = 0;      // valor inicial de x
    b = 7.5;    // valor constante de b
    c = c_min;  // valor inicial de c

    double precision = 1e-6;  // precisăo numérica desejada de 10^-6
    // Cíclo de cálculo dos valores da funçăo mapa
    while ((c - c_max) <= precision)  // enquato condição é verdadeira, executa-se o ciclo
    {
        x = mapaGaussiano(x, b, c);             // Atualiza-se o valor de X
        fprintf(saida, "%lf %30.16lf\n", c, x);  // Salva o par de valores c e x no arquivo de saída
        c = c + d_c;                            // Incrementa-se o valor de c no intervalo
    }

    fclose(saida);  // fechamento do arquivo de saída

    printf("Resultados escritos no arquivo texto bifurcacao.dat\n ");

    return 0;  // fim do programa
}
```
