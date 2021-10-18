// Floyd_Algorithm

    #include <iostream>
    #include <stdio.h>
    #include <string.h>
    #include <bitset>
    #include <windows.h>

    using namespace std;

    int main()
    {
        int const N = 3;
        int numbers[N][N];
        int i, j; //j-string,i-column

        for (i = 1; i <= N; i++)
            for (j = 1; j <= N; j++)
                numbers[i][j] = 0;
        printf(" Enter the length of the path from city to city.\n");
        printf(" If there is no road, you should write -1: \n");
        printf("\n");

    begin:

        for (i = 0; i <= N; i++)
        {
            if (i == 0)
                printf("    ");
            else
                printf("%d  ", i);
        }
        printf("\n");
        for (i = 1; i <= N; i++)
        {
            printf("%d: ", i);//вывод номера столбца
            for (j = 1; j <= N; j++)
            {
                if ((i == j) && (i == 1))
                    printf(" %d ", 0);
                else if ((i == j) && (i != 1) && (numbers[i][j - 1] / 10 == 0))
                    printf(" %d ", 0);
                else if ((i == j) && (i != 1) && ((numbers[i][j - 1] / 10 != 0) || (numbers[i][j - 1] == -1)))
                    printf(" %d ", 0);
                else
                {
                    if ((i != j) && (numbers[i][j] == 0))
                    {
                        if (i == 1)
                        {
                            printf(" ");
                            cin >> numbers[i][j];
                            system("cls");
                            goto begin;
                        }
                        else
                        {
                            cin >> numbers[i][j];
                            system("cls");
                            goto begin;
                        }
                    }
                    else
                    {
                        if ((j == 1) && (numbers[i][j] / 10 == 0) && (numbers[i][j] > 0))
                        {
                            printf(" %d ", numbers[i][j]);
                        }
                        else if ((j == 1) && ((numbers[i][j] / 10 != 0) || (numbers[i][j] == -1)))
                        {
                            printf("%d ", numbers[i][j]);
                        }
                        else if ((numbers[i][j] / 10 != 0) || (numbers[i][j] == -1))
                        {
                            printf("%d ", numbers[i][j]);
                        }
                        else if (numbers[i][j] / 10 == 0)
                        {
                            printf(" %d ", numbers[i][j]);
                        }
                    }
                }
            }
            printf("\n");
        }

        printf("\n");

        //начало смены
        int flag = 1;
        int MKR[N][N];


        for (i = 1; i <= N; i++)
        {
            for (j = 1; j <= N; j++)
            {
                MKR[i][j] = numbers[i][j];
            }
        }


        for (int i = 1; i <= N; i++)
        {
            for (int j = 1; j <= N; j++)
            {
                if (i == j)
                    continue;

                if (MKR[i][j] != -1)
                {
                    for (int k = 1; k <= N; k++)
                    {
                        if ((k != i) && (k != j) && (numbers[j][k] > 0) && ((MKR[i][j] + numbers[j][k] < MKR[i][k]) || MKR[i][k] == -1))
                        {
                            MKR[i][k] = MKR[i][j] + numbers[j][k];
                        }
                    }
                }
            }
        }

        printf("Now,you will see MKR: \n");
        printf("\n");

        for (i = 0; i <= N; i++)
        {
            if (i == 0)
                printf("    ");
            else
                printf("%d  ", i);
        }
        printf("\n");
        for (i = 1; i <= N; i++)
        {
            printf("%d: ", i);//вывод номера столбца
            for (j = 1; j <= N; j++)
            {
                if ((i == j) && (i == 1))
                    printf(" %d ", 0);
                else if ((i == j) && (i != 1) && (MKR[i][j - 1] / 10 == 0))
                    printf(" %d ", 0);
                else if ((i == j) && (i != 1) && ((MKR[i][j - 1] / 10 != 0) || (MKR[i][j - 1] == -1)))
                    printf(" %d ", 0);
                else
                {
                    if ((j == 1) && (MKR[i][j] / 10 == 0) && (MKR[i][j] > 0))
                    {
                        printf(" %d ", MKR[i][j]);
                    }
                    else if ((j == 1) && ((MKR[i][j] / 10 != 0) || (MKR[i][j] == -1)))
                    {
                        printf("%d ", MKR[i][j]);
                    }
                    else if ((MKR[i][j] / 10 != 0) || (MKR[i][j] == -1))
                    {
                        printf("%d ", MKR[i][j]);
                    }
                    else if (MKR[i][j] / 10 == 0)
                    {
                        printf(" %d ", MKR[i][j]);
                    }
                }
            }
            printf("\n");
        }

        printf("\n");
        printf("Let's talk about movement: \n ");

        int i1;

        for (i = 1; i <= N; i++)
        {
            for (j = 1; j <= N; j++)
            {
                if (i == j || numbers[i][j] == MKR[i][j])
                    continue;

                printf("%d -> %d (%d):\n %d ->", i, j, MKR[i][j], i);

                i1 = i;
                do
                {
                    for (int k = 1; k <= N; k++)
                    {
                        if ((numbers[i1][k] > 0) && (numbers[i1][k] + MKR[k][j] == MKR[i1][j]) || (k == j) && (numbers[i1][k] == MKR[i1][j]))
                        {
                            printf("   %d (%d)->", k, numbers[i1][k]);
                            i1 = k;
                            break;
                        }
                    }
                } while (i1 != j);
                printf("\b\b \n");
            }
        }


        return 0;
    }
