# Análise de segurança do site www.naomeperturbe.com.br 

Após determinação da ANATEL (Agência Nacional de Telecomunicações), empresas brasileiras do ramo, criaram o site [naomeperturbe.com.br](www.naomeperturbe.com.br) para cadastro de usuários que desejam não receber ligações ou SMS de telemarketing. 

O site é uma plataforma muito simples onde o usuário entra cria seu login e senha utilizando seu CPF (Cadastro de Pessoa Física) e após cadastrado, pode adicionar sua linha e de quais operadoras não deseja receber mais comunicações indesejadas. 

Devido a simplicidade da plataforma e a presença de dados sensíveis de usuários uma análise não muito profunda determinou diversos problemas que podem expor dados de usuários a terceiros. 

1. Enumeração de usuários 

É de boa prática não retornar, durante o formulário de "esqueci minha senha", se o usuário em questão já está cadastrado na plataforma, pois assim, um possível agente malicioso consegue através de um ataque de dicionário, enumerar e-mails validos na plataforma. 

2. Limitação de tentativas de acesso 

A plataforma, apresenta um formulário de acesso muito simples: ambos os campos user e password são codificados em forma de URL e são enviados através de uma requisição `POST` para o servidor `"https://s1.naomeperturbe.com.br/functions/login.php"`. O servidor então valida se os valores fornecidos são válidos e respondem com o status da validação, com o código do usuário, CPF e e-mail. O problema deste processo de login é a não limitação do número de tentativas de login, o que facilita a tentativa de um agente em explorar o formulário de login e conseguir acesso através de metodologias simples, como um ataque de dicionário contra este formulário. 

Devido aos problemas apontados nesta análise, é sugerido ao administrador do portal que reavalie sua estratégia de segurança para proteção dos seus consumidores, pois, se medidas simples de segurança estão sendo negligenciadas, outras precauções mais sérias podem não estar sendo consideradas na implementação desta ferramenta. 

 
