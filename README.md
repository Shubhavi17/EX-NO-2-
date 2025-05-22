## EX. NO:2 IMPLEMENTATION OF PLAYFAIR CIPHER

 

## AIM:
 

 

To write a C program to implement the Playfair Substitution technique.

## DESCRIPTION:

The Playfair cipher starts with creating a key table. The key table is a 5×5 grid of letters that will act as the key for encrypting your plaintext. Each of the 25 letters must be unique and one letter of the alphabet is omitted from the table (as there are 25 spots and 26 letters in the alphabet).

To encrypt a message, one would break the message into digrams (groups of 2 letters) such that, for example, "HelloWorld" becomes "HE LL OW OR LD", and map them out on the key table. The two letters of the diagram are considered as the opposite corners of a rectangle in the key table. Note the relative position of the corners of this rectangle. Then apply the following 4 rules, in order, to each pair of letters in the plaintext:
1.	If both letters are the same (or only one letter is left), add an "X" after the first letter
2.	If the letters appear on the same row of your table, replace them with the letters to their immediate right respectively
3.	If the letters appear on the same column of your table, replace them with the letters immediately below respectively
4.	If the letters are not on the same row or column, replace them with the letters on the same row respectively but at the other pair of corners of the rectangle defined by the original pair.
## EXAMPLE:
![image](https://github.com/Hemamanigandan/EX-NO-2-/assets/149653568/e6858d4f-b122-42ba-acdb-db18ec2e9675)

 

## ALGORITHM:

STEP-1: Read the plain text from the user.
STEP-2: Read the keyword from the user.
STEP-3: Arrange the keyword without duplicates in a 5*5 matrix in the row order and fill the remaining cells with missed out letters in alphabetical order. Note that ‘i’ and ‘j’ takes the same cell.
STEP-4: Group the plain text in pairs and match the corresponding corner letters by forming a rectangular grid.
STEP-5: Display the obtained cipher text.




## Program:
```
#include <stdio.h>
#include <string.h>
#define SIZE 5
char keyMatrix[SIZE][SIZE] = {
{'M', 'O', 'N', 'A', 'R'}, {'C', 'H', 'Y', 'B', 'D'}, {'E', 'F', 'G', 'I', 'K'}, {'L', 'P', 'Q', 'S', 'T'}, {'U', 'V', 'W', 'X', 'Z'}
};
void findPosition(char ch, int *row, int *col) {
for (int i = 0; i < SIZE; i++) {
for (int j = 0; j < SIZE; j++) {
if (keyMatrix[i][j] == ch) {
*row = i;
*col = j;
return;
}
}
}
}
void playfairCipher(char text[], char result[], int encrypt) {
int row1, col1, row2, col2;
int shift = encrypt ? 1 : -1;
for (int i = 0; text[i] != '\0'; i += 2) {
findPosition(text[i], &row1, &col1);
findPosition(text[i + 1], &row2, &col2);
if (row1 == row2) {
result[i] = keyMatrix[row1][(col1 + shift + SIZE) % SIZE];
result[i + 1] = keyMatrix[row2][(col2 + shift + SIZE) % SIZE];
} else if (col1 == col2) {
result[i] = keyMatrix[(row1 + shift + SIZE) % SIZE][col1];
result[i + 1] = keyMatrix[(row2 + shift + SIZE) % SIZE][col2];
} else {
result[i] = keyMatrix[row1][col2];
result[i + 1] = keyMatrix[row2][col1];
}
}
result[strlen(text)] = '\0';
}
int main() {
char plaintext[] = "SHUBHAVI";
char preparedText[100], encryptedText[100], decryptedText[100];
strcpy(preparedText, "SHUBHAVI");
playfairCipher(preparedText, encryptedText, 1);
printf("Encrypted Text: %s\n", encryptedText);
playfairCipher(encryptedText, decryptedText, 0);
printf("Decrypted Text: %s\n", decryptedText);
return 0;
}
```
Output:
![image](https://github.com/user-attachments/assets/97f7497e-3a40-4abb-95e1-b3a70801f3fd)

