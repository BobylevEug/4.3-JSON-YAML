# 4.3.-JSON-YAML

## 1.
``` python
{ "info" : "Sample JSON output from our service\t",
    "elements" :[
        { "name" : "first",
        "type" : "server",
        "ip" : "7175" 
        },
        { "name" : "second",
        "type" : "proxy",
        "ip" : "71.78.22.43"
        }
    ]
}
```
## 2.
```python
#!/usr/bin/env python3

import socket
import sys
import shutil
import os
import json
import yaml

domain_search = 'google.com'
domain_mail = 'mail.google.com'
domain_drive = 'drive.google.com'

def domain_name(x) : # объявление фунцкии
        ip = socket.gethostbyname(x) #определение ip 
        print(x,' - ', ip) #вывод в консоль
        
        with open('current_ip.txt', 'a') as f: # открытие файла на дозапись
            f.write(ip + '\n') #построчная запись в файл 
    
shutil.copy2(os.path.abspath('current_ip.txt'), os.path.abspath('past_ip.txt'))
#копируем файл current_ip в past_ip внутри текущей директории

f = open('current_ip.txt', 'w') #создание файла она же отчистка
f.close() #закрытие файла

domain_name (domain_search)
domain_name (domain_mail)
domain_name (domain_drive)

with open("past_ip.txt") as f1, open("current_ip.txt") as f2:
#построчное сравнение файлов
    for x1, x2 in zip(f1,f2):
        if x1 == x2: #если строка одного файла равна строке второго файла
            print(x1, 'не изменился')
        else:
            print('[ERROR] IP ' + x1 + 'сменился на IP', x2)

domain_search_ip = socket.gethostbyname(domain_search) # присваиваем переменной значение ip сервиса
domain_mail_ip = socket.gethostbyname(domain_mail) # присваиваем переменной значение ip сервиса
domain_drive_ip = socket.gethostbyname(domain_drive) # присваиваем переменной значение ip сервиса

dict_json = {
    domain_search : domain_search_ip, 
    domain_mail : domain_mail_ip, 
    domain_drive : domain_drive_ip
    } # создаем словарь JSON

with open('JSON_IP.json', 'w') as file: #создание и/или открытие файла на запись
    file.write(json.dumps(dict_json)) #заполнение файла JSON словарем JSON

with open('JSON_IP.json', 'r') as file: #открытие файла на чтение
    dict_yaml = yaml.safe_load(file) #запись в словарь YAML словаря JSON
    
with open('YAML_IP.yml', 'w') as file: #создание и/или открытие файла на запись
    file.write(yaml.dump(dict_yaml)) #заполнение файла YAML словарем YAML
```
