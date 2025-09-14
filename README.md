# Transfer-Learning-em-uma-rede-de-Deep-Learning
O projeto consiste em aplicar o método de Transfer Learning em uma rede de Deep Learning na linguagem Python no ambiente COLAB. 


# Transfer Learning em uma Rede de Deep Learning

Aplicação prática de **Transfer Learning** para classificação de imagens com notebook Jupyter (otimizado para **Google Colab**). O objetivo é treinar rapidamente um classificador reaproveitando pesos pré-treinados (ex.: ResNet/EfficientNet/MobileNet), com pipeline simples, reproducível e pronto para datasets pequenos.

---

## 🚀 Como executar

### Opção A — Google Colab (recomendado)
1. Abra o notebook `transfer_learning.ipynb` no Colab.
2. Em **Runtime** → **Change runtime type**, selecione **GPU**.
3. Execute as células de preparação do ambiente (instalação de pacotes) e siga o passo a passo.

### Opção B — Local
```bash
# Clonar o repositório
git clone https://github.com/ngrluiz/Transfer-Learning-em-uma-rede-de-Deep-Learning.git
cd Transfer-Learning-em-uma-rede-de-Deep-Learning

# (Opcional) criar ambiente virtual
python -m venv .venv
# Linux/macOS
source .venv/bin/activate
# Windows (PowerShell)
.venv\Scripts\Activate.ps1

# Instalar dependências mínimas
pip install -r requirements_local.txt

# Abrir o Jupyter
jupyter notebook
```
> Se preferir, copie/cole o conteúdo do notebook para um novo `.ipynb` em seu ambiente.

---

## 🗂 Estrutura esperada de dados (exemplo)

```
data/
  train/
    classeA/
    classeB/
  val/
    classeA/
    classeB/
```
- Use `train/` e `val/` com subpastas por classe (padrão *ImageFolder* do PyTorch ou *flow_from_directory* do Keras).
- No Colab, você pode montar o Google Drive e apontar para `data/`.

---

## ⚙️ Pipeline (alto nível)

1. **Carga e augmentations** do conjunto de dados.
2. **Backbone pré-treinado** (ImageNet): congela-se a base e treina-se o *head* (camadas finais).
3. **(Opcional)** *Fine-tuning* parcial: descongelar últimas camadas do backbone com *learning rate* menor.
4. **Avaliação**: acurácia, *loss*, matriz de confusão e F1-score.
5. **Checkpoint**: salvar melhor modelo por métrica de validação.

---

## 🔧 Hiperparâmetros sugeridos

- `img_size`: 224×224  
- `batch_size`: 16–64 (ajuste conforme VRAM)  
- `base_lr` (cabeça): 1e-3  
- `ft_lr` (fine-tuning): 1e-4 ou 1e-5  
- `epochs`: 10–30 (use *early stopping*)

---

## 🧪 Dicas e troubleshooting

- **GPU no Colab**: ative em *Runtime* → *Change runtime type* → *GPU*.
- **OOM (falta de VRAM)**: reduza `batch_size` ou `img_size`.
- **Overfitting**: aumente augmentations, adote *dropout*, use *early stopping*.
- **Conflito de versões**: no Colab, prefira instalar nas células do notebook; localmente, fixe versões em `requirements_local.txt`.

---

## 📦 Dependências

Há dois perfis de requisitos:
- `requirements_colab.txt`: minimalista, pensado para o ambiente do Colab.
- `requirements_local.txt`: inclui *pins* e comentários para execução local.

> O notebook pode instalar bibliotecas adicionais conforme o backbone escolhido. Ajuste conforme necessário.

---

## 📝 Licença

Se ainda não houver licença no repositório, recomenda-se **MIT** ou **Apache-2.0**.

---

## 🤝 Contribuições

Pull requests são bem-vindas! Abra uma *Issue* para bugs, melhorias e novas ideias (ex.: suportar novos backbones, métricas extras, *wandb* para tracking, etc.).
