# Unity Hub
1. Link da documentação da Unity Hub (pode te ajudar a compreender a plataforma)
    - https://docs.unity3d.com/Manual/unity-editor.html
      
# Organização da Documentação de um Projeto Unity
1. Estrutura padrão de pastas de um projeto Unity
    Quando você cria um projeto no Unity Hub, ele cria automaticamente algumas pastas:

    - Assets/ – onde ficam todos os arquivos do seu jogo (scripts, imagens, modelos, cenas, animações, prefabs).
    - Packages/ – onde ficam os pacotes que o projeto usa (como o sistema de input, render pipelines etc.).
    - ProjectSettings/ – configurações do projeto (resolução, qualidade, física, etc.).
    - Library/ – cache e dados temporários (gerado automaticamente).
    - Logs/ – registros de log de execução do projeto.

2. Organização recomendada da pasta Assets/
    Você mesmo pode criar essas subpastas dentro de Assets/:
    ```bash
        Assets/
        ├── _Scenes/          → Suas cenas (por ex: MainMenu, Fase1)
        ├── _Scripts/         → Seus scripts C#
        ├── _Prefabs/         → Objetos prontos para reutilizar
        ├── _Animations/      → Animações (e controladores)
        ├── _Art/             → Sprites, texturas, modelos 3D
        │   ├── Sprites/
        │   └── Models/
        ├── _Audio/           → Músicas e sons
        ├── _UI/              → Elementos de interface gráfica
    ```
# Como Criar um Objeto
1. Criando objetos na cena
    - Clique com o botão direito na aba Hierarchy.
    - Selecione o tipo de objeto que deseja criar:
    - 3D Object > Cube, Sphere, etc.
    - 2D Object > Sprite, se estiver em um projeto 2D.
    - UI > Button, Text, etc., se quiser adicionar interface.

2. Modificando um objeto

    - Use a aba Inspector para ajustar:
    - Position, Rotation, Scale (Transform)
    - Componentes (como Rigidbody, Colliders, Scripts, etc.)

# Prefabs – Salvando Objetos Reutilizáveis

1. Se você criou um objeto com várias configurações e quer usá-lo várias vezes:

    - Arraste o objeto da Hierarchy para a pasta _Prefabs/.
    - Agora ele vira um Prefab – você pode arrastar para a cena quantas vezes quiser.
    - Qualquer alteração no prefab afeta todas as instâncias (se você quiser).

# Animações – Criar e Organizar
1. Criando uma animação

    - Selecione um objeto na cena.
    - Vá em Window > Animation > Animation.
    - Clique em Create para criar um Animation Clip (salve na pasta _Animations/).
    - Com a janela de animação aberta, clique em Add Property (ex: transform.position, scale, etc.).
    - Use a timeline para definir os frames-chave (keyframes).

    - O que é gerado:
        - Um arquivo .anim (a animação em si).
        - Um Animator Controller (controlador que define como e quando as animações rodam).

2. Controlando as animações

    - O Animator Controller é ligado ao objeto via o componente Animator.
    - Você pode usar triggers, booleans, floats e integers no Animator para controlar transições.
    - Também pode controlar por script (ex: animator.SetTrigger("Jump")).

# Detalhes sobre Frame Rate e Timeline
- Unity roda a animação com base em tempo, não em frames.
- A timeline da janela de animação mostra tempo (ex: 0:00, 0:30, 1:00 → segundos).
- Mas você pode ativar o modo de frame clicando nos 3 pontinhos no canto da janela de animação.
- FPS padrão

- O Target Frame Rate depende da plataforma, mas você pode limitar:
    ```bash
        Application.targetFrameRate = 60;
    ```

    Isso garante que animações e movimento fiquem mais suaves.

# Exemplo de Documentação de Projeto (Resumo)
Projeto: Jogo de Plataforma 2D
Descrição: Um jogo onde o personagem pula entre plataformas e coleta moedas.

Estrutura:
- _Scenes/
  - MainMenu.unity
  - Fase1.unity

- _Scripts/
  - PlayerController.cs
  - GameManager.cs

- _Animations/
  - PlayerRun.anim
  - PlayerJump.anim
  - Player.controller (Animator)

- _Prefabs/
  - Player.prefab
  - Plataforma.prefab
  - Moeda.prefab

- _Art/Sprites/
  - player_idle.png
  - moeda.png

* Anotações:
    - O personagem é controlado com as setas e espaço para pular.
    - Quando colide com a moeda, a pontuação aumenta.
    - A animação muda para "Jump" quando estiver no ar.
