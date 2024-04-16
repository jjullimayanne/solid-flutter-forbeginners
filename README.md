# Solid Dart concepts for beginners

## O => Open Closed Principle


Nessa clínica, existe uma classe que trata das solicitações de exames. Inicialmente, o único exame possível é o exame de sangue. Por isso, temos o código:

```dart
void main() {
  var exame = Exame("sangue");
  var aprovaExame = AprovaExame();
  aprovaExame.aprovarSolicitacaoDeExame(exame);
}

class AprovaExame {
  bool aprovarSolicitacaoDeExame(Exame exame) {
    if (exame.tipo == "sangue") {
      print("Exame de sangue liberado para ser feito");
      return true;
    }
     print("Exame reprovado!");
    return false;
  }
}

class Exame {
  String tipo;
  Exame(this.tipo);
}


```

Agora, precisamos incluir uma nova funcionalidade ao sistema: a clínica vai começar a fazer exames de Raio-X. Como incluir isso no nosso código?




```dart
void main() {
  var exame = Exame("raiox");
  var aprovaExame = AprovaExame();
  aprovaExame.aprovarSolicitacaoDeExame(exame);
}


class AprovaExame {
  void aprovarSolicitacaoDeExame(Exame exame) {
    if (verificaCondicoesExamedeSangue(exame)) {
      print("Exame de sangue liberado para ser feito");
    } else if(verificaCondicoesExamedeRaioX(exame)){
       print("Exame de RAIO X liberado para ser feito");
    }  
  }
  
  bool verificaCondicoesExamedeSangue(Exame exame) {
    if(exame.tipo == "sangue") {
      return true;
    }
    return false;
  }
    bool verificaCondicoesExamedeRaioX(Exame exame) {
    if(exame.tipo == "raiox") {
      return true;
    }
    return false;
  }
}

class Exame {
  String tipo;
  Exame(this.tipo);
}

```


Mas, e se além de raio-x, a clínica passasse a fazer também ultrassons? Seguindo a lógica, iríamos adicionar mais um if no código e mais um método para olhar condições específicas do exame.

Essa definitivamente não é uma boa estratégia. Cada vez que incluir uma função, a classe (e o projeto como um todo) vai ficar mais complexa.

Por isso, é necessário uma estratégia para adicionar mais recursos ao projeto, sem modificar e bagunçar a classe original.


Objetos ou entidades devem estar abertos para extensão, mas fechados para modificação,

