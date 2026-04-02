# HPC Heisenberg — Guia e Recursos Práticos

O presente repositório reúne o material de referência e os recursos práticos para o uso do *cluster* HPC Heisenberg, disponibilizado ao alunos da [**Ilum - Escola de Ciência**](https://ilum.cnpem.br/). O ponto de partida é o guia principal em PDF, complementado por *templates* de submissão de *jobs* e uma atividade prática autocontida.

## Conteúdo do Repositório

```
HPC-Heisenberg/
├── README.md                    ← Este arquivo
├── Guia HPC Heisenberg.pdf      ← Documentação principal do cluster
├── LICENSE
├── .gitignore
│
├── jobs/                        ← Templates de submissão SLURM
│   ├── job_py.sh                ← Template para scripts Python
│   └── job_ipynb.sh             ← Template para Jupyter Notebook
│
└── hpc-pratica/                 ← Atividade prática guiada
    └── [...]                    ← Demais arquivos da prática guiada
    └── README.md                ← Instruções completas da atividade
```


## Guia HPC Heisenberg

O [**Guia HPC Heisenberg**](https://github.com/mateusjmd/HPC-Heisenberg/blob/main/Guia%20HPC%20Heisenberg.pdf) é o documento central deste repositório. Ele cobre desde o acesso inicial ao *cluster* até tópicos avançados de uso:

| Seção                                      | Conteúdo                                                                                                        |
|--------------------------------------------|-----------------------------------------------------------------------------------------------------------------|
| **Introdução ao HPC**                      | Definição, motivação e arquitetura de *clusters*; comparativo CPU vs. GPU; especificações dos nós do Heisenberg |
| **Acesso e Ambiente de Trabalho**          | Acesso via SSH, WinSCP e VS Code Remote-SSH; configuração de VPN                                                |
| **Comandos Bash Essenciais**               | Navegação, manipulação de arquivos, monitoramento de recursos e gerenciamento de módulos                        |
| **Ambientes Virtuais e Dependências**      | Gerenciamento de ambientes com Conda; resolução de conflitos de dependências                                    |
| **Modos de Execução**                      | Comparativo entre Jupyter Notebook e scripts Python como formas de execução no *cluster*                        |
| **Gerenciador de Jobs: SLURM**             | Estrutura de scripts de submissão e principais parâmetros `#SBATCH`                                             |
| **Submissão, Monitoramento e Diagnóstico** | Submissão e cancelamento de jobs; monitoramento de execução em tempo real                                       |
| **Workflow Completo**                      | Passo a passo do fluxo integral de uso do *cluster*, do acesso SSH à coleta de resultados                       |
| **Boas Práticas**                          | Uso responsável, organização de experimentos, logging e reprodutibilidade                                       |
| **Erros Comuns e Debugging**               | Diagnóstico de jobs em PENDING, OOM, problemas com GPU e kernel morto no Jupyter                                |
| **Apêndices (A, B, C e D)**                | Link para a atividade prática; tutorial de VPN; referências rápidas de comandos SLURM e Conda                   |



## Templates de Jobs SLURM

O diretório `jobs/` fornece *templates* prontos para submissão de *jobs* no SLURM. Eles devem ser copiados e adaptados para cada projeto.

### `job_py.sh` — Execução de Script Python

```bash
# Copie e edite conforme seu projeto
cp jobs/job_py.sh meu_projeto/jobs/job_py.sh
```

Parâmetros a ajustar antes de submeter:

```bash
#SBATCH --job-name=nome_job          # Identificador do job
#SBATCH --partition=gpu              # Partição: cpu ou gpu
#SBATCH --gres=gpu:1                 # Requisição de GPU (remova se usar CPU)
#SBATCH --mem=16G                    # Memória RAM
#SBATCH --time=DD-HH:MM:SS           # Tempo máximo de execução
#SBATCH --mail-user=usuarioXXX@ilum.cnpem.br

conda activate meu_env
python script.py --argumentos
```

### `job_ipynb.sh` — Jupyter Notebook Interativo

```bash
sbatch jobs/job_ipynb.sh
```

Após o job iniciar, obtenha o link de acesso:

```bash
tail -f logs/slurm-JOBID.out
```

Pressione CTRL e clique no link com estrutura `http://172.XX.XX.XX:8888/tree...`

## Atividade Prática

O subdiretório [`hpc-pratica/`](./hpc-pratica/) contém uma atividade guiada de demonstração: a **Simulação de Difusão por Random Walk**, com implementações em CPU (NumPy) e GPU (PyTorch) e análise de desempenho comparativo. Consulte o [**README**](./hpc-pratica/README.md) para instruções de uso.

## Pré-requisitos

- Conta de acesso ao *cluster* HPC Heisenberg (solicitada ao suporte do CNPEM)
- Conhecimento básico de terminal Linux
- Familiaridade com Python e Conda

> **📌 Observação:** Se estiver fora da rede do CNPEM, conecte-se primeiro à VPN (FortiClient → CNPEM-SSL) antes de tentar acessar o *cluster*.