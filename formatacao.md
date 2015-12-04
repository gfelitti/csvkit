Baixe os bancos de dados do TSE. Eles estão separados por estado.

Primeiro vamos mudar o nome dos arquivos. Prefira nomes curtos para facilitar na hora de digitar no terminal. Nesse caso, usaremos a sigla dos estados. Na linha de comando, escreva:

MV nome_antigo.XXX nome_novo.XXX

Depois, é preciso formatá-los corretamente. Todos os dados do TSE são divulgados na formatação ISO-8859-1, incapaz de lidar com carateres especiais, como acentos e cedilhas. É preciso formatá-lo para UTF-8, o padrão universal.

Na linha de comando, confirme a formatação do banco de dados com o comando
$ file -I arquivo.xxx


A resposta virá no modelo 
arquivo.xxx text/plain; charset=FORMATAÇÃO

Faça a conversão usando o comando iconv:

iconv -f ISO-8859-1 (a formatação original) -t UTF-8 (a formatação pretendida) arquivo_original.xxx > novo_arquivo.csv

Ainda que já no padrão UTF-8, o novo CSV ainda tem dificuldades com caracteres especiais. Para resolver isso, usaremos o Google Refine. Abra o programa, selecione Create Project e importe o CSV. O Refine mostrará algumas das primeiras linhas da tabela. Se parecer uma tabela, ótimo. Se não, selecione ou separados para as colunas (vírgula, tab ou custom). Na barra de baixo, escolha a formatação UTF-8. Crie o projeto no canto superior direito. Renomeie toda as colunas para que não tenham espaços entre as nomes (só precisa mudar o nome da coluna, não o conteúdo). Isso facilitará muito ao usar o csvkit para se referir a determinada coluna.

Com o projeto pronto, clique em Export, Comma-separated values. Esse banco de dados está pronto para ser trabalhado. 

Se o banco de dados é grande demais para abrir no Refine e suas colunas estão separadas por ponto e vírgulo, e não vírgulas, use o comando sed:

$ sed 's/;/,/g' nome_antigo > nome_novo
