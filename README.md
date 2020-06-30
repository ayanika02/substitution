# substitution
#include <stdio.h>
#include <cs50.h>
#include <ctype.h>
#include <string.h>

int repeat(string s) //checks if characters are repeated
{
    int c = 0;
    for (int i = 0; i < strlen(s); i++)
    {
        for (int j = i + 1; j < strlen(s); j++)
        {
            if (toupper(s[i]) == toupper(s[j]))
            {
                c++;
            }
        }
    }
    if (c > 0)
    {
        return 1;
    }
    else
    {
        return 0;
    }
}
int check1(string s) //checks if non-characters are present
{
    int c = 0;
    for (int i = 0; i < strlen(s); i++)
    {
        if (isalpha(s[i]) == false)
        {
            c++;
        }
    }
    if (c > 0)
    {
        return 1;
    }
    else
    {
        return 0;
    }
}
int check2(string s) //prints errors
{
    if (strlen(s) != 26)
    {
        printf("Key must contain 26 characters. \n");
        return 1;
    }
    else
    {
        if (repeat(s) == 1)
        {
            printf("Key must not contain repeated characters \n");
            return 1;
        }
        else if (check1(s) == 1)
        {
            printf("Key must not contain numbers ");
            return 1;
        }
        //return 1;
    }
    return 0;
}
int check3(char c) //mapping
{
    string str = "ABCDEFGHIJKLMNOPQRSTUVWXYZ";
    int i = 0;
    for (i = 0; i < 26; i++)
    {
        if (toupper(c) == str[i])
        {
            break;
        }
    }
    return i;
}
int main(int argv, string argc[]) //main
{
    if (argv != 2)
    {
        printf("Usage: ./substitution KEY \n");
        return 1;
    }
    else if (check2(argc[1]) == 1)
    {
        return 1;
    }
    else
    {
        //check2(argc[1]);
        if (check2(argc[1]) != 1)
        {
            string s = get_string("plaintext: ");
            char ciph[strlen(s)];
            //string ciph = "";
            for (int i = 0; i < strlen(s); i++)
            {
                if (isupper(s[i]))
                {
                    int x = check3(s[i]);
                    ciph[i] = toupper(argc[1][x]);
                }
                else if (islower(s[i]))
                {
                    int x = check3(s[i]);
                    ciph[i] = tolower(argc[1][x]);
                }
                else
                {
                    ciph[i] = s[i];
                }
            } // close of for
            printf("ciphertext: %s\n", ciph);
        } // close of if
    } //close of else
}
