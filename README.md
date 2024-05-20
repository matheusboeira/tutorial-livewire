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

O resultado será a criação dos arquivos `Livewire/Example.php` e `Views/Livewire/example.blade.php`. Estes arquivos podem ser visualizados (assim como o caminho de onde foram criados) após executar os comandos como mostra a figura abaixo.

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

> Este comando vai criar dois arquivos: `Livewire/Conducting/QualityAssessments.php` e `Views/Livewire/conducting/quality-assessments.blade.php`.

![quality assessment created](/images/quality-assessment-created.png)
