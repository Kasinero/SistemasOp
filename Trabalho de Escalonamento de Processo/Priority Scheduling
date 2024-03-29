#include <iostream>
#include <vector>
#include <thread>
#include <chrono>
#include <algorithm> // Adiciona a inclusão do cabeçalho para a função sort

using namespace std;

// Definição da estrutura para representar um processo
struct Process {
    int id;          // Identificador do processo
    int priority;    // Prioridade do processo (quanto menor o número, maior a prioridade)
    int duration;    // Duração do processo em segundos
};

// Função para simular a execução de um processo
void execute(Process p) {
    cout << "Processo " << p.id << " com prioridade " << p.priority << " iniciado." << endl;
    this_thread::sleep_for(chrono::seconds(p.duration));
    cout << "Processo " << p.id << " com prioridade " << p.priority << " concluído." << endl;
}

// Função para escalonar os processos com base em suas prioridades
void schedule(vector<Process>& processes) {
    cout << "Escalonamento de processos com Priority Scheduling:" << endl;
    
    // Ordena os processos com base na prioridade (menor número tem maior prioridade)
    sort(processes.begin(), processes.end(), [](const Process& a, const Process& b) {
        return a.priority < b.priority;
    });

    // Executa os processos na ordem de prioridade
    for (const Process& p : processes) {
        thread t(execute, p);
        t.join();
    }
}

int main() {
    // Definição dos processos com diferentes prioridades e durações
    vector<Process> processes = {
        {1, 2, 3},   // Processo de alta prioridade
        {2, 3, 2},   // Processo de média prioridade
        {3, 4, 5},   // Processo de baixa prioridade
        {4, 1, 4}    // Processo de prioridade mais alta
    };

    // Chama a função de escalonamento
    schedule(processes);

    return 0;
}
