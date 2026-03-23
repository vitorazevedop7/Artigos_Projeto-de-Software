# Resenha: On the Criteria To Be Used in Decomposing Systems into Modules
 
**Artigo:** On the Criteria To Be Used in Decomposing Systems into Modules  
**Autor:** D.L. Parnas  
**Publicação:** Communications of the ACM, Vol. 15, No. 12, dezembro de 1972  
**Disciplina:** Projeto de Software - Engenharia de Software · PUC Minas
 
---
 
## 1. Conceito
 
O artigo discute um problema que parece simples mas tem consequências profundas: como dividir um sistema em módulos. A motivação é clara desde o início. Modularização bem feita reduz o tempo de desenvolvimento, porque times diferentes podem trabalhar em paralelo com pouca necessidade de coordenação. Ela também torna o sistema mais fácil de mudar e mais fácil de entender.
 
O problema é que a maioria das abordagens da época dividia o sistema seguindo o fluxo de execução, ou seja, cada etapa do processamento virava um módulo. Parnas argumenta que esse critério é o errado. A alternativa que ele propõe é o information hiding: cada módulo deve ser responsável por esconder uma decisão de design do restante do sistema. As outras partes não precisam saber como aquele módulo funciona internamente, apenas o que ele oferece como interface.
 
Para ilustrar a diferença, o artigo usa um sistema de índice KWIC como exemplo e mostra duas formas de modularizá-lo. A primeira segue a abordagem convencional por etapas de processamento. A segunda aplica information hiding. A comparação entre as duas é o núcleo do artigo.
 
---
 
## 2. Análise
 
O que torna o artigo eficaz é a comparação direta entre as duas modularizações com o mesmo sistema. Não é uma discussão abstrata sobre princípios. Parnas pega um exemplo concreto e mostra, passo a passo, o que acontece quando uma decisão de design precisa mudar em cada uma das abordagens.
 
Na primeira modularização, uma mudança simples como alterar a forma de armazenar as linhas em memória afeta praticamente todos os módulos. Isso acontece porque o formato interno de armazenamento foi exposto como parte da interface entre os módulos. Todos dependem dessa estrutura e precisam ser atualizados quando ela muda. Na segunda, essa mesma mudança fica contida dentro de um único módulo. O restante do sistema nem sabe que ela aconteceu.
 
Esse contraste é importante porque mostra que modularização não é apenas uma questão de organização visual do código. Um sistema pode parecer bem dividido em módulos e ainda assim ser frágil a mudanças, se os módulos estiverem se comunicando por meio de detalhes internos que deveriam estar escondidos.
 
Parnas também observa algo que não é óbvio: os dois sistemas podem gerar código executável idêntico. A diferença entre eles não aparece no que o programa faz, mas em como ele é dividido para fins de desenvolvimento, manutenção e compreensão. Isso reforça a ideia de que arquitetura não é sobre fazer o sistema funcionar, é sobre garantir que ele possa ser mudado, entendido e evoluído ao longo do tempo.
 
Um ponto que vale destacar é a discussão sobre estrutura hierárquica no final do artigo. Parnas deixa claro que hierarquia e boa decomposição são propriedades independentes. Um sistema pode ter hierarquia sem ter módulos bem definidos, e pode ter módulos bem definidos sem uma hierarquia clara. Buscar as duas coisas é desejável, mas não são a mesma coisa.
 
O artigo tem uma limitação honesta: a segunda modularização pode ser menos eficiente em tempo de execução, porque a comunicação entre módulos via interfaces abstratas pode gerar overhead de chamadas de função. Parnas reconhece isso e sugere que a solução está nas ferramentas de implementação, não no design. É uma separação importante entre decisão de arquitetura e detalhe de implementação.
 
---
 
## 3. Aplicação Prática
 
O princípio de information hiding é uma das ideias mais duráveis da engenharia de software. Ele está por trás de conceitos que qualquer desenvolvedor usa hoje sem necessariamente saber de onde vieram, como encapsulamento em orientação a objetos, interfaces em TypeScript, repositórios em arquitetura de aplicações, e a separação entre API pública e implementação interna em qualquer biblioteca.
 
A situação descrita na primeira modularização é muito comum em projetos reais. Quando uma estrutura de dados compartilhada começa a ser usada diretamente por vários módulos, qualquer mudança nela se propaga pelo sistema inteiro. É o tipo de acoplamento que transforma uma alteração simples num trabalho de dias, porque ninguém sabe ao certo o que mais pode quebrar. Em projetos com banco de dados, isso aparece quando a estrutura das tabelas é acessada diretamente por várias partes do código em vez de passar por uma camada de repositório.
 
A ideia de começar a modularização identificando as decisões de design que podem mudar é um exercício útil antes de qualquer projeto. Em vez de perguntar "quais são as etapas do processo?", a pergunta passa a ser "o que eu não sei ainda, ou o que provavelmente vai mudar?". Formato de entrada de dados, forma de armazenamento, algoritmo de ordenação, protocolo de comunicação: cada um desses itens é um candidato a ser encapsulado em seu próprio módulo com interface estável.
 
Em um projeto de API, por exemplo, a forma como os dados são persistidos no banco é uma decisão que pode mudar: trocar PostgreSQL por outro banco, mudar o ORM, alterar o schema. Se essa decisão estiver escondida atrás de uma camada de repositório com interface bem definida, o restante da aplicação não precisa ser alterado quando a mudança acontece. Se estiver exposta, a mudança se espalha.
 
O argumento de Parnas também se aplica ao trabalho em equipe. Quando módulos se comunicam por interfaces simples e abstratas, times diferentes podem trabalhar em paralelo com muito menos necessidade de coordenação. Cada time precisa entender a interface do módulo que vai usar, não os detalhes internos de como ele funciona. Isso reduz o número de decisões que precisam ser tomadas em conjunto antes de o trabalho começar, e é exatamente um dos problemas que microsserviços tentam resolver décadas depois, em um contexto diferente mas com a mesma lógica por trás.
 
