<img src="assets/cover.webp" alt="ODAN" width="100%" />

# ODAN

**Do teclado e mouse para um controle virtual.**

O ODAN transforma teclado e mouse num controle virtual para jogos de PC. Foi feito em **C# (.NET)** com WPF e calibra a resposta de cada comando em tempo real.

A interface mostra uma réplica 3D do controle, renderizada com DirectX (SharpDX) e modelos importados via Assimp, que reage na hora a cada botão.

Cada botão, gatilho e direcional tem sua própria física. Com o jogo aberto, o ODAN vai para segundo plano e reduz o uso da GPU para não derrubar o FPS.

> Começou como um experimento para entender como os jogos leem dispositivos de entrada.

## Principais recursos

| Área | Recursos |
| --- | --- |
| **Stack** | C# (.NET) · WPF · ViGEmBus |
| **Gráficos 3D** | DirectX (SharpDX) · Importação via Assimp · Iluminação física · MSAA 2x · SSAO |
| **Física & Input** | Física vetorial por botão · Gatilhos analógicos · Direcional (DPad) · Resposta em tempo real |
| **Performance** | Gerenciamento de GPU · Modo segundo plano · Prioridade de FPS do jogo |

## Status

Funcional. O código não é aberto; este repositório documenta o projeto.

---

Feito por [Carlos Daniel](https://github.com/spullxxx) · [LinkedIn](https://www.linkedin.com/in/carlos-daniel-18787b362/) · [Instagram](https://www.instagram.com/carlaoodan/)
