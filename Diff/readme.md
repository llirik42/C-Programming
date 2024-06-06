# Утилита diff

## Задание

Написать 2 версии утилиты, которая показывает различия в двух файлах (упрощённый аналог утилиты *diff*).

* Первая версия работает только с текстовыми файлами: должна просто вывести номер байта и номер строки с первым несовпадением, две отличающиеся строки и маркера несовпадения:
	```
	Discrepancy at byte 133, at line 12('1' vs '2')

	строка из файла номер 1, в которой больше ничего нет

	                      +                          ++++  

	строка из файла номер 2, в которой больше ничего есть
	```

* Вторая версия умеет работать с бинарными файлами: Для бинарных файлов нет понятия конца строки и нет смысла выводить все данные, поэтому для таких файлов находится первый несовпадающий байт, на печать выводится его номер, и две группы по 16 байт из обоих файлов, в которых произошло несовпадение, в виде шестнадцатеричных чисел:
	```
	Discrepancy at byte 51(0x33) (EF vs 77)

	00000030     DD AD BE FF CD CD CD CD | 00 00 00 00 00 00 00 00

	                      ++             |

	00000030     DD AD BE 77 CD CD CD CD | 00 00 00 00 00 00 00 00
	```

## Требования

* Если файлы совпадают до единого байта, утилита должна вывести "OK" и завершиться с кодом возврата 0
* Если в файлах найдены различия — вывести первое и завершиться с кодом возврата 1
* Обе версии должны сначала вывести отличия в размерах файлов, или сообщить, что размеры совпадают
* Вторая версия должна понимать, как именно выводить отличия (имеет ли смысл печатать строки или нужно выбрать режим печати байтов, см. функцию `isprint()`)

## Использование

```Bash
./mydiff.out file1 file2  # Утилита проанализирует файлы чтобы понять, есть ли среди них бинарные
```

```Bash
./mydiff.out file1 file2 -b # Утилита будет считать файлы бинарными
```