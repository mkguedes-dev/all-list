# all-list
#include <stdio.h>
#include <string.h>

#define MAX_ITENS 100  // Define o tamanho máximo da lista de compras
#define MAX_NOME 50    // Define o tamanho máximo do nome de um item

int contador = 0; // Contador global para controlar o número de itens na lista

// Função para adicionar um item à lista
void adicionarItem(char lista[][MAX_NOME]) {
    if (contador < MAX_ITENS) {
        printf("Digite o nome do item: ");
        scanf(" %[^\n]s", lista[contador]); // Lê o item e o armazena na lista
        contador++;
        printf("Item adicionado com sucesso!\n");
    } else {
        printf("Lista de compras cheia! Não é possível adicionar mais itens.\n");
    }
}

// Função para remover um item específico da lista
void removerItem(char lista[][MAX_NOME]) {
    char item[MAX_NOME];
    printf("Digite o nome do item a ser removido: ");
    scanf(" %[^\n]s", item);

    int encontrado = -1;
    for (int i = 0; i < contador; i++) {
        if (strcmp(lista[i], item) == 0) {
            encontrado = i;
            break;
        }
    }

    if (encontrado != -1) {
        for (int i = encontrado; i < contador - 1; i++) {
            strcpy(lista[i], lista[i + 1]); // Move os itens para preencher a lacuna
        }
        contador--;
        printf("Item removido com sucesso!\n");
    } else {
        printf("Item não encontrado na lista.\n");
    }
}

// Função para exibir todos os itens da lista
void exibirLista(char lista[][MAX_NOME]) {
    if (contador == 0) {
        printf("A lista de compras está vazia.\n");
    } else {
        printf("Lista de compras:\n");
        for (int i = 0; i < contador; i++) {
            printf("%d. %s\n", i + 1, lista[i]);
        }
    }
}

// Função para ordenar a lista de compras em ordem alfabética
void ordenarLista(char lista[][MAX_NOME]) {
    for (int i = 0; i < contador - 1; i++) {
        for (int j = i + 1; j < contador; j++) {
            if (strcmp(lista[i], lista[j]) > 0) {
                char temp[MAX_NOME];
                strcpy(temp, lista[i]);
                strcpy(lista[i], lista[j]);
                strcpy(lista[j], temp);
            }
        }
    }
    printf("Lista de compras ordenada com sucesso!\n");
}

// Função para contar o número de itens na lista
void contarItens() {
    printf("Total de itens na lista: %d\n", contador);
}

int main() {
    char lista[MAX_ITENS][MAX_NOME];
    int opcao;

    do {
        printf("\nEscolha uma opção:\n");
        printf("1. Adicionar item\n");
        printf("2. Remover item\n");
        printf("3. Exibir lista\n");
        printf("4. Ordenar lista\n");
        printf("5. Contar itens\n");
        printf("0. Sair\n");
        printf("Opção: ");
        scanf("%d", &opcao);

        switch (opcao) {
            case 1:
                adicionarItem(lista);
                break;
            case 2:
                removerItem(lista);
                break;
            case 3:
                exibirLista(lista);
                break;
            case 4:
                ordenarLista(lista);
                break;
            case 5:
                contarItens();
                break;
            case 0:
                printf("Saindo...\n");
                break;
            default:
                printf("Opção inválida! Tente novamente.\n");
        }
    } while (opcao != 0);

    return 0;
}
  
