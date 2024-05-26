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

## (5) Tест случаи според Multiple Condition критериумот
Условот if (item.getPrice() > 300 && item.getDiscount() > 0 && item.getBarcode().charAt(0) == '0') вклучува три подуслови:

     item.getPrice() > 300 (Услов A)
     item.getDiscount() > 0 (Услов B)
     item.getBarcode().charAt(0) == '0' (Услов C)
За секоја состојба, имаме две можни вредности: точно (T) или неточно (F). Затоа, треба да ги тестираме сите можни комбинации на овие подуслови, што доведува до 2^3 = 8 тест случаи.

Тест случај 1: A = T, B = T, C = T

     - Влез: checkCart(List.of(new Item("item1", "0123", 400, 0.1f)), 100)
     - Очекуван излез: true
     - Објаснување: Сите услови се true; price > 300, discount > 0, barcode започнува со '0'. Сумата ќе се намали за 30.

Тест случај 2: A = T, B = T, C = F

     - Влез: checkCart(List.of(new Item("item1", "1123", 400, 0.1f)), 100)
     - Очекуван излез: false
     - Објаснување: Само barcode условот е false (не започнува со '0'). Сумата нема да се намали за 30.

Тест случај 3: A = T, B = F, C = T

     - Влез: checkCart(List.of(new Item("item1", "0123", 400, 0)), 100)
     - Очекуван излез: false
     - Објаснување: Само discount условот е false (discount is 0). Сумата нема да се намали за 30.

Тест случај 4: A = T, B = F, C = F

     - Влез: checkCart(List.of(new Item("item1", "1123", 400, 0)), 100)
     - Очекуван излез: false
     - Објаснување: Двата discount и barcode услови се false. Сумата нема да се намали за 30.

Тест случај 5: A = F, B = T, C = T

     - Влез: checkCart(List.of(new Item("item1", "0123", 200, 0.1f)), 100)
     - Очекуван излез: true
     - Објаснување: Само price условот е false (price <= 300). Сумата нема да се намали за 30.

Тест случај 6: A = F, B = T, C = F

     - Влез: checkCart(List.of(new Item("item1", "1123", 200, 0.1f)), 100)
     - Очекуван излез: true
     - Објаснување: Price и barcode условите се false. Сумата нема да се намали за 30.

Тест случај 7: A = F, B = F, C = T

     - Влез: checkCart(List.of(new Item("item1", "0123", 200, 0)), 100)
     - Очекуван излез: true
     - Објаснување: Price и discount условите се false. Сумата нема да се намали за 30.

Тест случај 8: A = F, B = F, C = F

     - Влез: checkCart(List.of(new Item("item1", "1123", 200, 0)), 100)
     - Очекуван излез: true
     - Објаснување: Сите услови се false. Сумата нема да се намали за 30.
