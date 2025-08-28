# TEMPLATE DE DOCUMENTAÇÃO DE PROJETO UNITY

Esse modelo você pode usar em um arquivo .md (Markdown) ou .txt, e ir preenchendo conforme cria seu projeto.

1. Projeto Unity – Documentação
    - Nome do Projeto:
        (ex: Aventura nas Nuvens)

    - Descrição Geral:
        (Resumo do jogo. Por exemplo: Jogo de plataforma onde o jogador pula entre nuvens e coleta estrelas)

    - Mecânicas Principais:
        Movimento do jogador (andar, pular)
        Coleta de itens
        Sistema de pontuação
        Animações
        Música e efeitos sonoros

2. Estrutura de Pastas
    ```bash
    Assets/
    ├── _Scenes/          → Cenas do jogo
    ├── _Scripts/         → Código do jogo
    ├── _Prefabs/         → Objetos reutilizáveis
    ├── _Animations/      → Animações e controladores
    ├── _Art/             → Sprites e modelos
    ├── _Audio/           → Sons e músicas
    ├── _UI/              → Elementos da interface
    ```

3. Personagens

    - Nome: Jogador
    - Sprite: player_idle.png
    - Animações:
        Idle (PlayerIdle.anim)
        Correndo (PlayerRun.anim)
        Pulando (PlayerJump.anim)
        Prefab: Player.prefab
        Scripts: PlayerController.cs

4. Animações

    | Nome | Descrição | Trigger no Animator | Arquivo `.anim`   |
    | ---- | --------- | ------------------- | ----------------- |
    | Idle | Parado    | `Idle`              | `PlayerIdle.anim` |
    | Run  | Correndo  | `Run`               | `PlayerRun.anim`  |
    | Jump | Pulando   | `Jump`              | `PlayerJump.anim` |

5. Lógica de Jogo

    - Quando o jogador estiver no chão e apertar seta → move e toca "Run"
    - Quando pressionar espaço → "Jump"
    - Quando parado → "Idle"
    - Colisão com moeda → aumenta pontuação e toca som

6. Testes Pendentes

    - Verificar se o personagem não pula duas vezes
    - Checar se a animação de "Jump" termina corretamente
    - Testar colisão com moedas

7. Notas e Aprendizados

    - Usei Animator.SetBool("isRunning", true) para trocar animações com lógica.
    - Prefabs ajudam muito a organizar objetos reutilizáveis.
    - Melhor usar FixedUpdate() para física (ex: pulo).

# GUIA PRÁTICO – Personagem Que Anda e Pula com Animações

1. Criar um novo projeto 2D

    - Abra o Unity Hub
    - Clique em New Project
    - Escolha o template 2D Core
    - Nomeie como: PlataformaTeste
    - Crie!
2. Importar Sprites

    - Crie a pasta Assets/_Art/Sprites/
    - Importe imagens do personagem:
      - player_idle.png
      - player_run_1.png, player_run_2.png ...
      - player_jump.png
3. Criar o Personagem

    - Na aba Hierarchy: Create > 2D Object > Sprite
    - Renomeie para Player
    - Aplique o sprite player_idle.png
    - Adicione os componentes:
    - Rigidbody2D (para gravidade)
    - BoxCollider2D (para colisão)
4. Criar Animações

    - Crie pasta Assets/_Animations/
    - Abra Window > Animation > Animation
    - Selecione o Player, clique Create
    - Crie PlayerIdle.anim
    - Adicione o sprite de idle

    - Faça o mesmo para:
        - PlayerRun.anim (adicione os frames de corrida)
        - PlayerJump.anim (sprite do pulo)

    - Salve os .anim na pasta _Animations/.
5. Animator Controller

    - Unity criará um Player.controller
    - Ele será ligado automaticamente ao componente Animator no Player
    - Vá em Window > Animator para ver o fluxo de animações

    - Crie transições:
        - Idle → Run → Jump
        - Use parâmetros:
        - isRunning (bool)
        - isJumping (bool)
6. Script de Movimento

    - Crie Assets/_Scripts/PlayerController.cs com o seguinte código:

        ```bash
        using UnityEngine;

        public class PlayerController : MonoBehaviour
        {
            public float speed = 5f;
            public float jumpForce = 10f;

            private Rigidbody2D rb;
            private Animator anim;
            private bool isGrounded = true;

            void Start()
            {
                rb = GetComponent<Rigidbody2D>();
                anim = GetComponent<Animator>();
            }

            void Update()
            {
                float move = Input.GetAxis("Horizontal");

                rb.velocity = new Vector2(move * speed, rb.velocity.y);

                if (move != 0)
                    anim.SetBool("isRunning", true);
                else
                    anim.SetBool("isRunning", false);

                if (Input.GetButtonDown("Jump") && isGrounded)
                {
                    rb.velocity = new Vector2(rb.velocity.x, jumpForce);
                    anim.SetBool("isJumping", true);
                    isGrounded = false;
                }
            }

            void OnCollisionEnter2D(Collision2D col)
            {
                if (col.contacts[0].normal.y > 0.5f)
                {
                    isGrounded = true;
                    anim.SetBool("isJumping", false);
                }
            }
        }
        ```
7. Testar

    - Crie um Ground com um Sprite > Box, adicione BoxCollider2D
    - Rode a cena: o personagem deve andar e pular com animações.
