# Blender + Rodin 3D Pipeline

Este repositório/pasta contém o fluxo de trabalho (pipeline) utilizado para converter imagens 2D em assets 3D por meio do **Rodin AI** e realizar o processo de retopologia, edição e remodelagem no **Blender**.

---

## 📌 Visão Geral do Fluxo

```text
[Imagem 2D] ──> (Rodin AI) ──> [Malha Bruta .OBJ/.GLB] ──> (Blender) ──> [Asset Final Refinado]

```

1. **Geração Inicial:** A partir de uma imagem de referência, o **Rodin AI** gera uma malha 3D base com texturas iniciais.
2. **Exportação:** O modelo gerado é exportado no formato de preferência (`.glb` ou `.obj`).
3. **Pós-processamento (Blender):**
* Limpeza de geometria (remoção de vértices soltos e faces duplas).
* Retopologia (conversão da malha densa/desorganizada para *quads*).
* Ajustes de proporção, escultura e refatoração de UVs.
* Aplicação de materiais e preparação para renderização/engine.



---

## 📁 Estrutura de Pastas Sugerida

```text
blender-rodin/
├── obj/          # Imagens 2D de referência (PNG, JPG) e Modelos 3D brutos exportados do Rodin (.obj, .glb, .gltf)
├── models/    # Arquivos de trabalho do Blender (.blend)
└── outputs/         # Modelos finais limpos e otimizados (.fbx, .glb, etc.)

```

---

## 🛠️ Passo a Passo do Processo

### 1. Geração no Rodin AI

* Faça upload de uma imagem 2D limpa, de preferência com fundo neutro e boa iluminação.
* Ajuste as configurações de geração (prompt extra, se necessário).
* Exporte o modelo gerado na pasta `02_rodin_raw/`.

### 2. Importação no Blender

* Abra o Blender e vá em `File > Import` para carregar o arquivo exportado da pasta `02_rodin_raw/`.
* Verifique a escala e a orientação do objeto no espaço 3D.

### 3. Remodelagem e Limpeza

* **Merge por Distância:** Em *Edit Mode* (`Tab`), selecione tudo (`A`) e pressione `M > By Distance` para remover vértices duplicados.
* **Retopologia:** Use ferramentas como *Quad Remesher*, a função nativa *Voxel Remesh*, ou faça a retopologia manual sobre a malha de alta densidade do Rodin.
* **UV Unwrapping:** Refaça o mapa de UVs para garantir uma distribuição limpa das texturas se for editar as cores.
* **Ajustes Finais:** Pincéis de escultura (*Sculpt Mode*) para ajustar detalhes anatômicos/superficiais.

---

## 💡 Dicas e Boas Práticas

* **Texturas do Rodin:** Como o Rodin costuma assar as luzes e sombras diretamente na textura, vale a pena recriar os materiais no Blender caso o objetivo seja usar iluminação em tempo real.
* **Preservar o Modelo Original:** Mantenha a malha bruta gerada pelo Rodin em uma coleção oculta no Blender para usar como referência (*snapping*) durante a retopologia.
* **Organização dos Arquivos:** Utilize nomes padronizados para as versões, ex: `objeto_v01.blend`, `objeto_final_lod0.fbx`.
