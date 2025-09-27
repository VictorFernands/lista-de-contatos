
#include <iostream>
#include <vector>
#include <string>

using namespace std;


class Contato {
private:
    string nome;
    string numero;

public:

    Contato(string nomeParam, string numeroParam) {
        nome = nomeParam;
        numero = numeroParam;
    }


    string getNome() const {
        return nome;
    }

    string getNumero() const {
        return numero;
    }

    void exibir() const {
        cout << "Nome: " << nome << ", Número: " << numero << endl;
    }
};

class Agenda {
private:
    vector<Contato> contatos;

public:
    void adicionarContato() {
        string nome, numero;
        cout << "Nome: ";
        getline(cin, nome);
        cout << "Número: ";
        getline(cin, numero);

        Contato novoContato(nome, numero);
        contatos.push_back(novoContato);
        cout << "Contato adicionado!\n";
    }

    void listarContatos() const {
        if (contatos.empty()) {
            cout << "Nenhum contato salvo.\n";
            return;
        }

        cout << "Lista de contatos:\n";
        for (int i = 0; i < contatos.size(); i++) {
            contatos[i].exibir();
        }
    }

    void pesquisarContato() const {
        string nomeBusca;
        cout << "Digite o nome para pesquisa: ";
        getline(cin, nomeBusca);

        bool encontrado = false;
        for (int i = 0; i < contatos.size(); i++) {
            if (contatos[i].getNome() == nomeBusca) {
                contatos[i].exibir();
                encontrado = true;
            }
        }

        if (!encontrado) {
            cout << "Contato não encontrado.\n";
        }
    }
};

int main() {
    Agenda agenda;
    int opcao;

    do {
        cout << "\n--- Menu ---\n";
        cout << "1. Adicionar contato\n";
        cout << "2. Listar contatos\n";
        cout << "3. Pesquisar contato por nome\n";
        cout << "0. Sair\n";
        cout << "Escolha uma opção: ";
        cin >> opcao;
        cin.ignore();

        switch (opcao) {
            case 1:
                agenda.adicionarContato();
                break;
            case 2:
                agenda.listarContatos();
                break;
            case 3:
                agenda.pesquisarContato();
                break;
            case 0:
                cout << "Encerrando...\n";
                break;
            default:
                cout << "Opção inválida.\n";
        }
    } while (opcao != 0);

    return 0;
}
