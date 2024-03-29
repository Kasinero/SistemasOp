#include <iostream>
#include <vector>
#include <algorithm>
#include <thread>
#include <chrono>

using namespace std;

// Estrutura para representar um processo
struct Process {
    int id;             // Identificador do processo
    int arrivalTime;    // Tempo de chegada do processo
    int burstTime;      // Tempo de execução necessário pelo processo
    int startTime;      // Momento em que o processo começa a ser executado
    int completionTime; // Momento em que o processo é concluído

    Process(int id, int arrivalTime, int burstTime) : id(id), arrivalTime(arrivalTime), burstTime(burstTime), startTime(0), completionTime(0) {}
};

// Função para simular a execução de um processo
void execute(Process& p) {
    cout << "Processo " << p.id << " iniciado." << endl;
    this_thread::sleep_for(chrono::seconds(p.burstTime)); // Simula a execução do processo
    cout << "Processo " << p.id << " concluído." << endl;
}

// Função que implementa o algoritmo Shortest Job Next (SJN)
void scheduleSJN(vector<Process>& processes) {
    int currentTime = 0; // Tempo atual do sistema

    cout << "Escalonamento de processos com Shortest Job Next (SJN):" << endl;

    // Ordena os processos com base no tempo de chegada
    sort(processes.begin(), processes.end(), [](const Process& a, const Process& b) {
        return a.arrivalTime < b.arrivalTime;
    });

    while (!processes.empty()) {
        // Filtra os processos que já chegaram
        vector<Process> arrivedProcesses;
        for (auto& p : processes) {
            if (p.arrivalTime <= currentTime) {
                arrivedProcesses.push_back(p);
            }
        }

        // Ordena os processos chegados com base no tempo de execução restante
        sort(arrivedProcesses.begin(), arrivedProcesses.end(), [](const Process& a, const Process& b) {
            return a.burstTime < b.burstTime;
        });

        // Executa o processo mais curto
        Process& currentProcess = arrivedProcesses.front();
        currentProcess.startTime = currentTime;
        currentProcess.completionTime = currentTime + currentProcess.burstTime;
        execute(currentProcess);

        // Atualiza o tempo atual do sistema
        currentTime = currentProcess.completionTime;

        // Remove o processo executado da lista de processos
        processes.erase(remove_if(processes.begin(), processes.end(), [&currentProcess](const Process& p) {
            return p.id == currentProcess.id;
        }), processes.end());
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

    // Chama a função que implementa o algoritmo SJN passando os processos como argumento
    scheduleSJN(processes);

    return 0;
}
