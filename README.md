# OP

from __future__ import unicode_literals
import random
import datetime
import re
def main():
    global u_win, c_win, i
    u_win, c_win = 0, 0
    input_wins()
    while int(c_win) != int(wins) and int(u_win) != int(wins):
        game()
        game_inf()	
    print("-------------------------------------\n"
          "Результат игры: ", winner_final(u_win, c_win),
          "\n-------------------------------------\n")
    i = 2
    output()
    error()
def input_wins():	
    global wins
    wins = input("Введите количество побед, до которого будет вестись игра: ")
    check1(wins)
def sign_tostring(a):
    if a == 0:
        return "камень"
    elif a == 1:
        return "ножницы"
    elif a == 2:
        return "бумага"
def winner_tostring(a):
    if a == -1:
        return "Победил " + comp
    elif a == 0:
            return "Ничья"
    elif a == 1:
            return "ПОБЕДИЛ " + name
def winner_final(a, b):
    if a > b:
        return "Победил " + name + "."
    elif a < b:
        return "Победил " + comp + "."
    else:
        return "Ничья."
def winner_name(a):
    if a == -1:
        return comp
    elif a == 0:
        return "ничья."
    elif a == 1:
        return name
      def winner(a, b):
    if a == 0 and b == 1 or a == 1 and b == 2 or a == 2 and b == 0:
        return 1
    elif a != b:
        return -1
    else:
        return 0
def count_win():
    global u_win, c_win
    if winner(u_sign, c_sign) == 1:
        u_win += 1
    elif winner(u_sign, c_sign) == -1:
        c_win += 1
def check1(a):
    global i
    i = 0
    if a.isdigit() and int(a) > 0:
        a = int(a)
        return a
    else:
        error()
    def check2(a):
    global i
    i = 1
    if a.isdigit():
        if int(a) == 0:
            return True
        elif int(a) == 1:
            return True
        elif int(a) == 2:
            return True
        else:
            error()
    else:
        error()
def error():
    global i, j, u_win, c_win, wins
    if i == 0:
        j = input("\nПроизошла ошибка.\nВернуться к вводу количества побед - 1     Выход из игры - 0\n")
        if j.isdigit():
            if int(j) == 0:
                exit()
            elif int(j) == 1:
                main()
            else:
                error()
        else:
                error()
    elif i == 1:
        j = input("\nПроизошла ошибка.\n"
                  "Вернуться к вводу количества побед - 1     "
                  "Вернуться к вводу игрового знака - 2     "
                  "Выход из игры - 0\n")
        if j.isdigit():
            if int(j) == 0:
                exit()
            elif int(j) == 1:
                main()
            elif int(j) == 2:
                game()
            else:
                error()
        else:
                error()
    elif i == 2:
        u_win, c_win = 0, 0
        j = input("Информация об игре была выведена в файл\n"
                  "Для продолжения нажмите любую клавишу\n"
                  "Выход из игры - 0\n")
        if j.isdigit():
            if int(j) == 0:
                exit()
            else:
                main()
        else:
            main()
def game():
    global u_sign, c_sign
    u_sign = input("Выберите игровой знак:\n0 - Камень    1 - Ножницы   2 - Бумага\n")
    check2(u_sign)
    u_sign = int(u_sign)
    c_sign = int(random.randint(0, 2))
    count_win()
def game_inf():
    global u_sign, c_sign, u_win, c_win
    print("-------------------------------------")
    print("Игровой знак игрока:", sign_tostring(u_sign))
    print("Игровой знак компьютера:", sign_tostring(c_sign))
    print("-------------------------------------")
    print("{qe:^37}".format(qe=winner_tostring(winner(u_sign, c_sign))))
    print("-------------------------------------",
          sep='')
    print("{qw:^37}".format(qw="Текущий счет:"))
    print("{qr:-^37}".format(qr=str(u_win) + "-" + str(c_win)))
def output():
    global f, comp, u_win, c_win
    f = open('game_inf.txt', 'a')
    f.write("Дата проведения игры: |" + datetime.datetime.now().strftime("%Y-%m-%d %H:%M:%S") +
            "|    Результат игры: |" + winner_final(u_win, c_win) +
            "|    Игровой счет: |" + name + " " + str(u_win) + "-" + str(c_win) + " " + comp +
            "|\n")
    f.close()
def name_input():
    global name
    name = input("Введите имя игрока: ").capitalize()
    name_check()
def name_check():
    global jj
    if name.isspace() or name == "":
        jj = input("\nПроизошла ошибка, для продолжения нажмите любую клавишу\n"
                   "Выход из игры - 0\n")
        if jj.isdigit():
            if int(jj) == 0:
                exit()
            else:
                name_input()
        else:
               name_input()
i = 0
comp, u_win, c_win, success = "Компьютер", 0, 0, 1
name_input()
main()

