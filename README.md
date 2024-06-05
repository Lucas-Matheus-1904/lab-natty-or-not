import os

def carregar_respostas(caminho_pasta):
    respostas = {}
    for arquivo in os.listdir(caminho_pasta):
        if arquivo.endswith("roteiro.txt"):
            caminho_arquivo = os.path.join(caminho_pasta, arquivo)
            with open(caminho_arquivo, 'r', encoding='utf-8') as file:
                conteudo = file.read()
                respostas[arquivo] = conteudo
    return respostas

def encontrar_resposta(pergunta, respostas):
    for arquivo, resposta in respostas.items():
        if pergunta.lower() in resposta.lower():
            return f"Resposta de {arquivo}:\n{resposta}"
    return "Desculpe, não encontrei uma resposta para essa pergunta."

if __name__ == "__main__":
    caminho_pasta_respostas = "."  # Pasta onde os arquivos de respostas estão
    respostas = carregar_respostas(caminho_pasta_respostas)

    while True:
        pergunta = input("Você: ")
        if pergunta.lower() == "sair":
            break
        resposta = encontrar_resposta(pergunta, respostas)
        print(f"Bot: {resposta}")
