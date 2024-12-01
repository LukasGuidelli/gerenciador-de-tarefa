import tkinter as tk
from tkinter import messagebox
from datetime import datetime

# Lista para armazenar tarefas
tarefas = []

# Função para adicionar uma nova tarefa com agendamento
def adicionar_tarefa():
    tarefa = entrada_tarefa.get()
    dia = entrada_dia.get()
    mes = entrada_mes.get()
    ano = entrada_ano.get()
    horas = entrada_horas.get()
    minutos = entrada_minutos.get()
    
    if tarefa.strip() == "" or dia.strip() == "" or mes.strip() == "" or ano.strip() == "" or horas.strip() == "" or minutos.strip() == "":
        messagebox.showwarning("Aviso", "Preencha todos os campos!")
        return
    
    try:
        # Validar data e hora
        agendamento = datetime.strptime(f"{dia}/{mes}/{ano} {horas}:{minutos}", "%d/%m/%Y %H:%M")
        tarefas.append({"nome": tarefa, "data_hora": agendamento, "concluida": False})
        entrada_tarefa.delete(0, tk.END)
        entrada_dia.delete(0, tk.END)
        entrada_mes.delete(0, tk.END)
        entrada_ano.delete(0, tk.END)
        entrada_horas.delete(0, tk.END)
        entrada_minutos.delete(0, tk.END)
        atualizar_lista()
    except ValueError:
        messagebox.showerror("Erro", "Data ou horário inválido! Use o formato DD/MM/AAAA e HH:MM.")

# Função para atualizar a lista de tarefas no Listbox
def atualizar_lista():
    # Ordenar as tarefas pela data e horário de forma crescente (mais próximas primeiro)
    tarefas.sort(key=lambda t: t["data_hora"])
    
    lista_tarefas.delete(0, tk.END)
    for i, tarefa in enumerate(tarefas):
        status = "✔" if tarefa["concluida"] else "✗"
        data_hora = tarefa["data_hora"].strftime("%d/%m/%Y %H:%M")
        lista_tarefas.insert(tk.END, f"{i + 1}. {tarefa['nome']} [{status}] - {data_hora}")

# Função para marcar uma tarefa como concluída
def concluir_tarefa():
    try:
        indice = lista_tarefas.curselection()[0]
        tarefas[indice]["concluida"] = True
        atualizar_lista()
    except IndexError:
        messagebox.showwarning("Aviso", "Selecione uma tarefa para marcar como concluída!")

# Função para remover uma tarefa
def remover_tarefa():
    try:
        indice = lista_tarefas.curselection()[0]
        tarefas.pop(indice)
        atualizar_lista()
    except IndexError:
        messagebox.showwarning("Aviso", "Selecione uma tarefa para remover!")

# Configuração da janela principal
janela = tk.Tk()
janela.title("Gerenciador de Tarefas com Agendamento")

# Entrada de nova tarefa
frame_entrada = tk.Frame(janela)
frame_entrada.pack(pady=10)
tk.Label(frame_entrada, text="Tarefa:").pack(side=tk.LEFT)
entrada_tarefa = tk.Entry(frame_entrada, width=30)
entrada_tarefa.pack(side=tk.LEFT, padx=5)

# Entrada de data (separada por dia, mês e ano)
frame_data = tk.Frame(janela)
frame_data.pack(pady=10)
tk.Label(frame_data, text="Dia:").pack(side=tk.LEFT)
entrada_dia = tk.Entry(frame_data, width=5)
entrada_dia.pack(side=tk.LEFT, padx=5)
tk.Label(frame_data, text="Mês:").pack(side=tk.LEFT)
entrada_mes = tk.Entry(frame_data, width=5)
entrada_mes.pack(side=tk.LEFT, padx=5)
tk.Label(frame_data, text="Ano:").pack(side=tk.LEFT)
entrada_ano = tk.Entry(frame_data, width=7)
entrada_ano.pack(side=tk.LEFT, padx=5)

# Entrada de hora (separada por horas e minutos)
frame_hora = tk.Frame(janela)
frame_hora.pack(pady=10)
tk.Label(frame_hora, text="Horas:").pack(side=tk.LEFT)
entrada_horas = tk.Entry(frame_hora, width=5)
entrada_horas.pack(side=tk.LEFT, padx=5)
tk.Label(frame_hora, text="Minutos:").pack(side=tk.LEFT)
entrada_minutos = tk.Entry(frame_hora, width=5)
entrada_minutos.pack(side=tk.LEFT, padx=5)

# Botão para adicionar tarefa
btn_adicionar = tk.Button(janela, text="Adicionar", command=adicionar_tarefa)
btn_adicionar.pack(pady=5)

# Lista de tarefas
frame_lista = tk.Frame(janela)
frame_lista.pack(pady=10)
lista_tarefas = tk.Listbox(frame_lista, width=70, height=15)
lista_tarefas.pack(side=tk.LEFT)
scroll_lista = tk.Scrollbar(frame_lista, orient=tk.VERTICAL)
scroll_lista.pack(side=tk.RIGHT, fill=tk.Y)
lista_tarefas.config(yscrollcommand=scroll_lista.set)
scroll_lista.config(command=lista_tarefas.yview)

# Botões de ação
frame_botoes = tk.Frame(janela)
frame_botoes.pack(pady=10)
btn_concluir = tk.Button(frame_botoes, text="Concluir Tarefa", command=concluir_tarefa)
btn_concluir.pack(side=tk.LEFT, padx=5)
btn_remover = tk.Button(frame_botoes, text="Remover Tarefa", command=remover_tarefa)
btn_remover.pack(side=tk.LEFT, padx=5)

# Loop da janela
janela.mainloop()