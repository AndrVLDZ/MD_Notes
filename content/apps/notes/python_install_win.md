---
title: "Python_install_win"
date: 2022-03-31T16:38:44+03:00
draft: true
images: true
---

# Правильная установка Python на Windows
## **Введение**
Для установки всех необходимых инструментов и Python используется пакетный менеджер Chocolatey, при помощи которого устанавливаются:  
* pyenv - менеджер версий для python
* poetry - инструмент для управления зависимостями внутри проекта   

## **Установка Choco**  
Ставим пакетный менеджер choсo по инструкции с [официального сайта](https://chocolatey.org/install), для установки в PowerShell под администратором необходимо выполнить следующую команду:
``` PowerShell
Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))
```
## **Установка Pyenv**
Ставим pyenv по [официальной инструкции](https://pyenv-win.github.io/pyenv-win/#installation) и проверяем версию после установки

``` PowerShell
choco install pyenv-win
pyenv --version
```

Если возникли проблемы - переводим политики запуска скриптов в PowerShell в байпас для обхода ограничений безопасности

```PowerShell
Set-ExecutionPolicy -ExecutionPolicy Bypass
```

И проверяем все ли переменные среды в PATH на месте 
<p align="center">
  <img src="static/images/pyenv_install.png"
  alt="Проверка переменных среды в PATH">
</p>

После успешной установки необходимо выполнить rehash 

``` PowerShell
pyenv rehash
```
Выводим список доступных версий и ставим необходимую

``` PowerShell
pyenv install -l
pyenv install 3.9.6
```

Командой global выбрать версию питона по умолчанию

``` PowerShell
pyenv global 3.9.6
```

Заходим через поиск в пуске в управление псевдонимами(alias) и выключаем 2 установщика python  

<p align="center">
  <img src="static/images/py_win_install.png"
  alt="alias">
</p>

<!-- ![alias](/imag/py_win_install.png) -->


## **Установка Poetry**
Как и с Pyenv инструкция есть на [официальном сайте](https://python-poetry.org/docs/), необходимо под администратором в PowerShell запустить следующую команду

``` PowerShell
(Invoke-WebRequest -Uri https://raw.githubusercontent.com/python-poetry/poetry/master/get-poetry.py -UseBasicParsing).Content | python -
```

Проверяем версию

``` PowerShell
poetry --version
```

Если не работает - добавляем вручную в PATH

``` PowerShell
%USERPROFILE%\.poetry\bin
```

Порядок использования 

``` PowerShell
poetry init
poetry install
poetry run python .\main.py
```

Добавление библиотеки mypy в основные и в dev-dependencies:

``` PowerShell
poetry add mypy
poetry add mypy -D
```

Удаление зависимости в в dev-dependencies и в основных происходит по тому же принципу

``` PowerShell
poetry remove mypy -D 
poetry remove mypy
```
