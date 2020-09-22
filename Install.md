1. Выкачать исходный код harmonyOS. Есть два способа.
1.1 Просто архив: https://repo.huaweicloud.com/harmonyos/os/1.0/code-1.0.tar.gz
1.2 Репозиторий:
repo init -u https://gitee.com/openharmony/manifest.git -b master
repo sync -c

Несмотря на то, что ядро - это небольшой подрепозиторий, приходится выкачивать их все, так как даже при сборке ядра используются другие.

2. Выкачать дополнительные инструменты
2.1 https://repo.huaweicloud.com/harmonyos/compiler/gn/1523/linux/gn.1523.tar
2.2 https://repo.huaweicloud.com/harmonyos/compiler/ninja/1.9.0/linux/ninja.1.9.0.tar
2.3 https://repo.huaweicloud.com/harmonyos/compiler/hc-gen/0.65/linux/hc-gen-0.65-linux.tar
2.4 https://repo.huaweicloud.com/harmonyos/compiler/clang/9.0.0-34042/linux/llvm-linux-9.0.0-34042.tar

3. Добавить пути в PATH. Важно! Пути нужно добавлять без / в конце, например, llvm/bin:$PATH.

4. Запустить сборку на верхнем уровне.
python3 build.py ipcamera_hi3516dv300

У меня она упала на этапе линковки. Это не так важно для сборки ядра. Смысл в том, что она настраивает внутренние репозитории.

4.1 Есть комманда ./build.sh hi3518ev300 clang внутри kernel/liteos_a/. Вроде бы, это и есть та настройка (копирования файла .config), но так как при сборке ядра участвуют другие репозитории, лучше выполнять общую сборку, которая пройдет сама по всем директориям.

5. Перейти в директорию kernel/liteos_a/, выполнить make clean и запустить clade make для перехвата комманд сборки.

