<!--
Modelos para copiar dentro de openspec/specs/<capacidade>/spec.md.
Um arquivo spec.md por capacidade (ex.: salas, reservas). RNFs em openspec/specs/rnf/<categoria>/spec.md.

Estrutura obrigatória do arquivo:

# <capacidade> Specification

## Purpose
<Uma ou duas frases (50+ caracteres) sobre o que esta capacidade cobre.>

## Requirements
<requisitos abaixo>
-->

### Requirement: RFnn — <Título curto>
O sistema DEVE <comportamento observável, uma ideia por requisito>.

**Prioridade:** Essencial | Importante | Desejável
**Casos de uso:** UCnn

#### Scenario: <caminho feliz>
- **GIVEN** <estado inicial>
- **WHEN** <ação do ator>
- **THEN** <resultado observável>

#### Scenario: <exceção ou caso de borda>
- **GIVEN** ...
- **WHEN** ...
- **THEN** ...

<!-- ===== Requisito não funcional ===== -->

### Requirement: NF-CAT-nn — <Título curto>
O sistema DEVE <qualidade> <critério mensurável: número + unidade + condição>.

**Prioridade:** Essencial | Importante | Desejável
**Casos de uso:** UCnn  <!-- omita se for do sistema como um todo -->

#### Scenario: <como medir>
- **GIVEN** <condição de teste, ex.: 200 usuários simultâneos>
- **WHEN** <procedimento de medição>
- **THEN** <limite numérico atingido>

<!--
Categorias sugeridas (CAT): USA usabilidade · DES desempenho · SEG segurança · CON confiabilidade ·
MAN manutenibilidade · POR portabilidade · LEG legal/normas · HSW hardware e software.
Pesquise outras na literatura (ISO/IEC 25010) e remova as que não usar.
-->
