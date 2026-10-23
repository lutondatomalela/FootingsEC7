# FootingsEC7

Aplicação Python para análise e dimensionamento de fundações superficiais e conjuntos **sapata + viga de equilíbrio + sapata**, com base nas normas NP EN 1997-1 (EC7) e NP EN 1992-1-1 (EC2).

## Estado

**Em desenvolvimento e validação.** A versão de trabalho v1.24.0 incorpora análise 3D experimental com OpenSeesPy 3.8.0. Os ensaios locais incluem casos de referência, equilíbrio de seis componentes, contacto com atrito e convergência de malha (173 testes aprovados). **Não constitui, nesta fase, uma ferramenta aprovada para dimensionamento final em projetos sensíveis.**

## Requisitos técnicos

- Python 3.12 ou 3.13
- `requirements.txt` para os módulos de base
- `requirements-opensees-optional.txt` para ensaios MEF 3D
- `pytest` e `scipy` para validação

## Execução (após publicar o código-fonte)

```bash
python -m pip install -r requirements.txt -r requirements-opensees-optional.txt pytest scipy
python -m pytest -q
python tools/validate_opensees_runtime.py --output artefactos/viga3d.json
python tools/validate_coupled_runtime.py --output artefactos/conjunto3d.json
```

## Validação contínua

O workflow [OpenSeesPy real and regression](.github/workflows/validate-opensees.yml) testa Python 3.12 e 3.13 e disponibiliza os relatórios de validação em GitHub Actions. **A publicação do workflow não implica que o programa já esteja publicado**: é necessário colocar as pastas `footingsec7/`, `tests/`, `tools/` e os `requirements*.txt` na raiz do repositório.

## Limites da validação

A convergência e o fecho do equilíbrio numérico não demonstram, isoladamente, a resistência geotécnica GEO, o comportamento ELS a longo prazo, nem as verificações e a pormenorização EC2. São necessários parâmetros geotécnicos fundamentados e verificação pelo engenheiro projetista.

Este repositório destina-se à investigação, desenvolvimento e verificação rastreável da ferramenta.
