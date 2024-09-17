from time import sleep
from datetime import datetime
from threading import Thread
#import requests

print ("Потоковая запись в файлы")

def write_words(word_count, file_name):
    """
    где word_write_wordscount - количество записываемых слов, file_name - название файла, куда будут
    записываться слова.
    """
    file = open(file_name, 'w', encoding="utf-8")

    for i in range (0, word_count):
        file.write(f"Какое-то слово {i} <номер слова по порядку>" + '\n')
        sleep (0.1)
        #print(f"Какое-то слово {i} <номер слова по порядку>")

    print(f"Завершилась запись в файл {file_name}\n\n")
    file.close()

start_time = datetime.now()
write_words(10, "example1.txt")
write_words(30, "example2.txt")
write_words(200, "example3.txt")
write_words(100, "example4.txt")
res_time = datetime.now() - start_time
print(f"Работа без потоков {res_time}")


start_time = datetime.now()

thread1 = Thread (target = write_words, args = (10, "example5.txt"))
thread2 = Thread (target = write_words, args = (30, "example6.txt"))
thread3 = Thread (target = write_words, args = (200, "example7.txt"))
thread4 = Thread (target = write_words, args = (100, "example8.txt"))

thread1.start()
thread2.start()
thread3.start()
thread4.start()

thread1.join()
thread2.join()
thread3.join()
thread4.join()

res_time = datetime.now() - start_time
print(f"Работа потоков {res_time}")
