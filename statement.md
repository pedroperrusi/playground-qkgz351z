# Exercício mapa Gaussiano

O mapa gaussiano é definido por:
```math
x_{n+1} = e^{(-b * x^2)} + c
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

    // Parâmetros do mapa Gaussiano
    x = 0;      // valor inicial de x
    b = 7.5;    // valor constante de b
    c_min = -1; // menor valor do intervalo
    c_max =  1; // maior valor do intervalo
    num_points = 50; // numero de pontos
    // Cálculo da variaçăo de C entre dois pontos do intervalo
    d_c = (c_max - c_min) / (num_points - 1);
    c = c_min;  // valor inicial de c

    double precision = 1e-6;  // precisăo numérica desejada de 10^-6
    // Cíclo de cálculo dos valores da funçăo mapa
    while ((c - c_max) <= precision)  // enquato condição é verdadeira, executa-se o ciclo
    {
        x = mapaGaussiano(x, b, c);             // Atualiza-se o valor de X
        printf("%lf %30.16lf\n", c, x);  // Salva o par de valores c e x no arquivo de saída
        c = c + d_c;                            // Incrementa-se o valor de c no intervalo
    }

    return 0;  // fim do programa
}
```
