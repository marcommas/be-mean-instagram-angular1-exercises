Nome: Marco Comassetto

Github: [marcommas](https://github.com/marcommas/)

Data: 12/05/2016
```html
<!doctype html>
<html lang="pt-br" data-ng-app="BeMEAN">
<head>
  <meta charset="utf-8">
  <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.6/css/bootstrap.min.css">
  <title>BeMEAN AngularJS - Ex 4</title>
</head>
<body data-ng-controller="UserController as User">
  <div class="container">

      <h1>{{User.titulo}}</h1>
      <label>Busca: <input ng-model="searchUser"></input></label>
      <span data-ng-init="predicate = 'city'; reverse = false;"></span>

      <table class="table">
        <thead>
          <tr>
            <th data-ng-repeat="(key, value) in User.users[0]">{{key}}</th>
          </tr>
        </thead>
        <tbody>
          <tr  data-ng-repeat="user in User.users | orderBy:predicate:reverse | filter:searchUser">
            <td data-ng-repeat="(key, value) in user">{{value}}</td>
          </tr>
        </tbody>
      </table>


      <div data-ng-controller="CursoController as Curso">
        <h2>{{Curso.titulo}}</h2>
         <label>Busca: <input ng-model="searchCurso"></input></label>
        <table class="table">
          <thead>
            <tr>
              <th data-ng-repeat="(key, value) in Curso.cursos[0]">{{key}}</th>
            </tr>
          </thead>
          <tbody>
            <tr  data-ng-repeat="curso in Curso.cursos | orderBy:predicate:reverse | filter:searchCurso">
              <td data-ng-repeat="(key, value) in curso">{{value}}</td>
            </tr>
          </tbody>
        </table>

      </div>


      <div data-ng-controller="ProfessorController as Professor">
        <h2>{{Professor.titulo}}</h2>
         <label>Busca: <input ng-model="searchProfessor"></input></label>
           <table class="table">
            <thead>
              <tr>
                <th data-ng-repeat="(key, value) in Professor.professores[0]">{{key}}</th>
              </tr>
            </thead>
            <tbody>
              <tr  data-ng-repeat="professor in Professor.professores | orderBy:predicate:reverse | filter:searchProfessor">
                <td data-ng-repeat="(key, value) in professor">{{value}}</td>
              </tr>
            </tbody>
          </table>


      
       
        <h2>BeMean - Maior de idade</h2>
        <label>Busca: <input ng-model="searchProfessorFilter"></input></label>
         <table class="table">

          <tbody>
            <tr  data-ng-repeat="professor in Professor.professores | orderBy:predicate:reverse | filter:searchProfessorFilter">
              <td>{{ professor.nome }}</td>
              <td>{{ professor.email }}</td>
              <td>{{ professor.idade }}</td>
              <td>{{ professor.idade | confereIdade}} </td>
              <td>{{professor.city}}</td>
            </tr>
          </tbody>
          </table>
      </div>


  </div>
  <script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.5.5/angular.min.js"></script>

  <script>
    angular.module("BeMEAN", [])
      .controller('UserController', UserController)
      .controller('CursoController', CursoController)
      .controller('ProfessorController', ProfessorController)

      .filter('confereIdade', function() {
        return function(text) {
          if (text) {
            if (isNaN(text)) return 'Idade inválida';
            if (text >= 18) return 'Maior de idade';
            else return 'Menor de idade';
          }
        }
      });

    function UserController() {
      var vm = this;
      vm.titulo = "Be MEAN - Listagem dos usuários";
      vm.users = [
        {name: 'Suissa', email: 'suissera@manoveio.com', city : 'Concórdia'}
      , {name: 'João', email: 'joao@macioesedoso.com', city : 'São José'}
      , {name: 'Franciele', email: 'fran@quimica.com', city : 'Floripa'}
      ];
    }

    function CursoController() {
      var vm = this;
      vm.titulo = "Be MEAN - Cursos";
      vm.cursos = [
        {name: 'Be Mean', teacher: 'suissa', city : 'Concórdia'}
      , {name: 'Learn Machine', teacher: 'Ivan', city : 'São José'}
      , {name: 'Laravel', teacher: 'Michel', city : 'Floripa'}
      ];
    }

    function ProfessorController(){
      var vm = this;
      vm.titulo = "BeMEAN - Professor";
      vm.professores = [
        {nome: 'Marco', email: 'marco@email.com', idade: '17', city : 'Concórdia'}
        ,{nome: 'Glimar', email: 'glimar@email.com', idade: 'abc', city : 'Joaçaba'}
        ,{nome: 'Dulce', email: 'dulce@email.com', idade: '18', city : 'São José'}
        ,{nome: 'Paola', email: 'paola@email.com', idade: '16', city : 'Curitiba'}
        ,{nome: 'Guilherme', email: 'gui@email.com', idade: '20', city : 'Floripa'}
      ];
    }

  </script>
</body>
</html>
