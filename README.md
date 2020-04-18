# hbase

## Atividade Prática – HBase

### Procedimentos iniciais
1. Crie a tabela com 2 famílias de colunas:
  a. personal-data
  b. professional-data
<pre>hbase(main):001:0&gt; create &apos;italians&apos;, &apos;personal-data&apos;, &apos;professional-data&apos;
Created table italians
Took 1.1538 seconds                                                             
=&gt; Hbase::Table - italians
</pre>  
2. Importe o arquivo via linha de comando
<pre>root@9095c7a74d74:/# hbase shell /tmp/italians.txt
2020-04-18 18:56:36,928 WARN  [main] util.NativeCodeLoader: Unable to load native-hadoop library for your platform... using builtin-java classes where applicable
Took 0.4233 seconds                                                             
...
...
Took 0.0021 seconds                                                             
HBase Shell
Use &quot;help&quot; to get list of supported commands.
Use &quot;exit&quot; to quit this interactive shell.
For Reference, please visit: http://hbase.apache.org/2.0/book.html#shell
Version 2.1.2, r1dfc418f77801fbfb59a125756891b9100c1fc6d, Sun Dec 30 21:45:09 PST 2018
Took 0.0012 seconds </pre>
### Operações:
1. Adicione mais 2 italianos mantendo adicionando informações como data de nascimento nas informações pessoais e um atributo de anos de experiência nas informações profissionais;

2. Adicione o controle de 5 versões na tabela de dados pessoais.

3. Faça 5 alterações em um dos italianos;

4. Com o operador get, verifique como o HBase armazenou o histórico.

5. Utilize o scan para mostrar apenas o nome e profissão dos italianos.

6. Apague os italianos com row id ímpar

7. Crie um contador de idade 55 para o italiano de row id 5

8. Incremente a idade do italiano em 1
