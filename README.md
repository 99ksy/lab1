
## Homework

1) Скачайте библиотеку *boost* с помощью утилиты **wget**. Адрес для скачивания `https://sourceforge.net/projects/boost/files/boost/1.69.0/boost_1_69_0.tar.gz`.
```bash
$ wget https://sourceforge.net/projects/boost/files/boost/1.69.0/boost_1_69_0.tar.gz
```
Распознаётся altushost-swe.dl.sourceforge.net (altushost-swe.dl.sourceforge.net)… 79.142.76.130
Подключение к altushost-swe.dl.sourceforge.net (altushost-swe.dl.sourceforge.net)|79.142.76.130|:443... соединение установлено.
HTTP-запрос отправлен. Ожидание ответа… 200 OK
Длина: 111710205 (107M) [application/x-gzip]
Сохранение в: «boost_1_69_0.tar.gz.1»

2) Разархивируйте скаченный файл в директорию `~/boost_1_69_0`
```bash
$ tar -xf boost_1_69_0.tar.gz -C ~
$ cd home/lis/boost_1_69_0
```
3) Подсчитайте количество файлов в директории `~/boost_1_69_0` **не включая** вложенные директории.
```bash
ls -l | grep "^-" | wc
find . -maxdepth 1 -type f | wc
tree -L 1
До компиляции: 12
После компиляции: 16
```
4) Подсчитайте количество файлов в директории `~/boost_1_69_0` **включая** вложенные директории.
```bash
ls -laR | grep "^-" | wc
find ! -type d | wc
tree
До компиляции: 61191
После компиляции: 62081
```
5) Подсчитайте количество заголовочных файлов, файлов с расширением `.cpp`, сколько остальных файлов (не заголовочных и не `.cpp`).
```bash
Заголовочных:
	$ find . -iname "*.h" | wc -l
	$ tree -P *.h
	До компиляции: 296
	После компиляции: 296

Файлов с расширением ".cpp":
    $ find . -iname "*.cpp" | wc -l
	$ tree -P *.cpp
	До компиляции:13774
	После компиляции:13789

Остальные файлы:
    find -type f ! -iname "*.h" -a ! -iname "*.cpp" | wc -l
	find -type f ! -name "*.h" -a ! -name "*.cpp" | wc -l
	До компиляции: 47121
	После компиляции:47996
```



6) Найдите полный пусть до файла `any.hpp` внутри библиотеки *boost*.
```bash
$ find -iname "any.hpp"
./boost/type_erasure/any.hpp
./boost/any.hpp
./boost/xpressive/detail/utility/any.hpp
./boost/hana/fwd/any.hpp
./boost/hana/any.hpp
./boost/fusion/include/any.hpp
./boost/fusion/algorithm/query/any.hpp
./boost/fusion/algorithm/query/detail/any.hpp
./boost/proto/detail/any.hpp
./boost/spirit/home/support/algorithm/any.hpp
```

7) Выведите в консоль все файлы, где упоминается последовательность `boost::asio`.
```bash
grep -lr "bogreost::asio"
Выводит много файлов
```

8) Скомпилирутйе *boost*. Можно воспользоваться [инструкцией](https://www.boost.org/doc/libs/1_61_0/more/getting_started/unix-variants.html#or-build-custom-binaries) или [ссылкой](https://codeyarns.com/2017/01/24/how-to-build-boost-on-linux/).
```bash
./bootstrap.sh
./b2 install
```

9) Перенесите все скомпилированные на предыдущем шаге статические библиотеки в директорию `~/boost-libs`.
```bash
$ mkdir ~/boost-libs
$ mv ~/boost_1_69_0/stage/lib/*.a ~/boost-libs
```
10) Подсчитайте сколько занимает дискового пространства каждый файл в этой директории.
```bash
$ du -ah 
$ ls -lsh | sort -hr
152K	./libboost_date_time.a
3,1M	./libboost_math_tr1l.a
468K	./libboost_thread.a
16K	./libboost_stacktrace_basic.a
84K	./libboost_random.a
1,2M	./libboost_serialization.a
2,8M	./libboost_regex.a
1,7M	./libboost_program_options.a
252K	./libboost_fiber.a
232K	./libboost_prg_exec_monitor.a
3,1M	./libboost_math_tr1f.a
620K	./libboost_math_c99.a
360K	./libboost_contract.a
3,1M	./libboost_math_tr1.a
4,0K	./libboost_atomic.a
24K	./libboost_stacktrace_backtrace.a
4,0K	./libboost_stacktrace_noop.a
20K	./libboost_context.a
4,7M	./libboost_wave.a
4,0K	./libboost_system.a
516K	./libboost_math_c99f.a
2,1M	./libboost_locale.a
176K	./libboost_iostreams.a
196K	./libboost_coroutine.a
56K	./libboost_timer.a
2,7M	./libboost_log_setup.a
24K	./libboost_stacktrace_addr2line.a
904K	./libboost_graph.a
4,0K	./libboost_exception.a
424K	./libboost_filesystem.a
2,4M	./libboost_unit_test_framework.a
2,4M	./libboost_test_exec_monitor.a
188K	./libboost_type_erasure.a
244K	./libboost_chrono.a
552K	./libboost_math_c99l.a
4,5M	./libboost_log.a
792K	./libboost_wserialization.a
156K	./libboost_container.a
40M	.
```
11) Найдите *топ10* самых "тяжёлых".
```bash
$ ls -lsh | sort -hr | head
4,7M -rw-rw-r-- 1 lis lis 4,7M мар 17 20:33 libboost_wave.a
4,5M -rw-rw-r-- 1 lis lis 4,5M мар 17 20:33 libboost_log.a
3,1M -rw-rw-r-- 1 lis lis 3,1M мар 17 20:33 libboost_math_tr1l.a
3,1M -rw-rw-r-- 1 lis lis 3,1M мар 17 20:33 libboost_math_tr1f.a
3,1M -rw-rw-r-- 1 lis lis 3,1M мар 17 20:33 libboost_math_tr1.a
2,8M -rw-rw-r-- 1 lis lis 2,8M мар 17 20:33 libboost_regex.a
2,7M -rw-rw-r-- 1 lis lis 2,7M мар 17 20:33 libboost_log_setup.a
2,4M -rw-rw-r-- 1 lis lis 2,4M мар 17 20:33 libboost_unit_test_framework.a
2,4M -rw-rw-r-- 1 lis lis 2,4M мар 17 20:33 libboost_test_exec_monitor.a
2,1M -rw-rw-r-- 1 lis lis 2,1M мар 17 20:33 libboost_locale.a
```
