#include <stdio.h>
#define MAX 5
int main() {
    int days[MAX][MAX] = {{7, 14, 21},
                          {28, 35, 42},
                          {49, 56,63}};
    int rows = 3, cols = 3;
    int choice, m, n, value;

    while (1) {
        printf("\n===== DAYS MATRIX OPERATIONS =====\n");
        printf("1. Traverse (print all)\n");
        printf("2. Display (element at [m][n])\n");
        printf("3. Insert (a row at position)\n");
        printf("4. Delete (a row at position)\n");
        printf("5. Update (element at [m][n])\n");
        printf("6. Exit\n");
        printf("Enter your choice: ");
        scanf("%d", &choice);

        switch (choice) {

        case 1:  // TRAVERSE
            printf("\nDays matrix:\n");
            for (m = 0; m < rows; m++) {
                for (n = 0; n < cols; n++)
                    printf("%d ", days[m][n]);
                printf("\n");
            }
            break;

        case 2:  // DISPLAY
            printf("Enter row (m) and column (n): ");
            scanf("%d %d", &m, &n);
            if (m >= 0 && m < rows && n >= 0 && n < cols)
                printf("Element at [%d][%d] = %d\n", m, n, days[m][n]);
            else
                printf("Invalid index!\n");
            break;

        case 3:  // INSERT ROW
            if (rows == MAX) {
                printf("Matrix is full!\n");
                break;
            }
            printf("Enter position to insert row (0 to %d): ", rows);
            scanf("%d", &m);
            if (m < 0 || m > rows) {
                printf("Invalid position!\n");
                break;
            }
            printf("Enter %d values for the new row: ", cols);
            // Step 1: shift rows down
            for (int i = rows; i > m; i--)
                for (int j = 0; j < cols; j++)
                    days[i][j] = days[i - 1][j];
            // Step 2: place new row
            for (int j = 0; j < cols; j++)
                scanf("%d", &days[m][j]);
            rows++;
            printf("Row inserted!\n");
            break;

        case 4:  // DELETE ROW
            if (rows == 0) {
                printf("Matrix is empty!\n");
                break;
            }
            printf("Enter row position to delete (0 to %d): ", rows - 1);
            scanf("%d", &m);
            if (m < 0 || m >= rows) {
                printf("Invalid position!\n");
                break;
            }
            // shift rows up to fill the gap
            for (int i = m; i < rows - 1; i++)
                for (int j = 0; j < cols; j++)
                    days[i][j] = days[i + 1][j];
            rows--;
            printf("Row deleted!\n");
            break;

        case 5:  // UPDATE
            printf("Enter row (m), column (n), and new value: ");
            scanf("%d %d %d", &m, &n, &value);
            if (m >= 0 && m < rows && n >= 0 && n < cols) {
                days[m][n] = value;
                printf("Updated successfully!\n");
            } else {
                printf("Invalid index!\n");
            }
            break;

        case 6:  // EXIT
            printf("Goodbye!\n");
            return 0;

        default:
            printf("Invalid choice, try again.\n");
        }
    }
}
