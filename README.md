# App de Login com Foto (Android)

Aplicativo Android de login que exibe uma tela de boas-vindas e permite tirar uma foto com a câmera.  
A foto tirada na tela de boas-vindas é devolvida para a tela principal usando a **Activity Result API** e exibida em uma **imagem circular**, centralizada entre o fundo da tela e os últimos botões. [web:52][web:71]

## Funcionalidades

- Tela de login com usuário e senha fixos (`emerson` / `admin`).
- Navegação para a `WelcomeActivity` após login bem-sucedido.
- Exibição de mensagem de boas-vindas com o nome do usuário via `Snackbar`.
- Captura de foto usando `MediaStore.ACTION_IMAGE_CAPTURE`.
- Retorno da foto para a `MainActivity` usando `ActivityResultLauncher` + `ActivityResultContracts.StartActivityForResult`.
- Exibição da foto em um `ShapeableImageView` circular, centralizado entre o botão **LOGAR** e os botões **ESQUECI A SENHA** / **CADASTRAR**.

## Fluxo das Activities

1. **MainActivity**
   - Valida usuário e senha.
   - Cria um `Intent` para `WelcomeActivity`, enviando o extra `"user_name"`.
   - Usa `ActivityResultLauncher<Intent>` para iniciar a `WelcomeActivity`.
   - No callback, lê:
     - `resultado` (String) para mostrar via `Toast`.
     - `foto_bitmap` (Bitmap) para exibir na imagem circular.

2. **WelcomeActivity**
   - Recebe o extra `"user_name"` e monta a mensagem de boas-vindas.
   - Abre a câmera com `startActivityForResult` e `MediaStore.ACTION_IMAGE_CAPTURE`.
   - No `onActivityResult`, obtém o `Bitmap` em `extras.get("data")`.
   - Mostra a miniatura na própria tela e devolve:
     - `resultado`: `"Bateu a foto."` ou `"Não bateu a foto."`
     - `foto_bitmap`: Bitmap com a miniatura da foto.

## Detalhes de Interface

- Layouts construídos com `ConstraintLayout`.
- Campos de entrada usando `TextInputLayout` e `TextInputEditText` (Material Components).
- Imagem circular implementada com `ShapeableImageView` e o estilo:

  ```xml
  <style name="ShapeAppearanceOverlay.App.CornerSize50Percent" parent="">
      <item name="cornerSize">50%</item>
  </style>
  ```

- A `ShapeableImageView` utiliza `app:shapeAppearanceOverlay="@style/ShapeAppearanceOverlay.App.CornerSize50Percent"` para recortar a foto em formato circular.

## Como executar

1. Clonar o repositório:
   ```bash
   git clone https://github.com/SEU_USUARIO/NOME_DO_REPO.git
   ```
2. Abrir o projeto no Android Studio.
3. Sincronizar o Gradle e rodar o app em um emulador ou dispositivo físico.
