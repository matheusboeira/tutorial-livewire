# Tutorial Livewire

Abaixo será demonstrado como criar e organizar os componentes do livewire na aplicação da `Thoth`. Os componentes do livewire servem para evitar o recarregamento desnecessário da página atual, isto é, executar alguma ação de CRUD e manter a página atual com os dados atualizados.

https://github.com/matheusboeira/tutorial-livewire/assets/76896958/86f966a6-dad9-41a6-b8dd-727be662732b

## Pré-Requisitos

- Criar uma branch com base na `develop` mais recente
- Executar os comandos básicos para executar a aplicação
- Executar `npm install` no container para habilitar algumas extensões (opcional)

## Entendendo a estrutura

Os componentes funcionam com apenas dois arquivos:
  - `app/Livewire/[ViewClass].php`: Onde é feita a lógica do componente _(classe php)_
  - `resources/views/livewire/[view].blade.php`: Onde é feita a parte visual do componente _(html, css, js)_

## Criando um componente

Para criar um componente, basta executar o comando `php artisan make:livewire [nome-do-componente]`. O comando irá criar os arquivos necessários para o componente. Como exemplo, irei executar os comandos abaixo:

```bash
# Para entrar no container
docker-compose exec app bash
```

```bash
# Para criar o componente
php artisan make:livewire Example
```

O resultado será a criação dos arquivos necessários (classe e view). Esses arquivos podem ser visualizados (assim como o caminho de onde foram criados) após executar os comandos como mostra a figura abaixo.

### Visualizando os arquivos criados

![component created](/images/component-created.png)

## Criando um componente para a aplicação

Para criar um componente para a aplicação, basta seguir o mesmo passo anterior, porém, com um nome mais específico e já passando o caminho de onde ficará.

Por exemplo, se eu quiser seguir as telas de Planning, eu coloco um prefixo `planning` para o nome do componente. O comando ficaria assim:

```bash
php artisan make:livewire planning.[nome-do-componente]
```

Isso vale para o restante também. Se eu quiser criar um arquivo da fase de "Conducting", eu coloco um prefixo `conducting` e assim por diante:

```bash
php artisan make:livewire conducting.quality-assessment
```
### Visualizando os arquivos criados
![quality assessment created](/images/quality-assessment-created.png)

## Exemplo Funcional

Para ajudar no entendimento de como prosseguir, acredito que já existem alguns bons exemplos criados. Todos os cards do `Overall` da fase de `Planning` já foram recriados nesse padrão. Os arquivos de views estão em `resources/views/livewire/planning/overall`.

https://github.com/matheusboeira/tutorial-livewire/assets/76896958/71a6c86e-2989-4d47-b0e9-e64082944205

Assim como as classes para essas views estão em `app/Livewire/Planning/Overall`. 

https://github.com/matheusboeira/tutorial-livewire/assets/76896958/10eeee3d-00f5-4651-8917-205b1ac7e6fd

## Como Usar

Para chamar os arquivos de view criadas pelo livewire, existem duas opções:

- Importar usando `@livewire('caminho.nome-do-componente')`
- Importar usando `<livewire:caminho.nome-do-componente />`

Ambas as opções funcionam da mesma forma, porém, usando a primeira opção pode ser mais fácil visualizar o componente, dependendo do editor que estiver usando.

![imports](/images/imports1.png)

![imports](/images/imports2.png)

## Padrões do livewire

Todas as tags do html possuem `binds` específicos para o livewire funcionar. Estes, são os atributos que começam com `wire:alguma-coisa`. 

Na tela de views do domain, é possível ver que todos os inputs possuem `wire:model` para que o livewire consiga capturar os valores dos inputs e fazer as ações necessárias. 

Assim como "wire:submit" para capturar o evento de submit do formulário.

![wire model](/images/code1.png)

É importante notar, que estes possuem valores específicos, como `wire:model="description"` e `wire:submit="submit"`.

Essas variáveis são as determinadas na classe do componente, e os métodos são os métodos que estão na classe do componente.

No exemplo dado, é feito um bind `wire:submit="submit"` para que o método `submit` seja chamado quando o formulário for submetido. O método `submit` deve estar contido na classe do componente.

![alt text](/images/code2.png)

## Rotas

Normalmente, se for feito uma refatoração, não será necessário criar nenhuma rota para utilizar o componente. Basta ir no arquivo onde já existe um caminho de acesso e importar o componente.

Em casos onde é necessário criar uma nova rota, basta ir no arquivo `web.php` e criar uma nova rota para o componente.

```php
# Método convencional
Route::get('/conducting/quality-assessment', [QualityAssessmentController::class, 'index'])
        ->name('conducting.quality-assessment.index')
        ->middleware('auth');

# Importando a classe do livewire diretamente
Route::get('/conducting/quality-assessment', [QualityAssessment::class, 'render'])
        ->name('conducting.quality-assessment')
        ->middleware('auth');
```

> Nota-se que esse `->name('alguma-coisa')` é usado nas páginas que possuem `tabs`. O nome é usado para identificar a aba que está sendo acessada. No exemplo abaixo, está sendo usada no atributo "route".

```php
$tabs = [
  'overview' => [
      'icon' => 'fas fa-info-circle',
      'label' => 'Overview',
      'route' => 'projects.show',
  ],
  'planning' => [
      'icon' => 'fas fa-calendar-alt',
      'label' => 'Planning',
      'route' => 'project.planning.index',
  ],
  'conducting' => [
      'icon' => 'fas fa-tasks',
      'label' => 'Conducting',
      'route' => null,
  ],
  'reporting' => [
      'icon' => 'fas fa-chart-bar',
      'label' => 'Reporting',
      'route' => 'reporting.index',
  ],
  'export' => [
      'icon' => 'fas fa-file-export',
      'label' => 'Export',
      'route' => null,
  ],
];
```


