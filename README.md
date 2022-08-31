# Projeto de um Compilador

## Parte I: Análise Léxica

Nesta parte do projeto, você irá implementar um analisador léxico para a [linguagem C-](../../language/README.md). 
O analisador léxico ou _scanner_ deve ler um programa fonte e produzir uma lista de _tokens_, sequencialmente, um _token_ de cada vez, anotado com as seguintes informações: tipo do _token_ (identificador, constante inteira, etc) e sua localização no código fonte.
Se uma entrada inválida for encontrada, ele deve informar _error_, anotado com o lexema incorreto.

Antes de iniciar a sua implementação, recomendamos que leia com atenção o [capítulo 3](../../resources/20-chapter3.pdf) do livro "Introduction to Compilers and Language Design" de Douglas Thain. 
Apesar da sintaxe de C- ser um pouco diferente da usada nesse livro, os exemplos de código e o material podem ser extremamente úteis.

Para conhecer Flex, pode utilizar texto [Flex in a Nutshell](../../resources/21-FlexInANutshell.pdf).

## Classes de _tokens_ 

Em sua implementação do analisador léxico, considere as seguintes classes de _tokens_ da linguagem:

__ID__      Identificador  
__NUM__     Literal decimal (integer)  
__KEY__     Keyword (palavra-chave) 
__SYM__     Símbolo Léxico  
__ERROR__   Lexema do primeiro erro encontrado

Comentários e caracteres de espacejamento (_white space_) devem ser descartados durante a fase de análise léxica do compilador. 
Você deve imprimir o número da linha na qual o _token_ foi encontrado, inclusive no caso de erro. 
O analisador léxico deve reportar todos os erros léxicos encontrados e prosseguir até o final do arquivo de entrada.
No caso de erro, retornar o _token_ __ERROR__. 
O formato de saída é: 

``` (line_num,token_class,"lexeme") ```
  
## Exemplo de arquivo de entrada em C- (main.c)
```
void main(void)
{
  int a;
  a = 4 + 5;
}
```

## Como executar (dois argumentos: entrada e saída)
Seu programa deve ler a entrada a partir de um arquivo (_source_) e escrever a saída em outro arquivo (_target_):
```
$ ./lexer main.c main.out
```

## Modelo de arquivo de saída gerado pelo analisador léxico
Após a execução de ./lexer, tendo como entrada o arquivo main.c (contendo um programa C-), a saída gerada no arquivo main.out deverá ser:
```
(1,KEY,"void")
(1,ID,"main")
(1,SYM,"(")
(1,KEY,"void")
(1,SYM,")")
(2,SYM,"{")
(3,KEY,"int")
(3,ID,"a")
(3,SYM,";")
(4,ID,"a")
(4,SYM,"=")
(4,NUM,"4")
(4,SYM,"+")
(4,NUM,"5")
(4,SYM,";")
(5,SYM,"}")
```

## Scripts

+ __compile.sh__
```
flex lexer.l     // colocar seu código FLEX no arquivo lexer.l
gcc -o lexer lex.yy.c -ll
```
+ __run.sh__ (recebe dois argumentos que deverão ser nomes de arquivos)
```
./lexer $1 $2
```

_Observação importante_: Arquivos de texto devem ser criados com Unix (usam apenas "\n" no final de linha).

-----
## Créditos 

Adaptação do material cedido pelo Prof. Vinicius Petrucci.
