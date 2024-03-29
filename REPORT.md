## Laboratory work I

Данная лабораторная работа посвещена изучению утилит для разработки проектов

## Tasks

- [+] 1. Ознакомиться со ссылками учебного материала
- [+] 2. Выполнить инструкцию учебного материала


## Tutorial

```bash
$ export GITHUB_USERNAME=AlexCoder47
$ export GIST_TOKEN=<сохраненный_токен>
$ alias edit=nano


$ mkdir -p ${GITHUB_USERNAME}/workspace
$ cd ${GITHUB_USERNAME}/workspace
```

```sh
$ pwd
/home/alexc/AlexCoder47/workspace
```

```sh
$ cd ..
```

```sh
$ pwd
/home/alexc/AlexCoder47
```

```sh
$ mkdir -p workspace/tasks/
$ mkdir -p workspace/projects/
$ mkdir -p workspace/reports/
$ cd workspace
```

```sh
$ wget https://nodejs.org/dist/v6.11.5/node-v6.11.5-linux-x64.tar.xz
https://gist.github.com/AlexCoder47/28adfe85185ac59a6eac399ab995651b/edit
```

```sh
$ tar -xf node-v6.11.5-linux-x64.tar.xz
$ rm -rf node-v6.11.5-linux-x64.tar.xz
$ mv node-v6.11.5-linux-x64 node
```

```sh
$ ls node/bin
node  npm


$ echo ${PATH}
/home/alexc/.nvm/versions/node/v20.11.0/bin:/home/alexc/.local/bin:/usr/local/sbin:/usr/local/bin:/usr/bin:/var/lib/flatpak/exports/bin:/usr/bin/site_perl:/usr/bin/vendor_perl:/usr/bin/core_perl


$ export PATH=${PATH}:`pwd`/node/bin
$ echo ${PATH}
/home/alexc/.nvm/versions/node/v20.11.0/bin:/home/alexc/.local/bin:/usr/local/sbin:/usr/local/bin:/usr/bin:/var/lib/flatpak/exports/bin:/usr/bin/site_perl:/usr/bin/vendor_perl:/usr/bin/core_perl:/home/alexc/AlexCoder47/workspace/node/bin


$ mkdir scripts
$ cat > scripts/activate<<EOF
export PATH=\${PATH}:`pwd`/node/bin
EOF
$ source scripts/activate
```

```sh
$ (umask 0077 && echo ${GIST_TOKEN} > ~/.gist)
```

## Report

```sh
$ export LAB_NUMBER=01
$ git clone https://github.com/tp-labs/lab${LAB_NUMBER} tasks/lab${LAB_NUMBER}
$ mkdir reports/lab${LAB_NUMBER}
$ cp tasks/lab${LAB_NUMBER}/README.md reports/lab${LAB_NUMBER}/REPORT.md
$ cd reports/lab${LAB_NUMBER}
$ edit REPORT.md


$ gist REPORT.md
```

## Homework

	1. Скачайте библиотеку *boost* с помощью утилиты **wget**. Адрес для скачивания `https://sourceforge.net/projects/boost/files/boost/1.69.0/boost_1_69_0.tar.gz`.

```sh
$ wget https://sourceforge.net/projects/boost/files/boost/1.69.0/boost_1_69_0.tar.gz
https://gist.github.com/AlexCoder47/647a21d6d0e8355915112743124079fd
```

2. Разархивируйте скаченный файл в директорию `~/boost_1_69_0`

```sh
$ mkdir ~/boost_1_69_0
$ tar -xvzf boost_1_69_0.tar.gz -C boost_1_69_0
https://gist.github.com/AlexCoder47/d1aa53e606a9271e8fb5c1299c99e841
```

3. Подсчитайте количество файлов в директории `~/boost_1_69_0` **не включая** вложенные директории.

```sh
$ cd boost_1_69_0/boost_1_69_0
$ find -maxdepth 1 -type f | wc -l
12
```

4. Подсчитайте количество файлов в директории `~/boost_1_69_0` **включая** вложенные директории.

```sh
$ find -type f | wc -l
61191
```

5. Подсчитайте количество заголовочных файлов, файлов с расширением `.cpp`, сколько остальных файлов (не заголовочных и не `.cpp`).

```sh
$ find -type f -name "*.h" | wc -l
296

$ find -type f -name "*.hpp" | wc -l
14912

$ find -type f -name "*.cpp" | wc -l
13774

$ find -type f ! -name "*.hpp" ! -name "*.cpp" ! -name "*.h" | wc -l
32209
```

6. Найдите полный пусть до файла `any.hpp` внутри библиотеки *boost*.

```sh
$ find -type f -iname "any.hpp"
./boost/hana/any.hpp
./boost/hana/fwd/any.hpp
./boost/proto/detail/any.hpp
./boost/type_erasure/any.hpp
./boost/xpressive/detail/utility/any.hpp
./boost/spirit/home/support/algorithm/any.hpp
./boost/any.hpp
./boost/fusion/algorithm/query/any.hpp
./boost/fusion/algorithm/query/detail/any.hpp
./boost/fusion/include/any.hpp
```

7. Выведите в консоль все файлы, где упоминается последовательность `boost::asio`.

```sh
$ grep -r "boost::asio"
https://gist.github.com/AlexCoder47/ce1bbafd3e2fa06fad360e04862494ca
```

8. Скомпилирутйе *boost*. Можно воспользоваться [инструкцией](https://www.boost.org/doc/libs/1_61_0/more/getting_started/unix-variants.html#or-build-custom-binaries) или [ссылкой](https://codeyarns.com/2017/01/24/how-to-build-boost-on-linux/).

```sh
$ ./bootstrap.sh --prefix=boost_output
https://gist.github.com/AlexCoder47/d26f841f8d08b7c05adf7f93e31867b7

$ ./b2 install -j 12
https://gist.github.com/AlexCoder47/916be55f2acef5b4a126d6c67f6542f2
```

9. Перенесите все скомпилированные на предыдущем шаге статические библиотеки в директорию `~/boost-libs`.

```sh
$ mv boost_output/lib/ ~/boost-libs/
```
10. Подсчитайте сколько занимает дискового пространства каждый файл в этой директории.

```sh
$ find . -type f -exec du -h {} +
https://gist.github.com/AlexCoder47/0c9b071eb45a0bd7195666da2857295b
```
11. Найдите *топ10* самых "тяжёлых".

```sh
$ find . -type f -exec du -h {} +|sort -rh | head -n 10
154M    ./bin.v2/libs/math/build/gcc-13.2.1/release/threading-multi/src/tr1/pch.hpp.gch
154M    ./bin.v2/libs/math/build/gcc-13.2.1/release/link-static/threading-multi/src/tr1/pch.hpp.gch
12M     ./libs/math/doc/math.pdf
4,5M    ./bin.v2/libs/wave/build/gcc-13.2.1/release/link-static/threadapi-pthread/threading-multi/visibility-hidden/libboost_wave.a
3,7M    ./status/expected_results.xml
3,2M    ./bin.v2/libs/regex/build/gcc-13.2.1/release/link-static/threading-multi/visibility-hidden/libboost_regex.a
3,0M    ./libs/gil/io/test_images/raw/RAW_CANON_D30_SRGB.CRW
2,7M    ./libs/asio/doc/reference.qbk
2,7M    ./libs/algorithm/test/search_test_data/0001.corpus
2,7M    ./bin.v2/libs/math/build/gcc-13.2.1/release/link-static/threading-multi/visibility-hidden/libboost_math_tr1l.a
```

```
Copyright (c) 2015-2021 The ISC Authors
```
