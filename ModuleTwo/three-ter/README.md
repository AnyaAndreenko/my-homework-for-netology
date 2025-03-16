# Домашнее задание к занятию «Управляющие конструкции в коде Terraform»

### Задание 1

### Задание 2

Нужно создать файл count-vm.tf. Описать в нём создание двух одинаковых ВМ  __web-1 и web-2__ (не web-0 и web-1) с минимальными параметрами, используя мета-аргумент count loop. 
Назначить ВМ созданную в первом задании группу безопасности.(как это сделать узнайте в документации провайдера yandex/compute_instance)
создать файл for_each-vm.tf. Описать в нём создание двух ВМ для баз данных с именами "main" и "replica" разных по cpu/ram/disk_volume, используя мета-аргумент for_each loop.

[count-vm.tf](https://github.com/AnyaAndreenko/ter-homeworks/blob/main/03/src/count-vm.tf)

[for_each-vm.tf](https://github.com/AnyaAndreenko/ter-homeworks/blob/main/03/src/for_each-vm.tf)


