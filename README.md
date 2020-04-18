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
```
put 'italians', '11', 'personal-data:name',  'Paolo Barbieri'
put 'italians', '11', 'personal-data:city',  'Rome'
put 'italians', '11', 'personal-data:birth', '1960-07-15'
put 'italians', '11', 'professional-data:role',  'TI'
put 'italians', '11', 'professional-data:salary',  '2500'
put 'italians', '11', 'professional-data:experience',  '5'
put 'italians', '12', 'personal-data:name',  'Vincenzo Lombardo'
put 'italians', '12', 'personal-data:city',  'Milan'
put 'italians', '12', 'personal-data:birth', '1975-03-11'
put 'italians', '12', 'professional-data:role',  'Analista de sistemas'
put 'italians', '12', 'professional-data:salary',  '5000'
put 'italians', '12', 'professional-data:experience',  '8'
```
2. Adicione o controle de 5 versões na tabela de dados pessoais.
<pre>hbase(main):019:0&gt; alter &apos;italians&apos;, NAME =&gt; &apos;personal-data&apos;, VERSIONS =&gt; 5
Updating all regions with the new schema...
1/1 regions updated.
Done.
Took 1.8716 seconds   </pre>
3. Faça 5 alterações em um dos italianos;
```
put 'italians', '11', 'personal-data:name',  'Paolo Barbieri 1'
put 'italians', '11', 'personal-data:name',  'Paolo Barbieri 2'
put 'italians', '11', 'personal-data:name',  'Paolo Barbieri 3' 
put 'italians', '11', 'personal-data:name',  'Paolo Barbieri 4'
put 'italians', '11', 'personal-data:name',  'Paolo Barbieri 5'
```
4. Com o operador get, verifique como o HBase armazenou o histórico.
<pre>hbase(main):001:0&gt; get &apos;italians&apos;,&apos;11&apos;,{COLUMN=&gt;&apos;personal-data:name&apos;,VERSIONS=&gt;5}
COLUMN                CELL                                                      
 personal-data:name   timestamp=1587237259981, value=Paolo Barbieri 5           
 personal-data:name   timestamp=1587237259197, value=Paolo Barbieri 4           
 personal-data:name   timestamp=1587237259183, value=Paolo Barbieri 3           
 personal-data:name   timestamp=1587237259168, value=Paolo Barbieri 2           
 personal-data:name   timestamp=1587237259156, value=Paolo Barbieri 1           
1 row(s)
Took 0.4270 seconds</pre>
5. Utilize o scan para mostrar apenas o nome e profissão dos italianos.
```
scan 'italians', {COLUMNS => 'personal-data:name'}
```
6. Apague os italianos com row id ímpar
```
deleteall 'italians', '1'
deleteall 'italians', '11'
deleteall 'italians', '3'
deleteall 'italians', '5'
deleteall 'italians', '7'
deleteall 'italians', '9'
```
7. Crie um contador de idade 55 para o italiano de row id 5
<pre>hbase(main):014:0&gt; incr &apos;italians&apos;, &apos;2&apos;, &apos;personal-data:age&apos;
COUNTER VALUE = 1
Took 0.0466 seconds </pre>
8. Incremente a idade do italiano em 1
<pre>hbase(main):015:0&gt; incr &apos;italians&apos;, &apos;2&apos;, &apos;personal-data:age&apos;
COUNTER VALUE = 2
Took 0.0091 seconds </pre>
