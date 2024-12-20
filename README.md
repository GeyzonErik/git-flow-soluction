# Git Flow: Visão Geral

## Introdução
Este documento apresenta nossa estratégia de branches e releases, desenhada para maximizar eficiência e qualidade do código.

## Por que este Flow?
- Desenvolvimento paralelo seguro
- Múltiplas camadas de validação
- Histórico limpo e rastreável
- Minimização de conflitos
- Gestão clara de releases

## Estrutura Principal
1. **Ambientes Estáveis**
   - `main`: Espelho da produção
   - `develop`: Código pronto aguardando release
   - `staging`: Ambiente de testes e integração

2. **Branches de Trabalho**
   - `feature/*`: Desenvolvimento de novas funcionalidades
   - `release/*`: Preparação para produção
   - `hotfix/*`: Correções emergenciais

## Ciclo de Vida Básico
1. Desenvolvimento em branches isoladas
2. Validação técnica em staging
3. Integração em develop
4. Preparação de release
5. Deploy em produção

## Benefícios
- Maior segurança nas entregas
- Facilidade de rollback
- Processos claros de review
- Rastreabilidade completa

<br>
<br>
<br>
<br>


# Git Flow: Diagramas Anotados

## 1. Visão Geral das Branches
![image](https://github.com/user-attachments/assets/be2f1c2e-f2bf-46bc-b928-e8bb6c9562f4)

**Anotações Importantes:**
- `main`: Produção - apenas código 100% testado e aprovado
- `develop`: Repositório de features prontas e integradas
- `staging`: Ambiente seguro para testes antes da develop
- `feature/*`: Trabalho isolado dos desenvolvedores
- `release/*`: Preparação e validação final para produção

## 2. Fluxo do Desenvolvedor

![image](https://github.com/user-attachments/assets/e07bd805-b70b-4b39-a5d9-3c44a74dc15b)


**Notas para Desenvolvedores:**
- Atualize sua feature branch diariamente com a develop
- Use `git pull origin develop` para evitar divergências
- Resolva conflitos sempre em sua branch feature
- Faça commits frequentes e bem descritos
- Use cherry-pick apenas quando estritamente necessário

## 3. Fluxo de Release
![image](https://github.com/user-attachments/assets/7cd1f55b-19fc-4d03-b0e2-e41cdaf84c13)


**Notas de Release:**
- `staging`: Primeira camada de testes integrados
- `develop`: Acumula features prontas para próxima release
- `release/*`: Branch para validação final do PO
- Feature flags: Configurar durante criação da release
- Deploy: Apenas após aprovação completa
- Versionamento: Seguir padrão semantic versioning (v1.2.3)

<br>
<br>
<br>
<br>

# Git Flow: Guia de Boas Práticas

## 1. Nomenclatura de Branches
### Padrões
- Features: `feature/taskID-[nome]`, `feature/MKT35-cart-validation`
- Releases: `release/v1.2.3`, `release/v1.2.3-rc1`
- Hotfixes: `hotfix/payment-error`, `hotfix/login-security`

### Exemplos Práticos
```
✓ feature/MKT10-user-authentication
✓ feature/MKT5-cart-checkout
✓ release/v2.1.0
✗ feature/jose-task     // Evitar nomes pessoais
✗ release/sprint-22     // Usar versionamento semântico
```

## 2. Commits
### Estrutura
```
<tipo>: <descrição concisa>

[corpo opcional]

[rodapé opcional]
```

### Tipos de Commit
- `feat`: Nova funcionalidade
- `fix`: Correção de bug
- `docs`: Documentação
- `style`: Formatação
- `refactor`: Refatoração
- `test`: Testes
- `chore`: Tarefas de manutenção

### Exemplos
```
✓ feat: adiciona validação de CPF no cadastro
✓ fix: corrige cálculo de frete
✗ updated files      // Muito vago
✗ WIP               // Evitar commits temporários
```

## 3. Proteções de Branch
### Main
- Requer aprovação do PO
- Requer aprovação técnica do Lead
- Testes automáticos passando
- Não permite force push

### Develop
- Requer review de código
- Testes automáticos passando
- Permite merge apenas via PR

### Staging
- Requer testes automáticos
- Permite merge apenas via PR

## 4. Feature Flags (Opcional)
### Quando Usar
- Features que precisam de lançamento controlado
- Testes A/B
- Releases graduais

### Implementação
```typescript
if (featureFlags.isEnabled('novo-checkout')) {
    // novo código
} else {
    // código atual
}
```

### Gestão
- Configurar durante criação da release
- Documentar no PR
- Remover flags obsoletas após release completa
