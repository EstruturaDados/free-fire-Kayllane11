
#include <stdio.h>
#include <string.h>
#include <stdlib.h>

#define MAX_ITENS 10

typedef struct {
    char nome[30];
    char tipo[20];
    int quantidade;
} Item;

void inserirItem(Item mochila[], int *total);
void removerItem(Item mochila[], int *total);
void listarItens(Item mochila[], int total);
void buscarItem(Item mochila[], int total);

int main() {
    Item mochila[MAX_ITENS];
    int total = 0;
    int opcao;

    while (1) {
        printf("\n========== MENU DO INVENTARIO ==========\n");
        printf("1 - Inserir item\n");
        printf("2 - Remover item\n");
        printf("3 - Buscar item\n");
        printf("4 - Listar itens\n");
        printf("5 - Sair\n");
        printf("Escolha uma opcao: ");
        scanf("%d", &opcao);

        switch (opcao) {
            case 1:
                inserirItem(mochila, &total);
                listarItens(mochila, total);
                break;
            case 2:
                removerItem(mochila, &total);
                listarItens(mochila, total);
                break;
            case 3:
                buscarItem(mochila, total);
                break;
            case 4:
                listarItens(mochila, total);
                break;
            case 5:
                printf("Saindo...\n");
                return 0;
            default:
                printf("Opcao invalida!\n");
        }
    }
}

void inserirItem(Item mochila[], int *total) {
    if (*total >= MAX_ITENS) {
        printf("\nMochila cheia!\n");
        return;
    }

    printf("\nNome do item: ");
    scanf("%s", mochila[*total].nome);

    printf("Tipo do item: ");
    scanf("%s", mochila[*total].tipo);

    printf("Quantidade: ");
    scanf("%d", &mochila[*total].quantidade);

    (*total)++;
    printf("Item inserido com sucesso!\n");
}

void removerItem(Item mochila[], int *total) {
    if (*total == 0) {
        printf("\nMochila vazia!\n");
        return;
    }

    char nome[30];
    printf("\nNome do item a remover: ");
    scanf("%s", nome);

    for (int i = 0; i < *total; i++) {
        if (strcmp(mochila[i].nome, nome) == 0) {
            for (int j = i; j < *total - 1; j++) {
                mochila[j] = mochila[j + 1];
            }
            (*total)--;
            printf("Item removido!\n");
            return;
        }
    }

    printf("Item nao encontrado!\n");
}

void listarItens(Item mochila[], int total) {
    printf("\n========== ITENS ===========\n");

    if (total == 0) {
        printf("Nenhum item na mochila.\n");
        return;
    }

    for (int i = 0; i < total; i++) {
        printf("%d) Nome: %s | Tipo: %s | Quantidade: %d\n",
               i + 1, mochila[i].nome, mochila[i].tipo, mochila[i].quantidade);
    }
}

void buscarItem(Item mochila[], int total) {
    char nome[30];
    printf("\nNome do item para buscar: ");
    scanf("%s", nome);

    for (int i = 0; i < total; i++) {
        if (strcmp(mochila[i].nome, nome) == 0) {
            printf("\nItem encontrado!\n");
            printf("Nome: %s\n", mochila[i].nome);
            printf("Tipo: %s\n", mochila[i].tipo);
            printf("Quantidade: %d\n", mochila[i].quantidade);
            return;
        }
    }

    printf("Item nao encontrado!\n");
}

 