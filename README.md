#include <iostream>
#include <cmath>
using namespace std;

int main() {
    int n;
    cout << "Enter number of equations (n): ";
    cin >> n;

    float a[20][21];  // augmented matrix (A|B)
    cout << "\nEnter coefficients and constants (a[i][j]) row-wise:\n";
    cout << "(For each row, enter n coefficients followed by the constant term)\n";

    for(int i = 0; i < n; i++) {
        for(int j = 0; j <= n; j++) {
            cin >> a[i][j];
        }
    }

    // 🔹 Forward Elimination
    for(int i = 0; i < n - 1; i++) {
        // Partial pivoting (for numerical stability)
        for(int k = i + 1; k < n; k++) {
            if(fabs(a[i][i]) < fabs(a[k][i])) {
                for(int j = 0; j <= n; j++) {
                    swap(a[i][j], a[k][j]);
                }
            }
        }

        for(int k = i + 1; k < n; k++) {
            float factor = a[k][i] / a[i][i];
            for(int j = i; j <= n; j++) {
                a[k][j] -= factor * a[i][j];
            }
        }
    }

    // 🔹 Back Substitution
    float x[20];
    for(int i = n - 1; i >= 0; i--) {
        float sum = a[i][n];
        for(int j = i + 1; j < n; j++) {
            sum -= a[i][j] * x[j];
        }
        x[i] = sum / a[i][i];
    }

    // 🔹 Output
    cout << "\n✅ Final Solution:\n";
    for(int i = 0; i < n; i++) {
        cout << "x" << i + 1 << " = " << x[i] << endl;
    }

    return 0;
}
