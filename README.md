# Documentação de Projeto – Gaia IA de Controle  
**Versão:** 1.4  
**Autores:** João Augusto, Felipe Augusto, Lucas Valente  
**Disciplina:** Projeto de Software  
**Data:** 29/05/2025  

---

## 📑 Tabela de Conteúdo  
1. [Introdução](#1-introdução)  
2. [Modelos de Usuário e Requisitos](#2-modelos-de-usuário-e-requisitos)  
   2.1 [Descrição de Atores](#21-descrição-de-atores)  
   2.2 [Modelo de Casos de Uso e Histórias de Usuários](#22-modelo-de-casos-de-uso-e-histórias-de-usuários)  
   2.3 [Diagrama de Sequência do Sistema](#23-diagrama-de-sequência-do-sistema)  
   2.4 [Contrato de Operações](#24-contrato-de-operações)  
3. [Modelos de Projeto](#3-modelos-de-projeto)  
   3.1 [Arquitetura (Diagrama de Implantação)](#31-arquitetura-diagrama-de-implantação)  
   3.2 [Diagrama de Componentes e Implantação](#32-diagrama-de-componentes-e-implantação)  
   3.3 [Diagrama de Classes (substituído por Diagrama de Sequência)](#33-diagrama-de-classes-substituído-por-diagrama-de-sequência)  
   3.4 [Diagramas de Sequência](#34-diagramas-de-sequência)  
   3.5 [Diagramas de Comunicação](#35-diagramas-de-comunicação)  
   3.6 [Diagramas de Estados](#36-diagramas-de-estados)  
4. [Modelos de Dados (Removido)](#4-modelos-de-dados-removido)  

---

## 1. Introdução  
Este documento agrega modelos de domínio e projeto para o sistema Gaia. É baseado no documento de visão de domínio do sistema.  

---

## 2. Modelos de Usuário e Requisitos  

### 2.1 Descrição de Atores  
- **Jogador:** Ator principal que interage com a IA através de coleta, compra e venda.  
- **IA:** Controla valores de mercado, disponibilidade de itens, e nascimento de criaturas.  
- **NPC:** Entidade influenciada pela IA, interage com jogadores e o mundo.  
- **Mundo:** Espaço virtual onde tudo acontece, controlado indiretamente pela IA.  

### 2.2 Modelo de Casos de Uso e Histórias de Usuários  
- **🧾 História 1 – Coleta de Recursos**  
  *Como jogador, quero coletar recursos para fabricar itens ou completar missões.*  
- **🧾 História 2 – Venda de Itens no Mercado**  
  *Como jogador, quero vender itens para obter lucro.*  
- **🧾 História 3 – Reação da IA ao Mundo**  
  *Como IA, quero monitorar ações para ajustar valores e raridades de itens.*  
- **🧾 História 4 – Controle de Criaturas e Missões**  
  *Como IA, quero gerar criaturas e missões com base nas ações dos jogadores.*  

### 2.3 Diagrama de Sequência do Sistema  
Representa a lógica de missões, coleta, IA e economia dinâmica. Destaca o papel da IA na definição de raridade e valor dos itens.  

### 2.4 Contrato de Operações  

#### 📌 Contrato: Venda de Item para NPC  
- **Operação:** `venderItem(jogador: Jogador, item: Item)`  
- **Referências:** Caso de Uso “Missão com coleta de recurso”; Diagrama de Sequência (2.3)  
- **Pré-condições:**  
  - Jogador possui o item  
  - Interação com NPC ativa  
- **Pós-condições:**  
  - Item removido do inventário  
  - Valor adicionado ao saldo do jogador  
  - NPC registra aquisição  
  - IA atualiza dados de mercado  

#### 📌 Contrato: Coleta de Recurso Acessível para Missão  
- **Operação:** `coletarRecurso(jogador: Jogador, tipoRecurso: string): Recurso`  
- **Referências:** Caso de Uso “Venda com NPC”; Diagrama de Sequência (2.3)  
- **Pré-condições:**  
  - Recurso coletado e disponível  
  - Avaliação positiva da IA  
- **Pós-condições:**  
  - Recurso usado na missão  
  - IA atualiza dados de demanda e raridade  

---

## 3. Modelos de Projeto  

### 3.1 Arquitetura (Diagrama de Implantação)  
- **Jogador:** Cliente que envia ações.  
- **Servidor Gaia:**  
  - IA de Controle  
  - Gerenciador de Recursos  
  - Módulo de Missões e Criaturas  
- **Banco de Dados:** Estado persistente do mundo.  

### 3.2 Diagrama de Componentes e Implantação  
Mostra os módulos internos do Servidor Gaia:  
- Interface do Jogador  
- Controlador da IA  
- Gerenciador de Recursos  
- Módulo de Missões e Criaturas  
- Persistência de Dados  

### 3.3 Diagrama de Classes (substituído por Sequência)  
- **Cenário: Caça de Criatura**  
  - Jogador caça  
  - Mundo envia dados à IA  
  - IA valida  
  - Drops calculados  
- **Cenário: Venda de Item**  
  - Jogador vende  
  - Mundo envia dados à IA  
  - IA calcula oferta/demanda  
  - NPC processa venda  

### 3.4 Diagramas de Sequência  
Interação entre Jogador, NPC e IA para aquisição e venda de itens.  

### 3.5 Diagramas de Comunicação  
Descreve como ações do jogador afetam o mundo, ativando a IA e a persistência no banco de dados.  

### 3.6 Diagramas de Estados  
Fluxo de ações do jogador:  
- Missão → Coleta → Venda ou Desistência  
- IA regula preços  

---

## 4. Modelos de Dados (Removido)  
