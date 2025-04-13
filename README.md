#include <iostream>
#include <vector>

using namespace std;

struct Process 
{
    int pid;    // Process ID
    int bt;     // Burst Time
    int ct;     // Completion Time
    int tat;    // Turnaround Time
    int wt;     // Waiting Time
};

int main()
{
    int n;
    cout << "Enter number of processes: ";
    cin >> n;

    vector<Process> p(n);

    for (int i = 0; i < n; i++) {
        p[i].pid = i + 1;
        cout << "Enter Burst Time for Process " << p[i].pid << ": ";
        cin >> p[i].bt;
    }

    int current_time = 0;
    float total_wt = 0, total_tat = 0;

    for (int i = 0; i < n; i++) {
        p[i].ct = current_time + p[i].bt;
        p[i].tat = p[i].ct; // Since AT = 0
        p[i].wt = p[i].tat - p[i].bt;
        current_time = p[i].ct;

        total_wt += p[i].wt;
        total_tat += p[i].tat;
    }

    cout << "\nProcess\tBT\tCT\tTAT\tWT\n";
    for (int i = 0; i < n; i++) {
        cout << "P" << p[i].pid << "\t" << p[i].bt << "\t" 
             << p[i].ct << "\t" << p[i].tat << "\t" << p[i].wt << "\n";
    }

    cout << "\nAverage Waiting Time: " << total_wt / n;
    cout << "\nAverage Turnaround Time: " << total_tat / n << endl;

    return 0;
}

