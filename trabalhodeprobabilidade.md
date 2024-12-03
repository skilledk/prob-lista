//Lista de probabilidade e estatistica
// Lista 1.
//Ex 2
#include <stdio.h>

#define NUM_SERVIDORES 5

void gerar_combinacoes(int posicao, char estado[]) {
    if (posicao == NUM_SERVIDORES) {
        printf("(");
        for (int i = 0; i < NUM_SERVIDORES; i++) {
            printf("%c", estado[i]);
            if (i < NUM_SERVIDORES - 1) {
                printf(", ");
            }
        }
        printf(")\n");
        return;
    }

    estado[posicao] = 'A'; // Estado ativo
    gerar_combinacoes(posicao + 1, estado);
    
    estado[posicao] = 'I'; // Estado inativo
    gerar_combinacoes(posicao + 1, estado);
}

int main() {
    char estado[NUM_SERVIDORES];
    gerar_combinacoes(0, estado);
    return 0;
}

//Ex 3
#include <stdio.h>

int fatorial(int n) {
    if (n == 0 || n == 1)
        return 1;
    int resultado = 1;
    for (int i = 2; i <= n; i++) {
        resultado *= i;
    }
    return resultado;
}


int coeficiente_binomial(int n, int k) {
    return fatorial(n) / (fatorial(k) * fatorial(n - k));
}

double probabilidade_binomial(int n, int k, double p) {
    double q = 1 - p; // Probabilidade de falha
    return coeficiente_binomial(n, k) * pow(p, k) * pow(q, n - k);
}

int main() {
    int n = 4; // Número total de pacotes
    int k = 3; // Número de pacotes que chegam com sucesso
    double p = 0.7; // Probabilidade de sucesso

    double probabilidade = probabilidade_binomial(n, k, p);
    
    printf("A probabilidade de exatamente %d pacotes chegarem com sucesso é: %.4f\n", k, probabilidade);
    
    return 0;
}

//Ex 4
#include <stdio.h>

int main() {
    double taxa_cpu = 0.02;   // 2%
    double taxa_memoria = 0.01; // 1%
    double taxa_disco = 0.005;   // 0.5%

    double p_falha = taxa_cpu + taxa_memoria + taxa_disco;

    double p_cpu = 1.0 / 3.0;

    double p_cpu_dado_falha = (taxa_cpu * p_cpu) / p_falha;

    printf("A probabilidade de que um componente que falhou seja a CPU é: %.4f\n", p_cpu_dado_falha);

    return 0;
}
//Ex 6
#include <stdio.h>

int main() {
    double p_A = 0.3; // Probabilidade de um nó ser inativo
    double p_B = 0.2;

    double p_A_ou_B = p_A + p_B;

    printf("A probabilidade de que o nó selecionado esteja inativo ou sobrecarregado é: %.2f\n", p_A_ou_B);

    return 0;
}
//Lista 2.
//Ex 1
#include <stdio.h>
#include <math.h>

double normal_cdf(double z) {
    return 0.5 * (1 + erf(z / sqrt(2)));
}

int main() {
    double media = 1000.0;          // Média
    double desvio_padrao = 200.0;   // Desvio padrão
    int total_lampadas = 2000;      // Total de lâmpadas

    double z_700 = (700 - media) / desvio_padrao;
    double p_700 = normal_cdf(z_700);
    int lampadas_queimaram_700 = total_lampadas * p_700;

    int lampadas_queimaram_mais_700 = total_lampadas - lampadas_queimaram_700;

    double z_1300 = (1300 - media) / desvio_padrao;
    double p_1300 = normal_cdf(z_1300);
    int lampadas_queimaram_entre_700_e_1300 = total_lampadas * (p_1300 - p_700);

    printf("Lâmpadas queimaram nas primeiras 700 horas: %d\n", lampadas_queimaram_700);
    printf("Lâmpadas queimaram com mais de 700 horas: %d\n", lampadas_queimaram_mais_700);
    printf("Lâmpadas queimaram entre 700 e 1300 horas: %d\n", lampadas_queimaram_entre_700_e_1300);

    return 0;
}
//Ex 2
#include <stdio.h>
#include <math.h>

// Função para calcular a CDF da normal padrão
double normal_cdf(double z) {
    return 0.5 * (1 + erf(z / sqrt(2)));
}

int main() {
    double media = 6000.0;          // Média
    double desvio_padrao = 100.0;   // Desvio padrão

    double x1 = 6250.0;
    double z1 = (x1 - media) / desvio_padrao;
    double p_menor_6250 = normal_cdf(z1);

    double x2 = 5800.0;
    double z2 = (x2 - media) / desvio_padrao;
    double p_menor_5800 = normal_cdf(z2);
    
    double p_entre_5800_e_6250 = p_menor_6250 - p_menor_5800;

    // Resultados
    printf("Probabilidade de resistência menor que 6250 kg/cm²: %.4f\n", p_menor_6250);
    printf("Probabilidade de resistência entre 5800 e 6250 kg/cm²: %.4f\n", p_entre_5800_e_6250);

    return 0;
}
//Ex 3
#include <stdio.h>
#include <math.h>

double normal_cdf(double z) {
    return 0.5 * (1 + erf(z / sqrt(2)));
}

int main() {
    double media = 0.5;          // Média em μm
    double desvio_padrao = 0.05; // Desvio padrão em μm

    double x1 = 0.6;
    double z1 = (x1 - media) / desvio_padrao;
    double p_maior_06 = 1 - normal_cdf(z1); // P(X > 0.6)

    double x2_lower = 0.47;
    double x2_upper = 0.63;
    
    double z2_lower = (x2_lower - media) / desvio_padrao;
    double z2_upper = (x2_upper - media) / desvio_padrao;

    double p_entre_047_e_063 = normal_cdf(z2_upper) - normal_cdf(z2_lower);

    printf("Probabilidade de largura maior que 0,6 μm: %.4f\n", p_maior_06);
    printf("Probabilidade de largura entre 0,47 e 0,63 μm: %.4f\n", p_entre_047_e_063);

    return 0;
}
//Ex 4
#include <stdio.h>
#include <math.h>

// Função para calcular a CDF da normal padrão
double normal_cdf(double z) {
    return 0.5 * (1 + erf(z / sqrt(2)));
}

int main() {
    double media = 0.2508;          // Média em polegadas
    double desvio_padrao = 0.0005;  // Desvio padrão em polegadas

    double limite_inferior = 0.2485;
    double limite_superior = 0.2515;

    double z_inferior = (limite_inferior - media) / desvio_padrao;
    double z_superior = (limite_superior - media) / desvio_padrao;

    double p_inferior = normal_cdf(z_inferior);
    double p_superior = normal_cdf(z_superior);

    double p_intervalo = p_superior - p_inferior;

    printf("Probabilidade de que o diâmetro do eixo esteja entre %.4f e %.4f polegadas: %.4f\n", 
           limite_inferior, limite_superior, p_intervalo);

    return 0;
}
