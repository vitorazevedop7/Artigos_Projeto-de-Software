# Resenha — *Big Ball of Mud*

**Artigo:** Big Ball of Mud  
**Autores:** Brian Foote e Joseph Yoder  
**Publicação:** PLoP '97 (Pattern Languages of Programs), 1997  
**Disciplina:** Projeto de Software — Engenharia de Software · PUC Minas

---

## 1. Conceito

O artigo fala sobre algo que todo programador já viu, mas que raramente alguém para para nomear: sistemas que crescem sem nenhum planejamento real, onde o código vai sendo remendado ao longo do tempo até virar uma bagunça difícil de entender e mais difícil ainda de mudar. Os autores chamam isso de **Big Ball of Mud (BBOM)**.

O que torna a leitura interessante é que Foote e Yoder não ficam jogando a culpa nos programadores. Eles reconhecem que esse tipo de sistema aparece por razões bem concretas: prazo curto, orçamento apertado, falta de experiência com o domínio do problema, requisitos que mudam no meio do caminho. Arquitetura bem feita custa caro e demora para dar retorno — e nem sempre existe tempo ou dinheiro pra isso.

A partir do BBOM, o artigo descreve mais cinco padrões que costumam andar junto: **Throwaway Code**, **Piecemeal Growth**, **Keep It Working**, **Sweeping It Under the Rug** e **Reconstruction**.

---

## 2. Análise

A maioria dos textos sobre arquitetura de software descreve como as coisas deveriam ser feitas. Este aqui faz o contrário: descreve como elas são feitas de verdade, e tenta entender por quê. Essa diferença de perspectiva já vale a leitura.

A comparação com cidades é um dos pontos mais interessantes do artigo. Cidades não crescem seguindo um plano — elas crescem respondendo ao que acontece no dia a dia. Brasília foi planejada do zero e até hoje tem dificuldade de se adaptar a demandas que não estavam no projeto original. São Paulo cresceu de forma caótica, mas é extremamente adaptável. Com software acontece a mesma coisa: sistemas muito planejados desde o início podem virar uma camisa de força quando os requisitos mudam.

Isso leva a um argumento que vai contra o senso comum: às vezes, não ter arquitetura no começo é melhor do que ter uma arquitetura errada. Kent Beck resume bem com a sequência "Make it work, make it right, make it fast" — primeiro faz funcionar, depois organiza, depois otimiza. Tentar fazer tudo ao mesmo tempo, antes de entender bem o problema, costuma criar mais complicação do que resolve.

O padrão **Throwaway Code** é o que mais acontece na prática. Você escreve um script rápido "só pra testar uma coisa", funciona, aí alguém pede pra adicionar mais uma feature, depois mais uma, e de repente aquele código descartável está rodando em produção há dois anos. O artigo conta exatamente isso com o sistema de inscrições de uma conferência de software: começou como experimento em shell script e HTML, deu certo, e ficou em uso por anos sem nenhuma reescrita.

Já o **Reconstruction** tem uma visão menos pessimista do que parece. Reescrever um sistema do zero não significa jogar tudo fora — o conhecimento sobre o domínio, os erros cometidos, o que funcionou e o que não funcionou, tudo isso fica. O que se descarta é só o código ruim. Na prática, uma reescrita bem feita é uma forma de aproveitar tudo que foi aprendido e começar com uma base melhor.

O artigo foi escrito em 1997, então não fala de coisas como integração contínua ou microsserviços. Mas as forças que ele descreve — pressão de prazo, custo, incerteza — continuam exatamente as mesmas hoje.

---

## 3. Aplicação Prática

É difícil ler esse artigo sem se reconhecer em alguma das situações descritas. Qualquer projeto que começa pequeno e vai crescendo sem revisão periódica da estrutura está no caminho do BBOM. Um sistema de agendamento que começa como uma planilha adaptada, por exemplo, se funciona, dificilmente vai ser reescrito do zero — vai sendo estendido até ficar irreconhecível. O cliente não vê o código por dentro, vê o que funciona. E o que funciona não costuma ser reescrito.

O **Keep It Working** tem uma relação direta com o que hoje chamamos de CI/CD. A ideia de sempre manter uma versão funcional do sistema, fazendo mudanças pequenas e verificando que nada quebrou, é exatamente o que pipelines de integração contínua automatizam. A Microsoft já exigia um *daily build* em 1997 por esse motivo — cada dia terminava com o sistema funcionando, o que tornava muito mais fácil identificar o que havia quebrado.

**Sweeping It Under the Rug** é o que acontece quando você cria uma camada de abstração em torno de um módulo bagunçado. Em vez de reescrever tudo, você expõe uma interface limpa e deixa a bagunça escondida por trás dela. Em projetos Next.js isso aparece bastante: integrações com APIs externas ou serviços antigos ficam encapsuladas dentro de um módulo próprio, e o resto da aplicação não precisa saber como aquilo funciona por dentro. Não é a solução perfeita, mas muitas vezes é a única que cabe no prazo.

**Piecemeal Growth** é basicamente o que metodologias ágeis pregam hoje: crescer o sistema aos poucos, entregando funcionalidades em ciclos curtos. O risco que o artigo aponta é real — esse crescimento incremental, se não tiver refatoração junto, vai degradando a estrutura sem que ninguém perceba. Quando alguém finalmente para pra olhar, o sistema já está num estado que ninguém mais entende completamente.

A decisão de fazer uma **Reconstruction** é sempre difícil. Reescrever tem custo alto e não garante resultado melhor — Brooks fala do "second system effect", onde a segunda versão tende a ser supercomplicada porque o time quer corrigir todos os erros da primeira de uma vez. Mas quando o sistema chegou num ponto em que ninguém mais consegue entender o que ele faz ou modificá-lo sem quebrar outra coisa, reescrever passa a ser mais barato do que continuar tentando remendar.

No fim, um dos maiores valores do artigo é mesmo o vocabulário que ele oferece. Quando uma equipe consegue dizer "esse código aqui virou um BBOM" ou "isso é um Throwaway Code que nunca foi descartado", a conversa sobre o que fazer fica mais fácil. Nomear o problema não resolve nada por si só, mas ajuda bastante a começar a resolver.
