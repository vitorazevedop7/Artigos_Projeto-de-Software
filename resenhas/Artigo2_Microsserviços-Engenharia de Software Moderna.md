# Resenha: Capítulo 7 - Arquitetura de Software

**Livro:** Engenharia de Software Moderna  
**Autor:** Marco Tulio Valente  
**Capítulo:** 7 - Arquitetura  
**Disciplina:** Projeto de Software - Engenharia de Software · PUC Minas

---

## 1. Conceito

O capítulo trata de arquitetura de software: o que é, por que importa e quais são os principais padrões usados na prática. O autor começa apresentando duas formas de entender o termo. A primeira define arquitetura como o projeto em alto nível, ou seja, a organização dos módulos, camadas e serviços de um sistema, deixando de lado os detalhes de classes individuais. A segunda, mais abrangente, considera arquitetura como o conjunto das decisões mais importantes de um projeto: escolha de linguagem, banco de dados, forma de comunicação entre sistemas. Essas decisões têm em comum o fato de serem difíceis ou quase impossíveis de reverter depois.

A partir daí, o capítulo apresenta os principais padrões arquiteturais: Arquitetura em Camadas, MVC, Microsserviços, Filas de Mensagens e Publish/Subscribe, além de padrões complementares como Pipes e Filtros e Cliente/Servidor. O capítulo fecha com a discussão de um anti-padrão, o Big Ball of Mud, que representa exatamente o oposto de uma arquitetura bem definida.

---

## 2. Análise

O capítulo funciona bem como introdução ao tema porque parte do concreto. Em vez de começar com definições abstratas, o autor usa exemplos reais para mostrar que decisões arquiteturais têm consequências duradouras. O debate entre Tanenbaum e Torvalds sobre o kernel do Linux é um deles: Ken Thompson, ainda nos anos 90, previu que a arquitetura monolítica do Linux viraria uma bagunça com o tempo. E virou. Em 2009, o próprio Linus admitiu publicamente que o kernel estava ficando grande demais. É um exemplo simples de como arquitetura é uma aposta no futuro que pode ou não se confirmar.

Um dos pontos mais úteis do texto é a distinção entre Arquitetura em Camadas e MVC, que costuma gerar confusão. MVC surgiu nos anos 70 para separar interface gráfica de lógica de negócio em aplicações desktop. Já a arquitetura em três camadas veio depois, pensada para sistemas distribuídos. Com a popularização da web e de frameworks como Spring, Rails e Django, os dois conceitos acabaram se misturando. O autor explica essa evolução histórica com cuidado, o que ajuda a entender por que hoje tanta gente usa os termos de forma intercambiável mesmo que tecnicamente sejam coisas diferentes.

A seção sobre Microsserviços é a mais densa e, de certa forma, a mais interessante. O ponto central é que microsserviços resolvem um problema bem específico: o gargalo entre times ágeis que desenvolvem rápido e processos de deploy lentos que existem em sistemas monolíticos. Ao separar o sistema em processos independentes, cada time pode fazer deploy do seu serviço sem precisar coordenar com todos os outros. Mas o capítulo é honesto sobre os custos: comunicação via rede é mais complexa e lenta do que chamadas de método locais, transações distribuídas são difíceis de garantir, e o sistema como um todo fica mais difícil de depurar. Microsserviços não são bala de prata. São uma solução para um problema específico que traz outros problemas junto.

As seções sobre Filas de Mensagens e Publish/Subscribe introduzem conceitos importantes para quem trabalha com sistemas distribuídos. O desacoplamento no espaço e no tempo que essas arquiteturas oferecem é um benefício real: sistemas que se comunicam via fila não precisam estar no ar ao mesmo tempo, e quem produz uma mensagem não precisa saber quem vai consumi-la. A diferença entre os dois padrões também está bem colocada. Fila de mensagens é comunicação ponto a ponto; pub/sub é comunicação em grupo. O exemplo da companhia aérea, onde uma venda dispara notificações simultâneas para o sistema de milhagens, de marketing e de contabilidade, ilustra bem quando pub/sub faz sentido.

O fechamento com o Big Ball of Mud como anti-padrão cria um contraste interessante com todo o conteúdo anterior. Se o capítulo inteiro é sobre como organizar bem um sistema, o anti-padrão mostra o que acontece quando isso não acontece. O caso do sistema bancário indiano com 25 milhões de linhas de código e 15 mil arquivos num único diretório torna isso concreto. O tempo de onboarding de novos engenheiros subindo de 3 para 7 meses em cinco anos é um dado que qualquer time de tecnologia deveria levar a sério.

---

## 3. Aplicação Prática

A maioria dos projetos reais passa por pelo menos um dos padrões discutidos no capítulo, às vezes sem que a equipe perceba. Um sistema web típico feito com Next.js e uma API em NestJS já segue, na prática, uma separação parecida com MVC: o frontend cuida da visão, a API cuida da lógica e da persistência. O problema é que quando esse projeto cresce sem planejamento, pode acabar no cenário oposto, com tudo misturado e sem fronteiras claras entre responsabilidades.

A Arquitetura em Camadas é provavelmente o padrão mais fácil de aplicar desde o início. Separar o código em camadas de apresentação, lógica de negócio e acesso a dados não exige nenhuma infraestrutura especial. É uma decisão de organização que qualquer time pode tomar. O benefício aparece na hora de trocar uma dependência: se o banco de dados estiver isolado numa camada própria, mudar de PostgreSQL para outro banco fica muito mais simples do que se as queries estiverem espalhadas por todo o código.

Microsserviços fazem sentido em contextos específicos. Para uma startup ou um projeto pequeno, a complexidade operacional de manter vários serviços independentes provavelmente não compensa. Mas à medida que o time cresce e diferentes partes do sistema passam a evoluir em ritmos diferentes, a separação em serviços começa a fazer mais sentido. A Lei de Conway ajuda a entender isso: o sistema tende a refletir a estrutura da organização. Times separados naturalmente produzem sistemas separados.

Filas de Mensagens são úteis sempre que dois sistemas precisam se comunicar mas não podem depender um do outro estar disponível ao mesmo tempo. No contexto de uma API de reembolso de despesas corporativas, por exemplo, integrar com um sistema de contabilidade externo via fila permite que os pedidos sejam processados mesmo que o sistema externo esteja temporariamente fora do ar. Os pedidos ficam na fila e são processados quando a conexão é restabelecida, sem perda de dados e sem impacto na experiência do usuário.

Por fim, o anti-padrão do Big Ball of Mud é um alerta útil para qualquer projeto em crescimento. Onboarding cada vez mais lento, correção de bugs que introduz novos bugs, funcionalidades simples levando tempo demais para implementar: esses são sinais de que a arquitetura precisa de atenção. E o mais importante é que práticas isoladas como documentação e revisão de código, como o caso do banco indiano mostrou, não resolvem um problema arquitetural. A solução precisa ser estrutural.
