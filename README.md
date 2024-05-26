# Втора лабораториска вежба по Софтверско Инженерство

Никола Сарафимов 223091

## (2) Control Flow Graph:

![CFG drawio](https://github.com/nikolasarafimov/SI_2024_lab2_223091/assets/134642898/1b1d0057-5eda-48d6-aa4a-61d6c26860ce)

## (3) Цикломатска комплексност:
Цикломатска комплексност на овој код = Е(број на ребра) - N(број на јазли) + 2 => 36-28+2 = 10

## (4) Тест случаи според критериумот Every Branch
Тест случај 1: allItems е null

     - Влез: checkCart(null, 100)
     - Очекуван излез: RuntimeException со порака "allItems list can't be null!"
     - Покриени гранки: 1, 2

Тест случај 2: allItems е empty

     - Влез: checkCart(Collections.emptyList(), 100)
     - Очекуван излез: true
     - Покриени гранки: 3, 21, 22

Тест случај 3: item со null име

     - Влез: checkCart(List.of(new Item(null, "123", 100, 0)), 100)
     - Очекуван излез: true
     - Покриени гранки: 3, 4.1, 4.2, 4.3, 5, 6, 7, 8, 9, 10.1, 10.2, 10.3, 11, 12, 14, 16, 17, 21, 22

Тест случај 4: item со invalid barcode character

     - Влез: checkCart(List.of(new Item("item1", "12a", 100, 0)), 100)
     - Очекуван излез: RuntimeException with message "Invalid character in item barcode!"
     - Покриени гранки: 3, 4.1, 4.2, 4.3, 5, 6, 8, 9, 10.1, 10.2, 10.3, 11, 12, 13

Тест случај 5: item со null barcode

     - Влез: checkCart(List.of(new Item("item1", null, 100, 0)), 100)
     - Очекуван излез: RuntimeException with message "No barcode!"
     - Покриени гранки: 3, 4.1, 4.2, 4.3, 5, 6, 8, 18

Тест случај 6: item со discount > 0

     - Влез: checkCart(List.of(new Item("item1", "123", 100, 0.1f)), 100)
     - Очекуван излез: true
     - Покриени гранки: 3, 4.1, 4.2, 4.3, 5, 6, 8, 9, 10.1, 10.2, 10.3, 11, 12, 14, 15, 17, 21, 22

Тест случај 7:  item со price > 300, discount > 0, barcode почнува со '0'

     - Влез: checkCart(List.of(new Item("item1", "0123", 400, 0.1f)), 100)
     - Очекуван излез: true
     - Покриени гранки: 3, 4.1, 4.2, 4.3, 5, 6, 8, 9, 10.1, 10.2, 10.3, 11, 12, 14, 15, 17, 19, 20, 21, 22

Тест случај 8: sum > payment

     - Влез: checkCart(List.of(new Item("item1", "123", 200, 0)), 100)
     - Очекуван излез: false
     - Покриени гранки: 3, 4.1, 4.2, 4.3, 5, 6, 8, 9, 10.1, 10.2, 10.3, 11, 12, 14, 16, 17, 21, 23

