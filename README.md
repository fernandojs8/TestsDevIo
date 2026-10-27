# TestsDevIo — testes de software em C#

Laboratório de testes automatizados desenvolvido durante o curso [Dominando os Testes de Software, do Desenvolvedor.io](https://desenvolvedor.io/curso-online-dominando-os-testes-de-software). Reúne exemplos de asserções, testes parametrizados e organização de cenários de domínio com xUnit.

## Visão técnica

| Componente | Papel |
| --- | --- |
| [Demo](TesteDeSoftwareDevIo/TestesDeUnidade/Demo) | Classes pequenas para exercitar operações numéricas, strings e regras de funcionários. |
| [Demo.Tests](TesteDeSoftwareDevIo/Demo.Tests) | Asserções de números, strings, coleções e outros comportamentos; exemplos com `Fact`, `Theory` e `InlineData`. |
| [Features](TesteDeSoftwareDevIo/Features) | Entidade Cliente, validação com FluentValidation e contratos de serviços/notificações com MediatR. |
| [Features.Tests](TesteDeSoftwareDevIo/Features.Tests) | Cenários de cliente válido/inválido, traits, fixtures compartilhadas e ordenação de testes. |

Os projetos usam `netcoreapp3.1`. Os projetos de teste referenciam xUnit 2.4.1, Microsoft.NET.Test.Sdk 16.7.1 e coverlet.collector 1.3.0; Features referencia FluentValidation.AspNetCore 10.2.1 e MediatR 9.0.0.

## Como os exemplos funcionam

Cada teste prepara seus dados, chama o comportamento e verifica o resultado, seguindo **Arrange → Act → Assert**. Em Features, `Cliente.EhValido()` executa o validador e disponibiliza os erros em `ValidationResult`. Fixtures centralizam a criação dos clientes usados por mais de uma classe de teste.

## Executar os testes

Pré-requisitos: Git e ambiente SDK/runtime compatível com .NET Core 3.1 e os pacotes antigos. A restauração pode exigir ajustes de compatibilidade; um SDK moderno isoladamente não garante a execução.

```bash
git clone https://github.com/fernandojs8/TestsDevIo.git
cd TestsDevIo/TesteDeSoftwareDevIo
dotnet restore TesteDeSoftwareDevIo.sln
dotnet build TesteDeSoftwareDevIo.sln --no-restore
dotnet test TesteDeSoftwareDevIo.sln --no-build
```

Para coletar cobertura, após o build:

```bash
dotnet test TesteDeSoftwareDevIo.sln --no-build --collect:"XPlat Code Coverage"
```

A coleta gera arquivos em `TestResults`; a presença do coletor não comprova uma porcentagem de cobertura. Para um subconjunto: `dotnet test Features.Tests/Features.Tests.csproj --filter FullyQualifiedName~Cliente`.

## Limitações e próximos passos

- Os exemplos de ordenação usam estado estático compartilhado para fins didáticos. Em uma suíte de produto, prefira testes independentes e reproduzíveis.
- Há pastas declaradas no projeto para mocks, AutoMock e FluentAssertions, mas elas não comprovam implementações nem dependências dessas bibliotecas.
- Não há aplicação web executável ou banco de dados a iniciar para esses exemplos de unidade.
- Próximos passos propostos: atualizar framework/pacotes, tornar o relógio das regras de data injetável, ampliar cenários de fronteira e adicionar CI com resultados e cobertura reais.
- Cloud não é requisito deste laboratório. A evidência mais útil para o portfólio seria um pipeline reproduzível com relatórios de testes e cobertura associados ao commit.

**Validação da documentação:** leitura dos projetos e testes; a suíte não foi executada nesta revisão porque o ambiente não possui `dotnet`. Não se afirma que todos os testes passam.

## Licença

[MIT](LICENSE). Material de estudo; a origem educacional é preservada.
