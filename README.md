# TANTLR

## Una mini-calculadora que soporte:

- Expresiones con + - * / y paréntesis

- Asignaciones: a = 3+4

- Uso de variables: a*2

- Cada sentencia termina en NEWLINE

- Imprime el valor de cada sentencia (como en el tour del cap. 4)

## Ejemplo de entrada:
```
a=5
b=6
a+b*2
(1+2)*3
```
Salida esperada (aprox):

5
6
17
9
1) Preparación del entorno en WSL (Ubuntu)
1.1 Java (JDK)
sudo apt update
sudo apt install openjdk-17-jdk -y
java -version
1.2 Descargar ANTLR jar
cd ~
curl -O https://www.antlr.org/download/antlr-4.13.1-complete.jar
1.3 Crear alias antlr4 y grun (TestRig)

Tus diapositivas muestran esta idea de alias para no escribir todo el comando (se ve en la parte de “Instalación” / alias). 

04_LP

nano ~/.bashrc

Al final pega:

export CLASSPATH=".:$HOME/antlr-4.13.1-complete.jar:$CLASSPATH"
alias antlr4='java -jar $HOME/antlr-4.13.1-complete.jar'
alias grun='java org.antlr.v4.gui.TestRig'

Recarga:

source ~/.bashrc

Prueba:

antlr4

Deberías ver el help del tool (como en la verificación de instalación). 

04_LP

2) Crear el proyecto
mkdir -p ~/antlr-calc
cd ~/antlr-calc
3) Escribir la gramática (Cap. 4 – Calculadora con Visitor)

Crea LabeledExpr.g4:

nano LabeledExpr.g4

Pega esto:

grammar LabeledExpr;

// parser rules
prog:   stat+ ;

stat
    : expr NEWLINE                # printExpr
    | ID '=' expr NEWLINE         # assign
    | NEWLINE                     # blank
    ;

expr
    : expr op=('*'|'/') expr      # MulDiv
    | expr op=('+'|'-') expr      # AddSub
    | INT                         # int
    | ID                          # id
    | '(' expr ')'                # parens
    ;

// lexer rules
MUL : '*' ;
DIV : '/' ;
ADD : '+' ;
SUB : '-' ;
ID  : [a-zA-Z]+ ;
INT : [0-9]+ ;
NEWLINE:'\r'? '\n' ;
WS  : [ \t]+ -> skip ;
