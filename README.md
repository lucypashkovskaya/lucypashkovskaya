import datetime as dt# Импортируйте необходимые модули

FORMAT = '%H:%M:%S'# Запишите формат полученного времени.
WEIGHT = 75  # Вес.
HEIGHT = 175  # Рост.
K_1 = 0.035  # Коэффициент для подсчета калорий.
K_2 = 0.029  # Коэффициент для подсчета калорий.
STEP_M = 0.65  # Длина шага в метрах.

storage_data = {}  
# Словарь для хранения полученных данных.
def check_correct_data(data):
    """Проверка корректности полученного пакета."""
    time,steps=data
    if len(data)!=2:
        return False
    elif (time is None) or (steps is None):
        return False
    else:
        return True# Если длина пакета отлична от 2
    # или один из элементов пакета имеет пустое значение -
    # функция вернет False, иначе - True.
def check_correct_time(time):
    """Проверка корректности параметра времени."""
    pack_time = dt.datetime.strptime(time, FORMAT).time()
    if len (storage_data)!= 0 and pack_time<=max(storage_data.keys()):
        return False
    else:
        return True# Если словарь для хранения не пустой
    # и значение времени, полученное в аргументе,
    # меньше или равно самому большому значению ключа в словаре,
    # функция вернет False.
    # Иначе - True 


def get_step_day(steps):
    """Получить количество пройденных шагов за этот день."""
    for steps_1 in storage_data.values():
        sum += steps_1
        steps_2= sum + steps
        return steps_2
       # Посчитайте все шаги, записанные в словарь storage_data,
    # прибавьте к ним значение из последнего пакета
    # и верните  эту сумму.
    

def get_distance(steps):
    """Получить дистанцию пройденного пути в км."""
    sum_dist=(steps*STEP_M)/1000
    return sum_dist
    # Посчитайте дистанцию в километрах,
    # исходя из количества шагов и длины шага.


def get_spent_calories(dist, pack_time):
    """Получить значения потраченных калорий."""
    hours = pack_time.hour + pack_time.minute / 60
    spent_calories = (K_1*WEIGHT + ((dist/hours)**2 / HEIGHT) * K_2*WEIGHT) * float(hours)*60
    return spent_calories
        # В уроке «Последовательности» вы написали формулу расчета калорий.
    # Перенесите её сюда и верните результат расчётов.
    # Для расчётов вам потребуется значение времени; 
    # получите его из объекта current_time;
    # переведите часы и минуты в часы, в значение типа float.

def get_achievement(dist):
    """Получить поздравления за пройденную дистанцию."""
    if dist >= 6.5:
        achievement = 'Отличный результат! Цель достигнута.'
    elif dist >= 3.9:
        achievement = 'Неплохо! День был продуктивным.'
    elif dist >= 2:
        achievement = 'Маловато, но завтра наверстаем!'
    else:
        achievement = 'Лежать тоже полезно. Главное — участие, а не победа!'
    return achievement
    # В уроке «Строки» вы описали логику
    # вывода сообщений о достижении в зависимости
    # от пройденной дистанции.
    # Перенесите этот код сюда и замените print() на return.


def show_message (time, steps, dist, spent_calories, achievement):
    return print(f'''Время: {time}
    Количество шагов за сегодня: {steps}
    Дистанция составила {f'{dist:.2f}'} км.
    Вы сожгли  {f"{spent_calories:.2f}"} ккал.
    {achievement}
    ''')
# Место для функции show_message.
def accept_package(data):
    """Обработать пакет данных."""
    if check_correct_data(data) == False:# Если функция проверки пакета вернет False
        return 'Некорректный пакет'
    
    time= data [0]
    pack_time = dt.datetime.strptime(time,FORMAT)
    pack_time = dt.datetime.time(pack_time)
    
# Распакуйте полученные данные #Преобразуйте строку с временем в объект типа time.
    if check_correct_time(time) == False:# Если функция проверки значения времени вернет False
        return 'Некорректное значение времени'

    day_steps = get_step_day (data [1]) # Запишите результат подсчёта пройденных шагов.
    dist = get_distance (data [1]) # Запишите результат расчёта пройденной дистанции.
    spent_calories = get_spent_calories(dist, pack_time) # Запишите результат расчёта сожжённых калорий.
    achievement = get_achievement (dist) # Запишите выбранное мотивирующее сообщение.
    return show_message(pack_time, day_steps, dist, spent_calories, achievement)# Вызовите функцию show_message().
    storage_data[pack_time] = steps
    return storage_data# Добавьте новый элемент в словарь storage_data.
    # Верните словарь storage_data.


# Данные для самопроверки.Не удаляйте их.
package_0 = ('2:00:01', 505)
package_1 = (None, 3211)
package_2 = ('9:36:02', 15000)
package_3 = ('9:36:02', 9000)
package_4 = ('8:01:02', 7600)

accept_package(package_0)
accept_package(package_1)
accept_package(package_2)
accept_package(package_3)
accept_package(package_4)
