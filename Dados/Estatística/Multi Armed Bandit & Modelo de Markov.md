https://www.youtube.com/watch?v=e3L4VocZnnQ

**Estratégia Epsilon Greedy** - balanceamento
escolhe-se uma porcentagem ε entre 0 e 1 para a probabilidade de haver exploração. Então o fator para explotação é 1 - ε.

No começo a exploração tende a ser maior para icentivar o entendimento da situação, porém com alguns de dados acumulados já é possível focar na explotação para melhor rendimento.


**Estratégia UCB** (Upper Confidence Bound Strategy) - benefício da dúvida
Se dois restaurante tem médias similares de "qualidade" devemos visitar o próximo com base na quantidade de vezes em que ele foi visitado, tendo em mente que provavelmente um pode ter sido menos visitado que o outro. Quando há uma discrepância muito grande no número de visitas a média pode não retratar bem a realidade

**Desvantagens**
- A UCB favorece ações que têm alta confiança em suas recompensas esperadas. No entanto, em sistemas com muitos cenários (também chamados de **espaço de ação grande**), ações que não foram suficientemente testadas podem ser negligenciadas.
- Isso ocorre porque a fórmula do UCB reduz o peso da exploração à medida que o número total de tentativas aumenta, mesmo para ações raramente escolhidas.
- A UCB depende de uma estimativa precisa da recompensa média e da incerteza associada. Se os dados iniciais forem esparsos ou enviesados, as decisões subsequentes podem ser comprometidas.

https://medium.com/itau-data/multi-armed-bandits-uma-alternativa-para-testes-a-b-d5db47d24006

---


https://leandrocruvinel.medium.com/cadeias-de-markov-com-python-ef27b3f21fc7![[aulas.descomplica.com.br-Aplicações estatísticas.pdf]]