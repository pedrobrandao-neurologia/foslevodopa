# Foslevodopa · Infusão + LEDD

Ferramenta de apoio à decisão para **doença de Parkinson avançada**: calculadora de conversão da terapia oral para **infusão subcutânea contínua de foslevodopa/foscarbidopa** e calculadora de **dose equivalente diária de levodopa (LEDD)** conforme as recomendações atualizadas da MDS.

Aplicativo de página única (`index.html`), sem dependências, sem servidor e sem envio de dados — tudo roda e fica salvo no navegador.

## Funcionalidades

O app é organizado em três abas:

### 💉 Infusão
Conversão da terapia oral com levodopa (± inibidor da COMT) para os parâmetros de programação da bomba:

- **Taxa basal contínua** (mL/h), com equivalências em mg de foslevodopa/h e levodopa/h
- **Taxas alta e baixa** (percentuais configuráveis acima/abaixo da basal)
- **Dose de ataque** calculada a partir da primeira dose matinal de levodopa IR (0,1–3,0 mL)
- **Dose extra (bolus)** programável (0,10–0,30 mL)
- Regime contínuo 24 h/dia ou somente vigília
- Detalhamento passo a passo do cálculo: TLD → foslevodopa (×1,3) → volume (÷240 mg/mL) → taxa (÷ horas de vigília)
- Alertas automáticos ao exceder os máximos das bulas FDA (3.525 mg/dia) e EMA (6.000 mg/dia)

### Σ LEDD total
Cálculo da dose equivalente diária de levodopa com os fatores de conversão de **Jost et al., *Mov Disord* 2023** (posição oficial da MDS), incluindo:

- Levodopa em todas as formulações: IR, dual-release (×0,85), CR (×0,75), ER/Rytary (×0,5), inalada (×0,69), LCIG (×1,11), LECIG (matinal ×1,11 / manutenção ×1,46), foslevodopa SC (×0,75)
- **Inibidores da COMT** (entacapona ×0,33; tolcapona e opicapona ×0,5) e **istradefilina** (×0,2) calculados automaticamente sobre a LED de levodopa, conforme o protocolo do artigo
- Inibidores da MAO-B: selegilina oral (×10) e sublingual (×80), rasagilina (×100), safinamida (LED fixa 150 mg), zonisamida (LED fixa 100 mg — validada apenas em coortes japonesas)
- Agonistas dopaminérgicos ergolínicos e não ergolínicos (pramipexol sal/base, ropinirol, rotigotina, piribedil, apomorfina SC/SL, lisurida, bromocriptina, pergolida, cabergolina, DHEC)
- Amantadina IR (×1), ER/Gocovri (×1,25) e IR-ER/Osmolex (×1)
- Triexifenidil por tomadas eficazes (100 mg LED por tomada com melhora ≥ 5 pontos no UPDRS-III)
- Total em mg/dia com detalhamento por classe farmacológica

### 👤 Paciente
- Nome, registro/prontuário e médico prescritor
- **Data de nascimento → idade** e **data do diagnóstico → tempo de doença**, calculados automaticamente

## Uso

Abra o `index.html` em qualquer navegador moderno — ou acesse a versão publicada, se o GitHub Pages estiver habilitado para este repositório.

- Os cálculos são atualizados instantaneamente a cada campo preenchido.
- **Salvamento automático**: todos os dados (paciente, medicações, aba ativa) ficam no `localStorage` do navegador e são restaurados ao reabrir a página. Nenhum dado sai do dispositivo.
- **Exportar relatório em PDF** gera um documento para impressão com identificação do paciente (idade e tempo de doença), a terapia de origem, os parâmetros da bomba, a tabela de LEDD e as orientações de uso — via diálogo de impressão do navegador.
- **Limpar tudo** apaga os dados salvos (com confirmação).

## Fórmulas principais

```
Taxa basal (mL/h) = [(TLD × 1,3) ÷ 240 mg/mL] ÷ horas de vigília
LEDD total (mg/dia) = Σ LED de cada fármaco (fatores de Jost et al. 2023)
```

TLD = dose total de levodopa na vigília, em equivalentes de levodopa IR, excluindo doses de resgate e noturnas, ajustada para inibidor da COMT quando aplicável.

## Referências

1. VYALEV™ (foscarbidopa/foslevodopa) — Full Prescribing Information, FDA, rev. 03/2026.
2. PRODUODOPA® — EMA SmPC.
3. Aldred J, et al. Continuous subcutaneous foslevodopa/foscarbidopa infusion: considerations for initiation and maintenance. *Clin Park Relat Disord*. 2024;10:100239.
4. Jost ST, Kaldenbach MA, Antonini A, et al. Levodopa dose equivalency in Parkinson's disease: updated systematic review and proposals. *Mov Disord*. 2023;38(7):1236-1252. doi:10.1002/mds.29410

## Aviso

**Ferramenta de apoio à decisão para uso por médico especialista.** Os resultados não substituem o julgamento clínico nem a consulta à bula aprovada localmente (ANVISA). A prescrição final é de responsabilidade do médico assistente.
