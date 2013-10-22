#Desafio: Validação de E mail

[Utilize o regexpal para testar e criar a sua expressão regular.](http://regexpal.com)

Segundo a spec, emails podem ser bem esquisitos, por exemplo, isto são emails válidos:

``` txt
"andré trevisani"@domain.com
andre=trevisani@domain.com
por" mais incrível"que'pareca'{isto.eh}um.email_valido@domain.com
```

### Regras
Mas para fins de aprendizado vamos especificar algumas regras do nosso email:
* O nome (o que vem antes do @)
  1. Só letras minúsculas, números e '_'
  2. Deve começar com uma letra
  3. PODE conter UM '.'
  4. Se houver um ponto, o próximo caractere deve ser uma letra, ou seja, isso não pode: andre.77@gmail.com
* Deve ter um @
* O domínio (o que vem depois do @)
  1. Só letras minúsculas e números (não pode '_')
  2. Deve começar com uma letra
  3. Devem terminar por ".algumacoisa" ou “.alguma.coisa”, não pode ter mais de 2 pontos! Nem terminar só com ponto, ou seja, isso não pode “andre@alguma.coisa.”
  4. Esse "algumacoisa" deve ser composto somente de letras: Ex: "teste.org", "teste.com", "teste.com.br"

### O que pode:

``` txt
eu@gmail.com
sou.eu@gmail.com
sou_eu@gmail.com
eu@g.com
eu@yahoo.com.br
eu@meudomino.net
sou.eu@gmail.com
eu07@gmail.com
sou.eu12@gmail.com
eu_@gmail.com
eu@g1.com
```

### O que não pode:
``` txt
eugmail.com
eu@7a.com.br
@gmail.com
eu@gmail
eu@.com
eu@gmail.
eu$gmail$com
sou.eu.mesmo@gmail.com
eu @gmail.com
sou-eu@gmail.com
EU@GMAIL.COM
eu@bol.com.
eu@rbs_tv.com.br
eu@domino.hpg.com.br
.@gmail.com
eu.@gmail.com
.eu@gmail.com
02@gmail.com
a02.@gmail.com
a02.12@gmail.com
1.a@gmail.com
_eu@gmail.com
" se_liga_no_inicio@efim.da.string "
```

### Dicas
Façam como o tio Jack, por partes! Fica mais fácil!

`REGEX_QUE_VALIDA_O_NOME@.*` depois `.*@REGEX_QUE_VALIDA_O_DOMINIO`        

Depois junta as duas: 

```
REGEX_QUE_VALIDA_O_NOME@REGEX_QUE_VALIDA_O_DOMINIO 
```
__________________

#Desafio: Validação de Palíndromos.

[Utilize o regexpal para testar e criar a sua expressão regular.](http://regexpal.com)

Palíndromos, são palavras ou frases que podem ser lidas em qualquer direção. Em caso de frases podemos ignorar os espaços. 

### Exemplos
``` txt
ovo
Hagah
Socorram-me subi no ônibus em marrocos
```

Entretanto, pesquisando na internet vi que identificar palíndromos com regex é BEM complicado, e dependendo da linguagem, não é possível.
Mas, podemos reduzir a complexidade, para aprendizado. Podemos identificar **palíndromos de tamanho fixo**, somente com letras minúsculas e espaços.

Uma das maneiras de verificar se um "match" ocorre novamente, é utilizando **capturing-groups** e **back references**.

Uma regex para pegar as palavras `ovo` e `eve` poderia ser assim:
`(o|e)v(o|e) // Um 'o' ou 'e', seguido de 'v', seguido de 'o' ou 'e'.`

Entretando ela dá match para `'ove'` e `'evo'`. E não queremos isso, queremos que ela pegue na terceira letra exatamente o que pegou na primeira. Para isso, modificamos a regex:
`(o|e)v\1 // Um 'o' ou 'e', seguido de 'v', seguido da mesma coisa que tu pegou no parênteses 1`

Podemos por exemplo, verificar quais emails tem o mesmo nome e domínio, finalizando com .com:
``` txt
andre@andre.com
gmail@gmail.com
```

A regex (somente para letras minusculas) seria assim:
`([a-z]+)@\1\.com`

Enfim, o desafio de hoje pode ser resolvido de várias formas, mas é bem provável que uma das mais simples é utilizando capturing groups, e back references.

### Regras

* Reconhecer palíndromos de 2 (`ovo`, `erre`), 3 (`rotor`) ou 4 (`sopapos`, `anilina`) caracteres, pode ser qualquer coisa, só que pra facilitar, não vamos brincar com acentos, nem maiúsculas. Ou seja, isso vai ter: `12aa21` mas isso não: `anã` ou `Alá`
* O caractere 'do meio' pode aparecer só uma vez. Ex: `ovo`
* Pode ter espaços. Ex: `123 44 3 21`
* A String **toda** deve ser um Palíndromo

###O que pode:
``` txt
1221
121
ovo
123321
12321
rotor
12344321
1234321
sopapos
anilina
1 234 43 21
12 34 321
o vo
ro tor
an il in a
```

### Oque não pode:
``` txt
isto é um palíndromo?
123123
1234432a
A23432B
isto não 123321 é um palíndromo!
1 1
 a a
 bb 
 c 
```

### Dicas
Os palíndromos de exemplo estão em ordem de complexidade. Solucione um, depois expanda sua regex para pegar o próximo. A regex final deve pegar todos os válidos, e nenhum dos inválidos!
