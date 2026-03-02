# Calculadora ANTLR – Capítulo 4
---

# 1. Objetivo

Implementar la calculadora presentada en el Capítulo 4 utilizando ANTLR como generador de analizadores sintácticos y Java como lenguaje objetivo, y documentar el proceso completo de instalación, generación de código, compilación y ejecución.

---

# 2. Entorno de Desarrollo

- Sistema operativo: Ubuntu (Máquina Virtual)
- Java: OpenJDK 17
- ANTLR: 4.13.1
- Terminal Linux

---

# 3. Verificación de Java

Se verifica la instalación de Java:

```bash
java -version
```
<img width="804" height="193" alt="Captura de pantalla 2026-03-01 230521" src="https://github.com/user-attachments/assets/4a4ad7ab-496b-4742-ab04-4e2ccfe2a5e1" />

# 4. Descarga de ANTLR

- Se descarga el archivo:
```
antlr-4.13.1-complete.jar
```
Verificación con:
```
ls
```
<img width="801" height="140" alt="Captura de pantalla 2026-03-01 231503" src="https://github.com/user-attachments/assets/4c72d484-628b-465b-90f0-b802832528f0" />

# 5. Creación del Proyecto

- Se crea la carpeta del proyecto:

```
mkdir antlr_calculadora
cd antlr_calculadora
```
<img width="807" height="92" alt="Captura de pantalla 2026-03-01 231551" src="https://github.com/user-attachments/assets/174b2670-1e7e-48ab-a950-ada1c9fc9d25" />

# 6. Gramática Expr.g4

Se crea el archivo Expr.g4 con la siguiente gramática:

<img width="802" height="462" alt="Captura de pantalla 2026-03-01 231617" src="https://github.com/user-attachments/assets/8adf037d-fb8a-4a3f-b88d-d81b37b86425" />

# 7. Generación del Parser y Visitor

Se ejecuta:
```
java -jar ../antlr-4.13.1-complete.jar -visitor Expr.g4
```

## Esto genera automáticamente:

ExprLexer.java

ExprParser.java

ExprBaseVisitor.java

ExprVisitor.java

Archivos .tokens y .interp
<img width="806" height="377" alt="Captura de pantalla 2026-03-01 231655" src="https://github.com/user-attachments/assets/c2c0145f-a589-4e4e-addd-f2d2d2b2ca9e" />

# 8. Implementación del EvalVisitor

- Archivo: EvalVisitor.java

- Este archivo extiende ExprBaseVisitor<Integer> y se encarga de evaluar el árbol sintáctico.

## Funciones principales:

- visitAssign → Guarda variables

- visitPrintExpr → Imprime resultados

- visitMulDiv → Multiplicación y división

- visitAddSub → Suma y resta

<img width="802" height="460" alt="Captura de pantalla 2026-03-01 231727" src="https://github.com/user-attachments/assets/17f5f224-273a-4581-a805-e82f1ec85e94" />

# 9. Implementación del Main

- Archivo: Main.java

## Este archivo:

- Lee la entrada del usuario

- Crea el Lexer

- Crea el Parser

- Construye el árbol

- Ejecuta el Visitor
<img width="804" height="410" alt="Captura de pantalla 2026-03-01 231754" src="https://github.com/user-attachments/assets/0671a179-15b9-486c-be22-e6ab35338c5b" />

# 10. Compilación

Se compila con:
```
javac -cp ".:../antlr-4.13.1-complete.jar" *.java
```
# 11. Ejecución

Se ejecuta con:
```
java -cp ".:../antlr-4.13.1-complete.jar" Main
```
Prueba realizada:
```
a=5
b=2
a+b*3
```
Resultado:
```
11
```
<img width="808" height="234" alt="Captura de pantalla 2026-03-01 232036" src="https://github.com/user-attachments/assets/b0111605-b69a-4c9c-9ae5-e28a9cb73ec9" />



