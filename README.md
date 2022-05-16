
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
ksy99@MacBook-Air-Ksenia ~ % tar -xvf boost_1_69_0.tar.gz.1
$ ksy99@MacBook-Air-Ksenia Desktop % cd /Users/ksy99/Desktop/boost_1_69_0
```
3) Подсчитайте количество файлов в директории `~/boost_1_69_0` **не включая** вложенные директории.
```bash
ksy99@MacBook-Air-Ksenia boost_1_69_0 % find . -maxdepth 1 -type f | wc -l
До компиляции: 13
```
4) Подсчитайте количество файлов в директории `~/boost_1_69_0` **включая** вложенные директории.
```bash
ksy99@MacBook-Air-Ksenia boost_1_69_0 % find . -type f|wc -l
```
61198

5) Подсчитайте количество заголовочных файлов, файлов с расширением `.cpp`, сколько остальных файлов (не заголовочных и не `.cpp`).
```bash
Заголовочных:
ksy99@MacBook-Air-Ksenia boost_1_69_0 % find . -iname "*.h" | wc -l
 296


Файлов с расширением ".cpp":
ksy99@MacBook-Air-Ksenia boost_1_69_0 % find . -iname "*.cpp" | wc -l
13774


Остальные файлы:
ksy99@MacBook-Air-Ksenia boost_1_69_0 % find -type f ! -iname "*.h" -a ! -iname "*.cpp" | wc -l
47121
```



6) Найдите полный пусть до файла `any.hpp` внутри библиотеки *boost*.
```bash
ksy99@MacBook-Air-Ksenia boost_1_69_0 % find -name “any.hpp” -print 
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
ksy99@MacBook-Air-Ksenia boost_1_69_0 % grep -Ril "boost::asio" .
./boost/beast/experimental/core/impl/timeout_socket.hpp
./boost/beast/experimental/core/impl/flat_stream.ipp
./boost/beast/experimental/core/impl/timeout_service.ipp
./boost/beast/experimental/core/flat_stream.hpp
./boost/beast/experimental/core/ssl_stream.hpp
./boost/beast/experimental/core/timeout_service.hpp
./boost/beast/experimental/core/timeout_socket.hpp
```

8) Скомпилирутйе *boost*. Можно воспользоваться [инструкцией](https://www.boost.org/doc/libs/1_61_0/more/getting_started/unix-variants.html#or-build-custom-binaries) или [ссылкой](https://codeyarns.com/2017/01/24/how-to-build-boost-on-linux/).
```bash
ksy99@MacBook-Air-Ksenia boost_1_69_0 % ./bootstrap.sh –prefix=boost_output
ksy99@MacBook-Air-Ksenia boost_1_69_0 % ./b2 install
```

9) Перенесите все скомпилированные на предыдущем шаге статические библиотеки в директорию `~/boost-libs`.
```bash
ksy99@MacBook-Air-Ksenia boost_1_69_0 % cd ~/boost-libs

```
10) Подсчитайте сколько занимает дискового пространства каждый файл в этой директории.
```bash
ksy99@MacBook-Air-Ksenia boost_1_69_0 % find . type -f -exec du -h {} +|sort -rh | head -n 10
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

```
11) Найдите *топ10* самых "тяжёлых".
```bash
ksy99@MacBook-Air-Ksenia boost_1_69_0 %  ls -lsh | sort -hr | head
28M ./libboost_wave.a
21M ./libboost_log_setup.a
20M ./libboost_log.a
16M ./libboost_test_exec_monitor.a
15M ./libboost_unit_test_framework.a
9,1M ./libboost_locale.a
8,9M ./libboost_regex.a
8,1M ./libboost_math_tr1f.a
7,8M ./libboost_math_tr1.a
7,7M ./libboost_math_tr1l.a
```
