# :cool: Open Closed Principle
> Princípio Aberto-Fechado - **Objetos ou entidades devem estar abertos para extensão, mas fechados para modificação.** Ou seja, quando novos comportamentos e recursos precisam ser adicionados no software, devemos estender e não alterar o código original.

### Como adicionar um novo comportamento sem alterar o código fonte já existente?
> Uncle Bob responde com as seguinte frases:
* Separe o comportamento extensível por trás de uma interface, e inverta as dependências.
* Se as abstrações são bem definidas, logo o software estará aberto para extensão.

### Exemplo
Utilizei o exemplo de uma classe de folha de pagamentos, que irá processar funcionário sênior e trainee.
##### Sem princípios
> Aqui a classe tem que verificar o tipo do funcionário, para então calcular sua remuneração. Veja a quantidade de **if e else** que seriam necessários caso fosse acrescentados novos tipos de funcionários. A chance de acrescentar uma nova regra e bugar todo o sistema é extremamente alta.
```typescript
class Payroll {
  protected balance: number = 0

  calculate (employe: any) {
    if (employe instanceof Senior) {
      this.balance = employe.salary()
    } else if (employe instanceof Trainee) {
      this.balance = employe.subsidy()
    }
    return this.balance
  }
}
```

##### Com princípios
> Veja que agora a classe de folha de pagamentos não precisa mais fazer verificações. Dessa forma essa classe **não precisa mais ser alterada** quando um novo tipo de cargo for cadastrado no sistema. Ela apenas precisa receber um funcionário do tipo **Remunerável**.
```typescript
class Payroll {
  protected balance: number = 0

  calculate (employe: Remunerable) {
    this.balance = employe.remuneration()
    return this.balance
  }
}
```

## Como executar?
```bash
npm install && npm run dev
```

## Créditos
:link: [O que é SOLID - João Roberto da Paixão](https://medium.com/desenvolvendo-com-paixao/o-que-%C3%A9-solid-o-guia-completo-para-voc%C3%AA-entender-os-5-princ%C3%ADpios-da-poo-2b937b3fc530)