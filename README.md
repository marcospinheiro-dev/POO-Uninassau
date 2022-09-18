# POO-Uninassau
Troabalho sobre os pilares de POO



#Herança
Ao olharmos no dicionário o conceito de herança, encontramos o seguinte:
“Conjunto de caracteres hereditários transmitidos pelos genes. Bem, direito ou obrigação transmitidos por disposição testamentária ou por via de sucessão.”
Como mencionei anteriormente, todas as pessoas herdam a aparência dos pais e as ações da espécie humana, como respirar e dormir. Trazendo para o contexto da programação, as classes podem herdar atributos e funções de outras classes.
Chamamos as classes que transferem comportamentos e atributos de super classes; e chamamos as classes que herdam esses comportamentos e atributos de sub Classes. Por isso, super classes normalmente são definições mais genéricas de uma entidade, enquanto que as sub classes são definições mais específicas.
Essas classes possuem uma relação de “é um(a)“. Por exemplo:
Todo cachorro é um mamífero, assim como todo Pinscher é um cachorro.
Seguindo essa lógica, todo cachorro tem comportamentos de mamífero e todo Pinscher possui os comportamentos de um cachorro. Consequentemente, todo Pinscher possui os comportamentos de um mamífero. Podemos modelar esse exemplo com o seguinte código:
class Mamifero {
	respirar() {
		console.log('Respirando...');
	}
}

/* 
 *	Utilizamos a palavra chave extends
 *	para definir essa relação
*/ 

class Cachorro extends Mamifero { 
	latir() {
		console.log('Woof Woof');
	}
}

class Pinscher extends Cachorro {
	modoRaiva() {
		console.log('Entrando em modo de raiva!');
	}
}
Repare que essa relação é apenas de uma via. Sub Classes só podem acessar características e comportamentos de Super Classes, mas o contrário não é verdadeiro. Uma Super Classe não tem acesso a características e comportamentos de uma Sub Classe.
É graças a esse pilar que podemos fazer reuso de código, porque não precisamos reescrever o mesmo comportamento em diferentes classes. 

#Polimorfismo
Com o polimorfismo espera-se que ao receber entradas de tipos diferentes, uma mesma ação possa ser executada de formas diferentes. Veja o exemplo:

class Impressora {
    fun imprimir(numero: Int) {
        println("Imprimindo um numero! $numero");
    }
    
    fun imprimir(palavra: String) {
        println("Imprimindo uma palavra! $palavra");
    }
}

fun main(args: Array<String>) {
	val impressora = Impressora();
    impressora.imprimir(3);
    impressora.imprimir("Opa!");

}

Ao sobrescrever o método, passando entradas diferentes, temos implementações diferentes. Ou seja, ao receber entradas de tipos diferentes, seja um Int, ou uma String, a mesma ação (imprimir) terá comportamentos diferentes.
Esse é um caso de polimorfismo estático (ou polimorfismo em tempo de compilação), mas existe também o polimorfismo dinâmico (ou polimorfismo de tempo de execução). Para entender esse segundo tipo, considere o seguinte cenário:
Você foi escolhido para trabalhar no desenvolvimento de um jogo de corrida. Nesse jogo, o jogador vai usar um Veículo para alcançar a linha de chegada antes de seus adversários. Dentre os veículos, você pode usar tanto um Carro quanto uma Motocicleta. Ambos podem Ligar e Acelerar.
Vamos elaborar esse cenário utilizando Herança? Nesse caso utilizando TypeScript. 
1. Defina uma classe Veiculo que possui 2 método, ligar e acelerar.
class Veiculo {
  ligar() {
    console.log("Ligando o veículo...");
  }
  acelerar() {
    console.log("Acelerando...");
  }
}
2. Em seguida, defina duas classes: Carro e Motocicleta. Ambas devem ter como Super Classe Veículo e sobrescrever os métodos ligar e acelerar para estarem de acordo com seu funcionamento no mundo real.
class Carro extends Veiculo {
  ligar() {
    console.log("Girando a chave...");
  }
  acelerar() {
    console.log("Pisando no acelerador...");
  }
}
class Motocicleta extends Veiculo {
  ligar() {
    console.log("Pisando no pedal...");
  }
  acelerar() {
    console.log("Girando a manopla do acelerador...");
  }
}
3. Fora dessas classes, defina uma função chamada dirigir que recebe como parâmetro um objeto do tipo Veiculo.

function dirigir(veiculo: Veiculo) {
  veiculo.ligar();
  veiculo.acelerar();
}
4. Invoque a função dirigir passando instâncias de cada um dos veículos criados
dirigir(new Carro());
dirigir(new Motocicleta());
5. O resultado final ser algo parecido com isso:
Girando a chave... 
Pisando no acelerador... 
Pisando no pedal... 
Girando a manopla do acelerador...

A função dirigir espera um objeto do tipo Veículo, mas mesmo assim conseguimos passar objetos do tipo Carro e Motocicleta. Isso só é possível porque as classes Carro e Motocicleta herdam de Veículo. Logo, Carro e Motocicleta são Veículos e, automaticamente, possuem os métodos ligar e acelerar.
Nesse exemplo, a função dirigir recebe objetos de tipos diferentes, executa uma mesma ação só que em suas respectivas implementações. O carro ligando com a chave na ignição, a moto pisando no pedal; o carro acelerando pisando no pedal, enquanto a moto gira a manopla do acelerador.








#Abstração
Quando buscamos o significado de abstração no dicionário, uma das definições que encontramos é a seguinte:
“Ação de abstrair, de analisar isoladamente um aspecto, contido num todo, sem ter em consideração sua relação com a realidade.”
Com esse pilar uma classe deve expor para outras classes apenas a ideia geral de uma propriedade ou funcionalidade, sem entrar nos detalhes. Por exemplo, um liquidificador possui 3 velocidades. Nós não sabemos como a velocidade da hélice é calculada, nem como internamente o apertar de um botão faz ela rodar, mas sabemos que ao apertar um botão a hélice irá girar de acordo com a velocidade escolhida.
Podemos alcançar abstração através de classes abstratas ou interfaces, que funcionam como uma espécie de contrato. Interfaces e classes abstratas apenas definem o que uma classe deve fazer, enquanto o dever da classe é implementar como a classe irá fazer. Uma possível refatoração do exemplo do veículo seria a seguinte:
1. Defina uma interface Veículo:
interface Veiculo { 
  ligar();
  acelerar(); 

}
As classes Carro e Motocicleta agora devem implementar a interface Veiculo
class Carro implements Veiculo {
  ligar() {
    console.log("Girando a chave...");
  }
  acelerar() {
    console.log("Pisando no acelerador...");
  }
}
class Motocicleta implements Veiculo {
  ligar() {
    console.log("Pisando no pedal...");
  }
  acelerar() {
    console.log("Girando a manopla do acelerador...");
  }
}
O resto do código permanece o mesmo



#Encapsulamento
O objetivo desse pilar é restringir a visibilidade e modificação de atributos e de acesso a comportamentos baseado em algumas regras definidas em código.
Para entender melhor essas restrições, considere o painel de um carro. Para o motorista, basta girar a chave que o painel acenderá e lá estarão as informações. No entanto, existe uma série de mecanismos envolvidos nessa operação. O painel não sabe qual o nível da água nem o nível da gasolina, ele apenas recebe esses dados e apresenta para o motorista.
Nesse exemplo, podemos ver que o painel do carro esconde o seu funcionamento interno dos usuários. Mas, em alguns casos, o próprio código esconde propriedades e/ou comportamentos do sistema como um todo. O painel do carro, sabe quanto de gasolina o carro ainda tem, mas não sabe como a gasolina é injetada no motor.
Na programação, isso só é possível porque existem vários níveis de restrição, indo do mais ao menos restrito. Chamamos esses níveis de restrição de modificadores de acesso, pois eles modificam a acessibilidade desses comportamentos e atributos.
Qual a diferença entre Encapsulamento e Abstração?
Esses dois pilares de Orientação a Objetos as vezes pode confundir, mas a diferença é bem clara. A abstração se limita ao design e modelagem da sua aplicação. Já o encapsulamento busca esconder o funcionamento interno relacionado ao código e a implementação.
Agora você já conhece os pilares da Orientação a Objetos e como eles melhoram o desenvolvimento da sua aplicação. Ao longo do tempo esse conceito ficará cada vez mais natural e a sua prática será cada vez melhor. Lembre-se, programação é treino! 

