#include <iostream>
#include <vector>
#include <algorithm>
#include <thread>
#include <chrono>
#include <climits> // Adiciona a inclusão do cabeçalho para a constante INT_MAX

using namespace std;

// Definição da estrutura para representar um processo
struct Process {
    int id;          // Identificador do processo
    int arrivalTime; // Tempo de chegada do processo
    int burstTime;   // Tempo de execução necessário pelo processo
    int remainingTime; // Tempo restante de execução necessário pelo processo
    bool completed;  // Flag para indicar se o processo foi concluído

    Process(int id, int arrivalTime, int burstTime) : id(id), arrivalTime(arrivalTime), burstTime(burstTime), remainingTime(burstTime), completed(false) {}
};

// Função para simular a execução de um processo
void execute(Process& p) {
    cout << "Processo " << p.id << " iniciado." << endl;
    while (p.remainingTime > 0) {
        this_thread::sleep_for(chrono::seconds(1)); // Simula a execução por 1 segundo
        p.remainingTime--;
    }
    p.completed = true;
    cout << "Processo " << p.id << " concluído." << endl;
}

// Função que implementa o algoritmo Shortest Remaining Time First (SRTF)
void scheduleSRTF(vector<Process>& processes) {
    int currentTime = 0; // Tempo atual do sistema

    cout << "Escalonamento de processos com Shortest Remaining Time First (SRTF):" << endl;

    while (true) {
        // Busca pelo processo com o menor tempo restante de execução
        int shortestIndex = -1;
        int shortestTime = INT_MAX;
        for (int i = 0; i < processes.size(); ++i) {
            if (!processes[i].completed && processes[i].arrivalTime <= currentTime && processes[i].remainingTime < shortestTime) {
                shortestIndex = i;
                shortestTime = processes[i].remainingTime;
            }
        }

        // Se nenhum processo for encontrado, todos os processos foram concluídos
        if (shortestIndex == -1) break;

        Process& currentProcess = processes[shortestIndex];
        currentProcess.completed = true;
        
        // Executa o processo atual
        thread t(execute, ref(currentProcess));
        t.join();

        // Atualiza o tempo atual do sistema
        currentTime += currentProcess.burstTime;
    }
}

int main() {
    // Definição dos processos com diferentes chegadas e tempos de execução
    vector<Process> processes = {
        {1, 0, 3},   // Processo de curta duração
        {2, 1, 8},   // Processo de longa duração
        {3, 2, 4},   // Processo
        {4, 0, 6},   // Processo com operações de I/O
        {5, 1, 4},   // Processo sem operações de I/O
        {6, 2, 6},   // Processo I/O-Bound
        {7, 3, 5},   // Processo I/O-Bound
        {8, 0, 8},   // Processo CPU-Bound
        {9, 1, 4},   // Processo CPU-Bound
        {10, 4, 10}  // Processo CPU-Bound
    };

    // Chama a função que implementa o algoritmo SRTF passando os processos como argumento
    scheduleSRTF(processes);

    return 0;
}
