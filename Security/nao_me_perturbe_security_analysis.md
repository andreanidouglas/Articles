# Analise de segurança do site www.naomeperturbe.com.br

Após determinação da ANATEL (Agencia Nacional de Telecomunicações), empresas brasileiras do ramo, criaram o site
[www.naomeperturbe.com.br](www.naomeperturbe.com.br) para cadastro de usuarios que desejam não receber ligações
ou SMS de telemarketing.

O site é uma plataforma muito simples onde o usuario entra cria seu login e senha utiliziando seu CPF (Cadastro de Pessoa Fisica) e após cadastrado, pode adicinar sua linha e de quais operadoras não deseja receber mais comunicações indesejadas.

Devido a simplicidade da plataforma e a presença de dados sensiveis de usuarios uma analise não muito profunda determinou diversos problemas que podem export os dados de usuarios a terceiros.

1. Enumeração de usuarios

    É de boa pratica não retornar, durante o formulario de "esqueci minha senha", se o usuario em questão ja esta cadastrado na plataforma, pois assim, um possivel agente malicioso consegue através de um ataque de dicionario, enumerar emails validos na plataforma.

2. Limitação de tentativas de acesso

    A plataforma, apresenta um formulario de acesso muito simples: ambos os campos user e password são codificados em forma de url e são enviados através de uma requisição `POST` para o servidor `"https://s1.naomeperturbe.com.br/functions/login.php"`. O servidor então valida se os valores fornecidos são válidos e respondem com o status da validação, com o codigo do usuario, CPF e email.
    O problema deste processo de login é a não limitação do número de tentativas de login, o que facilita a tentativa de um agente em explorar o formulario de login e conseguir acesso através de metodologias simples, como um ataque de dicionario contra este formulario.

Devido aos problemas apontados nesta analise, é sugerido ao administrador do portal que reavalie sua estratégia de segurança para proteção dos seus consumidores, pois, se medidas simples de segurança estão sendo neglegenciadas, outra precauções mais sérias podem não estar sendo consideradas na implementação desta ferramenta.
