# Ex.No:3
   RECOGNITION-OF-A-VALID-ARITHMETIC-EXPRESSION-THAT-USES-OPERATOR-AND-USING-YACC
## Register Number: 212224220056
## Date: 22-09-25
## AIM
To write a yacc program to recognize a valid arithmetic expression that uses operator +,- ,* and /.
## ALGORITHM
1.	Start the program.
2.	Write a program in the vi editor and save it with .l extension.
3.	In the lex program, write the translation rules for the operators =,+,-,*,/ and for the identifier.
4.	Write a program in the vi editor and save it with .y extension.
5.	Compile the lex program with lex compiler to produce output file as lex.yy.c. eg $ lex filename.l
6.	Compile the yacc program with yacc compiler to produce output file as y.tab.c. eg $ yacc –d arith_id.y
7.	Compile these with the C compiler as gcc lex.yy.c y.tab.c
8.	Enter an arithmetic expression as input and the tokens are identified as output.
## PROGRAM 
## arth.l:
%{
#include "arth.tab.h"   // so it knows the token names from YACC
%}

%%

"="          { printf("\n Operator is EQUAL"); return '='; }
"+"          { printf("\n Operator is PLUS"); return PLUS; }
"-"          { printf("\n Operator is MINUS"); return MINUS; }
"/"          { printf("\n Operator is DIVISION"); return DIVISION; }
"*"          { printf("\n Operator is MULTIPLICATION"); return MULTIPLICATION; }

[a-zA-Z]*[0-9]* { printf("\n Identifier is %s", yytext); return ID; }

.            { return yytext[0]; }
\n           { return 0; }

%%

int yywrap() { return 1; }
## arth.y:
%{
#include <stdio.h>
%}

%token ID PLUS MINUS MULTIPLICATION DIVISION

%%

statement:
    ID '=' E {
        printf("\nValid arithmetic expression");
        $$ = $3;   // semantic value (not needed here, but ok)
    }
;

E:
    E PLUS ID
  | E MINUS ID
  | E MULTIPLICATION ID
  | E DIVISION ID
  | ID
;

%%

extern FILE* yyin;

int main() {
    do {
        yyparse();
    } while (!feof(yyin));
    return 0;
}

void yyerror(char *s) {
    fprintf(stderr, "Error: %s\n", s);
}
## OUTPUT
## COMMANDS:
<img width="1037" height="428" alt="Screenshot 2025-09-28 150106" src="https://github.com/user-attachments/assets/2eb80ae6-c2a4-43a5-8379-64abf6fc5d6b" />

## VALID EXPRESSSION :

<img width="773" height="255" alt="Screenshot 2025-09-28 150159" src="https://github.com/user-attachments/assets/183f1e83-9569-44c3-a9be-e0f8d33b1ef6" />

## INVALID EXPRESSION:
<img width="848" height="724" alt="Screenshot 2025-09-28 150239" src="https://github.com/user-attachments/assets/b1b67a2f-1d29-4ada-abb3-078f78d40fca" />





## RESULT
A YACC program to recognize a valid arithmetic expression that uses operator +,-,* and / is executed successfully and the output is verified.
