<img src="assets/cover.webp" alt="ODAN" width="100%" />

# ODAN

**Do teclado e mouse para um controle virtual.** Um app para Windows que transforma teclado e mouse num controle de videogame que os jogos de PC reconhecem como real.

`C#` `.NET 8` `WPF` `DirectX (SharpDX)` `Helix Toolkit` `Assimp` `ViGEmBus` `ASP.NET Core` `Firestore`

---

## Sumário

- [Visão geral](#visão-geral)
- [Números](#números)
- [Como funciona](#como-funciona)
- [Recursos](#recursos)
- [Réplica 3D do controle](#réplica-3d-do-controle)
- [Calibração do mouse](#calibração-do-mouse)
- [Performance](#performance)
- [Licenciamento](#licenciamento)
- [Interface](#interface)
- [Stack completa](#stack-completa)
- [Status](#status)

---

## Visão geral

Muitos jogos de PC dão vantagem para quem joga no controle (como o aim assist) ou simplesmente funcionam melhor com ele. O ODAN captura o teclado e o mouse, traduz cada comando e entrega ao jogo como se fosse um controle de Xbox conectado.

Foi feito em **C# (.NET 8)** com WPF e calibra a resposta de cada comando em tempo real.

> Começou como um experimento para entender como os jogos leem dispositivos de entrada.

## Números

| | |
| --- | --- |
| Código do app (C#) | ~15 mil linhas |
| Projetos na solução | App, testes, API de licenças e ferramentas de validação |
| Controle emulado | Xbox 360 (via ViGEmBus) |

## Como funciona

```text
Teclado / mouse
      │
      ▼
Captura em nível de driver (Interception)
      │   o jogo não recebe o input original
      ▼
Mapeamento (tecla → botão, mouse → analógico)
      │
      ▼
Calibração (sensibilidade, curva, zona morta, suavização)
      │
      ▼
Controle virtual (ViGEmBus) ──► jogo
      │
      └──► Réplica 3D na interface reage em tempo real
```

- **Captura**: o input é interceptado no nível do driver, antes de chegar ao jogo. Isso evita que o jogo receba teclado e controle ao mesmo tempo.
- **Mapeamento**: cada tecla ou botão do mouse pode virar qualquer botão, gatilho ou direcional.
- **Emulação**: o ViGEmBus cria um controle de Xbox virtual, reconhecido pelo Windows e pelos jogos como um dispositivo físico.

## Recursos

| Área | Recursos |
| --- | --- |
| **Input** | Captura em nível de driver · Mapeamento livre de teclas · Troca rápida entre modo teclado e modo controle |
| **Física & Input** | Física vetorial por botão · Gatilhos analógicos · Direcional (DPad) · Resposta em tempo real |
| **Gráficos 3D** | DirectX (SharpDX) · Modelos via Assimp (GLB) · Iluminação física · MSAA 2x · SSAO |
| **Perfis** | Vários perfis por jogo · Renomear, duplicar e excluir · Configuração salva por perfil |
| **Performance** | Gerenciamento de GPU · Modo segundo plano · Prioridade de FPS do jogo |

## Réplica 3D do controle

A interface mostra um controle 3D renderizado com **DirectX** através do **Helix Toolkit (SharpDX)**. O modelo é importado de um arquivo GLB via **Assimp**, com iluminação física, **MSAA 2x** e **SSAO** (oclusão de ambiente).

Cada botão, gatilho e direcional tem sua própria física: aperta, afunda e volta como no controle de verdade. Os analógicos inclinam conforme o movimento do mouse, então dá para ver na hora se a calibração está boa.

## Calibração do mouse

O ponto mais difícil do projeto é fazer o mouse parecer um analógico. Para isso, cada perfil ajusta:

- **sensibilidade** por eixo;
- **curva de resposta**, para ter precisão em movimentos curtos e velocidade nos longos;
- **zona morta**, para o analógico não "vazar" quando o mouse para;
- **suavização**, para tirar a tremida sem criar atraso.

Tudo pode ser ajustado com o jogo aberto, e o efeito aparece na hora.

## Performance

O ODAN não pode custar FPS ao jogo. Por isso:

- com o jogo aberto, o ODAN vai para **segundo plano**;
- o uso da **GPU** pela interface é reduzido enquanto o jogo roda;
- o FPS do jogo tem prioridade sobre a réplica 3D.

## Licenciamento

O ODAN tem um sistema de licenças próprio:

- **API em ASP.NET Core** para ativar, renovar e desativar licenças;
- dados em **Google Firestore**;
- licença vinculada ao dispositivo por uma impressão digital de hardware;
- sessões com renovação automática;
- painel administrativo para gerar e gerenciar chaves.

## Interface

- **Dashboard** com o estado do controle e a réplica 3D;
- **Mapeamento** das teclas para cada botão;
- **Configuração** de sensibilidade, curva, zona morta e suavização;
- **Perfis** para cada jogo;
- tela de ativação da licença.

## Stack completa

| Camada | Tecnologias |
| --- | --- |
| App | C#, .NET 8, WPF, MVVM |
| 3D | Helix Toolkit, SharpDX (DirectX 11), Assimp |
| Input | Interception (captura em nível de driver), ViGEmBus |
| Backend | ASP.NET Core, Google Firestore, Docker |
| Qualidade | xUnit, ferramentas próprias de validação dos analógicos |

## Status

Funcional. O código não é aberto; este repositório documenta o projeto.

---

Feito por [Carlos Daniel](https://github.com/spullxxx) · [LinkedIn](https://www.linkedin.com/in/carlos-daniel-18787b362/) · [Instagram](https://www.instagram.com/carlaoodan/)
